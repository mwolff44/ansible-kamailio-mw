kamailio-mw
=============

[![Build Status](https://travis-ci.org/mwolff44/kamailio-mw.png)](https://travis-ci.org/mwolff44/kamailio-mw)
[![Galaxy](http://img.shields.io/badge/galaxy-mwolff44.kamailio--mw-blue.svg?style=flat-square)](https://galaxy.ansible.com/mwolff44/kamailio-mw)


Ansible role for Kamailio

Requirements
------------

- Tested on Ansible 2.0 or higher.

Ansible installation via pip
----------------------------


    sudo apt-get install -y ansible


You can also use the script supplied with this role :


    chmod +x ansible_install.sh && ./ansible_install.sh


Role Variables
--------------

The role variables and default values.

### Kamailio

    kamailio_version: 50 # Kamailio version 5.0 . for 4.4 enter 44 and for 4.4 enter 43
    kamailio_conf_dir: '/etc/kamailio' # Configuration directory
    kamailio_install_conf: False # Allow the installation of the configuration files - Could be disabled when updating
    kamailio_conf_backup_dir: '/etc/kamailio.orig' # Backup configuration directory
    kamailio_config_template_dir: ../templates/config/ # Templates directory used for kamailio configuration
    kamailio_config_files:
        - kamailio.cfg
        - kamctlrc
    kamailio_packages:
        - kamailio
        - kamailio-extra-modules
        - kamailio-postgres-modules
        - kamailio-mysql-modules

    kamailio_restart: false # restart kamailio after update process


### Kamailio settings


    kamailio_create_db: false # does the script create the kamailio DB (the engine must be installed before)
    kamailio_creatordb_host: 'localhost' # the kamailio host that is risponsible of DB creation
    kamailio_sip_domain: 'kamailio.org'
    kamailio_db_engine: 'MYSQL' # check Kamailio doc for supported DB engine (PGSQL)
    kamailio_db_host: 'localhost'
    kamailio_db_port: 3306 # default for MySQL engine !
    kamailio_db_root_user: 'root'
    kamailio_db_root_pass: 'root' # root user password of DB
    kamailio_db_name: 'kamailio'
    kamailio_db_user: 'kamailio'
    kamailio_db_pass: 'kamailiopass'
    kamailio_db_user_ro: 'kamailio' # readonly user
    kamailio_db_pass_ro: 'kamailiopass' # readonly pass
    kamailio_rpcfifo_path: '/var/run/kamailio/kamailio_rpc_fifo'


### Fail2ban


    fail2ban_install: False # Default : fail2ban will not be installed
    fail2ban_local_jail_file: /etc/fail2ban/jail.local # fail2ban jail file for Kamailio
    fail2ban_filter_dir: /etc/fail2ban/filter.d # fail2ban filter directory
    fail2ban_local_jail: ../templates/fail2ban/jail.local # fail2ban template jail for Kamailio
    fail2ban_kamailio: ../templates/fail2ban/kamailio.conf # Fail2ban filter template for Kamailio


### Sngrep


    sngrep_install: False # Default : sngrep will not be installed


### Time sync with systemd


    ntp_install: False # Default : time sync will not be configured
    ntp_servers: '{{ ntp_servers_map[ansible_distribution]
                      | d(ntp_servers_map["default"]) }}'
    ntp_servers_map:
      'Debian':  [ '0.debian.pool.ntp.org', '1.debian.pool.ntp.org',
                   '2.debian.pool.ntp.org', '3.debian.pool.ntp.org' ]
      'Ubuntu':  [ '0.ubuntu.pool.ntp.org', '1.ubuntu.pool.ntp.org',
                   '2.ubuntu.pool.ntp.org', '3.ubuntu.pool.ntp.org' ]
      'default': [ '0.pool.ntp.org', '1.pool.ntp.org',
                   '2.pool.ntp.org', '3.pool.ntp.org' ]
    ntp_timezone: 'Europe/Paris'
    ntp_timesyncd_template : ../templates/etc/systemd/timesyncd.conf.d/ansible.conf.j2


Dependencies
------------

No

Usage
-----

Add `mwolff44.kamailio-mw` to your roles ans setup the variables in your playbook file. Example :


    - hosts: all
      vars_files:
        - 'defaults/main.yml'
      tasks:
        - include: 'tasks/main.yml'
      handlers:
        - include: 'handlers/main.yml'



License
-------


Licensed under the GPL v3 license. See the LICENSE file for details.


Issue
-----


The project is managed via github. To open a new issue : [https://github.com/mwolff44/kamailio-mw/issues]


Author Information
------------------

Mathias WOLFF / [Blog des télécoms](http://www.blog-des-telecoms.com) - [PyFreeBilling](https://www.pyfreebilling.com)
