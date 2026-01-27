ogon_backend_sources = [
	'dmgbuf.c',
	'protocol.c',
	'transport.c',
	'service.c',
	'keycodes.c',
	'../common/security.c',
]

includes_backend = include_directories('.')

ogon_backend_lib = library('ogon-backend',
	sources: [ogon_backend_sources, generated_backend_proto],
	include_directories: [includes_ogon, includes_generated],
	dependencies: [deps_protobuf_c, deps_protobuf, deps_winpr, deps_freerdp],
	version: ogon_version_full,
	soversion: ogon_version[0],
	install: true,
	install_rpath: '$ORIGIN/../' + get_option('libdir'),
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


cmake_dir = join_paths(get_option('libdir'), 'cmake', 'ogon-backend@0@'.format(ogon_version[0]))

cmake.write_basic_package_version_file(name: 'ogon-backend',
	version: meson.project_version(),
	install_dir: cmake_dir
)
cmake.configure_package_config_file(
    name: 'ogon-backend',
    input: 'ogon-backendConfig.cmake.in',
    configuration: cdata,
    install_dir: cmake_dir
)

