Vector Ansible role
Logo

Build Status Ansible Galaxy

This ansible role installs Vector in a Debian environment. It has been tested for the following Debian versions:

Buster
Bullseye
This role has been generated using the cookiecutter tool, you can generate a similar role that fits your needs using the this cookiecutter template.

These instructions will get you a copy of the role for your Ansible playbook. Once launched, it will install Vector in a Debian system.

Prerequisities
Ansible 2.9.9 version installed.

Molecule 3.x.x version installed.

For testing purposes, Molecule with Docker as driver and Goss as verifier.

Installing
Create or add to your roles dependency file (e.g requirements.yml):

ansible-galaxy install -p roles -r requirements.yml -f
Use in a playbook:

- name: Vector
  hosts: vector
  roles:
    - vector-role
Usage
Look to the defaults properties file to see the possible configuration properties, it is very likely that you will not need to override any variables.


Versioning
For the versions available, see the tags on this repository.

Additionaly you can see what change in each version in the CHANGELOG.md file.

Authors
See also the list of contributors who participated in this project.

License
Apache 2.0 License

This project is licensed under the Apache 2.0 license - see the LICENSE file for details.

Contributing
Please read CONTRIBUTING.md for details on our code of conduct, and the process for submitting pull requests to us.

```
---
- name: Install Vector | APT Install
  become: true
  ansible.builtin.apt:
    deb: https://packages.timber.io/vector/{{ vector_version }}/vector_{{ vector_version }}-1_amd64.deb
  notify: Restart vector service

- name: Configure Vector | Rensure what directory exists
  ansible.builtin.file:
    path: "{{ vectore_config_dir }}"
    state: directory
    mode: "0644"
- name: Configure Vector | Template Configure
  become: true
  ansible.builtin.template:
    src: vector.yml.j2
    mode: "0644"
    dest: "{{ vectore_config_dir }}/vector.yml"
- name: Configure Vector | Template system unit
  become: true
  ansible.builtin.template:
    src: vector.service.j2
    dest: "/etc/systemd/system/vector.service"
    mode: "0644"
  notify: Restart vector service
```
