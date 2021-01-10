## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Topology](Images/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.

  - [ELK Stack Playbook](Ansible/ansible/roles/elk-stack-playbook.yml)
  - [Filebeat Playbook](Ansible/ansible/roles/filebeat-playbook.ym)
  - [Metricbeat Playbook](Ansible/ansible/roles/metricbeat-playbook.ym)
  -
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
- Configure maximum mapped memory with `sysctl` module
- Install `docker.io` and `python3-pip` packages with `apt` module
- Install docker `python` package with `pip`
- Enable systemd docker service
- Run ELK docker container


The following screenshot displays the result of running `docker ps -a` after successfully configuring the ELK instance.

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
- Filebeat parses and forwards system logs from the Web VMs to the ELK Stack in an easy to read format.
- Metricbeat reports system and service statistics about the ELK stack VM.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the `elk-stack-playbook.yml` playbook file to `/etc/ansible/roles/`
    directory inside the ansible container.
    `$ sudo docker cp elk-stack-playbook.yml ansible:/etc/ansible/roles/elk-stack-playbook.yml`

- **Optional:** Copy the whole directory for the Metricbeat and Filebeat
        playbooks and configuration files.
    `$ sudo docker cp Ansible/ansible ansible:/etc/ansible`

- Update the `/etc/ansible/hosts` file to include the ELK stack VM IP address.

    - Example configuration of `/etc/ansible/hosts`
```yaml
[elk]
10.1.0.100  ansible_python_interpreter=/usr/bin/python3
alpha.example.org  ansible_python_interpreter=/usr/bin/python3
192.168.1.100  ansible_python_interpreter=/usr/bin/python3
```
- Run the playbook, and navigate to `http://[your.VM.IP]:5601/app/kibana.` to check that the installation worked as expected.
    `$ ansible-playbook /etc/ansible/roles/elk-stack-playbook.yml`

    - Check that the ELK Stack playbook is functioning by accessing kibana from
        a web browser.

![ELK Webpage Screenshot](Images/elk_webpage_screenshot.png)

- **Optional:** To configure Filebeat on your web VMs run the following
    commands

  - Edit `/etc/ansible/files/filebeat-config.yml` to include the ELK Stack IP address.

```yml
output.elasticsearch:
hosts: ["<vm.ip.addr>:9200"]
username: "elastic"
password: "changeme"
```
```yml
setup.kibana:
host: "<vm.ip.addr>:5601"
```
	- Then run the playbook
  `$ ansible-playbook /etc/ansible/roles/filebeat-playbook.yml`


- **Optional:** To configure Metricbeat on your web VMs run the following command

  - Edit `/etc/ansible/files/metricbeat-config.yml` to include the ELK Stack IP address.

```yml
output.elasticsearch:
hosts: ["<vm.ip.addr>:9200"]
username: "elastic"
password: "changeme"
```
```yml
setup.kibana:
host: "<vm.ip.addr>:5601"
```
		
  - Then run the playbook
  `$ ansible-playbook /etc/ansible/roles/metricbeat-playbook.yml`
