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
| `phpfpm__pool_defaults_username`           | www-data                                 | Set default username for pools. |
| `phpfpm__pool_defaults_max_children`       | 100                                      | Set default maximum number of child processes to be created for pools. |
| `phpfpm__pool_defaults_min_spare_servers`  | 2                                        | Set default desired minimum number of idle server processes for pools. |
| `phpfpm__pool_defaults_max_spare_servers`  | 10                                       | Set default desired maximum number of idle server processes for pools. |
| `phpfpm__pool_defaults_enable_slowlog`     | `false`                                  | Set default for slowlog for pools. |
| `phpfpm__pool_defaults_open_basedir`       | `see phpfpm_pool_defaults_open_basedir`  | Set default open_basedir for pools. |


### Pools
| Name                           | Default Value                                   | Description                        |
|--------------------------------|-------------------------------------------------|------------------------------------|
| `name`                         | ""                                              | Set the name for the PHP FPM Pool. |
| `username`                     | `{{ phpfpm__pool_defaults_username }}`          | Set the username for the PHP FPM Pool. |
| `max_children`                 | `{{ phpfpm__pool_defaults_max_children }}`      | Set the maximum number of child processes to be created. |
| `start_servers`                | `see start_servers - Defaults`                  | Set the number of child processes created on startup. |
| `min_spare_servers`            | `{{ phpfpm__pool_defaults_min_spare_servers }}` | Set the desired minimum number of idle server processes. |
| `max_spare_servers`            | `{{ phpfpm__pool_defaults_max_spare_servers }}` | Set the desired maximum number of idle server processes. |
| `open_basedir`                 | `{{ phpfpm__pool_defaults_open_basedir }}`      | Set the open_basedir for the PHP FPM Pool. |
| `enable_redis_session_handler` | `false`                                         | Enable redis session handler for the PHP FPM Pool. |
| `redis_uri`                    | []                                              | List of redis uri's for the PHP FPM Pool. |
| `enable_slowlog`               | `{{ phpfpm__pool_defaults_enable_slowlog }}`    | Enable slowlog for the PHP FPM Pool. |
| `additional_php_admin_values`  | []                                              | List of additional php_admin_values for the PHP FPM Pool. |

#### start_servers - Defaults
  "{{{ pool.min_spare_servers + (pool.max_spare_servers - pool.min_spare_servers) / 2 }}"

### phpfpm__pool_defaults_open_basedir - Defaults
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
