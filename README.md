# ansible-huginn

Ansible Playbook to install Huginn from source



## About

[Huginn](https://github.com/huginn/huginn) is an automating agent, which allows you to run all kind of tasks on your behalf.

The Huginn [installation instructions](https://github.com/huginn/huginn/tree/master/doc/manual) specifically require a Ruby installation from source. This Playbook installs both Ruby and Huginn.

If possible, install all of this into a separate virtual machine or container.



## Usage

Check out this reporitory into your "roles/" directory:
```
cd roles
git clone https://github.com/andreasscherbaum/ansible-huginn.git
```

Then use this role in your Playbook:
```
- hosts: containers-huginn
  become: yes
  gather_facts: True
  any_errors_fatal: True
  force_handlers: True
  roles:
    - ansible-huginn

```


## Path names

The Playbook can create a OS user and group with the name "huginn".

The Playbook expects to have "/home/huginn" available as home directory.



## Configuration

The role will not work with default settings. You have to set a Rails Secret Token for the application, and change the database password.

The defaults are specified in "_defaults/main.yml_", copy the settings from there to either "_vars/main.yml_" or set the variables on your _hosts.cfg_.

Note: if you clone this repository, it is best practice not to commit credentials into a repository.



## Database

The Huginn installation uses a MySQL database by default, MariaDB works as well. This Playbook creates the database, if it does not exist. Sufficient database permissions are required.

You can pre-create the database, the Playbook will then skip this step.



## Invitation code

This Playbook changes the default invitation code used by Huginn. A new code is generated, and placed in "_huginn_invitation_code.txt_ in the Playbook directory. Change the file location by overriding the variable "_huginn_invitation_code_".



## Backups

Make sure you regularly backup the database!

This task is not included in this Playbook.



## More

I blogged about a couple things I found out while using Huginn.

Check my [blog here](https://andreas.scherbaum.la/blog/plugin/tag/Huginn).
