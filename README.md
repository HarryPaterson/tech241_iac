<h1 style="text-align: center;">Infrastructure as Code</h1>

### Contents
* Intro
* Setting up Controller, App and Database
* Ad-hoc Ansible commands
* Writing Nginx Playbook

### Intro

Infrastructure as Code (IaC) is an approach in software engineering that treats infrastructure configuration and management as code, enabling automation and version control. Among the popular IAC tools, Ansible stands out as an open-source configuration management and automation tool. It operates agentlessly using SSH, utilizes declarative YAML-based playbooks for defining desired system states, and boasts a large community and ecosystem with numerous built-in modules for extensive functionality. With its scalability, idempotent tasks, and ease of use, Ansible has become a favored choice for automating complex infrastructure and deployment tasks while following IAC principles.

### Setting up Controller, App and Database 
![](https://i.imgur.com/VkhIdCu.png)

1. Create 3 EC instances: running ubuntu 18.04 with SSH enabled
2. Name Controller, app and DB.
3. SSH into the Controller
4. sudo apt update -y
5. sudo apt-get install software-properties-common
6. sudo apt-add-repository ppa:ansible/ansible
7. sudo apt update -y
8. sudo apt install ansible -y
9. Update and Upgrade both App and Database
10. In Controller, cd /etc/ansible/
11. cd ~/.ssh
12. sudo nano tech241.pem
13. Copy in private key from local machine
14. sudo chmod 400 tech241.pem 
15. cd ..
16. sudo nano hosts
17. Add in:
```
[app]
app-instance ansible_host=54.77.128.148 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/tech241.pem
```
18. sudo ansible app -m ping
19. Output:
```
app-instance | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
20. Repeat for Database with correct name and IP.

### Ad-hoc Ansible commands
1.OS of VM
```
 ansible app -a "uname -a"
``` 
Location of VM
```
sudo ansible app -a "date"
```
Memory Available of VM
```
sudo ansible app -a "free"
``` 
Check files of VM
```
sudo ansible app -a "ls -l"
```
Copy file to VM
```
sudo ansible app -m copy -a "src=test.txt dest=test.txt"
```

###  Writing Nginx Playbook

Also in /etc/ansible. Create playbook with:
```
sudo nano nginx-playbook.yml
```
Fill with:
```
# Why YAML
# YAML file start with --- three dashes
# Why playbooks
# create a playbook to install nginx in web node
---


# which host to perform the task
- hosts: app

# see the logs by gathering facts
  gather_facts: yes

# admin access
  become: true
# add the instructions - install nginx - web
  tasks:
  - name: Installing Nginx
    apt: pkg=nginx state=present
# ensure the status of nginx is actively running
# adhoc command to check the status
```
Run playbook:
```
sudo ansible-playbook nginx-playbook.yml
```
Check status:
```
sudo ansible app -a "systemctl status nginx"
```
### Node and pm2 Playbook

Add port 3000 to SG

```
---

# Which host to perform the task
- hosts: app

# see the logs by gathering facts
  gather_facts: yes

# admin access (sudo)
  become: true

# add the instructions
  tasks:
  - name: Node key
    apt_key:
      url: "https://deb.nodesource.com/gpgkey/nodesource.gpg.key"
      state: present

  - name: NodeSource repository
    apt_repository:
      repo: "deb https://deb.nodesource.com/node_12.x {{ ansible_distribution_release }} main"
      state: present

  - name: Install Node.js
    apt:
      name: nodejs
      state: present
      update_cache: yes

  - name: Install PM2
    npm:
      name: pm2
      global: yes
      state: present

  - name: Install app dependencies
    command: npm install
    args:
      chdir: "app"

  - name: Start the Node.js app
    command: pm2 start app.js
    args:
      chdir: "app/app"


```
