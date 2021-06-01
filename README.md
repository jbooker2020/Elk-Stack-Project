# Elk-Stack-Project
Azure servers using elk and Kibana to monitor traffic.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](https://github.com/jbooker2020/Elk-Stack-Project/blob/main/Diagrams/Screen%20Shot%202021-05-20%20at%2011.14.09%20PM.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

![Elk](https://github.com/jbooker2020/Elk-Stack-Project/blob/main/Ansible/Elk)

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
 What aspect of security do load balancers protect? What is the advantage of a jump box?
  
  - Load balancers protect the system from DDoS attack by shifting attack traffic.The advantage of the jump box is to give access to the user from a single node that                could be  secured and monitored

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network.
 What does Filebeat watch for?
  - Filebeat watches for any information in the file system which has been changed and when it was changed.
 What does Metricbeat record?
 - Metric beat takes the metric and statistics it collects and dispributes them to where you specify.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP_Address | Operating_System |
|----------|----------|------------|------------------|
| Jump-Box | Gateway  | 10.0.0.4   |       Linux      |
| Web-1    | Server   | 10.0.0.5   |       Linux      |
| Web-2    | Server   | 10.0.0.6   |       Linux      |
| Elk      | SIEM     | 10.1.0.4   |       Linux      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 Add whitelisted IP addresses:
  - 73.206.89.41

Machines within the network can only be accessed by jump box provisioners.
 Which machine did you allow to access your ELK VM? What was its IP address?_
  - Jump Box VM: VNET IP 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Address |
|----------|---------------------|--------------------|
| Jump-Box |         Yes         |    73.206.89.41    |
| Web-1    |          No         |         N/A        |
| Web-2    |          No         |         N/A        |
| Elk      |         Yes         |         Any        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
 What is the main advantage of automating configuration with Ansible?
 - Free: Ansible is an open-source tool.
 - Very simple to set up and use: No special coding skills are necessary to use Ansible’s playbooks (more on playbooks later).
 - Powerful: Ansible lets you model even highly complex IT workflows.
 - Flexible: You can orchestrate the entire application environment no matter where it’s deployed. You can also customize it based on your needs.
 - Agentless: You don’t need to install any other software or firewall ports on the client systems you want to automate. You also don’t have to set up a separate management        structure.
 - Efficient: Because you don’t need to install any extra software, there’s more room for application resources on your server.

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.:
- Install: docker.io
- Install: python-pip
- Install: docker
- Command: sysctl -w vm.max_map_count=262144
- Launch docker container: elk 
- Enable service docker on boot systemd

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://github.com/jbooker2020/Elk-Stack-Project/blob/main/Ansible/Screen%20Shot%202021-05-25%20at%207.23.54%20PM.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 List the IP addresses of the machines you are monitoring:
   Web-1, 10.0.0.5
   Web-2, 10.0.0.6

We have installed the following Beats on these machines:
- Microbeats

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.
Winlogbeat collects Windows logs that track user logon events.
Filebeat allows the ELK Server to monitor files being accessed by granted or ungranted users. It monitors changes made to sensitive files, the user can figure out when this anevent takes place.If a user altered or accessed the shadow or passwd files, this allows us valuable intelligence into when and how this was done.
Metricbeat allows the ELK Server to monitor valuable usage metrics like CPU usage, memory usage, and monitors what is coming in and out of the server at specified moments in time. This allows for a user to further configure or change/add assets when there may be high traffic volume or usage volume.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to kibana to check that the installation worked as expected.

TODO: Answer the following questions to fill in the blanks:_
Which file is the playbook? Where do you copy it?
 - .yml files are playbook files that can be run with Ansible. Typically, it's copied into a container where ansible is installed to be deployed
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

- _Which URL do you navigate to in order to check that the ELK server is running?
     http://20.186.43.145/:5601/app/kibana
 
As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
- sudo docker start cool_tharp
- sudo docker ps
- sudo docker exec -ti cool_tharp bash
- sudo ansible-playbook filebeat-playbook.yml
- sudo ansible-playbook metricbeat-playbook.yml
