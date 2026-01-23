configure_file(input: 'ogon-rdp-server.service.in',
	output: 'ogon-rdp-server.service',
	format: 'cmake',
	configuration: cdata,
	install: true,
	install_dir: join_paths(get_option('sysconfdir'), 'systemd', 'system')
)
configure_file(input: 'ogon-session-manager.service.in',
	output: 'ogon-session-manager.service',
	format: 'cmake',
	configuration: cdata,
	install: true,
	install_dir: join_paths(get_option('sysconfdir'), 'systemd', 'system')
)

configure_file(input: 'config.ini.debian.in',
	output: 'config.ini.debian',
	configuration: cdata,
	install_dir: ogon_cfg_path
)

configure_file(input: 'config.ini.fedora.in',
	output: 'config.ini.fedora',
	configuration: cdata,
	install_dir: ogon_cfg_path
)

configure_file(input: 'debian-deploy-script.sh.in',
	output: 'debian-deploy-script.sh',
	configuration: cdata,
	install_dir: get_option('sbindir')
)

if get_option('with_openh264')
	configure_file(input: 'ogon-get-openh264-codec.in',
		output: 'ogon-get-openh264-codec',
		configuration: cdata,
		install_dir: get_option('sbindir')
	)
endif

configure_file(input: 'ogon-session-manager.init.in',
	output: 'ogon-session-manager.init',
	configuration: cdata
)
configure_file(input: 'ogon-rdp-server.init.in',
	output: 'ogon-rdp-server.init',
	configuration: cdata
)

install_data('ogonXsession', install_dir: ogon_cfg_path)
install_data('ogon_cleanup.sh', install_dir: ogon_cfg_path)

pam_d_dir = join_paths(get_option('sysconfdir'), 'pam.d')
install_data('pam.d/ogon.debian', install_dir: pam_d_dir)
install_data('pam.d/ogon.fedora', install_dir: pam_d_dir)
install_data('pam.d/ogon.suse', install_dir: pam_d_dir)

