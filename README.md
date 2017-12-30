Ansible Django Webapp Prepare Host Role
=======================================

Installs the necessary packages and services on a host for running a Django application and their deployment scripts.

This Ansible role performs the following:

* it creates a deployment user and installs its public key for remote login. The user will then be allowed to log in via ssh (or scp
  an archive), and deploy a new version of the Django application via a script (see role )
* it installs the necessary packages such as `NGINX` or `Apache`, `uWSGI` (and `pip`, `virtualenv` for python2)
* it gives the deployment user the permissions to restart `uWSGI`


Requirements
------------
Currently works (tested) only on Ubuntu, but should be easily adaptable to any other Linux variant.

Role Variables
--------------

|variable|default|meaning|
|----------|---------|---------|
|`django_deployment_user` | **required** | the user that will perform the deployments |
|`webserver`| `nginx` | the type of webserver serving the application (in front of uWSGI). Supported values are `apache2` and `nginx`|
|`django_deployment_user_ssh_public_key`| **required** | the ssh key of the deployment user|
|`host_additional_packages`| `[]` | additional packages to install on the host, if your web application needs eg. `rabbitmq`|
|`python_major`| **required** (defaults to `2`) | Major version of python|

After deployment, the user will not be allowed to change *his* home folder content.

### Notes
This role is just a preliminary host setup for the `raffienficiaud.ansible-django-webapp-deployment-role` role. 
Some design choices:

* the design is such that it is possible to deploy several applications on the same server
* the link between the web server and uWSGI is through Unix sockets (better performances)
* the role uses uWSGI for making the link between the webserver (Apache or NGinx) and the Django application. Only Debian/Ubuntu
  packages (uWSGI, NGinx/Apache) is supported.
* the role has support for both python2 and python3. Only required packages are installed by this role. For Python3 only versions 
  that have support for packages `venv` and `pip` are supported (`>= python 3.3`).
* django 2.0+ requires python3
* the SSH key can be installed later, depending on the needs, it should only be able to execute the deployment script and copy files
  to a version store on the server.


Dependencies
------------

None.


License
-------

BSD

Author Information
------------------

Any comments on the Ansible, PR or bug reports are welcome from the corresponding Github project.
