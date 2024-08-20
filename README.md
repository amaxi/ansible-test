Prepare the environment for k3s and rke2 cluster

Environments
- openSUSE Leap 15.6
- LeapMicro 6.0

Tested with:
- with Leap 15.6
- Latest stable rke2 and k3s version

Home Lab
- 2 rke2 servers (rancher)
- 2 k3s servers (one is impoert and one is created by rancher)
- 1 mgmt server (manage and test features)

Inventory
ansible-inventory -i inventory/inventory.ini -y --list > inventory.yml

SSH
ssh-keygen -t ed25519
eval `ssh-agent`
ssh-add
for managed_node in mgmt rke2-1 rke2-2 k3s-1 k3s-2; do ssh-copy-id root@${managed_node}; done

RUN
ansible-playbook -i inventory/hosts.ini playbooks/ping/site.xml

NOTE:
https://www.cyberciti.biz/faq/ansible-zypper-update-all-packages-on-opensuse-suse/