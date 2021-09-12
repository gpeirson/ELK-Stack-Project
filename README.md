## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.




These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  ~/etc/ansible/roles/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting unauthorized access to the network. Load balancers protect against Denial of Service attacks and help distrubute the traffic to multiple
web servers. The advantage of using a jump box is that it allows for secure access to the network from one machine. The access to and from that machine can then be controlled by a Network Security Group. For example, allowing ssh over port
22 from the local workstation to the jump box. The jump box can then be used to download containers which can distribute software to multiple virtual machines in the network with one playbook. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the syslog file and system traffic. Filebeat is software that sends log information to a desired analysis tool, in this example the data is being sent to Kibana.
Metricbeat is similar to Filebeat and sends data regarding operating system services.

The configuration details of each machine may be found below.


| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.9   | Linux            |
| Web-1    | Web Server | 10.0.0.10  | Linux            |
| Web-2    | Web Server | 10.0.0.11  | linux            |
| ELK-VM   | ELK        | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 68.107.79.134 (my public IP address)

Machines within the network can only be accessed by Jump-Box-Provisioner. The Jump-Box-Provisioner's IP address is 10.0.0.9


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 68.107.79.134        |
| Web-1    | No                  | 10.0.0.9             |
| Web-2    | No                  | 10.0.0.9             |
| ELK-VM   | No                  | 10.0.0.9             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because configuration on each individual virtual machine is not necessary. The pre-configured ansible container
allows the same configuration to be installed on multiple machines.


The playbook implements the following tasks:

1. Installs docker on the virtual machine which is used to install software
2. Specifies an increase in memory use for performance and reloads this preference on reboot
3. Downloads the ELK container using docker
4. Specifies the ports that ELK runs on (5601,9200,5044)
5. Enables the docker service and runs on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker PS](Images/'docker ps'.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 (10.0.0.10)
Web-2 (10.0.0.11)

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat is software that sends log information to a desired analysis tool, in this example the data is being sent to Kibana. Metricbeat is similar to Filebeat and sends data regarding operating system services.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook (.yml) file to ~/etc/ansible/.
- Update the playbook file to the web servers and ELK VM as they are listed in the virtual network.
- Run the playbook, and navigate to either the web servers or the ELK virtual machine to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? File is located at /etc/ansible.install-elk.yml. Copy the file to ansible container at /etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? To update Ansible to run the playbook on a specific machine(s), open the *.yml file and edit the "hosts:" to the desired machine(s). To install ELK on the ELK-VM specify the "elk" host, and to install filebeat on the Web servers update hosts to "webservers"
- _Which URL do you navigate to in order to check that the ELK server is running? Navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana


