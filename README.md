# Vagrant/Ansible LEMP Playbook

Creates a blank LEMP box for local and production use.

This repo was created for my own personal use and may not be ideal for your own setup.

The [Ansible Documentation](http://docs.ansible.com/intro.html) is a great place to start on the basics of using Ansible for provisioning.

You can also see the [Vagrant Documentation](http://docs.vagrantup.com/v2/provisioning/ansible.html) on using Ansible with Vagrant.

## Getting Started

Rename `group_vars/all.yml.example` to `group_vars/all.yml` and edit this file to configure common variables.

Run the playbook against your host.

## Creating encrypted user passwords

Taken from the Ansible documentation: http://docs.ansible.com/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module.

    $ pip install passlib

Once the library is ready, SHA512 password values can then be generated as follows:

    $ python helpers/encrypt.py password_goes_here

Copy/paste the generated string into the variable file.
