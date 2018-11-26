# ansible
Learning Ansible
----------------

Setup the infrastructure
------------------------
Usecase: Create a 3 tier application with a load balance, 2 app instances and 1 database.
Inventory
1. Control machine(Ansible tower)
2. Load balancer
3. Application sever 1
4. Application sever 2
5. Database server

Inventory setup
---------------
1. Install vagrant on your local machine[windows/mac]
2. Download the vagrant file and run the first 3 commands from your local machine
```
vagrant plugin install vagrant-hostmanager
vagrant up
vagrant ssh
```
3. Open the virtual box, you can see the Managed virtual machines running
4. once vagrant ssh is executed you will be on the primary machine(control)
5. Edit the ~/.bashrc and add below alias

```
alias lt='ls - ltra'
alias bashrc='vim ~/bashrc'
alias sbash='source ~/.bashrc'

alias pb='cd ~/ansible/playbook'
alias ans='cd ~/ansible'

alias control='ssh 192.168.135.10'
alias lb01='ssh 192.168.135.101' - load balancer
alias app01='ssh 192.168.135.111'
alias app02='ssh 192.168.135.112'
alias db01='ssh 192.168.135.121'
```
6. run below command
```
source ~/.bashrc
```
7. type below command
```
lb01
```
8. you will ssh to ssh 192.168.135.101 by running the below command as it is aliased

rename the hostname to lb01 to reflect the name given to the server.
update the bashrc files with alias and reload the source
repeat the step8 for app01, app02 and db01 server also.

9. After the setup is completed, run below commands to restart all the VMs
```
vagrant halt
vagrant up
vagrant ssh - in control machine
```
10. 
mkdir ansible
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

Copy the dev and ansible files to the control machine
```
ansible --list-host all

ansible -m ping all
ansible -m command -a 'echo Hi' all
ansible -m command -a hostname all
ansible --list-hosts webserver[0]
ansible --list-hosts webserver
```



```
---
- hosts: all
  tasks:
    - command: ping
      command: echo Hi
      command: hostname
      
```



```
 ansible-playbook playbook/hostname.yml
```
 ansible -a "service nginx status" lb01
 ansible -a "service apache2 status" app01
 ansible -a "service apache2 status" app02
 ansible -a "service mysql status" db01






