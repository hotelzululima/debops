DebOps installation instructions
================================

DebOps is designed to be used with multiple hosts, physical, virtual or
containers. The remote hosts are managed from "Ansible Controller" host, where
the administrator issues commands. This host can also be managed by DebOps if
it's set up on a compatible platform, that is a Debian or Ubuntu OS.

Requirements
------------

These are the software requirements for an Ansible Controller host:

- Bash 4.0+

- Python 2.7+

- Ansible 2.3+

- Python ``netaddr`` and ``passlib`` library

- EncFS and GPG for encrypted :file:`secret/` directory support (optional)

On the remote host side, DebOps is designed to work against a Debian
``netinst`` installation with OpenSSH server installed.


Debian GNU/Linux notes
----------------------

DebOps requires a current stable release of Ansible, at the moment ``v2.4.0+``.
The ``ansible`` package provided in your Linux distribution might not be
sufficient, for example Debian Stretch release includes
`ansible v2.2.1 package <https://packages.debian.org/stretch/ansible>`__
which will not work correctly with DebOps. You might consider installing
Ansible from ``stretch-backports`` repository, install current stable release
from PyPI or build a ``.deb`` package from source and install it manually.


Installation in a Python virtualenv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can install Ansible and DebOps in a Python :command:`virtualenv`
environment. These instructions are for Debian Jessie or Debian Stretch, they
should also work in Ubuntu.

.. code-block:: console

   sudo apt-get install python-virtualenv virtualenv build-essential \
                        python-dev libffi-dev libssl-dev
   virtualenv debops-venv
   cd debops-venv
   source bin/activate
   pip install --upgrade setuptools
   pip install ansible debops

   # Install or update roles and playbooks
   debops-update

After DebOps is installed, you might want to create symlinks to the ``debops``
scripts in :file:`/usr/local/bin/` to make the commands available outside of
the the Python virtual environment:

.. code-block:: console

   ln -s debops-venv/bin/ansible          /usr/local/bin/ansible
   ln -s debops-venv/bin/ansible-playbook /usr/local/bin/ansible-playbook
   ln -s debops-venv/bin/debops           /usr/local/bin/debops
   ln -s debops-venv/bin/debops-init      /usr/local/bin/debops-init
   ln -s debops-venv/bin/debops-update    /usr/local/bin/debops-update
   ln -s debops-venv/bin/debops-defaults  /usr/local/bin/debops-defaults
