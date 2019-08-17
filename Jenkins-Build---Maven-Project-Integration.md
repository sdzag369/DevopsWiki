# Triggering a Maven Build with Jenkins


### How does a normal build process look like ? 

![image](https://user-images.githubusercontent.com/44743158/63210925-1eaf0400-c10e-11e9-96cb-ee4ddc22429c.png)



***

### Performing a maven build manually 

> We will now perform a manual build by utilizing all the stages as a part of the build process 


***

### Stage: Checkout 

` git clone https://github.com/hub-kubernetes/jenkins-cicd.git` 

` cd jenkins-cicd/maven_integration_demo/spring-boot-samples/spring-boot-sample-tomcat` 

> We can now see two entities - pom.xml and src directory that contains all the code for this demo 


***

### Stage: Compile 

` mvn compile` 


***

### Stage Test 

` mvn test` 

***

### Stage Package

` mvn package` 


***

> Now that we have run the package directive on maven, go inside the **target** directory to see the jar that was created with the name spring-boot-sample-tomcat-1.4.0.BUILD-SNAPSHOT.jar

```
cd target
ls -ltra *.jar
-rw-r--r-- 1 root root 11643902 Aug 17 13:37 spring-boot-sample-tomcat-1.4.0.BUILD-SNAPSHOT.jar
```

***

### Run your Java code manually

`cd target` 

` java -jar -Dserver.port=8888 spring-boot-sample-tomcat-1.4.0.BUILD-SNAPSHOT.jar` 

Wait for the below output - 

` 2019-08-17 13:41:49.027  INFO 13104 --- [           main] sample.tomcat.SampleTomcatApplication    : Started SampleTomcatApplication in 33.029 seconds (JVM running for 33.593)
`

> On your browser you can now navigate to http://**YOUR_EXTERNAL_IP:8888** or just pull up a new terminal and execute `curl localhost:8888` to get the output as Hello World

~~~
root@master:~# curl localhost:8888
Hello World

~~~


***

> Now that we have seen how to fetch, compile, test, package and deploy our code, lets create a CI cycle that will use Jenkins as the primary integration tool and will automate the entire process. 

## Automating deployments using Jenkins 

### Configure maven global configuration

> Lets create a freestyle project to automate our deployment 

1. Log in to Jenkins Dashboard 

2. Click on **Manage Jenkins** on the Left panel 

3. Click on **Global Tool Configuration** 

4. Scroll down till **Maven** section 

5. Click **Add Maven** 

![image](https://user-images.githubusercontent.com/44743158/63212668-b79d4980-c125-11e9-8d1d-f30f208d271b.png)

6. Give it any name - I will give it the name as **maven**

7. Retain all other settings

![image](https://user-images.githubusercontent.com/44743158/63212691-f6330400-c125-11e9-83fb-5ad61cc37842.png)

8. Click **Save**


***

### Create a job to automate deployment

1. On the left panel click **New Item** to create a new project/Job 

![image](https://user-images.githubusercontent.com/44743158/63212773-e49e2c00-c126-11e9-92e8-fa0fedcee3b6.png)

2. Enter the name as **mavenautomation** and select **Freestyle Project** and click **OK**

![image](https://user-images.githubusercontent.com/44743158/63212802-3c3c9780-c127-11e9-8c5d-49e95100411a.png)

3. In the **General Section** select **Github Project** and provide the **PROJECT URL** of your github repository. 

![image](https://user-images.githubusercontent.com/44743158/63212830-92a9d600-c127-11e9-8ab1-6e93adf57fa3.png)

4. In the **Source Code Management** section select **Git** and provide the **REPOSITORY URL** of your github repository

![image](https://user-images.githubusercontent.com/44743158/63212909-735f7880-c128-11e9-829d-5e4bde775973.png)

5. **Credentials** are set as none because this is a public repository and anyone can clone 

6. In **Build Environment** select **Delete workspace before build starts** 

![image](https://user-images.githubusercontent.com/44743158/63212943-c0434f00-c128-11e9-9e9c-afd0772c3357.png)

7. In the **Build** stage, click **Add Build Step** and select **Invoke top level Maven target** 

![image](https://user-images.githubusercontent.com/44743158/63213414-bd952980-c129-11e9-80b2-c7a7ad4af1c9.png)

8. In the **Goals** textbox enter ` clean compile test package` 

9. Click Advanced

10. In the **POM** textbox enter the relative path of the pom.xml. In our case it will be - 

` maven_integration_demo/spring-boot-samples/spring-boot-sample-tomcat/pom.xml` 

![image](https://user-images.githubusercontent.com/44743158/63213518-f550a100-c12a-11e9-805c-6d1eec5dfd84.png)

11. Click **Save**


***

> Now that we have created the automation, we can now trigger the build by clicking **Build Now** in the left Panel. Monitor the log to follow the entire build stage 



