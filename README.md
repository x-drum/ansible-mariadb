ansible-mariadb
=========

This role installs and configures MariaDB - An enhanced, drop-in replacement for MySQL.

Supported Platforms
-------------------

* RHEL 6
* FreeBSD 10

It will likely run on other platforms, just drop in vars/ a new file to support your os variant, vars are parsed in the following order/format:
* {{ ansible_distribution }}_{{ ansible_distribution_major_version }}.yml
* {{ ansible_distribution }}.yml
* {{ ansible_os_family }}_{{ ansible_distribution_major_version }}.yml
* {{ ansible_os_family }}.yml"

Requirements
------------

* For FreeBSD a working pkgng setup is required (see: https://www.freebsd.org/doc/handbook/pkgng-intro.html )


Role Variables
--------------

By default this role will install MariaDB and provide a minimal (global) configuration, however variables can be passed to this role
and configuration can be overridden, for additional informations please have a look to **defaults/main.yml**


Dependencies
------------

None at this time.

Examples
----------------

1) Just install MariaDB, use the defaults
```yaml
- hosts: all
  remote_user: root
  sudo: no
  roles:
    - { role: mariadb }
```

2) Install MariaDB, customize bind address, listen port, root password and a few memory settings
```yaml
- hosts: all
  remote_user: root
  sudo: no
  vars:
    - mariadb_bind_address: 192.168.1.1
    - mariadb_port: 3309
    - mariadb_root_password: Sup3rs3cret
    - mariadb_key_buffer_size: 16K
    - mariadb_max_allowed_packet: 1M
    - mariadb_table_open_cache: 4
    - mariadb_sort_buffer_size: 64K
    - mariadb_read_buffer_size: 256K
  roles:
    - { role: mariadb }
```

3) Install MariaDB, using a custom, user provided, template
```yaml
- hosts: all
  remote_user: root
  sudo: no
  vars:
    mariadb_conf_server: templates/mariadb_production_template.j2
  roles:
    - { role: mariadb }
```

License
-------

GPLv2

Author Information
------------------

Alessio Cassibba (x-drum) http://blog.zerodev.it.
