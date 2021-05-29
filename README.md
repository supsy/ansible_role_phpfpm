PHP FPM
=======

Installation for PHP FPM


Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Name                                       | Default Value                            | Description                    |
|--------------------------------------------|------------------------------------------|--------------------------------|
| `phpfpm__show_ansible_management`          | `false`                                  | Enable to show hint in ansible managed files. |
| `phpfpm__version`                          | ""                                       | Version for PHP FPM to install. |
| `phpfpm__timezone`                         | `Controller: /etc/timezone`              | Set timezone for PHP configuration. |
| `phpfpm__php_config_defaults_fpm_template` | php_config/90-defaults_fpm_ini.j2        | Jinja2 Template for PHP configuration under FPM runtime (/etc/php/{{ phpfpm__version }}/fpm/conf.d/{{ phpfpm__php_config_defaults_fpm_filename }}) |
| `phpfpm__php_config_defaults_fpm_filename` | 90-defaults.ini                          | Specify the PHP configuration settings filename for FPM. |
| `phpfpm__php_config_defaults_cli_filename` | php_config/90-defaults_cli_ini.j2        | Jinja2 Template for PHP configuration under CLI runtime (/etc/php/{{ phpfpm__version }}/cli/conf.d/{{ phpfpm__php_config_defaults_fpm_filename }}) |
| `phpfpm__php_config_defaults_cli_filename` | 90-defaults.ini                          | Specify the PHP configuration settings filename for CLI. |
| `phpfpm__additional_php_modules`           | []                                       | List of additional php modules to be installed. |
| `phpfpm__vhost_root`                       | /var/www/vhosts                          | Specify the default Vhost path as default for the FPM pool. |
| `phpfpm__pools`                            | []                                       | List of FPM Pools. See `Pools` definition below. |
| `phpfpm_pool_defaults_username`            | www-data                                 | Set default username for pools. |
| `phpfpm_pool_defaults_open_basedir`        | `see phpfpm_pool_defaults_open_basedir`  | Set default open_basedir for pools. |


### Pools
| Name                           | Default Value                             | Description                        |
|--------------------------------|-------------------------------------------|------------------------------------|
| `name`                         | ""                                        | Set the name for the PHP FPM Pool. |
| `username`                     | `{{ phpfpm_pool_defaults_username }}`     | Set the username for the PHP FPM Pool. |
| `open_basedir`                 | `{{ phpfpm_pool_defaults_open_basedir }}` | Set the open_basedir for the PHP FPM Pool. |
| `enable_redis_session_handler` | `false`                                   | Enable redis session handler for the PHP FPM Pool. |
| `redis_uri`                    | []                                        | List of redis uri's for the PHP FPM Pool. |
| `additional_php_admin_values`  | []                                        | List of additional php_admin_values for the PHP FPM Pool. |


### phpfpm_pool_defaults_open_basedir - Defaults
  "{{ phpfpm__vhost_root }}/$pool"
  /usr/share/php
  /tmp

Dependencies
------------

None.


Example Playbook
----------------

    - hosts: phpfpm
      vars_files:
        - vars/main.yml
      roles:
        - { role: phpfpm }

License
-------

MIT


Author Information
------------------

This role was created by Noles
