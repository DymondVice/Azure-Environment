# Azure-Environment
Azure Network
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Azure_Network](https://github.com/DymondVice/AzureLabs/raw/main/AzureDiagram.png)

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
- First for my playbook i made the YAML file and started with --- then to name: config Web VM with docker so i could start there
- then i used ansible apt module to install the docker.io and python3-pip, with the update_cache so it will install the docker.io (its similar to running apt get)
- so with the [update_cache: yes] i will use the ip module to install docker.
- then i will run - name: Install Python Docker Module so that ansible can utilize the module to control docker containers.
- Used the Ansible docker-container module to install the cyberxsecuirty/dvwa container and published it to port 80 on the container to port 80 on the host
- i put my [restart_policy: always] to ensure that the container restarts if you restart the web vm. without it i would have to restart my container when i restart the machine.
- last i put in the [systemd] module to restart the docker service when the machine reboots.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![DockerRunningonELK](/DockerRunningonELK.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name  | Monitoring  | IP of machine |
|-------|-------------|---------------|
| Web-1 | YES         | 10.0.0.5      |
| Web-2 | YES         | 10.0.0.6      |
| Web-3 | YES         | 10.0.0.7      |

We have installed the following Beats on these machines:
| Name  | BEATS       | IP of machine |
|-------|-------------|---------------|
| Web-1 | Metric/file | 10.0.0.5      |
| Web-2 | Metric/file | 10.0.0.6      |
| Web-3 | Metric/file | 10.0.0.7      |

These Beats allow us to collect the following information from each machine:
- The data that my beats collect (file/metricbeat) are both a "lightweight shipper" filebeat is for forwarding and centralzing log data, just to help you keep the more plain things simple and offer a much ligher weight to forward them and centralize logs and the files that they belong with. Metricbeat is more for the metrics. With metricbeat the systems collect info from the CPU to memory, Redis to NGINX and a lot more. you should be getting all your data in a central area with both metric/filebeat that makes it easy to see and very human readable.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- I started my install of the filebeat by getting into my Ansible container 
- then i ran a curl command : curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat >> /etc/ansible/filebeat-config.yml
- then instead of editing individual lines in the /etc/filebeat/filebeat-config.yml it was easier to keep a copy of the intire config file with my ansible playbook and use the ansilbe copy module to copy the preconfigred file into place
- i configured the config file to include the IP address of the ELK VM
- went to line #1106 and #1806 and replaced the hosts line with the ip of my ELK VM e.g. 10.1.0.4.9200
- i saved the files in the /etc/ansible/files/filebeat-config.yml
- i then created another ansible playbook that accomplishes the linux filebeat install instructions
- i downlaoded the .deb file from  artifacts.elastic.co.
- installed the .deb file using the dpkg command: dpkg -i filebeat-7.4.0-amd64.deb
- then i coped the filebeat config file from my ansible containter to my webvms where i installed filebeat
- copied the entier config to the correct place 
- and placed it in my Files directory in ansible
- ran the filebeat modules enable system command 
- ran the filebeat setup command.
- ran the service filebeat start command.
- and enabled filebeat service on the boot.
- ran my filebeat install with :ansible-playbook filebeat-playbook.yml
- went to my Kibana page to verify it had correctly worked

