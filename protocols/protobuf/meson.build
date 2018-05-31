generated_backend_proto = custom_target('gen-backend',
       input: ['backend.proto'],
       output: ['backend.pb-c.c', 'backend.pb-c.h'],
       command: [protoc, '--proto_path', '@CURRENT_SOURCE_DIR@', '--c_out', '@OUTDIR@', '@INPUT@'],
)

generated_pbrpc_proto = custom_target('gen-pbrpc',
       input: ['pbRPC.proto'],
       output: ['pbRPC.pb-c.c', 'pbRPC.pb-c.h'],
       command: [protoc, '--proto_path', '@CURRENT_SOURCE_DIR@', '--c_out', '@OUTDIR@', '@INPUT@'],
)

generated_pbrpc_cpp_proto = custom_target('gen-pbrpc-cpp',
       input: ['pbRPC.proto'],
       output: ['pbRPC.pb.cc', 'pbRPC.pb.h'],
       command: [protoc, '--proto_path', '@CURRENT_SOURCE_DIR@', '--cpp_out', '@OUTDIR@', '@INPUT@'],
)

generated_icp_proto = custom_target('gen-icp',
       input: ['ICP.proto'],
       output: ['ICP.pb-c.c', 'ICP.pb-c.h'],
       command: [protoc, '--proto_path', '@CURRENT_SOURCE_DIR@', '--c_out', '@OUTDIR@', '@INPUT@'],
)

generated_icp_cpp_proto = custom_target('gen-icp-cpp',
       input: ['ICP.proto'],
       output: ['ICP.pb.cc', 'ICP.pb.h'],
       command: [protoc, '--proto_path', '@CURRENT_SOURCE_DIR@', '--cpp_out', '@OUTDIR@', '@INPUT@'],
)

generated_sbp_cpp_proto = custom_target('gen-sbp-cpp',
       input: ['SBP.proto'],
       output: ['SBP.pb.cc', 'SBP.pb.h'],
       command: [protoc, '--proto_path', '@CURRENT_SOURCE_DIR@', '--cpp_out', '@OUTDIR@', '@INPUT@'],
)

generated_module_cpp_proto = custom_target('gen-module-cpp',
       input: ['Module.proto'],
       output: ['Module.pb.cc', 'Module.pb.h'],
       command: [protoc, '--proto_path', '@CURRENT_SOURCE_DIR@', '--cpp_out', '@OUTDIR@', '@INPUT@'],
)


includes_generated = include_directories('.')

install_data(['backend.proto', 'ICP.proto', 'Module.proto', 'pbRPC.proto', 'SBP.proto'],
	install_dir: join_paths(get_option('datadir'), 'ogon', ogon_version[0], 'protobuf')
)
