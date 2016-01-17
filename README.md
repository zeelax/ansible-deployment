# hellofresh/ansible-deployment
[![Build Status](https://travis-ci.org/hellofresh/ansible-deployment.svg?branch=master)](https://travis-ci.org/hellofresh/ansible-deployment)

Ansible role to deploy applications.

### Role Variables
```yaml
---
## Deployment Information
# App name
deployment_name                     : "testApp"
# Where to get the code supported resolver ['github']
deployment_resolver                 : 'github'
# Git Resolver variables
deployment_git_repo                 : "git@github.com:hellofresh/ansible-deployment.git"
deployment_git_user                 : "{{ ansible_ssh_user }}"
# Version depands on resolver. If your using github as a resolver version could be branch/tag/git 40 char hash
deployment_version                  : "master"

## Deployment user/group and directroy
deployment_user                     : "{{ ansible_ssh_user }}"
deployment_group                    : "{{ ansible_ssh_user }}"
deployment_user_home                : "/home/{{ deployment_user }}"
deployment_base_dir                 : "{{ deployment_user_home }}/{{ deployment_name }}"
# Directory structure 
deployment_work_dir                 : "{{ deployment_base_dir }}/{{ deployment_version }}"
deployment_current_dir              : "{{ deployment_base_dir }}/current"
deployment_temp_dir                 : "/tmp/ansible-deployment/{{ deployment_version }}" 

## Config option
#  Shell environment variable 
deployment_env_vars                 : "none" # Variables that define the config
deployment_config_env_file          : "{{ deployment_base_dir }}/{{ deployment_name }}_environment.sh"
deployment_shell_init_file          : "{{ deployment_user }}/.bashrc" 
#  INI variable 
deployment_ini_vars                 : "none" # Variables that define the config
deployment_config_ini_vars_dest     : "{{ deployment_base_dir }}/{{ deployment_name }}_config.ini"

## Dependency managment
#deployment_dependency               : "composer"
#deployment_dependency_composer_args : 
#                        working_dir : "{{ deployment_work_dir }}"
#                        command     : "install"
#

## Cron jobs 
deployment_cron_jobs                : "none"
# TODO: Make an example of cron jobs


## By default you deploy once and to override you must pass true to force deployment 
deployment_force                    :  false
deployment_guard_file               :  "/var/local/deployment_first_boot_file"

````

### Contributors
* [Alfonso Fernandez](https://github.com/alfonsodev)
* [Adham Helal](https://github.com/ahelal)
* [Sergio Sola] (https://github.com/ssola)

### Todo
- Implement handler to restart/reload application
- Implement Post deployment checks


