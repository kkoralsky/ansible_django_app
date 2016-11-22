Django app
==========


Ansible role to pull and setup Django app ready to serve.

Requirements
------------

Make sure that you pasted SSH public key for given user when accessing git repo
via SSH.

Role Variables
--------------

basic (inherited from `django_common`)

- `app` - app label (base directory); required
- `app_name` - name of Django app defaults to `{{ app }}`, used only if you need to
    have couple applications on the same host

Git repo

- `git_repo` - address to git repo (required)
- `branch` - branch to pull from (default: `master`)

venv

- `py_ver` - python major version: either 2 or 3 (default: 3)
- `requirements` - path to requirements.txt file relative to project repo
- `force_venv` - force (re)creation of venv; default: `no`

Django

- `settings_tpl` - path to settings template; check `templates/_default_settings.py.j2` for default
- `db_host`, `db_port`, `db_name`, `db_pass` - database connection details; used in (default) settings template
- `secret` - value for `SECRET_KEY` in (default) settings template
- `force_manage` - if true, django manage.py's `compilemessage`, `collectstatic` & `migrate` is performed
    even if no change in git repo was made
- `fixtures` - list of fixtures to apply; if empty or undefined, step is omitted


Dependencies
------------

- https://github.com/xkoralsky/django_common.git

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
