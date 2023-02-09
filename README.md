# Ansible_playbooks
Ansible:
This is an open source configuration management tool created using python
The main machine where ansible is installed is called as "Controller"
and the remianing remote servers that we are configuring are called as 
"managed nodes/hosts"

From the controller to the managed nodes we should have passwordless
shh connectivity

Ansible is called as "agentless" ie we need not install any client 
s/w of ansible on the remote managed nodes.It uses "push" methodolgy
to push the configurations into the remote servers.

Setup of Ansible
1 Create 2 AWS ubuntu instances
2 NAme the 1st one as controller and remaining 1 as managed node
3 Establish Passwordless ssh from Controller to managed node
  a) Connect to managed node  using gitbash
  b) Setup password for the default user
     sudo passwd ubuntu
  c) Edit the ssh configuration file
     sudo vim /etc/ssh/sshd_config
     Search for "PasswordAuthentication" and change it from no to yes
  d) Restart ssh
     sudo service ssh restart
  e) Connect to Controller using git bash
  f) Generate the ssh keys
     ssh-keygen
  g) Copy the ssh keys
     ssh-copy-id ubuntu@private_ip_of_managed node
4 Installing Ansible
  a) Update the apt repository
     sudo apt-get update
  b) Install software-properties-common
     sudo apt-get install -y software-properties-common
  c) Add the latest version of Ansible to apt repository
     sudo apt-add-repository ppa:ansible/ansible
  d) Update the apt repository
     sudo apt-get update
  e) Install ansible
     sudo apt-get install -y ansible

5 To check the verision of ansible
  ansible --version
We should open this file and store the ipaddress of all the managed nodes here

sudo vim /etc/ansible/hosts
Here copy and paste the ipaddresses of the managed nodes
Step 1:
Create jenkins-install1.yml – playbook for Jenkins installation.
The “hosts” line in the playbook is a list of one or more groups or host patterns.
Step 2:
Roles expect files to be in certain directory names. Each directory must contain a main.yml file. Below is a description of each directory.
tasks – contains the main list of tasks to be executed by the role.
vars – other variables for the role.
Step 3:
Lets take a look at the jenkins-install1.yml file. We have included all the Jenkins tasks here.
Starting with downloading java, Jenkins, installing and configuring Jenkins and finally starting the Jenkins service and enabled.

To run the Ansible Playbook using this command.
 ansible-playbook jenkins-install1.yml -b
 
Post -installation Jenkins setup
Navigate to http://<jenkins public ip>:8080
(replace <jenkins public ip> with your own)
