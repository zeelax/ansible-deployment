# hellofresh/ansible-deployment
[![Build Status](https://travis-ci.org/hellofresh/ansible-deployment.svg?branch=master)](https://travis-ci.org/hellofresh/ansible-deployment)

Ansible role to deploy applications.

### Role Variables
```yaml
---
# App name
deployment_name                     : "testApp"
# Version depands on resolver. If your using github as a resolver version could be branch/tag/git 40 char hash
deployment_version                  : "master"

# Where to get the code supported resolver ['none', github', 's3']
deployment_resolver                 : 'none'

## GIT Resolver
deployment_git_repo                 : "git@github.com:hellofresh/ansible-deployment.git"
deployment_git_user                 : "{{ deployment_user }}"
deployment_git_repo_dir             : "{{ deployment_dir_base }}/repo"
## when doing rollbacks do you want to force copy from GIT
deployment_git_repo_force_copy      : False

## S3 Resolver
deployment_s3_bucket                : "a_bucket"
deployment_s3_object_name           : "testApp-{{ deployment_version }}.tgz"
deployment_s3_object_path           : "" # Optional path
deployment_s3_art_dir               : "{{ deployment_dir_base }}/artifacts"
deployment_s3_aws_key_id            : "{{ lookup('env','AWS_ACCESS_KEY_ID') }}"
deployment_s3_aws_secret_key        : "{{ lookup('env','AWS_SECRET_ACCESS_KEY') }}"

## Deployment user/group and directroy
deployment_user_manage              : False
deployment_user                     : "{{ lookup('env','USER') }}"
deployment_group                    : "{{ deployment_user }}"
deployment_user_shell               : "/bin/bash"
deployment_user_home                : "/home/{{ deployment_user }}"
# Set known hosts for ssh
deployment_user_manage_fingerprints : False
deployment_user_fingerprints        :
    - "bitbucket.org,131.103.20.167 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAubiN81eDcafrgMeLzaFPsw2kNvEcqTKl/VqLat/MaB33pZy0y3rJZtnqwR2qOOvbwKZYKiEO1O6VqNEBxKvJJelCq0dTXWT5pbO2gDXC6h6QDXCaHo6pOHGPUy+YBaGQRGuSusMEASYiWunYN0vCAI8QaXnWMXNMdFP3jHAJH0eDsoiGnLPBlBp4TNm6rYI74nMzgz3B9IikW4WVK+dc8KZJZWYjAuORU3jc1c/NPskD2ASinf8v3xnfXeukU0sJ5N6m5E8VLjObPEO+mN2t/FZTMZLiFqPWc/ALSqnMnnhwrNi2rbfg/rd/IpL8Le3pSBne8+seeFVBoGqzHM9yXw=="
    - "github.com,204.232.175.90 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ=="
# Create directory structure 
deployment_dir_structure            : True
deployment_dir_base                 : "{{ deployment_user_home }}/{{ deployment_name }}"
deployment_dir_work                 : "{{ deployment_dir_base }}/{{ deployment_version }}"
deployment_dir_current              : "{{ deployment_dir_base }}/current"
## Extra directory that needs to be created (should be a list) i.e. ['/var/log/myapp','/opt/blaaa']
deployment_extra_dirs               : 'none'
## Extra files that needs to be created (should be a list) i.e. ['/var/log/myapp.log','/somewhere/file.txt']
deployment_extra_files              : 'none'
# Default perm
deployment_dir_perm                 : "0755"
deployment_file_perm                : "0644"

## Config option
deployment_config_file_perm         : "0600"
# Shell environment variable
deployment_config_shell_vars        : "none" # Variables that define the config
deployment_config_shell_vars_export : True
deployment_config_shell_file        : "{{ deployment_dir_base }}/{{ deployment_name }}_environment.sh"
deployment_config_shell_profile     : "{{ deployment_user_home }}/.bashrc"
# INI variable
deployment_config_ini_vars          : "none" # Variables that define the config
deployment_config_ini_vars_dest     : "{{ deployment_dir_base }}/{{ deployment_name }}_config.ini"
# DotEnv variable
deployment_config_dotenv_vars       : "none"
deployment_config_dotenv_vars_dest  : "{{ deployment_dir_work }}/.env.php"
## YAML vars config 
deployment_config_yaml_vars         : "none"

## Dependency managment
# Supported dependency ['none', 'comoser']
deployment_dependency               : "none"
deployment_composer_user            : "{{ deployment_user }}"
deployment_dependency_composer_args :
                        working_dir : "{{ deployment_dir_work }}"
                        command     : "install"

## Cron jobs TODO: Make an example of cron jobs
deployment_cron_jobs                : "none"

## By default you deploy once and to override you must pass true to force deployment
deployment_force                    :  false
deployment_guard_file               :  "/var/local/deployment_first_boot_file"

````

### Contributors
* [Alfonso Fernandez](https://github.com/alfonsodev)
* [Adham Helal](https://github.com/ahelal)
* [Sergio Sola](https://github.com/ssola)

### Todo
- Implement handler to restart/reload application
- Implement Post deployment checks


