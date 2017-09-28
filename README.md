Ansible Django Webapp Prepare Host Role
=======================================

Installs the necessary packages and services on a host for running a Django application and their deployment scripts.

This Ansible role performs the following:

* it creates the deployment user and installs its public key for remote login
* it installs the necessary packages such as `NGINX` or `Apache`, `uWSGI`, `pip`, `virtualenv` (depending on the choosen configuration)
* it gives the deployment user the permissions to restart `uWSGI`


Requirements
------------
Currently works (tested) only on Ubuntu, but should be easily adaptable to any other Linux variant.

Role Variables
--------------

|variable|default|meaning|
|----------|---------|---------|
|django_deployment_user | **required** | the user that will perform the deployments |
|webserver| `nginx` | the type of webserver serving the application (in front of uWSGI). Supported values are `apache2` and `nginx`|
|django_deployment_user_ssh_public_key| **required** | the ssh key of the deployment user|
|host_additional_packages| `[]` | additional packages to install on the host, if your web application needs eg. `rabbitmq`|

After deployment, the user will not be allowed to change *his* home folder content.

### Notes
This role is just a preliminary role for the `ansible-django-webapp-deployment-role` role. It can be improved in the following ways:

* the SSH key can be installed later, depending on the needs, it should only be able to execute the deployment script and copy files
  to a version store on the server.
* the design is such that it is possible to deploy several applications on the same server

Dependencies
------------

None.


License
-------

BSD

Author Information
------------------

Any comments on the Ansible, PR or bug reports are welcome from the corresponding Github project.
