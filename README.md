# Ansible

Ansible is a simple way to automate infrastructure and application deployment. Ansible is opensource and more information about what it can do and how to use it can be found on its [website][awl] or its [Github][agh] page.

# Rancher
Rancher Labs builds open source software for building a private container service. Rancher makes running Docker on any infrastructure simple and scalable. More information can be found [here][rwl].

# This Github repository purpose
This repo is for my personal use around deploying a few Rancher environments for Lab use at home. These playbooks likely will not work for you out of the box or may required editing for functionality. They are expected to run against Centos 7.2+ nodes and will do the following:

  - Setup basic server settings (NTP/SNMP)
  - Update operating systems via YUM and install docker version 1.12.6 (current version of rancher recommends this)
  - Install Controller software via docker 
  - Install Agent software via docker 

# Getting it to work in your environment
Unfortunately Agent nodes will not install on one full run, you will need to run the control.yml playbook then login to your rancher node and pull the ADD HOST docker commands.

### Running Control Playbook
```
ansible-playbook -i hosts control.yml -k
```
To get the add host string [follow these directions][rah] and update the variable file located at /group_vars/all.yml - lines 21 and 24 are what we are looking at. 

### Running Agent Playbook
Once the group_vars file is updated, verify IP addresses are correct in your host file then simply deploy:
```
ansible-playbook -i hosts agent.yml -k
```
After a few minutes you should see nodes populate in the Rancher UI under infrastructure.

# Need Help?
I am always happy to answer questions around this playbook, but if you are having issues with Rancher or Ansible commands I recommend you visit there help/support forums.
 - [Ansible Google Groups][af]
 - [Rancher Forums][rf]

   [awl]: <https://ansible.com>
   [rwl]: <http://rancher.com/>
   [rah]: <https://docs.rancher.com/rancher/v1.4/en/hosts/custom/>
   [af]: <https://groups.google.com/forum/#!forum/ansible-project>
   [agh]: https://github.com/ansible/ansible
   [rf]: https://forums.rancher.com/