# OpenVPNScripts

scripts and templates to create and manage OpenVPN in different configurations

## folders

- 'scripts' ... scripts to create configurations, manage certificates and oaths to add, revoke or reactivate clients
- 'client_templates' ... templates for OpenVPN client configurations
- 'server_configurations' ... some files for the OpenVPN and the Apache server

## dependings

- all users should have an local account (by using a configured OpenLDAP server)
- the OpenVPN server should be avaliable (feel free to change the port numbers and protocol type)
- you should change the settings in the scripts, templates and configurations

# notes

- the script auto_manage_accounts should create, revoke and reactivate client configuration files
- users should download here configurations files, after login on https://.../configuration
- you should use a self signed CA for the certificates