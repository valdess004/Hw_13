## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![REDTEAM_NETWORK](Redteam.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - dvwa.yml
    filebeat-config.yml    
    my_fist_playbook.yml
    ELK_Installation.yml  
    filebeat-playbook.yml


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.
- The prupose of load balancers is to protect the network from going offline. Since it allows for redundancy, it means that if any of the other VM goes down, or is in need ofbeing shut down, the lowad balancer can shift the load to another VM. Meaning the applications still up, and no downtime is needed. Moving on to the JBox, the JBox, is a way for the people to access the DVWA without needing to see anything else. With our NSG making sure that nothing else really makes it in, the only exposed access to the world wide web is the IP of our JBox. THis is for the purpose of encapsulating all the other components, as when the DVWA is launched it runs of the IP address of our given JBox IP. 


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.
- Filebeats reads and forwards and keeps tracks of log lines.
- Metric beats keeps track of aspects of your given host OS. Like memory, file system, CPU usage, etc.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| WEB-1    | DVWA-1   | 10.0.0.5   | Linux            |
| WEB-2    | DVWA-2   | 10.0.0.6   | Linux            |
| ELK      |ELK stack | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 40.112.169.175

Machines within the network can only be accessed by SSH through the JBox.
- 10.0.0.4, 10.0.0.5, 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.1 10.0.0.2    |
| WEB-1    | No                  | None                 |
| WEB-2    | No                  | None                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible allows for a more systematic way of updating a mass quantity of VMs without goint through the rigorous process of doing each VM individualy. With the help of containers, ansible make use of YAML files to allow for the update, installation and management of software over all the VM's. This makes it easier to make sure that the network vm's are up to date, and all have the same/necessary software to complete its necessary functions.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install the Docker Module using pip3
- Setup necessary memory space for ELK VM
- Download and Launch a docker ELK container


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5, 10.0.0.6

We have installed the following Beats on these machines:
- _We have installed filebeats. TO be specific filebeat-7.4.0-amd64

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the YAML file to /etc/ansible in given container.
- Update the hosts file to include your VM's IP in the ansible hosts. Make sure to differentatie between the Elk and webservers
- Run the playbook, and navigate to ELK IP to connect trhough url and check that the installation worked as expected.



_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._