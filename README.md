# Ansible-Project-01
## Pre-requisite
### Review Prerequisites and System Requirements Before Starting Your Ansible Project for Seamless Execution:


- **Basic Understanding of Ansible:** Familiarity with Ansible playbooks, roles, and modules. Knowledge of how to run Ansible commands (e.g., ansible, ansible-playbook) and manage inventories.
> First basic run-command using ansible.
```
ansible -i inventory.ini -m ping all
```

- **AWS Account:** You need an active AWS account to create EC2 instances and AWS access keys for the Ansible control node to interact with AWS resources.

- **IAM User:** Create an IAM user with the required permissions to manage EC2 instances (EC2 full access or custom policy with EC2 and key pair creation permissions).

- **Ansible Control Node:** Set up a local Ansible control node (Ubuntu) where Ansible is installed and configured.

***Install Ansible via pipx:***
``` sudo apt-get install pipx -> pipx install ansible -> ansible --version -> pipx ensurepath -> source ~/.bashrc```

***Install Ansible via apt:***
``` sudo apt update -> sudo apt install ansible -> ansible --version ```

To check if Ansible is installed or not
> ls /home/ubuntu/.local/bin | grep ansible

- **SSH Key Pair:** Create an SSH key pair in AWS to enable SSH access to the EC2 instances.
> Required to setup passwordless authentication among hosts and nodes
```
ssh-keygen -t rsa
```

- **Python & Boto3:** Ensure Python 3 and the boto3 library are installed on the Ansible control node to interact with AWS services.
> Installing python | For Ubuntu/Debian:

``` sudo apt update -> sudo apt install python3 python3-pip -y ```

> Installing boto3 (AWS SDK for Python)

``` python3 -m pip install boto3 ```

- **Ansible Configuration:** Set up Ansible with correct inventory files and configurations (use ansible.cfg for AWS integration).

> setup inventory.ini, playbooks and log output in

```
> /etc/ansibe/ansible.conf
```

- **Security Group:** Open required ports (22 for SSH) on the EC2 instances’ security group.

- **Local SSH Access:** Ensure the control node has SSH access to the instances (via key-based authentication)/(passwordless authentication).

- **Ansible Collection for AWS:** Install the amazon.aws collection for Ansible to manage EC2 instances and community.docker to utilize docker containers and features.

> allows you to use amazon awscli commands in playbook, acts as an API
```
ansible-galaxy collection install amazon.aws
```

> allows you to interact with Docker programmatically from your Ansible playbooks.
```
ansible-galaxy collection install community.docker
```


- **Basic Knowledge of YAML and Ansible Modules:** Understanding of YAML syntax and commonly used Ansible modules (e.g., ec2, ansible.builtin.command, ansible.builtin.shell).

- **Boto3 Credentials:** Set up AWS credentials (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_DEFAULT_REGION) for AWS API interaction.

> Optional cuz it can be configured in the playbook also

``` aws configure ```

This will prompt you for the following:

1. AWS Access Key ID
2. AWS Secret Access Key
3. Default region name
4. Default output format (json, text, etc.)
5. These credentials will be stored in ~/.aws/credentials.

**Alternatively, you can add these lines to your ~/.bashrc file to make them persistent:**

```
echo 'export AWS_ACCESS_KEY_ID="your_access_key_id"' >> ~/.bashrc

echo 'export AWS_SECRET_ACCESS_KEY="your_secret_access_key"' >> ~/.bashrc

echo 'export AWS_DEFAULT_REGION="us-east-1"' >> ~/.bashrc

source ~/.bashrc
```

# Now let's START 🚀👨‍💻

## Task 1
### Create 3 instances on AWS, i.e.. ec2 instances using Ansible LOOPS.

**Configuration:**

* 2 with Ubuntu image
* 1 with Amazon linux image

## Task 2
### Set up passwordless authentication between Ansible control node and newly created instances.

**To-do:**

* In one of the Ubuntu instance setup a passwordless authentication and in the other use password for ssh.

## Task 3
### Automate the shutdown of Ubuntu Instances only using Ansible Conditionals.

**Purpose:**
* To understand Ansible's idempotent nature

**Hints:**
* Use when condition on ansible gather_facts

## Task 4
### Configure a Web Server on Ubuntu EC2 Instances

**Steps:**

* Use the apt module to install Nginx.
* Start and enable Nginx to run on system boot using the service module.
* Deploy a sample index.html page to /usr/share/nginx/html.
* Ensure that the web server is accessible by testing the HTTP connection from the control node.

## Task 5
### Install Docker on CentOS Instance & run a simple 3 tier application

**Objective:** Install and start Docker service on the CentOS instance.

**Steps:**

* Use the yum module to install Docker on the CentOS instance.
* Enable Docker service to start on boot using service module.
* Deploy a simple 3 tier application consisting of frontend, backend and database.

## Task 6
### Create and Configure a User Account

**Objective:** Create a user account on both Ubuntu and CentOS instances.

**Steps:**

* Create a new user using the user module.
* Set up the user with appropriate sudo privileges.
* Ensure the user has access to specific directories by modifying file permissions using ansible.builtin.file.

