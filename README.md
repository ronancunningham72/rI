# RI Exercise

## My Attempt:
I've used the following tools in a Python based solution with some commonly available modules.

1) Python PIP - Python Package Installer.
2) Flask - Flask is a micro web framework written in Python.
3) Ansible - Software that automates software provisioning, configuration management, and application deployment over ssh.

The solution is a simple REST API to add the ssh keys.

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
- The API will run on an instance that users can access without being blocked by a firewall.
- The target instances already exist and all remote administration access must happen over ssh (no Kerberos,LDAP etc).
- All users log on as the same default system user account account on the target instances e.g a user named default-user.
- The API will execute as a user with ssh access to the 'default-user' account on remote machines.
- Users have software available (Curl, Postman etc) to make HTTP PUT requests.

## 2) Usage

2.1) Adding a key

curl http://targethost:5000/add -d "host=54.236.243.206" -d "host=34.234.100.40" -d "key=${key}" -X PUT

2.2) Deleting a Key

curl http://targethost:5000/delete -d "host=54.236.243.206" -d "host=34.234.100.40" -d "key=${key}" -X PUT

The value of 'key' should be the contents of the public key to add to the '~/.ssh/authorized_keys'









