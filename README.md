borgbackup
=========

Install and configure the Borg backup application for Linux

Requirements
------------

This role currenly works for Debian-based systems. It will install the necessary packages, create directories, and initialize the repo.

Role Variables
--------------

- borbackup_group: Group for files and directories
    - Default: borgbackup

- borgbackup_user: User for files and directories
    - Default: borgbackup

- borgbackup_config_dir: Directory for configuration files
    - Default: /etc/borgbackup/

- borgbackup_log_dir: Directory for log files
    - Default: /var/log/borgbackup/

- borgbackup_repo: Directory for repo (backup files)
    - Default: /etc/borgbackup/repo/

- borgbackup_passphrase: **Secret** Encryption passphrase for backup files
    - Default: *none*

- borgbackup_include_paths:
    - Default: /home

- borgbackup_exclude_patterns: PATTERNS to exclude from backup. See ```borg help patterns``` for details.
    - Default: *none*

Defaults
--------

The default configuration file, template ```borg_config.j2``` renders to the execution script ```backup-script.sh``` in the ```borgbackup_config_dir```. This script backs up specified directories and will prune at the weekly, monthly, and yearly level. Backups and pruning runs daily from the borgbackup user's crontab. Future iterations will add the ability to modify run and prune scheduling.

Dependencies
------------

None


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

[Ed Summers](https://blog.edwinsummers.net)