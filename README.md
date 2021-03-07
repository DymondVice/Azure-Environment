# Azure-Environment
Azure Network
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/DymondVice/AzureLabs/blob/ff5bcd846d1c6d8f4b11bc87954325cdc1723be9/AzureDiagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

 https://github.com/DymondVice/Azure-Environment/tree/main/AnsibleScipts

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
-The load balncers play very special roles with cyber security, the helps to move evermore  computing to the cloud. The assistance of the off-load function of a load balncer helps to defend the organization against the DoS attacks in specifics. it helps that by shifting the attack traffic from the organization servers to the server to a public cloud provider. There is an advantage to having a jumpbox with the fact that any tools in place for the SAn system are maintained through the single system. Therefore, when an update is needed for the software it is able to be done through a single system.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system and system data.
-Filebeat is for Forwarding and centralizing log data. it monitors the log files or loactions that youre are being specified, collects the logged events and forwards them to either elasticseartch or Logstash.
- Metricbeat is a lightweight shipper that you can installl on your servers to periodically collect metrics from the operation system and from other services running on the servers. it takes the metcis and statistics that it collects and ships them to the output that you specify like Elasticsearch or Logstash.

The configuration details of each machine may be found below. 
| Name    | Function       | IP       | Operating System |
|---------|----------------|----------|------------------|
| Jumpbox | Gateway        | 10.0.0.4 | Linux            |
| ELK-VM  | System Monitor | 10.1.0.4 | Linux            |
| Web-1   | Example system | 10.0.0.5 | Linux            |
| Web-2   | Example system | 10.0.0.7 | Linux            |
| Web-3   | Example System | 10.0.0.7 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Home/Personal IP #changeme

Machines within the network can only be accessed by SSH connection.
- The machine i allowed to access my ELK VM was the JumpBox provisioner. The IP address is 52.158.249.100/10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly accessible  | Allowed IP Addresses |
|----------|----------------------|----------------------|
| Jump Box | Yes/SSH              | HomeIP/10.0.0.4      |
| ELK VM   | yes/5601,SSH         | HomeIP/ SSH any      |
| WEB-1    | no-from jumpbox only | HomeIP/SSH           |
| WEB-2    | no-from jumpbox only | HomeIP/SSH           |
| WEB-3    | no-from jumpbox only | HomeIP/SSH           |
 
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
The main advantage of using Ansible is that it helps to allow the IT admins to automate the toiling from the daily taskts. That then Helps to free them to focus their efforts on other things to help deliver more value to the business and by spending time on the more important tasks.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/DymondVice/Azure-Environment/blob/bbdf3e9b35fb1d6924695e86f50f4c66bc6d2191/DockerRunningonELK.jpg

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
