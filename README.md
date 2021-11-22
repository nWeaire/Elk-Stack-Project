# Elk-Stack-Project
The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _/etc/ansible/my-elkservers.yml_

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly Redundant, in addition to restricting strain to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
- Load balancers protect against DDOS attacks as they spread any incoming traffic between VMs to reduce the strain, this also allows us to still connect if one of the VMs in the load balancer pool goes down. 
- Jump boxes allow us to monitor all access to the network through 1 single point rather then dozens of access points, and allows us to focus our security on one point.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_
- Filebeat checks for any changes in the file system and tracks when those changes are made.
- _TODO: What does Metricbeat record?_
- Metricbeat collects metrics and stats from the operating system and other applications, then outputs them in a file type you specific for example logstash or elasticsearch

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| Web-1    | Server   | 10.0.0.8   | Linux            |
| Web-2    | Server   | 10.0.0.9   | Linux            |
| Web-2    | Server   | 10.0.0.11  | Linux            |
| Elk-Sever| Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
- 120.156.214.136 

Machines within the network can only be accessed by The Jumpbox.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
- Jumpbox VM 10.0.0.5

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses         |
|-------------|---------------------|------------------------------|
| Jump Box    | Yes                 | Home IP                      |
| Web-1       | No                  | 10.0.0.4                     |
| Web-2       | No                  | 10.0.0.4                     |
| Web-3       | No                  | 10.0.0.4                     |
| Elk-Server  | No                  | 10.0.0.4 or 120.156.214.136  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
Allows you to update a range of servers exactly the same with one command rather then connecting to each individually and installing everything at one of a time

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- install docker.io
- install python-pip
- install docker python module
- Increase memory availability
- download and lauch a docker elk container on ports 5601, 9200, 5044
- enable docker service


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- Web-1 - 10.0.0.8 
- Web-2 - 10.0.0.9
- Web-3 - 10.0.0.11

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
- Metricbeat and Filebeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- filebeat monitors and read log files in the location specified to find changes to the log files and then uploads thoses changes in a log to something like elasticsearh or logstash
- metricbeat collects metrics from applications that are running as well as the operating system, then outputs that data.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Ansible file to /etc/.
- Update the hosts file to include the VMs you wish to update
- Run the playbook, and navigate to each web VM to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- /etc/ansible/ELK.yaml or /etc/ansible/filebeat.yml or /etc/ansible/metricbeat.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- The hosts file located at /etc/ansible/hosts to add the ip address for filebeat/metricbeat under [webservers], and the elk server under [ELK]
- _Which URL do you navigate to in order to check that the ELK server is running?
- www.ELKSERVERPUBLICIP:5601 for example www.20.211.187.243:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
