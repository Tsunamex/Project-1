## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](https://user-images.githubusercontent.com/78612951/122715911-98970380-d237-11eb-9c45-f4db6568cb9d.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - Installing-elk.yml.txt
  - filebeat-playbook.yml.txt
  - metricbeat-playbook.yml.txt

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting indbound access to the servers.
-Loadbalancers protect the system against DDos attacks. They can reroute traffic between servers incase of an attack. 
The can divert attack traffic away from corporate servers to cloud servers. 
The advantage of a jumpbox is that you create a single node from which to monitor and configue your systems and servers. Also restricts entry into your network
to a single point of entry. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.
- Filebeat watches log files or locations that are specified, logic events, it indexes this data for logstash or elastic search
- Metricbeat records metrics and statistics and forwards it to logstash or elastic search.

The configuration details of each machine may be found below.

| Name               | Function   | IP Address   | OS    |
|--------------------|------------|--------------|-------|
| Jumpbox-Provsional | Gateway    | 13.64.195.91 | Linux |
| Web-1              | Web-sever  | 10.0.0.11    | Linux |
| Web-2              | Web-server | 10.0.0.12    | Linux |
| Elk-Stack          | ELK Server | 10.3.0.4     | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox-Provisonal machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- [Localhost IP]

Machines within the network can only be accessed by the Jumpbox-Provsional
- The Jumpbox-Provisonal can access the ELK-Stack machine. The IP address is [Localhost IP].
A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible           | Allowed IP Addresses |
|--------------------|-------------------------------|----------------------|
| Jumpbox-Provsional | Yes (from local host)         | [LocalHostIP]        |
| Web-1              | No/Yes accessible via Jumpbox | 10.0.0.4             |
| Web-2              | No/Yes accessible via Jumpbox | 10.0.0.4             |
| Elk-Stack          | No/Yes accessible via Jumpbox | 10.0.0.4             |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- automation allows you to delegate tedious, time-consuming tasks so that we can focus on higher-priority tasks. 
For using ansible, coding is not a prerequiste. It can execute compicated IT task flows in a simple manner.

The playbook implements the following tasks:
- Install-elk.yml: The following playbook is used to configure the ELK server. It downloads and installs docker, and the pulls correct container into ELK VM. 
It configures the machine to use more memory. And has a restart policy in place start elk container every time the machine boots. It configures that ports 5601 to be used 
to host the Kibana GUI.
- filebeat-playbook.yml: The playbook configures filebeat for the kibana GUI. This playbook downloads, installs and configures filebeat correctly. It starts the filebeat service, 
and has a restart policy in place for it to run on systemboot
- metricbeat-playbook.ymk: The playbook configures metricbeat for the kibana GUI. This playbook downloads, installs and configures metricbeat correctly. It starts the metricbeat service,
 and has a restart policy in place for it to run on systemboot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker_ps_output](https://user-images.githubusercontent.com/78612951/122716171-ea3f8e00-d237-11eb-9696-adfd733d0722.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.11 & 10.0.0.12

We have installed the following Beats on these machines:
- filebeat and metricbeat 

These Beats allow us to collect the following information from each machine:
-filebeat collects log events specified by log files and location. While metric beats collects metrics and statistics from servers. The metrics could vary from system resources to metrics of services being run on 
the given system

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yaml file to /etc/ansible/roles
- Update the hosts file to include private IP of ELK-Server
- Run the playbook, and navigate to ELK-Server to check that the container is running.

- Install-elk is the playbook. It is copied into /etc/ansible/roles
- The host file is updated to make Ansible run the playbook on a specific machine. We specify the [elk] header followed by the IP of machine ensure ELK-stack is installed in the correct machine. 
We declaree the private IPs 
of Web-1 and Web-2 under [webservers] to ensure filebeat is installed on the correct machine. 
- We navigate to http://137.117.94.210:5601/app/kibana to access the kibana-GUI
