## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.

  - [ELK](https://github.com/Majohn89/Works-Completed/blob/0b639865de7a76eb1e6ce84519d44e0699f6504a/Ansible/install-elk.yml)
  - [Filebeat](https://github.com/Majohn89/Works-Completed/blob/f8c9f0fa77c2af80dc75e78e78936a4b437782f8/Ansible/filebeat-playbook.yml)
  - [Metricbeat](https://github.com/Majohn89/Works-Completed/blob/f8c9f0fa77c2af80dc75e78e78936a4b437782f8/Ansible/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- Load balancing plays an important security role as computing moves evermore to the cloud.
The offloading function of a load balancer defends an organization from DDOS attacks. 
It does this by shifting attack traffic from the corporate server to a public cloud provider.

This system is utilizing jump box VM to manage the network. 
- This is advantageous because we have implemented more hardened security measures on it and it can manage the other systerms within our security zone and overall network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files of VMs on the network and system metrics. We are using Filebeat and Metricbeat on our system.
- **Filebeat** is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. 
- **Metricbeat** is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Web-1    | Webserver  | 10.0.0.5   | Linux            |
| Web-2    | Webserver  | 10.0.0.6   | Linux            |
| Web-3    | Webserver  | 10.0.0.7   | Linux            |
| ELK      | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.7.95.212

Machines within the network can only be accessed by Jump Box virtual machine.
- 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.7.95.212          |
| Web1     | No                  | 10.0.0.4             |
| Web2     | No                  | 10.0.0.4             |
| Web3     | No                  | 10.0.0.4             |
| ELK      | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- it allows IT administrators to automate away the drudgery from their daily tasks. That frees them to focus on efforts that help deliver more value to the business by spending time on more important tasks.

The playbook implements the following tasks:
- Install Docker
- Install python3-pip
- Install Docker python module
- Set the vm.max_map_count to 262144

You can view the playbook here:
- [ELK](https://github.com/Majohn89/Works-Completed/blob/69d903e99b94a18bdd08ce87c33ba6550f2e12d0/Ansible/install-elk.yml)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Diagrams/ELKStack sebp 2.22.21.PNG](https://github.com/Majohn89/Works-Completed/blob/8d5c7a740f4cf6081eb69885345a30165cc4b4cd/Diagrams/ELKStack%20sebp%202.22.21.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- **Web1** 10.0.0.5
- **Web2** 10.0.0.6
- **Web3** 10.0.0.7

We have installed the following Beats on these machines:
- **Filebeat**
- **Metricbeat**

These Beats allow us to collect the following information from each machine:
- **Filebeat** detects changes to the filesystem. We use is to to collect Apache logs.
- **Metricbeat** detects changes in the system metrics, such as CPU usage. Weuse it to detect SSH login attempts, failed **sudo** escalation, and CPU/RAM statistics.

The following playbooks will install Filebeat and Metricbeat:
- [Filebeat](https://github.com/Majohn89/Works-Completed/blob/4d2427801ff3edfa7594dadbb4101c9e918dcf75/Ansible/filebeat-playbook.yml)
- [Metricbeat](https://github.com/Majohn89/Works-Completed/blob/4d2427801ff3edfa7594dadbb4101c9e918dcf75/Ansible/metricbeat-playbook.yml)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml playbook to the Ansible Control Node.
- Update the hosts file to include the ip addresses of your DVWA machines and your ELK Stack machine
- Run the playbook, and navigate to **http://[YOUR.VM.IP]:5601/app/** to check that the installation worked as expected.

You will see this screen if the installation succeeded.

- ![Success](https://github.com/Majohn89/Works-Completed/blob/60bfdb43ebb360360b03efd471ffe4fc3dfbf7aa/Diagrams/successfullaunch%203.4.21.PNG)

Repeat this process for the Filebeat and Metricbeat playbooks.

A success installation of Filebeat should yield the following response on Kibana:

- ![Success](https://github.com/Majohn89/Works-Completed/blob/018057e0afd64e94bacf4a4c48bfffe05e757811/Diagrams/FileBeatModuleStatus%202.27.21.PNG)

A successfult insllation of Metricbeat should yield the following response on Kinbana:

- ![Sucess](https://github.com/Majohn89/Works-Completed/blob/018057e0afd64e94bacf4a4c48bfffe05e757811/Diagrams/MetricBeatModuleStatus%202.27.21.PNG)


