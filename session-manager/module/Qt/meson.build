mod_qt = library('ogon-mod-qt',
	'qt_module.cpp',
	'qt_module.h',
	'../common/module_helper.cpp',
	'../common/module_helper.h',
	include_directories: [includes_version, includes_ogon],
	link_with: ogon_backend_lib,
	dependencies: [deps_winpr, deps_freerdp ],
	install: true,
	install_rpath: '$ORIGIN/../..',
	install_dir: ogon_module_lib_path
)