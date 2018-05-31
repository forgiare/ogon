
ogon_otsapi_lib = shared_library('ogon-otsapi',
	['otsapi_thrift.cpp', generated_ots_thrift],
	cpp_args: ['-DFORCE_BOOST_SMART_PTR'],
	include_directories: [includes_version, includes_ogon, includes_generated_ots, include_directories('..')],
	dependencies: [deps_winpr, libthrift_deps],
	install: true,
	install_dir: ogon_app_lib_path,
)
