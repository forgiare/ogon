includes_version = include_directories('..')

configure_file(input: 'version.h.in',
       output: 'version.h',
       format: 'cmake',
       configuration: cdata,
       install_dir: join_paths(get_option('includedir'), 'ogon@0@'.format(ogon_version[0]), 'ogon'),
)

configure_file(input: 'build-config.h.in',
       output: 'build-config.h',
       format: 'cmake',
       configuration: cdata,
       install_dir: join_paths(get_option('includedir'), 'ogon@0@'.format(ogon_version[0]), 'ogon'),
)

install_headers(
	['api.h', 'backend.h', 'dmgbuf.h', 'message.h', 'module.h', 'service.h'],
	subdir: join_paths('ogon@0@'.format(ogon_version[0]), 'ogon'),
)