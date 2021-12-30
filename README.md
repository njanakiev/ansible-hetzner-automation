# hetzner-ansible-automation

Ansible playbooks to create and setup [Hetzner](https://hetzner.cloud/?ref=FkpdQcqbGXhP) cloud instances with a dynamic inventory.

# Requirements

The playbooks use the [hetzner.hcloud.hcloud](https://docs.ansible.com/ansible/latest/collections/hetzner/hcloud/hcloud_inventory.html) dynamic inventory plugin and the [hetzner.hcloud.hcloud_server](https://docs.ansible.com/ansible/latest/collections/hetzner/hcloud/hcloud_server_module.html) collection. The playbooks were tested using Ansible `2.11.7` and Python `3.7.11`.

# Configuration

To configure the servers define the types of servers you want in [config.yml](config.yml) as follows:

```yml
---
server_names:
- server1
- server2

hcloud_ssh_key_name: key_name

server_type: cx11
server_image: ubuntu-20.04
server_location: nbg1
```

You need to have an existing ssh key defined in the project, whose name you need to add in the `hcloud_ssh_key_name` variable. The `server_names` list is only used for [hcloud-create-servers.yml](hcloud-create-multiple-servers.yml) and [hcloud-destroy-servers.yml](hcloud-destroy-servers.yml).

# Usage

First, export your `HCLOUD_TOKEN` as a variable from Hetzner with:

```bash
export HCLOUD_TOKEN=XXXX
```

To create a server defined in you can run the playbook:

```bash
ansible-playbook hcloud-create-server.yml
```

To create multiple servers with docker pre-installed and a dedicated user added, run the playbook:

```bash
ansible-playbook hcloud-create-multiple-servers.yml \
  --extra-vars "username=user password=XXXXXXX"
```

The server configuration can be found in [config.yml](config.yml).

To list all available servers, type:

```bash
ansible-inventory --list
ansible-inventory --graph
```

To run ad-hoc commands, type:

```bash
ansible all -u root -a "free -m"
```

To delete all servers, run the following playbook:

```bash
ansible-playbook hcloud-destroy-servers.yml
```

# License 
This project is licensed under the MIT license. See the [LICENSE](LICENSE) for details.
