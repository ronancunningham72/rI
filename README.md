# RI Exercise

## My Attempt:
I've used the following tools in a Python based simple REST API with some commonly available modules.

1) Python PIP - Python Package Installer.
2) Flask - Flask is a micro web framework written in Python.
3) Ansible - Software that automates software provisioning, configuration management, and application deployment over ssh.

## 1) Installation
1.1) Install PIP 
   
   yum install -y pip
   
1.2) Install Flask
   
   pip install flask
   
1.3) Install Ansile
   
   pip install ansible

1.4) Run the app

   python simple_flask_app.py
   
This will create an api running on port 5000 on the host machine.

## 2) Assumptions
- The API will run on an instance that users can access within their home network without being blocked by a firewall.
- The target instances already exist and all remote administration access must happen over ssh (no Kerberos,LDAP etc).
- The API will execute as a user with ssh access to the default-user account on remote machines. Ansible only needs to be   installed on the host where the API executes.
- Users have software available (Curl, Postman etc) to make HTTP PUT requests.

## 2) Usage

2.1) Adding a key to a single host.

curl http://targethost:5000/add -d "host=54.236.243.206" -d "key=${key}" -X PUT

2.2) Deleting a Key from multiple hosts.

curl http://targethost:5000/delete -d "host=54.236.243.206" -d "host=34.234.100.40" -d "key=${key}" -X PUT

The value of 'key' should be the contents of the public ssh key to add to the '~/.ssh/authorized_keys'.

## 3) BackEnd processing

The Python Flask module implements a basic class that calls an Ansible command line process to call the 
'lineinfile' module'
This Ansible module ensures a particular line (public ssh key) is present or absent in a file (~/.ssh/authorized_keys).

http://docs.ansible.com/ansible/latest/modules/lineinfile_module.html

## 4) Future Improvements

The solution is a simple Minimum Viable Product to meet the basic requirements of allowing a user to add their ssh public key to a remote machine.

Future hardening efforts would look to:

3.1) Use a Production grade Web Server Gateway Interface (WSGI) server to implement the API.
3.2) User authentication
3.3) Use a Javascript based form to allow form based requests and file uploads.
3.4) Persistent storage to allow users to query all their previously added keys and make it easier to delete these keys.
3.5) A message queue to ensure requests can be re-processed on failure.
3.6) Email confirmation.










