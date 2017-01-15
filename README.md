Ansible role: Docker-Pi
=========

[![Build Status](https://travis-ci.org/Benaud12/docker-pi.svg?branch=master)](https://travis-ci.org/Benaud12/docker-pi)

###**Ansible role for Docker installation on a Raspberry Pi**

Requirements
------------

Assumes Raspbian OS or equivalent.

Raspbian Jessie Lite can be downloaded from here <https://www.raspberrypi.org/downloads/raspbian>

Role Variables
--------------

###Varaibles are shown below along with their default values

####Install:

All tasks are run with privilege escalation by default. As per the [Ansible documentation](http://docs.ansible.com/ansible/become.html) `become_user` defaults to the root user, so installation will be run as root by default.

```yml
# vars/main.yml

become: yes
```

####Login:

The [Docker Hub](https://hub.docker.com/) username, password are required for login. The task will be skipped if any are missing.

This is also run as the root user by default. If a specific user needs to be logged in, register this under the `docker_pi_user` variable.

```yml
# defaults/main.yml

docker_pi_user: root

docker_pi_hub_username: ""
docker_pi_hub_password: ""
```

####Users:

List all users that need to be added to the docker group under the `docker_pi_group_users` variable. Users must already exist on the machine.

```yml
# defaults/main.yml

docker_pi_group_users: []
```

Dependencies
------------

No dependencies on other Ansible roles.

Example Playbook
----------------

Basic installation, without login to Docker hub or adding additional 'docker' users:

    - hosts: raspberry-pi
      roles:
        - role: Benaud12.docker-pi

Install with login and additional users:

    - hosts: raspberry-pi
      roles:
        - role: Benaud12.docker-pi
          docker_pi_user: mick.dundee
          docker_pi_hub_username: croc_killer123
          docker_pi_hub_password: knifeySpoony
          docker_pi_group_users:
            - mick.dundee
            - sue.charlton
            - donk
            - pi