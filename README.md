# OpenVPNScripts

## configuration examples
- 'openvpn_server_check_ldap_login.conf' check only (Open-)LDAP login and password of users
- 'openvpn_server_check_cert_and_openvpn-auth-ldap.so.conf' check (Open-)LDAP login and password (via openvpn-auth-ldap.so) of users and any valid certificate
- 'openvpn_server_check_cert_and_auth-user-pass-verify.conf' check (Open-)LDAP login and password (via patched auth-ldap-with-pam.pl) and check that the user certificate has the same login name
- 'openvpn_server_check_ldap_login_and_totp.conf' check (Open-)LDAP login and password (via openvpn-auth-ldap.so) and (normmaly every hour) the (time based) user one-time password
- 'openvpn_server_check_ldap_login_and_cert_and_totp.conf' check (Open-)LDAP login and password (via openvpn-auth-ldap.so) of users and the certificate and (normmaly every hour) the (time based) one-time password

## scripts
- 'add_user_oath' ................... create a TOTP secret for a account
- 'auto_manage_accounts' ............ check local users and create, enable or disable VPN accounts
- 'config.cfg' ...................... the configuration file for this scripts
- 'create_client_certificate' ....... create new client certificates for the VPN account
- 'create_client_configuration' ..... create new VPN configuration files for a account
- 'create_root_ca' .................. create the first root CA of the VPN service
- 'create_server_certificate' ....... create the VPN server certificate
- 'del_user_oath' ................... remove a TOTP secret for a account
- 'delete_certificate' .............. remove a client certificate of a VPN account
- 'disable_user_oath' ............... disable a TOTP secret for a account
- 'enable_user_oath'  ............... enable a TOTP secret for a account
- 'reactivate_certificate' .......... reactivate a revoked client certificate
- 'revoke_and_rename_certificate' ... revoke a client certificate and move all files away to allow creating a new one
- 'revoke_certificate' .............. revoke a client certificate an keep it for reactivation
- 'show_client_certificate' ......... show information from the client certificate

## folders
- 'scripts' ... a lot of scripts to create configurations, manage certificates and one-time password authentification
- 'client_templates' ... templates for OpenVPN client configurations
- 'server_configurations' ... some files for the OpenVPN and the Apache server

## dependings
- all users should have an local account (by using a configured OpenLDAP server)
- the OpenVPN server should be avaliable (feel free to change the port numbers and protocol type)
- you should change the settings for the scripts, templates and configurations

# notes
- for checking user certificates, you should patch the file /usr/share/doc/openvpn/examples/sample-scripts/auth-pam.pl with the 'auth-ldap-with-pam.pl.patch' (patch .../auth-pam.pl .../auth-ldap-with-pam.pl.patch)
- try "apt install openvpn" or download the package from https://packages.debian.org/bookworm/openvpn to get the file 'auth-pam.pl'
- you need the package "libauthen-pam-perl" to use the authentification agains 'auth-pam.pl'
- please configure your MFA method in 'auto_manage_accounts'
- after setup a cronjob the script auto_manage_accounts should automatically create, revoke and reactivate client access, based on the users of the defined unix group
- configure your webserver that, users can download her configurations files, after (htaccess protected) login on "https://vpn.example.org/~login/configuration"
- depending on the configuration, you need not all files and scripts