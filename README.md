# Cloud-Security
Cloud Security (Azure)
# Cloud-Security
Cloud Security (Azure)
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![]project 1 Kamran Diagram.drawio(Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _YML____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: elk_playbook.yml_

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly ___effective__, in addition to restricting ___Access__ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
For Traffic Balancing and for jumpbox aad security and there is no access from the public
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the ___Config or Setupo__ and system __files___.
- _TODO: What does Filebeat watch for?_ Files 
- _TODO: What does Metricbeat record?_Like recording or monitoring on the server

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web 3   |   Webserver  10.0.0.8     |   Linux         |                  |
| Web 4    |  Webserver   10.0.0.9     |        Linux    |                  |
| Web 5    |  Webserver  10.0.0.12      |          Linux  |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ___Jumpbox__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by __Virtual Machine ___.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?  My Computer 40.71.189.212 _

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.8 10.0.0.9    |
|  Web 3       No |                     |           40.71.189.212           |
|  Web 4   |  No                   |                      |40.71.89.212
                                                        40.71.189.212
   Web 5        No                                        40.71.189.212
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_ change whatever in VM

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...Install   Docker.io
     Install python3-pip  (Nano)
- ...Download Docker , Container , Run 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png) photo 2021-09-20-17-56-55.jpg

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
        10.0.0.1
		10.0.0.8
		10.0.0.9
		10.0.0.12
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
        Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

 Filebeat gonna monitor files and whatever happend and any unwanted issue will prevent
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ____Configg_ file to ___playbook__.
- Update the __elkand_ansible and __ file to include...
- Run the playbook, and navigate to __Redteam ![Project 1 Kamran Diagram](https://user-images.githubusercontent.com/63748371/134783966-b8cce048-f752-4d7a-bd8c-b26c1134191f.jpg)
__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
 elk-playbook.yml file
- _Which file do you update to make Ansible run the playbook on a specific machine? elk file 
How do I specify which machine to install the ELK server on versus which to install Filebeat on?_checking the Server
- _Which URL do you navigate to in order to check that the ELK server is running?  http://24.90.212.156:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
 Ansible Playbook and Configuration 
 files
  Elk-playbook.yml
   - name: Config ELK with Docker
     hosts: elk
      become: true
 tasks:
 - name: Install docker.io
 apt:
 update_cache: yes
 name: docker.io
 state: present
 - name: Install pip3
 apt:
 force_apt_get: yes
 name: python3-pip
 state: present
 - name: Install Docker Python Module
 pip:
 name: docker
 state: present
 - name: Download and launch a Docker web container
 docker_container:
 name: elk
 image: sebp/elk:761
 state: started
 restart_policy: always
 published_ports:
 - 5601:5601
 - 9200:9200
 - 5044:5044
 - name: Configure elk VM to use more memory
 sysctl:
 name: vm.max_map_count
 value: "262144"
 state: present
 reload: yes
 - name: Enable Docker service
 systemd:
 name: docker
 
 
 
 Ansible Hosts
[webservers]
10.0.0.8 ansible_python_interpreter=/usr/bin/python3
10.0.0.9 ansible_python_interpreter=/usr/bin/python3
10.0.0.12 ansible_python_interpreter=/usr/bin/python


Ansible-playbook.yml
 - name: Config Web VM with Docker
 hosts: webservers
 become: true
 tasks:
 - name: docker.io
 apt:
 update_cache: yes
 name: docker.io
 state: present
 - name: Install pip3
 apt:
 name: python3-pip
 state: present
 - name: Install Python Docker Module
 pip:
 name: docker
 state: present
 - name: Download and launch a docker web container
 docker_container:
 name: dvwa
 image: cyberxsecurity/dvwa
 state: started
 restart_policy: always
 published_ports: 80:80
 
 
 - name: Installing and Launch Filebeat   hosts: webservers   become: yes   tasks:     # Use command module   - name: Download filebeat .deb file     command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb      # Use command module   - name: Install filebeat .deb     command: dpkg -i filebeat-7.4.0-amd64.deb      # Use copy module   - name: Drop in filebeat.yml     copy:       src: /etc/ansible/files/filebeat-config.yml       dest: /etc/filebeat/filebeat.yml      # Use command module   - name: Enable and Configure System Module     command: filebeat modules enable system      # Use command module   - name: Setup filebeat     command: filebeat setup      # Use command module   - name: Start filebeat service     command: service filebeat start

    # Use systemd module
  - name: Enable service filebeat on boot
    systemd:
      name: filebeat
      enabled: yes



- name: Configure Elk VM with Docker   hosts: elk   remote_user: azadmin   become: true   tasks:     # Use apt module     - name: Install docker.io       apt:         update_cache: yes         name: docker.io         state: present        # Use apt module     - name: Install pip3       apt:         force_apt_get: yes         name: python3-pip         state: present        # Use pip module     - name: Install Docker python module       pip:         name: docker         state: present        # Use sysctl module     - name: Use more memory       sysctl:         name: vm.max_map_count         value: "262144"         state: present         reload: yes        # Use docker_container module     - name: download and launch a docker elk container       docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044

      # Use systemd module
    - name: Enable service doc
    
	
	- name: Installing and Launch Filebeat   hosts: webservers   become: yes   tasks:     # Use command module   - name: Download filebeat .deb file     command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb      # Use command module   - name: Install filebeat .deb     command: dpkg -i filebeat-7.4.0-amd64.deb      # Use copy module   - name: Drop in filebeat.yml     copy:       src: /etc/ansible/files/filebeat-config.yml       dest: /etc/filebeat/filebeat.yml      # Use command module   - name: Enable and Configure System Module     command: filebeat modules enable system      # Use command module   - name: Setup filebeat     command: filebeat setup      # Use command module   - name: Start filebeat service     command: service filebeat start

    # Use systemd module
  - name: Enable service filebeat on boot
    systemd:
      name: filebeat
      enabled: yes



- name: Configure Elk VM with Docker   hosts: elk   remote_user: kamra  become: true   tasks:     # Use apt module     - name: Install docker.io       apt:         update_cache: yes         name: docker.io         state: present        # Use apt module     - name: Install pip3       apt:         force_apt_get: yes         name: python3-pip         state: present        # Use pip module     - name: Install Docker python module       pip:         name: docker         state: present        # Use sysctl module     - name: Use more memory       sysctl:         name: vm.max_map_count         value: "262144"         state: present         reload: yes        # Use docker_container module     - name: download and launch a docker elk container       docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044

      # Use systemd module
    - name: Enable service doc

