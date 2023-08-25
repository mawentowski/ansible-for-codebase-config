## Configuration

Use this project as a template to create your own project to manage Ansible configurations.

### Set up hosts

Ansible retrieves host details from `inventory.yaml`. The file contains two groups, local and webserver, with hosts and connection details. Modify this file to include the desired hosts for playbook execution.

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

In the `roles/local_repos/templates` folder, Jinja syntax is employed in Markdown files with `.md.j2` extensions. Explore the [Jinja Template Designer Documentation](https://jinja.palletsprojects.com/en/latest/templates/) for a deeper understanding.
