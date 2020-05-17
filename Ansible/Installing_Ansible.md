## Install and Configure Ansible on Ubuntu 18 and above

For pre requisite please [click here](https://github.com/ymaher/DevOps_Prerequisite/edit/master/Ansible/Prereq_Setup.md)

### Step 1 — Installing Ansible

- Firstly Update apt package with:
> `$ sudo apt update`

- Install the Ansible software with:
> `$ sudo apt install ansible -y`

### Step 2 — Setting Up the Inventory File

To edit the contents of your default Ansible inventory, open the `/etc/ansible/hosts` file using your text editor of choice, on your Ansible control node:
> `$ sudo nano /etc/ansible/hosts`

The default inventory file provided by the Ansible installation contains a number of examples that you can use as references for setting up your inventory. The following example defines a group named [servers] with three different servers in it, each identified by a custom alias: server1, server2, and server3. Be sure to replace the IPs with the IP addresses of your Ansible hosts.
```
/etc/ansible/hosts

[servers]
server1 ansible_host=203.0.113.111
server2 ansible_host=203.0.113.112
server3 ansible_host=203.0.113.113

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

When you’re finished, save and close the file by pressing `CTRL+X` then `Y` and `ENTER` to confirm your changes.

Whenever you want to check your inventory, you can run:

> `$ ansible-inventory --list -y`

You’ll see output similar to this, but containing your own server infrastructure as defined in your inventory file:

```
OUTPUT:
Output
all:
  children:
    servers:
      hosts:
        server1:
          ansible_host: 203.0.113.111
          ansible_python_interpreter: /usr/bin/python3
        server2:
          ansible_host: 203.0.113.112
          ansible_python_interpreter: /usr/bin/python3
        server3:
          ansible_host: 203.0.113.113
          ansible_python_interpreter: /usr/bin/python3
    ungrouped: {}
```

## Step 3 — Testing Connection

After setting up the inventory file to include your servers, it’s time to check if Ansible is able to connect to these servers and run commands via SSH.

From your local machine or Ansible control node, run:
> `$ ansible all -m ping -u root`

The ping module will test:

- if hosts are accessible;
- if you have valid SSH credentials;
- if hosts are able to run Ansible modules using Python.

You should get output similar to this:

```
Output
server1 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
server2 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
server3 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

If this is the first time you’re connecting to these servers via SSH, you’ll be asked to confirm the authenticity of the hosts you’re connecting to via Ansible. When prompted, type yes and then hit ENTER to confirm.

Once you get a "pong" reply back from a host, it means you’re ready to run Ansible commands and playbooks on that server.

