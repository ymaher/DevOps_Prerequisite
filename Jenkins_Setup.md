## Setting up Jenkins

### Pre- requisites for jenkins
- [Host](https://github.com/ymaher/DevOps_Prerequisite/blob/master/Host_Setup.md)
- [JDK](https://github.com/ymaher/DevOps_Prerequisite/blob/master/Java_Setup.md)

### Steps to set up jenkins in ubuntu

- go to https://pkg.jenkins.io/debian-stable/ (for more details)

- commands to setup jenkins
> `$ wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -`
  
  - Then add the following entry in your /etc/apt/sources.list:
  > deb https://pkg.jenkins.io/debian-stable binary/


> `$ sudo apt-get update  $ sudo apt-get install jenkins`

- Open `https://localhost:8080/` to verify if you able to see jenkins home page


## OR Alternative way is mentioned as below

- Download and install the necessary GPG key with the command 
>`$ wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -`
- Add the necessary repository with the command 
> `$ sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list' `
- Add the universe repository with the command 
>`$ sudo add-apt-repository universe`.
- Update apt with the command 
> `$ sudo apt-get update`.
- Install Jenkins with the command 
> ` $sudo apt-get install jenkins -y ` 
- Allow the installation to complete then Open `https://localhost:8080/` to verify if you able to see jenkins home page
