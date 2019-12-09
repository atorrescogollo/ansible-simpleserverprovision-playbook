# server-provision-ansible
## Usage

#### 1. Download

```bash
$ git clone https://github.com/atorrescogollo/server-provision-ansible.git
$ cd server-provision-ansible/ansible-playbook/
```

#### 2. Test connectivity [Optional]

```bash
$ ANSIBLE_HOST_KEY_CHECKING=False ansible all -i inventory/servers.hosts -m setup
```

#### 3. Edit vars
 - `group_vars/servers.yaml`:
```yaml
#
# Servers Variables
#

nameservers:
  - 1.1.1.1
  - 8.8.8.8

authorized_keys: ~/.ssh/id_rsa.pub
sethostname: 'yes'
```
 - `inventory/servers.hosts`:
```ini
#
# Servers Inventory
#

[servers]
testdebian1.domain.es ansible_host=10.0.8.56
testdebian2.domain.es ansible_host=10.0.8.57
testdebian3.domain.es ansible_host=10.0.8.58
testdebian4.domain.es ansible_host=10.0.8.59

[servers:vars]
ansible_user=root
ansible_ssh_pass=r
```
#### 4. Run the playbook
```bash
$ ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory/servers.hosts setup-servers.yaml
```
```ansible
PLAY [Setup Servers] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************************************************************************************************
...

TASK [setup-server : Setup hostname] ************************************************************************************************************************************************************************
...

TASK [setup-server : Setup /etc/hosts] **********************************************************************************************************************************************************************
...

TASK [setup-server : Setup /etc/resolv.conf] ****************************************************************************************************************************************************************
...

TASK [setup-server : Ensure /root/.ssh dir exists] **********************************************************************************************************************************************************
...

TASK [setup-server : Setup ssh authorized_keys] *************************************************************************************************************************************************************
...

TASK [setup-server : Reboot server] *************************************************************************************************************************************************************************
...

RUNNING HANDLER [setup-server : Wait for server recovery] ***************************************************************************************************************************************************
...

PLAY RECAP **************************************************************************************************************************************************************************************************
testdebian1.domain.es      : ok=8    changed=6    unreachable=0    failed=0
testdebian2.domain.es      : ok=8    changed=6    unreachable=0    failed=0
testdebian3.domain.es      : ok=8    changed=6    unreachable=0    failed=0
testdebian4.domain.es      : ok=8    changed=6    unreachable=0    failed=0

```
