## About Jenkins with Java Maven Project

### Steps to build War file out of Java Project 

- Create a new job
  - Provide name of the project
  - Select Maven Project, click OK
- Provide description of the project
- Select GitHub Project and provide url
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
- Post Build Action
  - Select War/Ear and give `**/*.war`
  - Provide `Tomcat URL` ex:`https://localhost:8888/` which is hosted with [docker](https://github.com/ymaher/DevOps_Prerequisite/blob/master/Docker/TomcatOnDocker.md) click on docker to set up tomcat
- Save the configuration and click on Build now.
- The `War` file will be created under `tomcat/webapps/target`
