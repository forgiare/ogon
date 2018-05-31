

mod_weston = library('ogon-mod-weston',
	'weston_module.cpp',
	'weston_module.h',
	'../common/module_helper.cpp',
	'../common/module_helper.h',
	include_directories: [includes_version, includes_ogon],
	link_with: ogon_backend_lib,
	dependencies: [deps_winpr, deps_freerdp ],
	install: true,
	install_dir: ogon_module_lib_path,
	install_rpath: '$ORIGIN/../..'

)