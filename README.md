# Ansible Control

> Building an ansible control node with Vagrant

## Usage example

```
vagrant up
vagrant ssh ansible
cd playbook
ansible all -m ping
workstation | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```