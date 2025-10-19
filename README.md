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

