# Interview Questions

## Network Security: Faulty Firewall

  There is a firewall on a network, it is supposed to block SSH connections,
but it is letting the connections through. How might I debug this?

  In a our recent project, I set up my network security group to block all SSH
traffic coming into the vLAN, except coming from my home IP address to the
Jump Box Control Node. The control node was then set up to be able to access
all the virtual machines in the resource group via SSH. If I were to try and
connect to the ELK Stack VM or one of the Web VMs over SSH, the connection
would fail. This would happen because the networking rules are set up such that
the control node VM is the only machine that can access the rest of the network
via SSH, and that control node is the only machine that responds to SSH traffic
coming from the public internet. 

  If one of my virtual machines from Project 1 was accessible from the
internet, I would initially assume it is due to a misconfiguration When 
troubleshooting settings and configurations on the remote system,
I would start by checking the status of the control node VM through the
"Virtual Machines" panel in Azure, if it is stopped, it should be running. 
Next place I would check would be at the Network Security Group corresponding
to the control node and its rules. Next I would use my client machine to check
my own external IP, and the `ssh_config` on the control node to get the port
that the SSH daemon is running on. I would use my home IP, and the SSH server
port number to double check that the rules in the NSG are correct.  Next, I 
would use `systemctl status` to make sure the SSH daemon is running with no 
errors. Lastly I would see if my client machine has a host based firewall that 
may be interfering with the traffic. Assuming everything is up-to-date and all
the machines and services are running, I would then try to connect to the 
control node over the port specified in `ssh_config` to test the settings. 

  The configuration used in Project 1 does not mean that the virtual network is
immune to attacks. However, by adding a central administration point and
blocking all other traffic, it will be easier to monitor and use strict access
control policies to try and make the attack surface smaller. 


## Cloud Security: Containers

  When should a company look into using containerization in their cloud
deployments, and what are the security implications of doing so?

  In my most recent project, we used containers for quite a range of services
and purposes. Initially we used an ansible container on the Jump Box Control
Node to administer all the other virtual machines on the network. I wrote
playbooks to configure the virtual machines and run containerized images of
various applications, such as an ELK Stack as an IDS/log monitoring, DVWA web 
servers for our test web applications, and the aforementioned ansible container
for administration. 

  Like any technology, containers have a list of pros and cons, and in a cloud
environment, containers are a great fit. Some of these benefits include:
segmentation, bundled dependencies and requirements, isolated networking,
consistent configuration, quick setup, and a virtualization layer between the
host OS and the OS within the container. All of these benefits apply to the
containers I configured in Project 1. Some of the security benefits I expected
were the use of application/network segmentation, a layer of abstraction, and
bundled dependencies. 

  In Project 1, I used ansible playbooks to configure the containers running on
all the virtual machines in my Resource Group. These playbooks would be written
to run a series of tasks, each of which would use `systemd` to start `docker`,
configure any necessary settings, and download and run a specific container image.
Once an ansible playbook was run successfully, I needed to check if they were
running. Using DVWA and the ELK Stack as an example, I would navigate to the
IP or webpage of that container in my web browser. For something like the
ansible container on my control node, I could run `# docker ps -a` to get
a list of all containers installed on the OS and their status. 

  It is possible to achieve a similar configuration with regular virtual
machines instead of containers. It is also possible to configure all of these
functions on the host OS without VMs or containers, as well. If the
applications are installed on the host OS, it is often times cheaper because
less overhead would be necessary to run the apps. Since Virtual Machines work
differently, by having their own OS, they are more secure and more isolated
than containers. But some of the trade-offs of VMs is hardware overhead and
more complex configuration. Lastly, downsides of running the software on bare
metal is a severe loss in security and isolation, as well as, more complex
maintenance of dependencies, libraries, and their versions. Patching and
updating would be much more involved and prone to error.

## Logging and Monitoring: Setting Alerts in a New Monitoring System

  What alerts should I set in a new monitoring system?

  I configured various virtual machines for Project 1. I configured three
identical "web servers" to host DVWA containers, which were not publicly
accessible. These sat behind a load balancer, which was publicly accessible. 
I had a Jump Box Control Node, which could access all VMs on the network, but
was only accessible from my home IP for administration and ansible. Lastly,
I configured an ELK Stack VM for monitoring and log collection. The web
interface, Kibana, is publicly accessible from my home IP. 

  The VMs that are not publicly accessible should have alerts about any traffic
coming from outside the vLANs to the VM. For example, the web servers should
have an alert of any connection over port 80 from outside of the two vLANs
created for my cloud network. In addition, they should have alerts for any
`SYN` scans or any other type of reconnaissance. Even if potential enumeration
traffic comes from within the network, it is possible that there is another
machine on the network that is compromised. For a VM like the control node,
I should set up alerts for SSH related traffic. 

  It is possible to use Kibana apps to make alerts. An example alert for the
web servers would send an alert if any external IP ran a port scan or
attempted connection. For a publicly accessible VM, like the jump box, I would
set an alert to notify me in the event of a failed SSH login. There are things
alerts do not address. A huge hole is the fact that they do not account for log
tampering, phished credentials, or other attacks to the administration
channels. They also do not stop or take preventative or responsive action to
these alerts like an intrusion prevention system might
