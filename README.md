# Ansible Windows Facts

A repository for Ansible playbook that gathers Windows facts using the Ansible setup module.
Creates the following output using the facts:

* RAW JSON
* RAW YAML
* Formatted CSV (select fields)
* Formated Markdown (select fields)
* Interactive HTML Mind Map (select fields)

Copywrite John Capobianco July 25,2020

## Instructions for Linux users

### Linux / Ansibe Host prequisites

These playbooks have been developed and tested under Ansble 2.9.1 on CentOS 7.8.2003

You will require Git, Ansible, Node.js 12, Mark Map, WinRM, and Kerberos on your Linux / Ansible host.

### Windows / Target Host prequisites

Your Windows host targets need to have WinRM installed.

The playbook uses WinRM over HTTP and authenticates using Kerberos (domain credentials).

## REFERENCES

Windows Hosts Requirements for Ansible - https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html#host-requirements

Windows Remote Management - https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html

Using Ansible and Windows - https://docs.ansible.com/ansible/latest/user_guide/windows_usage.html

Ansible Setup - Gather Facts - https://docs.ansible.com/ansible/latest/modules/setup_module.html

This playbook assumes the Windows target has WinRM installed and listening on 5985 and that the Ansible host is configured correctly and can reach the target Windows host via this HTTP port.

It is very important when prompted for your username that you use username@MY.DOMAIN.COM. This whole string is case sensitive and the domain portion *must* be in upper case.

#### Install steps - CentOS

1. Update yum

$ sudo yum -y update

2. Install Ansible

$ sudo yum install epel-release
$ sudo yum install ansible

3. Install node.js 12

$ curl -sL https://rpm.nodesource.com/setup_12.x | sudo bash -
$ sudo yum install -y gcc-c++ make
$ sudo yum install -y nodejs

4. Install Mark Map

$ npm install markmap-lib -g

5. Install WinRM

pip install "pywinrm>=0.3.0"

6. Install Kerberos

yum -y install python-devel krb5-devel krb5-libs krb5-workstation

7. Install the Python WinRM Kerberos wrapper

pip install pywinrm[kerberos]

#### Install steps - Ubuntu

1. Update Ubuntu - this step will take some time. 

$ sudo apt update
$ sudo apt-get upgrade -y

2. Make sure Python is installed.

$ sudo apt-get install python -y

3. Install Ansible.

$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible -y

4. Install node.js

$ sudo apt install npm

5. Install Mark Map 

$ npm install markmap-lib -g

6. Install WinRM

apt-get install -y python3-winrm

7. Install Kerberos

sudo apt-get install python-dev libkrb5-dev krb5-user

8. Install the Python WinRM Kerberos wrapper

pip install pywinrm[kerberos]

## Instructions for Windows Users

### Windows Prequisites

These playbooks require the Windows Subsystems for Linux and the Ubuntu OS from the Microsoft Store.
Aside from this requirement, the Linux prequisites similarly apply to Windows 10.

#### Install Steps - Windows 10

1. Right-click the Windows Start icon - select Apps and Features.

![image](./images/appsfeatures.png)

2. In the Apps and Features window - click Programs and Features under Related Settings on the right side of Apps and Features.

![image](./images/programsfeatures.png)

3. Click Turn Windows Features On or Off in the left (with the shield icon) side of the Programs and Features window.

![image](./images/turnon.png)

4. Scroll to bottom of the Features window and put a check mark beside Windows Subsytem for Linux; Click Ok and close the open windows.

![image](./images/wsl.png)

5. Launch the Microsoft Store.

![image](./images/store.png)

6. Search for Ubuntu - click the first result.

![image](./images/ubuntusearch.png)

7. Click Install.

![image](./images/install.png)

8. Wait for Ubuntu to install.

9. Press Windows Key and start typing Ubuntu - click and launch Ubuntu.

10. The first time Ubuntu launches it has to setup - give this some time.

11. Enter your username and password for Ubuntu.

12. Update Ubuntu - this step will take some time. 

$ sudo apt update

$ sudo apt-get upgrade -y

13. Make sure Python is installed.

$ sudo apt-get install python -y

14. Install Ansible.

$ sudo apt-add-repository ppa:ansible/ansible

$ sudo apt-get update

$ sudo apt-get install ansible -y

15. Install node.js.

$ sudo apt install npm

16. Install Mark Map.

$ sudo npm install markmap-lib -g

17. Install WinRM

apt-get install -y python3-winrm

18. Install Kerberos

sudo apt-get install python-dev libkrb5-dev krb5-user

8. Install the Python WinRM Kerberos wrapper

pip install pywinrm[kerberos]

## Clone the repository

1. git clone https://github.com/automateyournetwork/WindowsFacts.git

2. Modify the permissions 

chmod -R 755 /home/"username"/WindowsFacts

3. Ubuntu Bug fix 

To work around a bug that prevents the Ansible playbook from running on certain versions of Ubuntu please run the following:

sudo mv /usr/bin/sleep /usr/bin/sleep.dist
sudo ln -s /bin/true /usr/bin/sleep

## Run the playbook(s)

1. Update your hosts file and include the Windows hostname under [Windows]. If FQDN is required for the Ansible Linux host please use the FQDN. 

[Windows]

yourhost.your.domain.com

2. cd WindowsFacts/playbooks

### All Hosts

ansible-playbook WindowsFacts.yml

Provide your domain username@YOUR.DOMAIN.COM

**EXTREMELY_IMPORTANT_NOTE**

The username above is case sensitive and *must* include the @YOUR.DOMAIN.COM or the kerberos token will be invalid and the playbook will fail. 

Provide your domain password.

The playbook will run.

Provide a Git Commit Message.

Provide your Git repository username.

Provide your Git repository password.

### Select Hosts

ansible-playbook WindowsFacts.yml --limit <host>

Provide your domain username@YOUR.DOMAIN.COM

**EXTREMELY_IMPORTANT_NOTE**

The username above is case sensitive and *must* include the @YOUR.DOMAIN.COM or the kerberos token will be invalid and the playbook will fail. 

Provide your domain password.

The playbook will run.

Provide a Git Commit Message.

Provide your Git repository username.

Provide your Git repository password.

## Review the reports

The Reports are stored in documentation/servers/WINDOWS/.

/csv

Contains comma separated format. Fully searchable / sortable / filterable.

/json

Contains the RAW JSON from the Ansible Facts.

/markdown

Contains mark down format.

/mindmaps

Contains HTML mind maps best viewed in Google Chrome.

/yaml

Contains the RAW YAML from the Ansible Facts.