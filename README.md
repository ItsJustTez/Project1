Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![Project1_Diagram drawio](https://user-images.githubusercontent.com/89175796/156714635-420d30b5-213d-4134-b550-f5eca46d1c08.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

Install-elk.yml
This document contains the following details:

Description of the Topology
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting unwanted and potently malicious traffic to the network.

Load Balancers protect the network from Dos and Ddos attacks. A Jump Box provides a public facing server behind which are the web servers. This reduces the attack surface and increases security.

A Jump Box provides a public facing server behind which are the actual web servers. This reduces the attack surface and increases security.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.


Metricbeat is a lightweight agent that can be installed on target servers to periodically collect metric data from your target servers, this could be operating system metrics such as CPU or memory or data related to services running on the server. It can also be used to monitor other beats and ELK stack itself


The configuration details of each machine may be found below.

Name	Function	IP Address	Operating System
Jump-Box-P	Gateway	Private: 10.0.0.4 // Public: 40.69.163.132	Linux Ubuntu 18.04-Its-gen2

Web-1	Server	Private: 10.0.0.5	Linux Ubuntu 18.04-Its-gen2

Web-2	Server	Private: 10.0.0.6	Linux Ubuntu 18.04-Its-gen2

Web-3	Server	Private: 10.0.0.8	Linux Ubuntu 18.04-Its-gen2

ELK-SERVER	Monitoring	Private: 10.1.0.4 // Public: 20.106.226.87	Linux Ubuntu 18.04-Its-gen2
Access Policies
The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box-P machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

172.58.16.6
Machines within the network can only be accessed by SSH.

The ELK-SERVER can only be accessed by the Jump-Box-P through SSH or from a web request from the whitelisted IP address 172.58.16.6
A summary of the access policies in place can be found in the table below.

Name	Publicly Accessible	Allowed IP Addresses
Jump-Box-P	Yes	172.58.16.6
Web-1	No	10.0.0.4
Web-2	No	10.0.0.4
Web-3	No	10.0.0.4
ELK-SERVER	No	10.0.0.4 // 172.58.16.6
Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

There are several advantages to automating configuration with Ansible, most notably you can efficiently configure multiple servers exactly the same.
The playbook implements the following tasks:

Install docker.io
Install Python
Increase Memory
Download and launch a docker elk container
Enable service docker on boot
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

![docker_ps_output](https://user-images.githubusercontent.com/89175796/156713905-e05afb34-e758-4be8-8682-7c92d96f4b0a.png)

Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1 10.0.0.5 
Web-2 10.0.0.6 
Web-3 10.0.0.8

We have installed the following Beats on these machines:

Filebeat
Metricbeat
These Beats allow us to collect the following information from each machine:

Filebeat collects system log data which can be usefull in many ways such as monitoring when and from when someone attempted to ssh into the jump box.

Metricbeat collects OS and services data from machines running the service. We can use this data to monitor system resources such as memory usage.

Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Copy the ansible-playbook file to ansible docker container.

Update the /etc/ansible/hosts file to include:

[webservers] 10.0.0.5 ansible_python_interpreter=/usr/bin/python3 10.0.0.6 ansible_python_interpreter=/usr/bin/python3 10.0.0.8 ansible_python_interpreter=/usr/bin/python3

[ELK] 10.1.0.4 ansible_python_interpreter=/usr/bin/python3

Run the playbook, and navigate to "ansible -m ping all" to check that the installation worked as expected.

Which file is the playbook?
Pentest.yml

Where do you copy it?
/etc/ansible/pentest.yml

Which file do you update to make Ansible run the playbook on a specific machine?
/etc/ansible/hosts

How do I specify which machine to install the ELK server on versus which to install Filebeat on?
Within the each yaml file there is a specification, “hosts”, that allows you to dictate where it is to be installed. Here you would indicate “elk” or “webservers”
