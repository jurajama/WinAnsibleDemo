## Overview
Demonstration of how to deploy Windows VM in Azure with Ansible. 
Ansible communicates with Windows via WinRM interface. _azurevm_ role automatically installs WinRM to VM so that no manual steps are required.

## Preconditions
Linux machine that acts as Ansible client. It could be also a Docker container, for example centos:latest.

Install Ansible and other required modules:
```
yum -y install epel-release
yum -y install git python-pip
pip install ansible
pip install pywinrm packaging msrestazure ansible[azure]
```

Clone git repository:
```
git clone https://github.com/jurajama/WinAnsibleDemo.git
cd WinAnsibleDemo
```

Study configuration parameters defined in _host_vars/wintestvm001.yml_. Those override the default values defined in _roles/azurevm/defaults/main.yml_. Also have a look at _hosts_ file that is the Ansible inventory file.

## Execution:
Set environment variables to refer to your Azure account:
```
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_SECRET=xxxxxxxx
export AZURE_TENANT=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

See more information in https://docs.ansible.com/ansible/2.6/scenario_guides/guide_azure.html

Run playbook:
```
ansible-playbook create-winserver.yml
```

## Resource deletion
Delete the created resource group using Azure Portal GUI.
