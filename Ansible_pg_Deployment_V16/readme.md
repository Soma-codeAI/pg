# Ansible PostgreSQL Deployment

This project provides an Ansible playbook for setting up a PostgreSQL replication environment. The playbook configures a primary server and two replica servers for PostgreSQL version 16 with replication slots and WAL archiving.

## Features

- Installs PostgreSQL 16 on primary and replica servers
- Configures PostgreSQL for replication
- Sets up WAL archiving
- Creates and uses replication slots for replicas
- Handles multiple replica environments

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Ansible 2.9 or later
- PostgreSQL 16
- Ansible collections - community.postgresql [Link](https://galaxy.ansible.com/ui/repo/published/community/postgresql/docs)
- SSH access to the servers with root privileges or a user with sudo privileges
- Firewall settings allowing PostgreSQL replication traffic (port 5432)

## Project Structure

```text
.
├── ansible.cfg
├── inventory/
│   └── inventory.yml
├── playbooks/
│   └── install_configure_pg.yml
├── roles/
├── templates/
├── vars/
└── README.md

```
- ansible.cfg: Configuration file for Ansible.
- inventory/: Inventory files for Ansible, specifying the servers to manage.
- playbooks/: Ansible playbooks for various tasks.
- roles/: Roles for Ansible, which contain tasks, handlers, files, templates, and related resources.
- templates/: Jinja2 templates used in playbooks.
- vars/: Variable files used in playbooks.

## Inventory Setup

Create an Ansible inventory file (`inventory.yml`) with the following content:

```
[primary]
primary ansible_host=10.0.0.1

[replica]
replica1 ansible_host=10.0.0.2 slot_name=replica1_slot
replica2 ansible_host=10.0.0.3 slot_name=replica2_slot
```

```
ansible-playbook -vv -i ./inventory/hosts ./playbooks/install_configure_pg.yml
```

