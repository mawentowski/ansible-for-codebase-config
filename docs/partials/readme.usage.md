## Usage

<!-- To do playbook checkout to clone github repos, your SSH agent must be running and attached to your SSH key, as described here: /Users/mawentowski/Repos/notes/coding-notes/ssh-agent.md -->

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
