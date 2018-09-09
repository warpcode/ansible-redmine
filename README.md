Ansible Redmine Role
=========

Ansible role for installing redmine.

Requirements
------------

This role is setup to install redmine for Ubuntu servers.

This role by default uses sqlite. You must setup your own mysql/postgres server if you wish to use a different database

This role does not setup a http server.

Role Variables
--------------

| Variable                       | Default                               | Comments                                                              |
| :---                           | :---                                  |:---                                                                   |
| `redmine_create_user_and_group`| true                                  | Whether to create the user and group in this role                     |
| `redmine_path_owner`           | redmine                               | Default user to own the installation                                  |
| `redmine_path_group`           | redmine                               | Default group to own the installation                                 |
| `redmine_git_url`              | https://github.com/redmine/redmine.git| Path to the redmine github repo                                       |
| `redmine_version`              | 3.4-stable                            | Git branch to checkout                                                |
| `redmine_path`                 | /var/lib/redmine                      | Path to install redmine                                               |
| `redmine_db_driver`            | sqlite3                               | DB driver to use. Can also use mysql2 or postresql                    |
| `redmine_db_database`          | db/redmine.sqlite3                    | If sqlite, specify path. Can be relative to redmine_path or a db name |
| `redmine_db_host`              | null                                  | Host address. Required if using other than sqlite3                    |
| `redmine_db_user`              | null                                  | DB user. Required if using other than sqlite3                         |
| `redmine_db_pass`              | null                                  | DB password. Required if using other than sqlite3                     |

Dependencies
------------

No Dependencies

License
-------

BSD
