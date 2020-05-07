## About Jenkins with Java Maven Project

### How to access Jenkins

To start we need initial password and to fetch the initial password:

> `$ sudo less /var/lib/jenkins/secrets/initialAdminPassword`

- Copy the password paste in the browser `https://localhost:8080/`

- We can proceed with the `Install suggested Plugin`

- Once done continue as admin or can -create a new admin user-

- Log in and change the password by clicking on -admin's configure-

- It will log out automatically, log in with new credentials

### Steps to build War file out of Java Project 

- Create a new job
  - Provide name of the project
  - Select Maven Project, click OK
- Provide description of the project
- Source Code Management select as Git
  - Provide the project github link
  - Provide the credentials if it is private project
- Build trigger
  - Select Poll SCM
  - \* \* \* \* \* for each min, hour, sec
- Build Environment
  -Delete workspace before build starts
- Build
  - POM.xml
  - Goals- like clean install package
- Save the configuration and click on Build now.
- The `War` file will be created under `tomcat/webapps/target`
