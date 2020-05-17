## Install and Configure Ansible on Ubuntu 18 and above

### Pre requisites for setting ansible

- **One Ansible machine/VM** which is running on ubuntu 18 or above which will act as **Ansible Control Node**
  - Non-root user with sudo privileges.
    - **To set up user with sudo privileges:**
    
    > `$ sudo su -`
    
    > `$ sudo adduser <user_name>`
    
    You will be asked a series of questions. The password is required, and all other fields are optional.
    ```
    OUTPUT
    Enter new password: 
    Retype new password: 
    passwd: password updated successfully
    Changing the user information for username
    Enter the new value, or press ENTER for the default
	    Full Name []: 
	    Room Number []: 
	    Work Phone []: 
	    Home Phone []: 
	    Other []: 
    Is the information correct? [Y/n] 
    ```
    - As root, run this command to add your new user to the sudo group.
    
    > `$ sudo usermod -aG sudo <user_name> `
 
  - **An SSH keypair associated with this user:**
    - Creating the Key Pair
    > `$ sudo ssh-keygen`
    
    After entering the command, you should see the following output:
    ```
    OUTPUT
    Generating public/private rsa key pair.
    Enter file in which to save the key (/your_home/.ssh/id_rsa):
    ```
    Press enter to save the key pair into the .ssh/ subdirectory in your home directory, or specify an alternate path.
    
    If you had previously generated an SSH key pair, you may see the following prompt:
    ```
    OUTPUT
    /home/your_home/.ssh/id_rsa already exists.
    Overwrite (y/n)?
    ```
    If you choose to overwrite the key on disk, you will not be able to authenticate using the previous key anymore. Be very careful when selecting yes, as this is a destructive process that cannot be reversed.

    You should then see the following prompt:
    ```
    OUTPUT
    Enter passphrase (empty for no passphrase):
    
    ```
    
- **One or more Ansible Hosts:** An Ansible host is any machine that your Ansible control node is configured to automate.
	- The Ansible control node’s SSH public key added to the authorized_keys of a system user. This user can be either root or a regular user with sudo privileges. 
	
	To set this up, you can follow above above steps for **SSH keypair associated with this user**
    
    

    
    
