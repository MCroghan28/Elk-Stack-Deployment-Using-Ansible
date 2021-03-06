## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram of Elk Stack Deployment](Images/Ansible-Docker-Elk.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

- [ansible.cfg](https://github.com/MCroghan28/Ansible-for-WashU/blob/94dc069617ff0f84eb4eeb704fcb2ec582ccf2be/Ansible/ansible.cfg)
- [docker-playbook.yml](https://github.com/MCroghan28/Ansible-for-WashU/blob/94dc069617ff0f84eb4eeb704fcb2ec582ccf2be/Ansible/docker-playbook.yml)
- [filebeat-config.yml](https://github.com/MCroghan28/Ansible-for-WashU/blob/94dc069617ff0f84eb4eeb704fcb2ec582ccf2be/Ansible/filebeat-config.yml)
- [filebeat-playbook.yml](https://github.com/MCroghan28/Ansible-for-WashU/blob/94dc069617ff0f84eb4eeb704fcb2ec582ccf2be/Ansible/filebeat-playbook.yml)
- [install-elk.yml](https://github.com/MCroghan28/Ansible-for-WashU/blob/94dc069617ff0f84eb4eeb704fcb2ec582ccf2be/Ansible/install-elk.yml)
- [metricbeat-playbook.yml](https://github.com/MCroghan28/Ansible-for-WashU/blob/94dc069617ff0f84eb4eeb704fcb2ec582ccf2be/Ansible/metricbeat-playbook.yml)
- [metricbeat.yml](https://github.com/MCroghan28/Ansible-for-WashU/blob/94dc069617ff0f84eb4eeb704fcb2ec582ccf2be/Ansible/metricbeat.yml)

 This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load balancing ensures availability by
distributing traffic over multiple servers and ensures traffic is sent to only servers that are online. Jump boxes allow for more easy administration of multiple 
systems and provide an additional layer between the outside and internal assets.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system metrics.

The configuration details of each machine may be found below.

| Name       | Function | IP Address | Operating System |
|------------|----------|------------|------------------|
| Jump Box   | Gateway  | 10.0.0.4   | Linux            |
| Web 1      | Server   | 10.0.0.5   | Linux            |
| Web 2      | Server   | 10.0.0.6   | Linux            |
| Elk-Ubuntu | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 75.132.53.123

Machines within the network can only be accessed by the Jump Box.
The Elk-Ubuntu server can be accessed over port 5601 from 75.132.53.123.

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses |
|----------    |---------------------|----------------------|
| Jump Box     | Yes                 | 75.132.53.123        |
| Web 1        | No                  |                      |
| Web 2        | No                  |                      |
| Elk -Ubuntu  | Yes                 | 75.132.53.123        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time, reduces 
the chance of human error, and makes it easy to configure multiple machines at once and ensures the configurations are identical. 


The playbook implements the following tasks:

  -installs docker.io, python3, and docker

  -configures the virtual machine where Elk is being installed to use more memory *The Elk container will not run without this setting!*

  -uses Ansible's sysctl module to automatically run in case the virutal machine is restarted

  -configures the Elk container to start with port mappings: 
    
    -5601:5601
    
    -9200:9200
    
    -5044:5044
    
  -starts the container
  
  -enables the docker service on boot so if the virtual machine is restarted, the docker service run automatically:
  
  ![Screenshot of the Elk-install Playbook](Images/Screenshot-Elk-Install.PNG)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Screenshot of docker ps ](Images/Screenshot-docker-ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1: 10.0.0.5
- Web 2: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log data from specific files on remote machines. An example is an Apache log that logs events handled by the Apache web server such as requests 
the server received from other sources, it's response and internal actions taken by the apache server.
- Metricbeat collects metrics of the remote system. An example is how much CPU is being used which helps determine the health of the system.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [Install-Elk-playbook](Ansible/install-elk.yml) file to the Ansible container.
- Update the hosts file found in /etc/ansible/hosts to include the Elk virtual machine along with its IP address as a separate group.
- Run the playbook, and navigate to [(Public IP Address of Elk VM):5601/app/Kibana](http://[your.Elk-VM.External.IP]:5601/app/kibana) to check that the installation worked as expected.


