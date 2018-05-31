
ogon_backend_launcher = executable('ogon-backend-launcher',
	'SystemSession.cpp',
	'../session-manager/common/module/RemoteModuleTransport.cpp',
	'ModuleCommunication.cpp',
	'main.cpp',
	generated_pbrpc_cpp_proto,
	generated_module_cpp_proto,
	include_directories: [includes_ogon_server, includes_ogon, includes_version],
	dependencies: [deps_winpr, deps_protobuf, deps_pam],
	install: true,
	install_dir: get_option('sbindir'),
)
