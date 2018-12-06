## Overview
Demonstration of how to deploy Windows VM in Azure with Ansible. 
Ansible communicates with Windows via WinRM interface. _azurevm_ role automatically installs WinRM to VM so that no manual steps are required.

## Preconditions
Linux machine that acts as Ansible client. You can install the tools also in a Docker container, for example centos:latest. 

Install Ansible and other required modules:
```
yum -y install epel-release
yum -y install git python-pip
pip install ansible
pip install pywinrm packaging msrestazure ansible[azure]
```

If you don't want to install any SW yourself, you can use ready-made container https://github.com/jurajama/OS_ansible_client.

Clone git repository:
```
git clone https://github.com/jurajama/WinAnsibleDemo.git
cd WinAnsibleDemo
```

## Customizing your deployment

Study configuration parameters defined in _host_vars/wintestvm001.yml_. Those override the default values defined in _roles/azurevm/defaults/main.yml_. Also have a look at _hosts_ file that is the Ansible inventory file.

You should not use the default username, password and hostname defined in this example code but instead modify them according to your needs. In practise modify hostname in _hosts_ file and note that also the _ansible_host_ FQDN depends on which zone you deploy the VM. When you change the hostname in _hosts_ file, also your host configuration file under _host_vars_ should correspond to the modified hostname so that Ansible finds the variables.

Have a look at also other parameters of _roles/azurevm/defaults/main.yml_ that you may want to override, for example _az_location_ which defines the Azure zone where the VM is deployed.

## Execution:
Set environment variables to refer to your Azure account:
```
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_SECRET=xxxxxxxx
export AZURE_TENANT=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

See more information in https://docs.ansible.com/ansible/2.6/scenario_guides/guide_azure.html and https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal.

Run playbook:
```
ansible-playbook create-winserver.yml
```

The playbook takes a few minutes to complete. After it is successfully executed, you should be able to connect to the VM using the Remote Desktop Connection client of Windows, with the hostname, username and password that was configured in the Ansible inventory.

## Resource deletion
Delete the created resource group using Azure Portal GUI.
