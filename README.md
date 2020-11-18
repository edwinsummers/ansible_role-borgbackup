borgbackup
=========

Install and configure the Borg backup application for Linux

Requirements
------------

This role currenly works for Debian-based systems. It will install the necessary packages, create directories, and initialize the repo.

Role Variables
--------------

|Name|Description|Default|Required|
|:---|:---|:---|:---:|
|borgbackup_group|Group for borgbackup files and directories|`root`|no|
|borgbackup_gid|Group ID for borgbackup group||no|
|borgbackup_user|User for borgbackup process and files|`root`|no|
|borgbackup_uid|User ID for borgbackup user||no|
|borgbackup_config_dir|Directory for borgbackup configuration files|`/etc/borgbackup`|no|
|borgbackup_log_dir|Directory for borgbackup log files|`/var/log/borgbackup`|no|
|borgbackup_repo|Directory for backup repository|`/etc/borgbackup/repo/`|no|
|borgbackup_passphrase|**secret** Encryption passphrase for backup files *ansible-vault recommended*||no|
|borgbackup_include_paths|Space-delimited list of paths to include in backups (use folded string '>')|`/home`|no|
|borgbackup_exclude_patterns|`PATTERNS` to exclude from backup. See `borg help patterns` for details.||no|

Defaults
--------

The default configuration file, template ```borg_config.j2``` renders to the execution script ```backup-script.sh``` in the ```borgbackup_config_dir```. This script backs up specified directories and will prune at the weekly, monthly, and yearly level. Backups and pruning runs daily from the borgbackup user's crontab. Future iterations will add the ability to modify run and prune scheduling.

Dependencies
------------

None


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - hosts: linux_hosts
      become: true

      tasks:
        - name: "include role - borgbackup"
          include_role:
            name: borgbackup


Additional Information
----------------------

Consult the [Borgbackup documentation](https://borgbackup.readthedocs.io "ReadtheDocs") for additional information on usage such as include paths, exclude patterns, etc.

Note that if a user other than the default `root` is desired, this user (or group) must have privileges to read all of the files/directories in `borgbackup_include_paths`.

License
-------

[MIT](https://choosealicense.com/licenses/mit/)

Author Information
------------------

[Ed Summers](https://blog.edwinsummers.net)
