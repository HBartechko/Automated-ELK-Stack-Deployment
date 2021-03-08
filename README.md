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

- Part 1: Installing Filebeat on the DVWA Container
- Make sure that the ELK server container is up and running:
- Navigate to http://[your.VM.IP]:5601/app/kibana. Use the public IP address of the ELK server that you created.
- Click 'Explore on my Own'
--If you do not see the Kibana server landing page, open a terminal on your computer and SSH into the ELK server.
- Run docker container list -a to verify that the container is on.
--If it isn't, run sudo docker start elk.
-Use the ELK server's GUI to begin installing Filebeat on your DVWA VM.
--Navigate to your ELK server's IP address:
- Click Add Log Data.
--Choose System Logs.
- Click on the DEB tab under Getting Started.
- 
- Part 2: Creating the Filebeat Configuration File
- Open a terminal and SSH into your jump box:
- Start the Ansible container.
- Use the correct Docker command to attach to your Ansible container.
-	Run: curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml 
-- root@6160a9be360e:/etc/ansible# curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > filebeat-config.yml

- Once you have this file on your Ansible container, edit it as specified:
-- The username is elastic and the password is changeme.
-- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine.
-- output.elasticsearch:
-- hosts: ["10.1.0.4:9200"]
-- username: "elastic"
-- password: "changeme"
-- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine.
-- setup.kibana:
-- host: "10.1.0.4:5601"
- Save this file in /etc/ansible/files/filebeat-config.yml.
Part 3: Creating the Filebeat Installation Play
5.	Next, create a new playbook that installs Filebeat and then copies the Filebeat configuration file you just made to the correct location.
o	On the Ansible VM, create a playbook file, filebeat-playbook.yml.
	Locate this file in your /etc/ansible/roles/ directory.
o	Open your playbook and implement the following tasks:
	Download the .deb file from artifacts.elastic.co.
	Install the .deb file using the dpkg command shown below:
	dpkg -i filebeat-7.4.0-amd64.deb
	Copy the Filebeat configuration file from your Ansible container to your WebVM's where you just installed Filebeat. Make sure it is copied to: /etc/filebeat/filebeat.yml
	Use Ansible's copy module to copy the entire configuration file to the correct place.
	Run the following commands:
	filebeat modules enable system
	filebeat setup
	service filebeat start
	Enable the filebeat service on boot.
	Hint: Use the Ansible module systemd to make sure the filebeat service is running. More info at Ansible.com.
o	You may find the following hints and links helpful:
	This play should only run on the web machines that are running the DVWA containers.
	Refer to the Ansible playbook documentation if needed.
	Use the Ansible copy module to move filebeat-config.yml onto the Web VMs.
	You can use the command module to run curl, dpkg, and Filebeat commands.
	Use curl -O or curl -o to download the dpkg file.
Note: You can use the following template for configuring the Filebeat playbook: Filebeat Playbook Template. You can also build your own if you'd like an additional challenge.
After you create and save this file, run it to install Filebeat on the DVWA machines.
Part 4: Verifying Installation and Playbook
6.	After the playbook completes, follow the steps below to confirm that the ELK stack is receiving logs from your DVWA machines:
o	Navigate back to the Filebeat installation page on the ELK server GUI.
o	On the same page, scroll to Step 5: Module Status and click Check Data.
o	Scroll to the bottom of the page and click Verify Incoming Data.

- ansible-playbook filebeat_playbook.yml
