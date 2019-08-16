# Maven Installation

## What is Maven ? 

> Apache Maven is a free and open source project management and comprehension tool used primarily for Java projects. Maven uses a Project Object Model (POM) which is essentially a XML file containing information about the project, configuration details, the project’s dependencies, and so on.

## Where will be maven installed? 

> Maven will be installed on all hosts that can trigger builds. We have one master and one slave which both can trigger builds. Hence, maven will be installed on both servers 

## Are there any prerequisite? 

> Since Apache Maven works majorly with Java projects, you need to have Java installed. If you are following this series of demos java would be installed already on your system while installing Jenkins. 

## Installation steps 

> The below command will be installed on both - master and slave nodes 

` apt-get update && apt-get install -y maven`

Check the version by executing - 

` mvn -version` 

## Install maven plugin on Jenkins 

> Jenkins might not come with the maven plugin by default. We will have to install Jenkins plugin for maven builds 

* Log in to Jenkins Dashboard 

* On the left panel Click **Manage Jenkins** -> **Manage Plugins** 

* Click **Available**

* In the filter section search for **Maven Integration** 

* Check the **Maven Integration** plugin and select **Install without restart** 

![image](https://user-images.githubusercontent.com/44743158/63194276-2c707500-c08d-11e9-8055-1394dc4499e9.png)

* On the next page - check **Restart Jenkins after install** to enable auto restart

**NOTE**

> If you run into any error during soft restart perform the below steps 

* Log in to your master virtual machine 

* Log in as root 

` sudo -i ` 

* Restart Jenkins 

` systemctl restart jenkins`

* Reload Jenkins webpage, login and your plugin should be installed 