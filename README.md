## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

![Network Topology](Images/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

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
- A load balancer is used in this topology because it increases the
    availability from the CIA Triad. In addition to high availability, a load
    balancer will also restrict access to the internal network that may sit
    beheind the applications servers. 
- A jump box is an advantage for administrators becuase it restricts them to
    use a machine that is only used for administration tasks, so this
    potentially negates possible breaches on a personal computer. In addition
    to this, it is easier to audit and keep track of access, since it is the
    only way to manage the resources in the network. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.

| Name                 | Function           | Private IP Address | Public IP Address | Operating System |
|----------------------|--------------------|--------------------|-------------------|------------------|
| Jump-Box-Provisioner | Gateway            | 10.0.0.4           | 168.62.21.152     | Ubuntu LTS 18.04 |
| Web-1                | Application Server | 10.0.0.5           | N/A               | Ubuntu LTS 18.04 |
| Web-2                | Application Server | 10.0.0.6           | N/A               | Ubuntu LTS 18.04 |
| Web-3                | Application Server | 10.0.0.7           | N/A               | Ubuntu LTS 18.04 |
| elk-stack            | ELK Stack          | 10.1.0.4           | 23.96.81.242      | Ubuntu LTS 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 74.243.14.13

Machines within the network can only be accessed by Jump-Box-Provisioner.

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump-Box-Provisioner | Yes                 | 73.243.14.13         |
| elk-stack            | Yes                 | 73.243.14.13         |
| Web-1                | No                  | 10.0.0.4             |
| Web-2                | No                  | 10.0.0.4             |
| Web-3                | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous 
because it allows a consistent and predictable configuration. In addition to consistency, with an automated setup, the ELK stack
can be created and configured very quickly.  

The playbook implements the following tasks:
- Configure maximum mapped memory with sysctl module
- Install docker and python3-pip with aptitude
- Install docker python package with pip
- Enable docker systemd service
- Run ELK docker container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Screenshot](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6
- Web-3: 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

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
