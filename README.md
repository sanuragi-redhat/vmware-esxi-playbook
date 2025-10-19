# vmware-esxi-playbook
esxi vmware playbook

	[root@rhel-kvm ansible]# cat ansible.cfg 
	[defaults]
	remote_user = root 
	inventory = ./inventory_vmware.yml
	roles_path = /usr/share/ansible/roles:/etc/ansible/roles:/root/ansible/roles
	deprecation_warnings=False
	command_warnings = False
	[privilege_escalation]
	become = true
	become_user = root 
	become_method = sudo 
	become_ask_pass = false 

	[root@rhel-kvm ansible]# cat inventory_vmware.yml 
	localhost

	[vmware]
	192.168.1.207  ansible_user=root ansible_ssh_pass='password'

	[root@rhel-kvm vmware]# ansible-playbook 007.poweroff_vm_prompt.yml 
	[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
	[WARNING]: Collection community.vmware does not support Ansible version 2.16.14
	Enter ESXi username [root]: 
	Enter ESXi password: 
	Enter ESXi hostname or IP [192.168.1.207]: 
	Enter vSphere datacenter name [ha-datacenter]: 
	Available VMs:
	windows-template, rhel-8-template, centos-stream9-template

	Enter comma-separated VM names to power off from the above list (or 'all' to power off all):
	: all

	PLAY [Power Off All the Virtual Machines] ************************************************************************************************************************

	TASK [Get VM list from report file] ******************************************************************************************************************************
	ok: [localhost]

	TASK [Determine VMs to power off based on input] *****************************************************************************************************************
	ok: [localhost]

	TASK [Debug vm_list] *********************************************************************************************************************************************
	ok: [localhost] => {
    	"vm_list": [
        	"windows-template",
        	"rhel-8-template",
        	"centos-stream9-template"
    	]
	}

	TASK [Power off specified VMs] ***********************************************************************************************************************************
	changed: [localhost] => (item=windows-template)
	changed: [localhost] => (item=rhel-8-template)
	changed: [localhost] => (item=centos-stream9-template)

	PLAY RECAP *******************************************************************************************************************************************************
	localhost                  : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

	[root@rhel-kvm vmware]# 




