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
	install: true
)



cmake = import('cmake')
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

