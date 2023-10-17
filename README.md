# OpenVPNScripts

scripts and templates to create and manage OpenVPN in five different configurations, without and with MFA (multi-factor authentication)
- 'openvpn_server_check_ldap_login.conf' check only (Open-)LDAP login and assword of users
- 'openvpn_server_check_cert_and_openvpn-auth-ldap.so.conf' check (Open-)LDAP login and password (via openvpn-auth-ldap.so) of users and any valid certificate
- 'openvpn_server_check_cert_and_auth-user-pass-verify.conf' check (Open-)LDAP login and password (via patched auth-ldap-with-pam.pl) and if the certificate has the same login name
- 'openvpn_server_check_ldap_login_and_totp.conf' check (Open-)LDAP login and password (via openvpn-auth-ldap.so) and (normmaly every hour) a (time based) one-time password
- 'openvpn_server_check_ldap_login_and_cert_and_totp.conf' check (Open-)LDAP login and password (via openvpn-auth-ldap.so) of users and any valid certificate and (normmaly every hour) a (time based) one-time password

## folders

- 'scripts' ... a lot of scripts to create configurations, manage certificates and one-time password authetification
- 'client_templates' ... templates for OpenVPN client configurations
- 'server_configurations' ... some files for the OpenVPN and the Apache server

## dependings

- all users should have an local account (by using a configured OpenLDAP server)
- the OpenVPN server should be avaliable (feel free to change the port numbers and protocol type)
- you should change the settings for the scripts, templates and configurations

# notes

- you should patch the file /usr/share/doc/openvpn/examples/sample-scripts/auth-pam.pl with the 'auth-ldap-with-pam.pl.patch' (patch .../auth-pam.pl .../auth-ldap-with-pam.pl.patch)
- try "apt install openvpn" or download the package from https://packages.debian.org/bookworm/openvpn to get the file 'auth-pam.pl'
- you need the package "libauthen-pam-perl" to use the authentification agains 'auth-pam.pl'
- please configure your MFA method in 'auto_manage_accounts'
- after setup a cronjob the script auto_manage_accounts should automatically create, revoke and reactivate client access, based on the users of the defined unix group 
- users should can download configurations files, after login on "https://vpn.example.org/~login/configuration"
- depending on the configuration, you need not all files and scripts
