# Vagrant example with ansible provisioners

This will fire up an Ubuntu VirtualBox VM. 

You will need to edit main.yaml to select or deselect different roles as follows.

```
---
- name: Install and configure all components
  hosts: all
  become: yes
  become_method: sudo
  roles: 
  - base
  - timezone
  - ntp
  - ros2
```

The roles are git sub-modules. You can add more sub-modules as follows.

```
git submodule add https://github.com/asundaresan/ansible-role-timezone.git roles/timezone
```

# To compile 

In order to build ROS2, do the following from the home folder 

```
mkdir -p projects/ros2/src 
cd projects/ros2
wget https://raw.githubusercontent.com/ros2/ros2/release-latest/ros2.repos
vcs import src < ros2.repos
```
