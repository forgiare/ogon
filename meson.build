project('ogon', 'c', 'cpp',
       version : '1.0.0',
       license : 'AGPL',
       meson_version : '>= 1.1.0'
)


ogon_version_full = meson.project_version()
ogon_version = ogon_version_full.split('.')

# git revision
git = find_program('git', required: false)
if git.found() == true
       git_cmd = run_command(git, 'rev-parse', 'HEAD', check: true)
       if git_cmd.returncode() == 0
               git_version = git_cmd.stdout().strip()
       else
               git_version = 'n/a'
       endif
else
       git_version = 'n/a'
endif

# Compiler setup
cc = meson.get_compiler('c')
cpp = meson.get_compiler('cpp')

add_global_arguments(['-DHAVE_CONFIG_H', '-DFREERDP_SETTINGS_INTERNAL_USE'], language: ['c', 'cpp'])

check_headers = [
        'unistd.h',
        'sys/epoll.h',
        'sys/eventfd.h',
]

cdata = configuration_data()
cdata.set('OGON_VERSION_MAJOR', ogon_version[0])
cdata.set('OGON_VERSION_MINOR', ogon_version[1])
cdata.set('OGON_VERSION_REVISION', ogon_version[2])
cdata.set('OGON_VERSION', '@0@.@1@'.format(ogon_version[0], ogon_version[1]))
cdata.set('OGON_VERSION_FULL', meson.project_version())
cdata.set('OGON_VERSION_SUFFIX', '')
cdata.set('VENDOR', '')
cdata.set('GIT_REVISION', git_version)

prefix = get_option('prefix')
sysconfdir = join_paths(prefix, 'etc')
datadir = join_paths(prefix, 'share')
localstatedir = join_paths(get_option('prefix'), get_option('localstatedir'))
ogon_cfg_path = join_paths(sysconfdir, 'ogon')
ogon_lib_path = join_paths(get_option('prefix'), get_option('libdir'))
ogon_app_lib_dir = 'ogon@0@'.format(ogon_version[0])
ogon_app_lib_path = join_paths(ogon_lib_path, ogon_app_lib_dir)
ogon_module_lib_path = join_paths(ogon_app_lib_path, 'modules')
protocols_paths = join_paths(get_option('datadir'), 'ogon', ogon_version[0])

cdata.set('OGON_PREFIX_PATH', prefix)
cdata.set('OGON_CFG_PATH', ogon_cfg_path)
cdata.set('OGON_LIB_PATH', ogon_lib_path)
cdata.set('OGON_BIN_PATH', get_option('bindir'))
cdata.set('OGON_SBIN_PATH', get_option('sbindir'))
cdata.set('OGON_VAR_PATH', localstatedir)
cdata.set('OGON_PID_PATH', join_paths(localstatedir, 'run'))
cdata.set('OGON_APP_LIB_DIR', ogon_app_lib_dir)
cdata.set('OGON_APP_LIB_PATH', ogon_app_lib_path)
cdata.set('OGON_MODULE_LIB_PATH', ogon_module_lib_path)
cdata.set('OGON_AUTH_MODULE_LIB_PATH', join_paths(ogon_app_lib_path, 'auth'))

cdata.set('PACKAGE_OGON_INCLUDE_DIR', '${PACKAGE_PREFIX_DIR}/include/ogon@0@'.format(ogon_version[0]))
cdata.set('PACKAGE_OGON_PROTOCOL_DIR', '${PACKAGE_PREFIX_DIR}/share/ogon/@0@'.format(ogon_version[0]))


if get_option('with_openh264')
	cdata.set('OGON_OPENH264_LIBRARY', join_paths(ogon_app_lib_path, 'libogon-openh264.so'))
else
	cdata.set('OGON_OPENH264_LIBRARY', '')
endif

foreach h : check_headers
  if cc.has_header(h)
    cdata.set('HAVE_' + h.underscorify().to_upper(), 1)
  endif
endforeach

deps_thread = dependency('threads')
deps_ssl = dependency('openssl')
deps_winpr = dependency('winpr2')
deps_freerdp = dependency('freerdp2')
deps_freerdp_server = dependency('freerdp-server2')
deps_winpr_utils = dependency('winpr-tools2')
deps_systemd = dependency('libsystemd', required: get_option('with_sm'))
deps_pam = dependency('pam')


if cc.has_member('SURFACE_BITS_COMMAND', 'bmp', prefix: '#include <freerdp/update.h>', dependencies: deps_freerdp)
	cdata.set('HAVE_SURFACECMD_BMP', 1)
endif


# protocol buffer
deps_protobuf = dependency('protobuf')
deps_protobuf_c = dependency('libprotobuf-c')
deps_dbus = dependency('dbus-1')
protoc = find_program('protoc')

# thrift
thrift = find_program('thrift', required: false)
if not thrift.found()
	local_thrift = subproject('thrift')

	thrift = local_thrift.get_variable('thrift')
endif
libthrift_deps = dependency('thrift', fallback: ['thrift', 'libthrift_deps'])

configure_file(input: 'config.h.in',
       output: 'config.h',
       format: 'cmake',
       configuration: cdata)

configure_file(input: 'buildflags.h.in',
       output: 'buildflags.h',
       configuration: cdata)

includes_ogon = include_directories('.', 'include')

subdir('include/ogon')
subdir('protocols/protobuf')
subdir('protocols/thrift')
subdir('backend')
subdir('rdp-server')
subdir('backend-launcher')
subdir('cli')
subdir('misc')
subdir('session-manager/otsapi')
subdir('snmon')

if get_option('with_sm')
	subdir('session-manager')
endif


pkgconfig = import('pkgconfig')
pkgconfig.generate(
	filebase: 'ogon@0@'.format(ogon_version[0]),
	name: 'ogon',
	description: 'ogon RDP server',
	version: meson.project_version(),
	url: 'http://ogon-project.com/',
	variables: [
		'protocol_dir=${prefix}/@0@'.format(protocols_paths),
		'module_dir=${prefix}/@0@/@1@/modules'.format(get_option('libdir'), ogon_app_lib_dir),
	],
	subdirs: 'ogon@0@'.format(ogon_version[0]),
)

pkgconfig.generate(ogon_backend_lib,
	filebase: 'ogon-backend@0@'.format(ogon_version[0]),
	name: 'ogon backend',
	description: 'ogon RDP server backend library',
	version: meson.project_version(),
	libraries: ogon_backend_lib,
	url: 'http://ogon-project.com/',
	subdirs: 'ogon@0@'.format(ogon_version[0]),
	variables: [
		'protocol_dir=${prefix}/@0@'.format(protocols_paths),
		'module_dir=${prefix}/@0@/@1@/modules'.format(get_option('libdir'), ogon_app_lib_dir),
	]
)

cmake = import('cmake')
cmake_dir = join_paths(get_option('libdir'), 'cmake', 'ogon@0@'.format(ogon_version[0]))
cmake.write_basic_package_version_file(name: 'ogon',
	version: meson.project_version(),
	install_dir: cmake_dir
)
cmake.configure_package_config_file(
    name: 'ogon',
    input: 'ogonConfig.cmake.in',
    configuration: cdata,
    install_dir: cmake_dir
)
