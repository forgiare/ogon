subdir('icp')

ogon_sources = [
	'app_context.c',
	'backend.c',
	'channels.c',
	'encoder.c',
	'eventloop.c',
	'ogon.c',
	'frontend.c',
	'graphics.c',
	'peer.c',
	'PMurHash.c',
	'state.c',
	'rdpgfx.c',
	'openh264.c',
	'bandwidth_mgmt.c',
	'../common/procutils.c',
]

includes_ogon_server = include_directories('.', '../backend')

ogon_rdp_server = executable('ogon-rdp-server',
       sources: ogon_sources,
       include_directories: [includes_ogon_server, includes_ogon, includes_generated, includes_backend, includes_version],
       link_with: [ogon_backend_lib, ogon_icp_lib],
       dependencies: [deps_protobuf, deps_protobuf_c, deps_ssl, deps_freerdp_server, deps_freerdp, deps_winpr],
       install: true,
       install_dir: get_option('sbindir'),
       install_rpath: '$ORIGIN/../' + get_option('libdir'),
)

