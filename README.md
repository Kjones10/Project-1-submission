# Project-1-submission
Project 1 - GitHub fundamentals and Elk stack
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Project-1-submission / Diagrams / Project 1 diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook_file may be used to install only certain pieces of it, such as Filebeat.

ansible-playbook-install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box?_Load balancers protect against DDoS attacks by shifting the attack traffic and dispersing it elsewhere. The advantage of a jump box is that you are able to access and manage devices (through the jump box) in a separate security zone. Any tools that are used within the jump box are also maintained on that system.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
What does Filebeat watch for?_Filebeat monitors and collects log files and forwards the data to be indexed.
What does Metricbeat record?_Metricbeat records metrics and statistics from the system and services running.

The configuration details of each machine may be found below.







|   Name   | Function | IP Address | Operating System |
|:--------:|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| Web 1    | Server   | 10.0.0.6   | Linux            |
| Web 2    | Server   | 10.0.0.7   | Linux            |
| ELK      | Server   | 10.1.0.4   | Linux            |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 137.117.105.199

Machines within the network can only be accessed by jumpbox.
Which machine did you allow to access your ELK VM? What was its IP address?_10.0.0.5 jumpbox

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | yes                 | 86.53.134.175/23     |
| Web 1    | no                  | 10.0.0.5             |
| Web 2    | no                  | 10.0.0.5             |
| ELK      | no                  | 10.0.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?_Ansible is very powerful and efficient. 

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
-Install docker.io
-Install python3-pip
-Install docker module
-download and launch a docker elk container
-enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.  

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_ 10.0.0.5 10.0.0.6 10.0.0.7 

We have installed the following Beats on these machines:
Specify which Beats you successfully installed_ Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects any activity changes made on the system.
Metricbeat collects the metrics and statistics on the system.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ssh-keygen file to ssh public key
- Update the hosts file to include the IP address
- Run the playbook, and navigate to your terminal to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ 
src: /etc/ansible/files/filebeat-config.yml
dest: /etc/filebeat/filebeat.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? Update the hosts file
How do I specify which machine to install the ELK server on versus which to install Filebeat on?_Use the -c flag to specify the path to the config file.
- _Which URL do you navigate to in order to check that the ELK server is running? http://[your_elk_server_ip]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._


- Sudo apt install ansible
- Sudo apt update
- curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.4.0-amd64.deb
- dpkg -i metricbeat-7.4.0-amd64.deb
- metricbeat modules enable docker
- metricbeat setup
- service metricbeat start
- curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb
- dpkg -i filebeat-7.4.0-amd64.deb
- filebeat modules enable system
- filebeat setup
- service filebeat start
