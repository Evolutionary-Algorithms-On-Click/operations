# Deploy EvOC on Infrastructure

# Requirements

-   `Ansible CLI` installed
-   `SSH sudo access` to the target server

# Configure Hosts

In the inventory file, specify the target server's IP address or hostname under the `[myhosts]` group.

```ini
[myhosts]
user1@ip1
user2@ip2
user3@ip3
```

# Execute the Playbook

Run the following command to execute the playbook from the `ansible` directory on your local machine. It will prompt for the SSH password and the sudo password for the target server. Do provide the correct passwords when prompted.

```bash
ansible-playbook -i inventory playbook.yml -kK
```
