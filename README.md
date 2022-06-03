## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

[Project 1 Network Diagram](https://github.com/Moonzarinh/Project-1/blob/main/Project%201%20Network%20Diagram%20Assignment.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - [ymlfiles](https://github.com/Moonzarinh/Project-1/tree/main/Ansible)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box?
Load Balancers protect web-security, web-traffic and availability. Jump Box is like automation and access control. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for? Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- What does Metricbeat record? They take metrics and statistics that collects and ships them to the output that specify such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| WEB 1    |Web Server| 10.0.0.5   | Linux            |
| WEB 2    |Web Server| 10.0.0.6   | Linux            |
| WeB 3    |Web Server| 10.0.0.7   | Linux            |
| ELK      |ELK Server| 10.2.0.4   | Linux            |
|LoadBalan |Load bal  |20.29.86.155| Linux            |
|



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ElK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Workstation Public IP through TCP 5601.


Machines within the network can only be accessed by Workstation and Jump-Box-Provisioner.
- Which machine did you allow to access your ELK VM? What was its IP address?
Jump-Box-Provisioner IP : 10.0.0.4 via SSH port 22
Workstation Public IP via port TCP 5601

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | Workstation Public IP on SSH 22
| WEB 1    | NO                  |10.0.0.1 on SSH 22
| WEB 2    | NO                  |10.0.0.1 on SSH 22
| WeB 3    | NO                  |10.0.0.1 on SSH 22
| ELK      | NO                  |Workstation Pub IP using TCP 5601
|LoadBalan | NO                  |Workstation Public IP on HTTP 80


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because asible lets you quickly and easily deploy multitier apps. You won't need to write custom code to automate your systems; you list the tasks required to be done by writing a playbook, and Ansible will figure out how to get your systems to the state you want them to be in.
- What is the main advantage of automating configuration with Ansible?_
No special coding skills are necessary to use Ansible's playbooks. 

The playbook implements the following tasks:

In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Making a azure virtual machine VM named " ELK " 
- Add an [elk] group to your Ansible VM's hosts file by following the steps below on the command line
- Once you've created the [elk] group, you'll create a playbook to configure it.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

![Elk Screenshot image](https://github.com/Moonzarinh/Project-1/blob/main/README%20Assignemnt/Images/ELk.png) 

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 : 10.0.0.5
-Web2 : 10.0.0.6

We have installed the following Beats on these machines:
- ELK Server, Web1 and Web2
- The ELK Stack Installed are: FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc
- The filebeat has log events, which is a lightweight shipper for forwarding and centralizing log data.The Metricbeat has metric and system statistics which helps you monitor your servers by collecting metrics from the system and services running on the server, such as: Apache.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the '/etc/ansible/files/filebeat-config.yml' file to '/etc/ansible/files/filebeat-playbook.yml'.
- Update the filebeat-playbook.yml file to include installer
- Run the playbook, and navigate to filebeat to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- Which file is the playbook? Where do you copy it?
The Ansible is the playbook. It will create the my-playbook.yml 
The Filebeat we will create filbeat-playbook.yml as our playbook.
For Metricbeat we will create metricbeat-playbook.yml as our playbook.
- Which file do you update to make Ansible run the playbook on a specific machine? 
The host file 

How do I specify which machine to install the ELK server on versus which to install Filebeat on?
Filebeat is inside the monitor. They push logs into the logs stash. 

- _Which URL do you navigate to in order to check that the ELK server is running?
Test Kibana on web : http://[your.ELK-VM.External.IP]:5601/app/kibana
Test Kibana on localhost: sysadmin@10.1.0.4: curl localhost:5601/app/kibana


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

On the Jump box run the command to get the playbook: curl https://github.com/benjhaddock/CyberSecurityP1/blob/main/Ansible/elk_install.yml > /etc/ansible/roles/elk_install.yml

Edit the hosts file in /etc/ansible and add the details from the screenshot and update your ip addresses

To run the Playbook: ansible-playbook /etc/ansible/roles/elk_install.yml

Installing Filebeats:

Download the playbook with the command: curl https://github.com/benjhaddock/CyberSecurityP1/blob/main/Ansible/filebeat_playbook.yml > /etc/ansible/roles/filebeak_playbook.yml
Run the playbook with: ansible-playbook /etc/ansible/roles/filebeat_playbook.yml