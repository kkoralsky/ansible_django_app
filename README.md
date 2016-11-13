Django uWsgi container
======================


Django app in uWsgi container

Requirements
------------

Make sure that you pasted SSH public key for given user when accessing git repo
via SSH.

Role Variables
--------------

basic

- `app` - name of Django app to install - preferably - a git repo name

Git repo

- `git_repo` - address to git repo (required)
- `branch` - branch to pull from (default: `master`)

venv

- `py_ver` - python major version: either 2 or 3 (default: 3)
- `requirements` - path to requirements.txt file relative to project repo

Django

- `django_settings_module` - defaults to `www.settings`
- `settings_template` - path to settings template; check `templates/_default_settings.py.j2` for default
- `db_host`, `db_port`, `db_name`, `db_pass` - database connection details (used in default template)

uWsgi customization

- `uwsgi_ini_template` - uwsgi.ini template; check `templates/_default_uwsgi.ini.j2` for default one
- `uwsgi_host` - defaults to `127.0.0.1` (used in default template)
- `uwsgi_port` - defaults to `8000` (used in default template)


Dependencies
------------

- `xkoralsky.debian_common`

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: django_uwsgi
          git_repo: https://github.com/xkoralsky/sample.git
          branch: develop
          deployment_key: ~/deployments/sample_deployment.pub

License
-------

BSD
