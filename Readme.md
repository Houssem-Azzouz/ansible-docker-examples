# Run docker containers using ansible

## Description:
This repo contains playbooks that:
- Install docker and its dependencies on the remote server (docker host)
- Create and start a container that runs the official nginx dockerhub image on the docker host
- Build an image locally, create and start a container that runs it on the docker host

It is recommended to run within virtual envs (python 2.7 or python 3.6)
Written for Ubuntu 20.04

Credits for the 404 page used in the locally built image go to: https://codepen.io/AsyrafHussin
## Preparations
1. Clone repo to a path of your chosing
2. In prepare-docker.yml, set the following variable under vars:
    - 'play_user' to the username of the user running ansible-playbook
3. In run_custom image.yml, set the following variable under vars:
    - 'clone_dir': The directory to which you have cloned the repo
4. In ansible.cfg, set the following:
    - 'remote_user' to the username of the user running ansible-playbook
    - if you want to install collections in a custom directory, uncomment 'collections_path' and set it to the path of your choosing.
5. Install the community.docker collection:
    ```
    ansible-galaxy collection install community.docker
    ```
    In case you wish to install in a custom directory, make sure to enter it to 'collections_path' in ansible.cfg and run the following:
    ```
    ansible-galaxy collection install community.docker [-p /path/to/custom/collections/path]
    ```
6. Modify the inventory file to match your target hosts.

## Setup the docker host
Run the playbook prepare-docker.yml to make sure the docker package as well as the python docker library are installed:
```
ansible-playbook -i inventory.ini prepare-docker.yml
```

## Run sample playbooks:
### Spin an nginx container:
The following playbook creates and starts a container running the dockerhub official nginx image with port binding 8080 (host) to 80 (container):
```
ansible-playbook -i inventory.ini run_nginx_image.yml
```
### Spin a container based on a locally built image:
The following playbook creates and starts a container running a custom image that is locally built with port binding 8081 (host) to 80 (container):
```
ansible-playbook -i inventory.ini run_custom_image.yml
```
### Run all playboooks
```
ansible-playbook -i inventory.ini main.yml
```