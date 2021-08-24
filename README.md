# Project1
Project 1 Cybersecurity Bootcamp Columbia

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

 ![RedTeam Diagram](https://user-images.githubusercontent.com/89435904/130558428-1746334d-0b93-4b82-9c4a-610341281383.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

  ![Alt text](Ansible/elk_install.yml)
  https://github.com/ArnaudBMB/Project1/blob/8a91e438f53882157d608d99f76b5ad50995b0ea/Ansiblefilebeat-playbook.yml
  https://github.com/ArnaudBMB/Project1/blob/8a91e438f53882157d608d99f76b5ad50995b0ea/Ansible/pentest.yml
  https://github.com/ArnaudBMB/Project1/blob/8a91e438f53882157d608d99f76b5ad50995b0ea/Ansible/metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

What aspect of security do load balancers protect?

Load balancers protect against DDoS attacks (Denial-of-Service) by allocating resources to the different systems.

What is the advantage of a jump box?_

The advantages of a jump is that it is gateway for other systems and allows for easier and safer access to the those systems.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.

What does Filebeat watch for?_

Filebeat watches and records system logs.

What does Metricbeat record? 

Metricbeat records metrics of your systems and resources and services running on these same systems..

The configuration details of each machine may be found below.

| Name                 | Function      | IP Address | Operating System |
|----------------------|---------------|------------|------------------|
| Jump-Box-Provisioner | Gateway       | 10.0.1.4   | Linux            |
| Web-1                | Web           | 10.0.1.5   | Linux            |
| Web-2                | Web           | 10.0.1.6   | Linux            |
| Web-3                | Web           | 10.0.1.7   | Linux            |
| Elk-VM               | ElasticSearch | 10.1.0.4   | Linux            |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

•	$home_IP

Machines within the network can only be accessed by the Jumpbox.

•	Public IP: 52.224.184.235
•	Private IP: 10.0.1.4
 
A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible   | Allowed IP Addresses        |
|------------|-----------------------|-----------------------------|
| Jumpbox    | Yes                   | $home_IP                    |
| Web 1-3    | No                    | RedTeam-LB (52.170.136.117) |
| RedTeam-LB | Yes - HTTP - 80       | *                           |
| ELK        | Yes - Kibana - 5601   | *                           |
| ELK        | Yes - HTTP API - 9200 | 10.0.0.0/16                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

The automation allows to reduce the numbers of configurations mistakes that could be done if performed manually.

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.

- Install Docker: Install Docker to the Jumpbox VM
- Install Python3_pip to allow to install different dockers more easily in the future.
-Docker Module: Installs the docker component modules.
-Increase the memory and use more memory: This allows the ELK Docker Image to launch.
-Install ELK Container: Installs the ELK docker container and launches it with corrects ports.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker_output](https://user-images.githubusercontent.com/89435904/130558492-8b38c1bf-a112-45ec-a376-4239ed5b49d0.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

•	10.0.1.5
•	10.0.1.6
•	10.0.1.7
•	10.1.0.4


We have installed the following Beats on these machines:						
We installed Filebeat and Metricbeat on Web-1, Web-2, Web-3.

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.
•	Filebeat collects system logs.
•	Metricbeat collects metric logs such as CPU usage, memory and data logs.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /ect/ansible.
- Update the hosts file to include [elk] as well as the IP of the ELK Server
- Run the playbook, and navigate to http://40.75.122.15/5601/app/kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?

The file for the Elk Playbook is this:  https://github.com/ArnaudBMB/Project1/blob/db56e8dcbddb3b146ab0c4b43978ed675282fe40/Ansible/elk_install.yml
The file for the Filebeat Playbook is:  https://github.com/ArnaudBMB/Project1/blob/db56e8dcbddb3b146ab0c4b43978ed675282fe40/Ansible/filebeat-playbook.yml
Both files should be copied in /etc/ansible

-Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

The file to update on Ansible to run the playbook on a specific machine is the hosts. To specify you need to create different groups such as webservers and elk, to then know on which you're installing the ELK server or Metricbeat.


- Which URL do you navigate to in order to check that the ELK server is running? 

http://[your.ELK-VM.External.IP]:5601/app/kibana


As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

•	Command to download the Elk playbook:

curl https://github.com/ArnaudBMB/Project1/blob/db56e8dcbddb3b146ab0c4b43978ed675282fe40/Ansible/elk_install.yml > /etc/ansible/elk_install.yml

•	Edit the hosts files in /etc/ansible with the IP Address from your ELK VM.

•	Run the playbook in /etc/ansible with ansible-playbook elk-install.yml

•	Check Kibana to see if the install worked with the URL: http://[your.ELK-VM.External.IP]:5601/app/kibana

Command to download the Filebeat playbook:

curl https://github.com/ArnaudBMB/Project1/blob/db56e8dcbddb3b146ab0c4b43978ed675282fe40/Ansible/filebeat-playbook.yml > /etc/ansible/filebeat-playbook.yml

•	Run the playbook in /etc/ansible with ansible-playbook filebeat-playbook.yml

•	Check Kibana to see if the install worked with the URL: http://[your.ELK-VM.External.IP]:5601/app/kibana. Go to Add Log Data then System Logs.

Command to download the Metricbeatplaybook:

curl https://github.com/ArnaudBMB/Project1/blob/db56e8dcbddb3b146ab0c4b43978ed675282fe40/Ansible/metricbeat-playbook.yml > /etc/ansible/metricbeat-playbook.yml

•	Run the playbook in /etc/ansible with ansible-playbook metricbeat-playbook.yml

•	Check Kibana to see if the install worked with the URL: http://[your.ELK-VM.External.IP]:5601/app/kibana. Go to Add Metric Data then Dockers Metric.



