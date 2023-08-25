### Run the Playbook

By default, the host targetted by Ansible is _this_ project.

Examine `repo.yaml` to find metadata such as `name`, `description`, and `license`.

Change each property property of this file to fit your new Ansible project.

Run the following command to run the playbook and regenerate the project documentation located in the root:

```bash
ansible-playbook master_playbook.yaml
```

### View Generated Files

In the root, of the directory, open a file such as `CODEOWNERS`, and you'll notice the `github_repo_owner` you entered in `repo.yaml` is shown. Similarly, other files now incorporated your repository-specific details from `repo.yaml`, including this `README`!

This showcases Ansible's ability to dynamically generate documentation based on YAML data.

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
