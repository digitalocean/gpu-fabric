This repository contains a simple Ansible playbook to configure multi-node GPU Droplets.

To use this playbook:

1. On the machine that you will use to run this playbook, first [install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) and then [clone this repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).

2. In the `inventory/droplets` file in your cloned version of this repository, in the `[multinode_gpu_droplets]` section, specify the public IP addresses of your GPU Droplets.

3. Ansible uses SSH under the hood to configure Droplets. If you have never connected to your Droplets with SSH and the `.ssh/config` file on your machine does not include `StrictHostKeyChecking no`, add the following line to the `inventory/droplets` file:

```
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

4. Save the file, then run the playbook from the root of the repository:

```
ansible-playbook -i inventory/droplets customer-play.yaml
```

The output of a successful run looks similar to the following:

```
PLAY [multinode_gpu_droplets] ***********************************************************************************

TASK [Gathering Facts] ******************************************************************************************
ok: [10.10.10.10]

TASK [read /etc/netplan/50-cloud-init.yaml] *********************************************************************
ok: [10.10.10.10]

TASK [extract /etc/netplan/50-cloud-init.yaml] ******************************************************************
ok: [10.10.10.10]

TASK [set a unique index for each droplet] **********************************************************************
ok: [10.10.10.10] => (item=10.10.10.10)

TASK [adjust /etc/netplan/50-cloud-init.yaml] *******************************************************************
ok: [10.10.10.10]

TASK [write /etc/netplan/50-cloud-init.yaml] ********************************************************************
ok: [10.10.10.10]

TASK [install lldp] *********************************************************************************************
ok: [10.10.10.10]

PLAY RECAP ******************************************************************************************************
10.10.10.10             : ok=7    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
