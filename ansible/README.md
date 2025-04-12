# Deploy EvOC on Infrastructure

# Requirements

-   `Ansible CLI` installed
-   `SSH sudo access` to the target server

# Configure Hosts

In the inventory file, specify the target server's IP address or hostname under the `[master]` and `[worker]` group. Also, specify the SSH user that has sudo access to the target server.

```ini
# Define all unique hosts and their
# connection details ONCE using logical names.

[nodes]
master-node  ansible_host=<your_master_node_ip>
worker-node1 ansible_host=<your_worker_node1_ip>
worker-node2 ansible_host=<your_worker_node2_ip>

[master]
master-node

[workers]
worker-node1
worker-node2

[cockroachdb]
worker-node1
worker-node2

# ------IMPORTANT---------
# Exactly one node only
# should be used for MinIO.
[minio]
worker-node2

[all:children]
master
workers

[all:vars]
ansible_user=<your_ssh_user>
```

# CockroachDB License Key

Get a cockroachdb enterprise-free license key by declaring usage of cockroachdb for `academic research` as that's the goal of this project. You can get the license key from the [CockroachDB docs](https://www.cockroachlabs.com/docs/stable/licensing-faqs). After that, create a file in path `ansible/vars/crdb_secrets.yml` and paste the license key in the file. The file should look like this:

```yml
crdb_enterprise_license_key: "<<YOUR_LICENSE_KEY>>"
```

# Minio Config

To use Minio as the object storage for EvOC, you need to create a file in path `ansible/vars/minio_secrets.yml` and paste the access key and secret key in the file. The file should look like this:

```yml
minio_root_user: "<username>"
minio_root_password: "<password>"
```

# Execute the Playbook

Run the following command to execute the playbook from the `ansible` directory on your local machine. It will prompt for the SSH password and the sudo password for the target server. Do provide the correct passwords when prompted.

```bash
ansible-playbook -i inventory.ini playbook.yml -kK
```
