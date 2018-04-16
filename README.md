Django app
==========


Ansible role to pull and setup Django app ready to serve.

Requirements
------------

Make sure that you pasted SSH public key for given user when accessing git repo
via SSH.

Role Variables
--------------

basic:

- `app` - app label (base directory); required
- `app_name` - name of Django app defaults to `{{ app }}`, used only if you need to
    have couple deployments for single app/repo

git repository

- `git_repo` - address to git repo (required)
- `branch` - branch to pull from (default: `master`)

venv

- `py_ver` - python major version: either 2 or 3 (default: 3)
- `requirements` - path to requirements.txt file relative to project repo
- `django_venv` - force (re)creation of venv; default: `no`

Django

- `django_settings_tpl` - path to settings template; it can be set to `_default_settings.py.j2`,
  or use it to roll your own
- `django_settings_module` - *dot seperated* python module holding settings for Django
- `db_host`, `db_port`, `db_name`, `db_pass` - database connection details; used in (default) settings template
- `secret` - value for `SECRET_KEY` in (default) settings template

manage.py

- `django_commands` - list of manage.py commands to run; by default this is:
  - compilemessages
  - collectstatic
  - syncdb
  - migrate
- `django_manage` - empty string is set by default, which means that commands are
  run only if changes in git were introduced; if set to true, even if no change in
  was made - commands are run, if false, no manage.py commands are run even if changes
  were made; 
- `django_fixtures` - list of fixtures to apply
- `django_admins` - list of dictionaries w/ `email`, `username` keys &
  optionally `user` & `pass` that will be used to set password for each given user
- `django_users` - list of dictionaries w/ `user`, `pass` keys for password set
- `django_ignore_manage_errors` - ignore manage.py's errors; this is true by default,
  due to the fact that password setup, adding admin users is not idempotent

OS

- `django_packges` - list of `.deb` packages that should be installed for venv & app 

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: django_app
          git_repo: https://github.com/xkoralsky/sample.git
          requirements: requirements.txt
          branch: develop

License
-------

BSD
