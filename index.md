# Development Configuration

!SLIDE

# Development Configuration

## Setup should be the easy part

### Caleb Woods

!SLIDE left

## The Problem

* Consultants work on many varied projects
* Every developer has setup they like best
* Some dependencies conflict between projects
* Moving to a new project usually requires help to it setup

!SLIDE left

## Solutions

* Bundler
* Homebrew
* Boxen
* Shoestring
* Vagrant / Ansible

!SLIDE left

## Vagrant

From [website](http://www.vagrantup.com/)

  Create and configure lightweight, reproducible, and portable development environments.

!SLIDE left

## How Vagrant Works

* Virtual Machine Host ([VirtualBox](https://www.virtualbox.org/), VMWare)
* Configuration File (Vagrantfile)
* Provisioning Tool (Shell, Ansible, Chef, Puppet)

!SLIDE left snippet

## Starting Vagrant

```bash
$ vagrant up
```

* Downloads base image if needed
* Creates virtual machine (VM)
* Boots the VM
* Runs the provision tool

!SLIDE left snippet

## Using Vagrant

```bash
$ vagrant ssh
cd /vagrant # directory shared with local file system

$ rspec spec
$ rails server
$ foreman start
$ shoestring
```

!SLIDE left

## Ansible

* Written in Python
* No server component
* Simple - YAML files
* Idempotent

!SLIDE left snippet

## Ansible Playbooks

```yml
---
- hosts: all

  vars:
    ruby_version: 2.0.0-p247
    pg_version: 9.2
    phantomjs_version: '1.9.7'

  roles:
   - zzet.rbenv
   - zzet.postgresql
   - nicolai86.ansible-phantomjs
   - geos

  tasks:
    - name: do something
      shell: echo 'Hello World'
```

!SLIDE left

## Ansible Modules

* Wrapper on many system tools (files, databases, AWS)
* Abstracts differences of target OSes

```yml
tasks
  - name: Install nginx
    sudo: yes
    apt: pkg=nginx state=installed

  - name: template config files
    sudo: yes
    copy: src=templates/nginx_main.conf dest=/etc/nginx/nginx.conf force=yes

  - name: create application-specific config files
    sudo: yes
    template: src=templates/nginx.conf dest=/etc/nginx/conf.d/{{application}}.conf force=yes

  - name: start or restart nginx
    sudo: yes
    service: name=nginx state=restarted enabled=yes
```

!SLIDE left

## Ansible Roles

* Divide provisioning components into reusable chunks
* Easier to share between development and production
* [Ansible Galaxy](https://galaxy.ansible.com/)

!SLIDE left

## Demo

