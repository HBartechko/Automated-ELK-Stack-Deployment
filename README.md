## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Elk Stack Deployment]( https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/Diagrams/ELK%20Stack%20Deployment.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

- ![ansible_config.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/ansible_config.yml)
- ![hosts.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/hosts.yml)
- ![elk_install.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/elk_Install.yml)
- ![filebeat_config.yml]( https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/filebeat-config.yml)
- ![filebeat.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/filebeat.yml)
- ![filebeat_playbook.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/filebeat_playbook.yml)
- ![metricbeat-config.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/metricbeat-config.yml)
- ![metricbeat.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/metricbeat.yml)
- ![metricbeat_playbook.yml](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/metricbeat_plabook.yml)

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
- What aspect of security do load balancers protect?
- Answer: Load balancers availability of the security triad. Load balancers add redundacy.
- What is the advantage of a jump box?
- Answer: A Jump box provides a secure gateway to a network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for?
- Answer: Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- What does Metricbeat record?
- Answer: Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7 / 52.234.179.212   | Linux |
| Load Balancer| Load Balancing | Static External IP | Linux |
| Web-1    | DVWA | 10.0.0.5    | Linux |
| Web-2    | DVWA | 10.0.0.6    | Linux |
| Web-3    | DVWA | 10.0.0.4    | Linux  |
|ELK Stack | Monitoring| 10.1.0.4 / 52.247.127.34| Linux |
|Local Workstation| Access Control | Public IP | Windows |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Public IP address from local workstation can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses: 
- Public IP address from local workstation. 

Machines within the network can only be accessed by Jump Box VM:.
- Which machine did you allow to access your ELK VM? What was its IP address?
- Jump Box: VNET IP 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | Local Workstation IP   |
| ELK Stack| No                  |  10.0.0.7              |
| Web-1    | No                  |  10.0.0.7              |
| Web-2    | No                  |  10.0.0.7 |
| Web-3    | No                  | 10.0.0.7|


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
- Answer: No code experience is need and it simplifies deployment of VMs

The playbook implements the following tasks:

In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
- Create a new VM for ELK
- Add the new VM to Ansible hosts file in your provisioner.
- Create an Ansible playbook that installs Docker and configures an ELK container.
- Run the playbook to launch the container
- Restrict access to the ELK VM

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Screenshot of docker ps output](https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/Images/ELK%20Container%20Image.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring
- 10.0.0.4, 10.0.0.5, 10.0.0.6, 10.1.0.4

We have installed the following Beats on these machines:
Specify which Beats you successfully installed
- Filebeats and Metricbeats

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.
- Filebeat logs the changes done on any files
- Metric beat collects metrics and statistics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _elk_install.yml_ file to  _/etc/ansible/elk_install.yml_.
- Update the _hosts_ file to include
_[elk} 10.1.0.4 ansible_python_interpreter_=/usr/bin/python3
- Run the playbook, and navigate to http://52.177.223.47:5601/app/kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook?_ Where do you copy it? 
- Answer: _/etc/ansible/file/filebeat-config.yml_

- _Which file do you update to make Ansible run the playbook on a specific machine?_ How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- Anwser: nano the _/etc/ansible/host_ file to add _ip address ansible_python_interpreter=/usr/bin/python3_ to _[webserver]or [elk]_
- _Which URL do you navigate to in order to check that the ELK server is running? 
- Answer: http://52.177.223.47:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

For Filebeat playbook

- ssh into the Jump Box : ssh username@jump-box_IP_Address
- sudo docker start _docker container name
- sudo docker attach_docker container name
- cd /etc/ansible/files
- curl https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/filebeat-config.yml > /etc/ansible/files/filebeat-config.yml
- cd /etc/ansible/roles
- curl https://github.com/Wtaoist9/GitHub-Fundamentals-HWK13/blob/main/ansible/filebeat_playbook.yml > /etc/ansible/roles/filebeatt_playbook.yml
- Run: ansible-playbook filebeat_playbook.yml
- curl http://<ELK.VM.External.IP>:5601/app/kibana 

