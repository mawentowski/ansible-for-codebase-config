Ansible for Code Base Configuration
============

Ansible for Code Base Configuration simplifies managing code base documentation and files by leveraging Ansible's dynamic templating capabilities.

## Table of contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Getting Started](#getting-started)
   - [Prerequisites](#prerequisites)
   - [Clone the Repository](#clone-the-repository)
   - [Run the Playbook](#run-the-playbook)
   - [View Generated Files](#view-generated-files)
- [Project structure](#project-structure)
- [Usage](#usage)
   - [Run playbook on all hosts](#run-playbook-on-all-hosts)
   - [Optional: Specifying an Inventory File](#optional-specifying-an-inventory-file)
   - [Run playbook on all hosts in specific group](#run-playbook-on-all-hosts-in-specific-group)
   - [Run playbook on specific host](#run-playbook-on-specific-host)
- [Configuration](#configuration)
   - [Set up hosts](#set-up-hosts)
   - [Configure `repo.yaml`](#configure-repoyaml)
   - [Optional: Set default inventory file in `ansible.cfg`](#optional-set-default-inventory-file-in-ansiblecfg)
   - [Create playbooks](#create-playbooks)
   - [Create Jinja templates](#create-jinja-templates)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## About the Project

While Ansible is often associated with server configuration, its potential extends to automating documentation by utilizing Jinja templating. Ansible's support for injecting variables from sources like YAML makes it a valuable tool for generating files and content specific to each code repository.

As a newcomer to Ansible, my initial objective was to establish consistent boilerplate files such as a `README`, `CODE_OF_CONDUCT`, `CODEOWNERS`, and `SECURITY` across my repositories. This involved maintaining uniformity while incorporating dynamic repository-specific content during playbook execution.

My search for a basic project template featuring playbook-driven file generation, file templates, and customizable code base variables in a `repo.yaml` file was futile. I found official Ansible documentation less pragmatic and YouTube tutorials too narrow in scope.

The Simple Ansible Playbook Starter was born from this predicament. It delivers a minimal configuration to kickstart Ansible utilization, with a primary focus on dynamic file generation. This template serves as a foundation for more complex Ansible configurations tailored to diverse use cases.

To begin, define local hosts (repositories on your system) for testing purposes. Subsequently, configure `inventory.yaml` to extend these tasks to remote systems through SSH or other APIs.

## Features

- **Consistent Documentation:** Generate standardized files across repositories for a uniform codebase.
- **Dynamic Templating:** Inject dynamic content using Ansible's Jinja templating for personalized documentation.
- **Custom Repository Details:** Define unique attributes like name and license in `repo.yaml` for easy customization.
- **Local Testing:** Simulate repository configurations locally, facilitating pre-deployment checks.
- **Version Control Integration:** Include generated files in version control, keeping documentation in sync with code.

## Getting Started

### Prerequisites

Before installing Ansible, follow the general steps outlined in the [Ansible installation guidelines](https://docs.ansible.com/ansible/latest/installation_guide/index.html), tailored to your operating system.

### Clone the Repository

1. Clone the repository:

   ```bash
   git clone git@github.com:mawentowski/ansible-for-codebase-config.git

2. Navigate to the repository:

   ```bash
   cd ansible-for-codebase-config
   ```
### Run the Playbook

Within the root directory, locate the `localhost_demo` folder, which represents a code base targeted by Ansible. This folder contains a `repo.yaml` file.

Examine `localhost_demo/repo.yaml` to find metadata such as `name`, `description`, and `license`.

Execute the following command to run the playbook and generate files for localhost_demo:

```bash
ansible-playbook master_playbook.yaml
```

### View Generated Files

Check the `localhost_demo` folder to observe the new files. The generated `README.md` contains the repository name, inserted based on the `repo.yaml` definition. Similarly, other files incorporate repository-specific details from `repo.yaml`.

This showcases Ansible's ability to dynamically generate documentation.

## Project structure

Take a moment to familiarize yourself with the project structure:

```txt
root
├─ localhost_demo                          # Sample local repo targetted by the playbook
├─ roles                                   # Used to organize playbook, tasks, and templates
│  └─ local_repos                          # Role specific to hosts on a local machine               
│     ├─ tasks                             # Tasks the role performs
│     └─ templates                         # Role-specific Jinja templates containing variables
├─ ansible.cfg                             # Ansible configuration file
├─ inventory.yaml                          # Inventory file containing hosts details
├─ master_playbook.yaml                    # Main playbook that triggers role-specific tasks
└─ repo.yaml                               # File defining variables inserted into templates
```

## Usage

### Run playbook on all hosts

To execute the playbook on all hosts within all groups, use the following command:

```bash
ansible-playbook master_playbook.yaml
```

Let's break it down:

- `ansible-playbook`: This is the command used to run Ansible playbooks.
- `master-playbook.yml`: This is the name of the Ansible playbook that will be executed.

### Optional: Specifying an Inventory File

Use the `-i` argument to specify a custom inventory file. By default, Ansible searches for hosts in `inventory.yaml`.

For example:

```shell
ansible-playbook -i <your-inventory-file>.yaml master-playbook.yml
```

### Run playbook on all hosts in specific group

To run a playbook against all hosts in a specific group, pass a `limit` argument followed by the name of the group. For example:

```shell
ansible-playbook --limit local master_playbook.yaml
```

### Run playbook on specific host

To run a playbook on a specific host, pass a `limit` argument followed by the name of the host:

```shell
ansible-playbook --limit localhost_demo master_playbook.yaml
```

## Configuration

Use this project as a template to create your own project to manage Ansible configurations.

### Set up hosts

Ansible retrieves host details from inventory.yaml. The file contains two groups, local and webserver, with hosts and connection details. Modify this file to include the desired hosts for playbook execution.

### Configure `repo.yaml`

`repo.yaml` holds configuration data for a project. Defined variables are utilized within Ansible playbooks to influence tasks and templates. Update this file with values pertinent to your project.

### Optional: Set default inventory file in `ansible.cfg`

Change the default inventory file in `ansible.cfg`:

For example:

```shell
inventory = ./<your-inventory-file>.yaml
```

### Create playbooks

Refer to the official [Using Ansible playbooks](https://docs.ansible.com/ansible/latest/playbook_guide/index.html) guide for comprehensive details on creating Ansible playbooks.

Execute a playbook using the following command:

```shell
ansible-playbook <your-playbook>.yaml
```

### Create Jinja templates

In the `roles/local_repos/templates` folder, you'll find Jinja templates using syntax such as:

```jinja
mawentowski
```

Jinja is employed in Markdown files with `.md.j2` extensions. Explore the [Jinja Template Designer Documentation](https://jinja.palletsprojects.com/en/latest/templates/) for a deeper understanding.

## Roadmap

- [ ] Implement schema validation of `repo.yaml`
- [ ] Add support for inserting partial Markdown files stored within a `/docs` folder referenced by `repo.yaml` for extensive documentation.
- [ ] Replace `.yaml` extensions with `.yml` per Ansible standards.
- [ ] Output the CODEOWNERS file to a `.github` folder.
- [ ] Implement automated Markdown TOC for the README.

## Contributing

Community contributions are appreciated. Report bugs, suggest improvements, or submit code changes by forking the repository and creating a pull request

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for more information.

## Contact

- Mark Wentowski (project owner) - <mawentowskigit@gmail.com>


