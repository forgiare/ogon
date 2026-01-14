
mod_pam = library('ogon-auth-pam',
	'pam_auth.c',
	'pam_auth.h',
	include_directories: [includes_version, includes_ogon, '.'],
	dependencies: [deps_winpr, deps_freerdp, deps_pam ],
	install: true,
	install_dir: join_paths(ogon_app_lib_path, 'auth')
)