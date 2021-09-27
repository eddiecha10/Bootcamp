## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](Diagrams/Week 12 Network Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metric and statistics and system logs.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                |Function  | IP Address | Operating System |
|---------------------|----------|------------|------------------|
| Jump Box Provisioner| Gateway  | 10.0.0.4   | Linux            |
| Web-1               | DVWA     | 10.0.0.5   | Linux            |
| Web-2               | DVWA     | 10.0.0.6   | Linux            |
| Web-3               | DVWA     | 10.0.0.7   | Linux            |
| ELK                 | Monitor  | 10.0.1.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
98.255.91.163

Machines within the network can only be accessed by SSH
- Jumpbox Provisioner via ansible container
- 20.106.142.121

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump Box Provisioner | no                  | 20.106.142.121       |
| Web-1                | no                  | 10.0.0.4             |
| Web-2                | no                  | 10.0.0.4             |
| Web-3                | no                  | 10.0.0.4             |
| ELK                  | no                  | 10.0.1.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is time efficient as well as if it is
done correctly via script it can be ran again for errorless mass configuration. 

The playbook implements the following tasks:
- Installation and configuration of Docker on multiple VMs
- Installation and configuration of DVWA, Filebeat and Metricbeat on corresponding VMs
- Installation and configuration of ELK stack onto separate VM.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](Ansible/Images/elk docker.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- filebeat: log data/events (e.g. audit logs, deprecation logs, server logs) from specified logs/locations
- metricbeat: metric data from specified servers such as CPU usage, memory usage.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the "install-elk.yml" and " filebeat-playbook.yml" files to etc/ansible.
- Update the "hosts" file to include 
  -"[Internal IP of desired machine for ELK installation] ansible_python_interpreter=/usr/bin/python3 under a [elk] headline you inputted
  -"[Internal IP of desired machines for filebeat and metricbeat] ansible_python_interpreter=/user/bin/python3 under a [webserver] headline you inputted
- Run the playbook, and navigate to "http://[public IP of ELK machine]:5601/app/kibana to check that the installation worked as expected.
- Run "filebeat-playbook.yml" to install filebeat and metricbeat onto Web-1/2/3
