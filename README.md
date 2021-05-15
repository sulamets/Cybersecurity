# Cybersecurity

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[ELK-Diagram](diagram/ELK-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

[playbook.yml](linux/playbook.yml)

[elk.yml](linux/elk.yml)

[filebeat.yml](linux/filebeat.yml)

[hosts](ansible/hosts)

[ansible.cfg](ansible/ansible.cfg)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly `available`, in addition to restricting `inbound access` to the network.
```
Load Balancing plays an important security role as computing moves evermore to the cloud. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider.

Jump box prevents all Azure VM's to expose to the public. This means that this will be our entry point connecting via Remote Desktop Protocol (RDP) from our on-premise network. It also helps us to open only one port instead of several ports to connect different virtual machines present in the Azure cloud.
```

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the `file systems of the VMs on the network` and system `system metrics`.
```
Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.
```

The configuration details of each machine may be found below.

| Name        | Function   | IP Address | Operating System |
| ------------ | ----------- | ------------- | -------------------- |
| Jump Box | Gateway  |   10.0.0.7   | Linux                      |
| Web-1       |       VM     |   10.0.0.8   | Linux                      |
| Web-2       |       VM     |   10.0.0.9   | Linux                      |
| Web-3       |       VM     |  10.0.0.12  | Linux                      |
| Elk             |      VM      |   10.2.0.4   | Linux                      |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the `jump box` machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
`23.99.64.136`

Machines within the network can only be accessed by `each other`.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |        Yes          |    23.99.64.136      |
|   Web-1  |         No          |    10.0.0.1-254      |
|   Web-2  |         No          |    10.0.0.1-254      |
|   Web-3  |         No          |    10.0.0.1-254      |
|   ELK    |         No          |    10.2.0.1-254      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- easy to manage
- easy to restart and deploy

The playbook implements the following tasks:
- install docker io
- install pip
- install docker python
- increase virtual memory 
- use more memory
- download and launch docker container
- enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[A screenshot of docker ps output](image/docker_ps_output)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.8
- 10.0.0.12

We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat: it detects changes to the filesystem. Specifically, we use it to collect Apache logs.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the `yml` file to `/etc/ansible`.
- Update the `hosts` file to include `webservers` and `elk`
- Run the playbook, and navigate to `curl http://10.2.0.4:5601` to check that the installation worked as expected.

Q&A:
- Which file is the playbook? Where do you copy it? `/etc/ansible`
- Which file do you update to make Ansible run the playbook on a specific machine? `hosts`
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? `Port 5601 for ELK server and Port 9200 for Filebeat`
- Which URL do you navigate to in order to check that the ELK server is running? `http://10.2.0.4:5601`
