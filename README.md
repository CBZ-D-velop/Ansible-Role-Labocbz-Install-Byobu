# Ansible role: labocbz.install_byobu

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Cbz-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian](https://img.shields.io/badge/Tech-Debian-orange)
![Tag: Tmux](https://img.shields.io/badge/Tech-Tmux-orange)
![Tag: Byobu](https://img.shields.io/badge/Tech-Byobu-orange)
![Tag: Neofetch](https://img.shields.io/badge/Tech-Neofetch-orange)

An Ansible role to install Byobu and import your configuration.


The Ansible role installs Byobu, a terminal multiplexer that enhances the terminal experience by providing various features and customization options. Additionally, the role has the option to install Neofetch, a small utility that displays system information and ASCII art at the shell's startup.

Byobu enriches the terminal environment by providing the ability to split the terminal into multiple panes, creating a more efficient workflow. It offers essential keybindings and shortcuts for managing the terminal sessions, making it an excellent tool for power users and system administrators.

With the role, administrators can enable Byobu for all users, making it the default terminal environment when users log in. Similarly, Neofetch can also be enabled for all users, providing a visually appealing system information display at each shell's startup.

Furthermore, administrators can choose to log commands for all users, which allows users to access their command history and easily recall previous commands.

The role supports configuring Byobu's default backend to "tmux," providing the flexibility to customize the terminal multiplexer according to specific requirements.

In summary, the Byobu role simplifies the installation and configuration of Byobu and optionally Neofetch. Byobu's versatility in enhancing the terminal experience, combined with Neofetch's system information display, provides an efficient and visually pleasing terminal environment for all users.

## Folder structure

By default Ansible will look in each directory within a role for a main.yml file for relevant content (also man.yml and main):

```PYTHON
.
├── README.md  # Contains an overview of the role and its purpose.
├── defaults
│   ├── main.yml  # Contains default variables for the role that can be overridden by users.
│   └── README.md  # Contains documentation for the default variables.
├── files
│   └── README.md  # Contains documentation for the files in the directory.
├── handlers
│   ├── main.yml  # Contains handlers that can be called by tasks within the role.
│   └── README.md  # Contains documentation for the handlers.
├── meta
│   ├── main.yml  # Contains metadata about the role, including dependencies and supported platforms.
│   └── README.md  # Contains documentation for the role metadata.
├── tasks
│   ├── main.yml  # Contains tasks to be executed by the role on the managed nodes.
│   └── README.md  # Contains documentation for the tasks.
├── templates
│   └── README.md  # Contains documentation for the templates.
└── vars
    ├── main.yml  # Contains variables that are specific to the role and are not meant to be overridden.
    └── README.md  # Contains documentation for the role variables.
```

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the role) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This role contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your role
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this role, just copy/import this role or raw file into your fresh playbook repository or call it with the "include_role/import_role" module.

## Usage

### Vars

Some vars a required to run this role:

```YAML
---
install_byobu_install_neofetch: true

install_byobu_enable_byobu_for_all: true
install_byobu_enable_neofetch_for_all: true
install_byobu_log_commands_for_all: true
install_byobu_set_nano_as_default_for_all: true

install_byobu_default_backend: "tmux"

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---

inv_install_byobu_install_neofetch: true
inv_install_byobu_enable_byobu_for_all: true
inv_install_byobu_enable_neofetch_for_all: true

```

```YAML
# From AWX / Tower
---
all vars from to put/from AWX / Tower
```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
- name: "Include labocbz.install_byobu"
    tags:
    - "labocbz.install_byobu"
    vars:
    install_byobu_install_neofetch: "{{ inv_install_byobu_install_neofetch }}"
    install_byobu_enable_byobu_for_all: "{{ inv_install_byobu_enable_byobu_for_all }}"
    install_byobu_enable_neofetch_for_all: "{{ inv_install_byobu_enable_neofetch_for_all }}"
    ansible.builtin.include_role:
    name: "labocbz.install_byobu"
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-04-27: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
