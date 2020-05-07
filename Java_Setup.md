## Setting up Jenkins

### Pre-requisite 
- Host [~we have ubuntu~]
- Latest version of Java [JDK](https://www.oracle.com/in/java/technologies/javase-downloads.html)

### To install Java on system

- First, update the apt package index with:
> `$ sudo apt update`
- Once the package index is updated install the default Java OpenJDK package with:
> `$ sudo apt install default-jdk`
- Verify the installation, by running the following command which will print the Java version:
> `$ java -version`

### Set the Default Java Version

- If you have multiple Java installations to change the default versio: 
> `$ sudo update-alternatives --config java`
  - type the number 1,2,3 to set the default Java configuration.

### Set the JAVA_HOME Environment Variable

- To set the **_JAVA_HOME_** environment variable, first, you need to find out the Java installation paths using the `update-alternatives` command:
> `$ sudo update-alternatives --config java`
- Copy the installation path of your preferred installation. Next, open the `/etc/environment` file:
> `$ sudo nano /etc/environment`

- Add the following line, at the end of the file:
> ` JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"`

- To verify that the JAVA_HOME environment variable is correctly set, run the following echo command:
> ` $ echo $JAVA_HOME`
