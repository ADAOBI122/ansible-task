Automating a Simple Web Server Deployment on AWS Using Ansible
Overview

As a Junior DevOps Engineer, your task is to automate the setup of a simple web server on an AWS EC2 instance using Ansible. The goal is to:

Connect to the EC2 instance via SSH
Install Apache Web Server
Start and enable Apache so it runs on boot
Replace the default web page with a custom HTML page containing your name

This guide explains step by step how to accomplish this, including inventory setup, playbook creation, running the playbook, and verifying deployment.

1️⃣ Prerequisites

Before you start, ensure you have the following:

AWS EC2 instance running Ubuntu (or similar Linux)
SSH private key (PEM file) for connecting to the EC2 instance
Vagrant VM  with Ansible installed on it (most recent version of ansible)
Python 3 installed on  host machine (latest version)
Internet access on your host and EC2 instance

Check Ansible installation:

ansible --version


installed Ansible via:
pip3 install --upgrade --user ansible
The installer put the binaries here:
/home/vagrant/.local/bin/
Your old ansible was at:
/usr/bin/ansible
That old system binary is gone (or ignored)
Bash still looks at /usr/bin first → says No such file or directory
 Step 1: Add pip’s local bin to your PATH

Run this:

export PATH=$HOME/.local/bin:$PATH
 Step 2: Verify the new Ansible works
ansible --version

You should now see:

ansible [core 2.17.14]
python version = 3.10.12
 Step 3: Make PATH permanent

So you don’t have to type export every time:

echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
 Step 4: Test your inventory
ansible web1 -i inventory.yml -m ping
Should return:
web1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}


Clean up old system Ansible

If you want to remove the old apt version completely:

sudo apt remove ansible -y
sudo apt autoremove -y


Running the Playbook
Test connectivity to your EC2 instance:
ansible -i text.yml web1 -m ping

Expected output:

web1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
Run the playbook:
ansible-playbook -i inventory.yml text.yml

Verifying Deployment
Open a browser and navigate to:
http://<AWS_EC2_PUBLIC_IP>
You should see your custom HTML page with your name:


Deliverables Checklist
Inventory file screenshot → shows host and SSH key configuration
Ansible playbook screenshot → shows tasks for Apache installation and HTML deployment
Deployed HTML page screenshot → shows your name on the web page
