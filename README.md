# Elk-Stack-Project-1
Class Project-1, Elk Stack Deployment 
 Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
 
 



   These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

       /etc/ansible/install-elk-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


 Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network.

- What aspect of security do load balancers protect?
   	- Load balancers protects the system from DDoS attacks by shifting attack traffic.
  	- Load Balancing contributes to the Availability aspect of security in regards to the CIA Triad.
 
- What is the advantage of a jump box?
   	- The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.
   	- The advantage of a JumpBox is the orgination point for launching Administrative Tasks. This ultimately sets the JumpBox as a SAW (Secure Admin Workstation). All Administrators when conducting any Administrative Task will be required to connect to the JumpBox (SAW) before perfoming any task/assignment.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the changes to the Logs and system traffic.

- What does Filebeat watch for?_
   	- Filebeat watches for any information in the file system which has been changed and when it has.  
   	- Filebeat watches for log files/locations and collects log events
- What does Metricbeat record?_
  	- Metricbeat takes the metrics and statistics that collects and ships them to the output you specify.
   	- Metricbeat records metric and statistical data from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name      |  Function | IP Address | Operating System   |
|------------ |----------  |-------------- |-------------------------|
| JumpBox | Gateway  |  10.0.0.8    |  Linux(ubtntu 18.04)|           
| Web-1     | Server      |  10.1.0.9    |  Linux(ubtntu 18.04)|                     
| Web-2     | Server      |  10.1.0.10  |  Linux(ubtntu 18.04)|                       
| Web-3     | Server      |  10.1.0.11  |  Linux(ubtntu 18.04)|            
| Elk-VM1 | Elk Server|  10.0.0.4    |  Linux(ubtntu 18.04)|

           
 Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses_
    	- Public IP address which changes everytime when the VM is on/off eg of Public IP 137.135.115.14

Machines within the network can only be accessed by SSH.

- Which machine did you allow to access your ELK VM? What was its IP address? JumpBox VM, its private Ip address(Vnet IP)-10.1.0.8

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|--------------|----------------------- |---------------------------|
| Jump Box  |     NO                    |    10.1.0.8                   |
| Web-1       |     NO                    |     10.1.0.9                  |
| Web-2       |     NO                    |    10.1.0.10                 |
| Web-3       |     NO                    |    10.1.0.11                 |
| Elk-VM1   |     NO                    |    10.0.0.4                   |


 Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
  	- This allows you to deploy to multiple servers using a single playbook

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install docker.io
- Install Python-pip
- Install docker container
- Launch docker container: elk
- Command: sysctl -w vm.max_map_count=262144

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
 
 

Target Machines & Beats

This ELK server is configured to monitor the following machines:

- List the IP addresses of the machines you are monitoring:-
    	- Web-1(10.1.0.9) Web-2(10.1.0.10)and Web-3(10.1.0.11)

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed:-
    	-  Filebeat
    	-  Metricbeat

These Beats allow us to collect the following information from each machine:

    - In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

   	- Filebeat monitors log files or locations you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
   	- Metricbeat collects metrics from the operating system and from services running on the server.

 Using the Playbook-install-elk.yml

     In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

   - Copy the playbook file to /etc/ansible.
   - Update the the configuration file to include the webservers and ElkVM (private Ip address. 
   - Run the playbook, and navigate to ElkVM to check that the installation worked as expected.
/etc/ansible/host should include:

[webservers]
[10.1.0.9] ansible_python_interpreter=/usr/bin/python3
[10.1.0.10] ansible_python_interpreter=/usr/bin/python3
[10.1.0.11] ansible_python_interpreter=/usr/bin/python3

[elk]
[10.0.0.4] ansible_python_interpreter=/usr/bin/python3

Run the playbook, and SSH into the Elk vm, then run docker ps to check that the installation worked as expected.
Playbook: install_elk.yml Location: /etc/ansible/install_elk.yml
Navigate to  http://[your.ELK-VM.External.IP]:5601/app/kibana to confirm ELK and kibana are running.  You may need to try from multiple web browsers
Click 'Explore On Your Own' and you should see the following:

 


Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?
    	 /etc/ansible/file/filebeat-configuration.yml 
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
        edit the /etc/ansible/hosts file to add webserver/elkserver ip addresses
- Which URL do you navigate to in order to check that the ELK server is running?
    	 http://[your.ELK-VM.External.IP]:5601/app/kibana

 Using the Playbook-filebeat-playbook.yml

 - Copy the filebeat.yml file to the /etc/ansible/files/ directory.
 - Update the configuration file to include the Private IP of the Elk-Server to the ElasticSearch and Kibana sections of the configuration file.
 - Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the filebeat setup, and start the filebeat service.
- Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the metricbeat setup, and start the metricbeat service. 
 - Run the playbooks, and navigate back to the installation page on the ELk-Server GUI, click the check data on the Module Status
 - Click the verfiy incoming Data to check and see the receiving logs from the DVWA machines.  

      you should see the following:

 

 
   The commands needed to run the Ansible configuration for the Elk-Server are:

	- ssh azadmin@JumpBox(Public IP)
	- sudo docker container list -a (locate your ansible container)
	- sudo docker start container (name of the container)
	- sudo docker attach container (name of the container)
cd /etc/ansible/
	- ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server
	- cd /etc/ansible/roles/
	- ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat)
	- open a new web browser (http://[your.ELK-VM.External.IP]:5601/app/kibana)                                           This will bring up the Kibana Web Portal
	- check the Module status for file beat and metric beat to see their data receiving.

**You will need to ensure all files are properly placed before running the ansible-playbooks.




