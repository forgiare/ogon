

srcs = [
	'common/call/Call.cpp',
	'common/call/CallIn.cpp',
	'common/call/CallOut.cpp',
	'common/call/CallFactory.cpp',
	'common/call/CallInPing.cpp',
	'common/call/CallOutPing.cpp',
	'common/call/CallInLogonUser.cpp',
	'common/call/CallInDisconnectUserSession.cpp',
	'common/call/CallOutOtsApiVirtualChannelOpen.cpp',
	'common/call/CallOutOtsApiVirtualChannelClose.cpp',
	'common/call/CallInAuthenticateUser.cpp',
	'common/call/CallOutSwitchTo.cpp',
	'common/call/CallOutLogOffUserSession.cpp',
	'common/call/CallInEndSession.cpp',
	'common/call/CallInPropertyBool.cpp',
	'common/call/CallInPropertyNumber.cpp',
	'common/call/CallInPropertyString.cpp',
	'common/call/CallInPropertyBulk.cpp',
	'common/call/CallOutDisconnectUserSession.cpp',
	'common/call/CallInSBPVersion.cpp',
	'common/call/TaskCallInLogonUser.cpp',
	'common/call/TaskAuthenticateUser.cpp',
	'common/call/TaskEndRemoteControl.cpp',
	'common/call/CallOutOtsApiStartRemoteControl.cpp',
	'common/call/CallOutOtsApiStopRemoteControl.cpp',
	'common/call/CallInRemoteControlEnded.cpp',
	'common/call/CallOutMessage.cpp',
	'common/pbRPC/RpcEngine.cpp',

	'main.cpp',
	'common/appcontext/ApplicationContext.cpp',
	'common/session/SessionStore.cpp',
	'common/session/Session.cpp',
	'common/session/ConnectionStore.cpp',
	'common/session/Connection.cpp',
	'common/session/TaskSessionTimeout.cpp',
	'common/session/TaskLogonUser.cpp',
	'common/session/TaskDisconnect.cpp',
	'common/session/TaskCallIn.cpp',
	'common/session/TaskSwitchTo.cpp',
	'common/session/TaskShutdown.cpp',
	'common/session/TaskEnd.cpp',

	'common/otsapi/OTSApiHandler.cpp',
	'common/otsapi/OTSApiServer.cpp',
	'common/otsapi/TaskDisconnect.cpp',
	'common/otsapi/TaskLogoff.cpp',
	'common/otsapi/TaskStartRemoteControl.cpp',
	'common/otsapi/TaskStopRemoteControl.cpp',

	'common/module/ModuleManager.cpp',
	'common/module/LocalModule.cpp',
	'common/module/RemoteModule.cpp',
	'common/module/RemoteModuleTransport.cpp',
	'common/module/AuthModule.cpp',
	'common/module/CallBacks.cpp',
	'common/config/PropertyManager.cpp',
	'common/config/PropertyCWrapper.cpp',
	'common/utils/StringHelpers.cpp',
	'common/utils/TimeHelpers.cpp',
	'common/utils/MakeCert.cpp',
	'common/task/Executor.cpp',
	'common/permission/PermissionManager.cpp',
	'common/permission/LogonPermission.cpp',
	'common/session/SessionNotifier.cpp',
	'common/process/ProcessMonitor.cpp',
	'../common/security.c',
	'../common/procutils.c'
]



sm = executable('ogon-session-manager', srcs + generated_icp_cpp_proto + generated_sbp_cpp_proto + generated_pbrpc_cpp_proto + generated_module_cpp_proto,
	link_with: ogon_otsapi_lib,
	include_directories: [includes_version, includes_ogon, includes_generated, includes_icp, includes_generated_ots, include_directories('..', '.', 'common')],
	dependencies: [deps_protobuf, deps_winpr, deps_freerdp, deps_winpr_utils, libthrift_deps, deps_dbus],
	install: true,
	install_dir: get_option('sbindir'),
	install_rpath: '$ORIGIN/../' + get_option('libdir') + '/' + ogon_app_lib_dir,
)

subdir('auth/pam')
subdir('module/Qt')
subdir('module/Weston')
subdir('module/X11')

install_data('config/ogon.SessionManager.conf',
	install_dir: join_paths(get_option('sysconfdir'), 'dbus-1', 'system.d')
)
