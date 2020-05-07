## About hosting tomcat on docker container

### Steps to create a docker container for tomcat
- We must have ubuntu or any Linux dist

- We must have docker installed on host

- I have already set up a docker container containing tomcat

- Please enter the following cmd to pull the image
> `$ sudo docker pull ymaher/tomcat_user`

- To run the container on desired port follow the below cmd
> `$ sudo docker run --rm -it -dp 8888:8080 ymaher/tomcat_user  `
