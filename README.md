## A Demo Role for a Demo Flask Application running on Gunicorn and Nginx 

This is just a side project that I am working on to learn how to create my own Ansible-Galaxy role. You can also use the `Vagrantfile` to provision your Vagrant environment. This deployment will bind the gunicorn to `:8000` with wsgi and then proxy the requests from `:80` with nginx.
**Note:** This role will only work on Ubuntu 14.04

### Getting Started

This README file is inside a folder that contains a `Vagrantfile`, which tells Vagrant how to set up your virtual machine in VirtualBox.

To use the vagrant file, you will need to have done the following:

  1. Download and Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  2. Download and Install [Vagrant](https://www.vagrantup.com/downloads.html)
  3. Install [Ansible](http://docs.ansible.com/intro_installation.html)
  4. Open a shell prompt (Terminal app on a Mac and cmd on Windows) and cd into the folder containing the `Vagrantfile`

### Setting up your hosts file

You need to modify your host machine's hosts file (Mac/Linux: /etc/hosts; Windows: %systemroot%\system32\drivers\etc\hosts), adding the line below:

192.168.33.33  flaskapp

(Where flaskapp) is the hostname you have configured in the Vagrantfile).

### How to use the role
You can download or clone this project and then place it under '/etc/ansible/roles' and use it as a role in your projects.

### Role Variables

These are the important variables on 'defaults/main.yml'

`project_name:` Default is `flaskapp`. You should change this parameter to your own application name. This will make it easier to troubleshoot after deployment.

`project_path:` Default is `home/ubuntu/flaskapp`. You should change this parameter to your own application path or if you are going to use the test application `flaskapp` under `tests`, you should move or copy it to `/home/ubuntu`.

If you're going to use this role for provisioning Ansible, please change this path to your synced folder so you can work on your project on your own OS and Vagrant together.

`venv_path:` Default is `home/ubuntu/flaskapp/flaskappenv`. If you are going to use the test application `flaskapp` under `tests`, you should move or copy it to `/home/ubuntu`.

### Example Playbook

You can test the role with `test/inventory` and `test/test.yml` and the `flaskapp` I've written just to see if the ansible deployment is working.

### License

MIT
