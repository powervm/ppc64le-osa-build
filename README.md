=================
ppc64le-osa-build
=================

A repository of playbooks for performing builds of various dependencies
needed for ppc64le-based installations of OpenStack-Ansible

Setup
=====

Hosts
-----

Before running this playbook, you'll need a ppc64le-based system to perform the build
on up and running Ubuntu 16.04 LTS. It must also have the following packages installed:

* openssh-server
* python

Ansible
-------

This repo is designed to be run from a remote host running Ansible. To get started,
make sure Git is installed on your system, clone this repository, then install
Ansible on the system. There are various methods for installing Ansible documented
at:

[Installing Ansible](http://docs.ansible.com/ansible/intro_installation.html)

SSH Keys and SSH Agent
----------------------

Ansible heavily uses SSH keys as a way to avoid password-based authentication with systems.

If you don't have an existing system for distributing ssh keys to your servers, you can
distribute your SSH keys onto systems to be managed using ssh-copy-id as follows:

 ssh-copy-id username@build-hostname.domainname

Once you've deployed your SSH keys to the nodes to be managed, you'll also want
to use ssh-agent to manage your passphrase for multi-node deployments. Installation
will vary per platform, but once installed, run::

 ssh-agent bash
 ssh-add [path-to-your-rsa-private-key]

Running this before running Ansible commands will allow you to only enter your passphrase
once per session, rather than once for every time ansible connects to a remote server.

Usage
=====

To run this repo against one or more Ubuntu installs, perform the following steps:

* Copy the 'build-hosts.yml.example' file to 'build-hosts.yml'
* Edit the build-hosts file to contain the connection information for your host(s)
* Run 'ansible-playbook <build-playbook>.yml -i build-hosts.yml'

Ansible will then remotely connect to your Ubuntu installs over SSH and perform the build
and copy the built files back to your host (by default to the /tmp directory).
