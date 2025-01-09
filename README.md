Project: Automate Jenkins Deploy Using Ansible

Usage

This project demonstrates how to automate the deployment of Jenkins on an AWS EC2 instance using Ansible. It allows users to easily set up and configure Jenkins without manual intervention, ensuring a repeatable and consistent process. The playbook installs Jenkins, its dependencies, and ensures the service is running and enabled for startup on reboot.
This automation is especially useful for DevOps engineers who need a quick and consistent way to set up Jenkins in their CI/CD pipelines.


Prerequisites

1: AWS EC2 Instance

An Ubuntu-based EC2 instance (e.g., Ubuntu 20.04 or 22.04).

A valid security group with the following inbound rules:

SSH (Port 22): For Ansible to connect and run commands.

HTTP (Port 80): For accessing Jenkins via a browser.

Custom TCP Rule (Port 8080): If Jenkins is not running on the default HTTP port.

2: Ansible Installed on Control Node

Install Ansible on the local machine or control node:

sudo apt update && sudo apt install -y ansible

Verify Ansible installation:

ansible --version

3: SSH Access to EC2

The private key file for SSH access

Ensure permissions for the key file are secure:

chmod 400 key.pem

4: Ansible Inventory File

A properly configured inventory file with the public IP of the target EC2 instance:

[jenkins]
<EC2-instance-public-IP> ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/key.pem

5: Internet Access

Ensure the EC2 instance has outbound internet access to download the necessary packages (e.g., Jenkins, Java).

6: Network Configurations

Open necessary ports for Jenkins access (HTTP or Custom TCP 8080) in the security group attached to the EC2 instance.

7: Updated APT Package Manager

The Ubuntu instance's APT package manager should be up-to-date to avoid package installation errors.

8: Access to Jenkins Repository

Use the correct Jenkins repository key and URL to install Jenkins:

Key: https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

Repository: https://pkg.jenkins.io/debian-stable binary/


Step-by-Step Guide to Run the Playbook

Step 1: Prepare Your Playbook

The playbook file (deploy-jenkins.yml) should contain the necessary tasks to:

Add the Jenkins repository key.

Add the Jenkins APT repository.

Install Jenkins and its dependencies.

Start and enable the Jenkins service.

Step 2: Verify Your Inventory

Update the inventory file to include your EC2 instance details

Step 3: Test Connectivity

Ensure that the Ansible control node can connect to the EC2 instance:

ansible -i inventory all -m ping

Step 4: Run the Playbook

Execute the playbook:

ansible-playbook -i inventory deploy-jenkins.yml

Step 5: Access Jenkins

After a successful playbook run, Jenkins will be installed and running on the EC2 instance.

Connect to the EC2 instance:

ssh -i /path/to/key.pem ubuntu@<instance-public-IP>

Retrieve the initial admin password:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Access Jenkins via a web browser at:

http://<instance-public-IP>:8080

Paste the initial admin password to unlock Jenkins.
