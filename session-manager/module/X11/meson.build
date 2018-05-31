deps_Xau = dependency('xau')

mod_x11 = library('ogon-mod-x11',
	'x11_module.cpp',
	'x11_module.h',
	'../common/module_helper.cpp',
	'../common/module_helper.h',
	include_directories: [includes_version, includes_ogon],
	link_with: ogon_backend_lib,
	dependencies: [deps_winpr, deps_freerdp, deps_Xau ],
	install: true,
	install_dir: ogon_module_lib_path,
	install_rpath: '$ORIGIN/../..'
)