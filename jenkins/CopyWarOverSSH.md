## How to copy War file on local system/ server file system

### Steps to follow

- Install plugin called publish over SSH

- Go to Configure System, scroll down to publish over SSH

- Before adding credentials, you can use local user of vm/host or create a new user on host with below cmd
> `$ sudo useradd <name of the user> `

> `$ sudo passwd <password>`

- Add new SSH Server
  - Name as you wanna give to server
  - Host Name can be you local `127.0.0.1` or the ip address of the server you can find it via `$ sudo ip addr`
  - Username as the name of the user
  - Click on advance provide the password and click on Test Config
  - If it fails to connect you can go to `/etc/ssh/sshd_config` and enable `PasswordAuthentication Yes`
  > `$ sudo service ssh restart`
  
### Actual job to copy War file
  
- Create a new job or you can copy from [here](https://github.com/ymaher/DevOps_Prerequisite/blob/master/Work_within_Jenkins_2.md)
  
- Remove the Post Build Action and choose Send artifact over SSH
  - Enter the Name of the SSH Server
  - Transfers: Provide the Source file as : afterjob name `/Webapp/target/*.war`
  - Remove prefix: /webapp/target
  - Remote directory: path of the file you want to receive artifact or you can just give `. for current directory`
  - Assuming you have a dockerfile already on the same location
  - Exec cmd
  ```
  cd Documents/webapps; sudo docker build -t devops-image .; sudo docker run --rm -it -dp 8888:8080 devops-image;
    
