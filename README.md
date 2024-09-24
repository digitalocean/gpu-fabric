# gpu-fabric
Simple Ansible playbook to configure GPU droplets.

# Pre-requisites

This procedure assumes you have familiary with Ansible and have Ansible available on the machine that you
will use to run the following command. For instructions on how to make Ansible available on this device,
please refer to the Ansible [installation guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html).

It is also worth noting that Ansible uses ssh under the hood to configure your droplets. If you have never
ssh'ed into your droplets, and you do not have `StrictHostKeyChecking no` in your `.ssh/config` file, you can
add the following:

```
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

At the bottom of the `inventory/droplets` file.

# how-to

Edit the `droplets` file under the `inventory` directory to specify the list of droplet's public addresses
under the `[multinode_gpu_droplets]` section. Leave the rest unchanged, save and close the file.

After that, run the following command:

```
ansible-playbook -i inventory/droplets customer-play.yaml
```

With success you should see the following similar output:

```
PLAY [multinode_gpu_droplets] *************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************************************************************************************************************************************
ok: [10.10.10.10]

TASK [read /etc/netplan/50-cloud-init.yaml] ***********************************************************************************************************************************************************************************************************
ok: [10.10.10.10]

TASK [extract /etc/netplan/50-cloud-init.yaml] ********************************************************************************************************************************************************************************************************
ok: [10.10.10.10]

TASK [set a unique index for each droplet] ************************************************************************************************************************************************************************************************************
ok: [10.10.10.10] => (item=10.10.10.10)

TASK [adjust /etc/netplan/50-cloud-init.yaml] *********************************************************************************************************************************************************************************************************
ok: [10.10.10.10]

TASK [write /etc/netplan/50-cloud-init.yaml] **********************************************************************************************************************************************************************************************************
ok: [10.10.10.10]

TASK [install lldp] ***********************************************************************************************************************************************************************************************************************************
ok: [10.10.10.10]

PLAY RECAP ********************************************************************************************************************************************************************************************************************************************
10.10.10.10             : ok=7    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
