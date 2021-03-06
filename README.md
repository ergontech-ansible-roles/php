PHP Name
=========

Installs and configures PHP CLI and FPM

Role Variables
--------------

```
# Varialbes with default values
---

# Specify PHP version installable via the Onrej PPA for PHP
php_version: 5.6

# List extensions installed with the following pattern:
# php{{ php_version }}-{{ php_extension }}
php_extensions:
  - curl
  - cli
  - gd
  - mysql
  - redis
  - mcrypt
  - opcache
  - xdebug
  - xml

# Option to disable PHP FPM as a service
php_fpm_install: false


##################
# PHP CLI Settings
##################
php_disable_functions: ""
php_disable_classes: ""
# Resource Limits
php_max_execution_time: 30
php_max_input_time: 60
php_max_input_vars: 1000
php_memory_limit: -1
# Date
php_date_timezone: "etc/UTC"
# Errors
php_error_reporting: "E_ALL & ~E_DEPRECATED & ~E_STRICT"
php_display_errors: "Off"
php_display_startup_errors: "Off"
php_log_errors: "On"
php_error_log: "php_errors.log"
php_log_errors_max_len: 1024
php_track_errors: "Off"
# Uploads
php_upload_max_filesize: 2M
php_max_file_uploads: 20
php_post_max_size: 8M
# Opcache
php_opcache_enable: "0"
php_opcache_enable_cli: "0"
php_opcache_memory_consumption: 64
php_opcache_interned_strings_buffer: 4
php_opcache_fast_shutdown: "0"
php_opcache_max_accelerated_files: 2000
php_opcache_revalidate_freq: 2

# For additional options, use this variable
#php_additional_configuration:
#  - name:
#    value:

##################
# PHP FPM Settings
##################

# php.ini
# -------
# php-fpm will default to cli settings. Override with php_fpm_<setting_name>: <setting_value>
# example php_fpm_memory_limit: 256M
php_fpm_memory_limit: 128M

# www.conf
php_fpm_pm: dynamic
php_fpm_listen: "/run/php{{ php_version }}-fpm.sock"
php_fpm_max_children: 100
php_fpm_start_servers: 20
php_fpm_min_spare_servers: 20
php_fpm_max_spare_servers: 40
php_fpm_max_requests: 10000


# For fpm ini additional options, use this variable
#php_fpm_ini_additional_configuration:
#  - name:
#    value:

# For fpm www.conf additional options, use this variable
#php_fpm_www_additional_configuration:
#  - name:
#    value:
```


Usage
----------------

```
# requirements.yml

- src: https://github.com/ergontech-ansible-roles/php-role
  version: master
  name: php-base
```

Tags can be used to run only php-fpm or php-cli tasks

```
# example
$ ansible-playbook <playbook> -t php,php-fpm
```

License
-------

MIT

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

TODO's
------

- xdebug configuration
- multiple php-fpm pools