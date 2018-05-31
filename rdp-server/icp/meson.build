ogon_icp_sources = [
       'pbrpc/pbrpc.c',
       'pbrpc/pbrpc_utils.c',
       'pbrpc/pipe_transport.c',
       'icp.c',
       'icp_client_stubs.c',
       'icp_server_stubs.c',
]

includes_icp = include_directories('.', './pbrpc')

ogon_icp_lib = static_library('ogon-icp',
       sources: [ogon_icp_sources, generated_pbrpc_proto, generated_icp_proto],
       include_directories: [includes_version, includes_icp, includes_ogon],
       dependencies: [deps_protobuf, deps_freerdp, deps_winpr],
)
