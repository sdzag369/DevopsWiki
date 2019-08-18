Lets understand how to create a Jenkins Pipeline Job. In order to understand a pipeline job, we will first create a Freestyle job and then convert it to a pipeline job. It helps if you understand the groovy language, however even if you are fairly new to Jenkins or have no experience in groovy, Jenkins provides you a bunch of utilities that you can use to create your pipeline script. 

## Create a Free style job for a java project. 

> By now you should be aware about how to create a new freestyle project. We will now create a new freestyle project with the below parameters

General Section

* Project name - freestyle_spring
* Description - Job to compile spring backend
* Check Discard old builds 
* check GitHub project - https://github.com/hub-kubernetes/jenkins-cicd/
* Check Restrict where this project can be run - slave1

SCM section 

* check POLL SCM - H * * * *

Build Environment section 

* check Delete workspace before build starts

Build Section

* Select Invoke top level maven targets 

* Goals : clean compile test package

* Click advanced

* POM: maven_integration_demo/spring-boot-samples/spring-boot-angular/pom.xml


Post build actions 

* Select archive the artifact

* Files to archive: maven_integration_demo/spring-boot-samples/spring-boot-angular/target/*.jar


> Click save and run the project and run the project to understand what happens 

![image](https://user-images.githubusercontent.com/44743158/63222965-23d28880-c1cc-11e9-9031-6fca28a70139.png)


Now that we have a reference pipeline, lets convert it to a Pipeline Project 

* Go to your jenkins Dashboard 

* on the left panel click **New Project** 

* Give the name as **spring_pipeline**

* Select the type as **Pipeline** and click **OK** 

![image](https://user-images.githubusercontent.com/44743158/63224349-643c0180-c1e0-11e9-8aa8-c3d29c04d897.png)


General Section - 

* Check Github Project and enter the URL as https://github.com/hub-kubernetes/jenkins-cicd/

Build Trigger Section - 

* Check Poll SCM and enter - H * * * * 

![image](https://user-images.githubusercontent.com/44743158/63224433-b3366680-c1e1-11e9-889d-60a66b260920.png)

* Scroll down to the Pipeline Section 

* Click on the **Pipeline Syntax** hyperlink at the bottom and open it in a new tab 

![image](https://user-images.githubusercontent.com/44743158/63224476-86368380-c1e2-11e9-913f-09582a768a62.png)

* The pipeline syntax page helps you to create the pipeline script for different phases in the code

* Additionally open the freestyle_spring project in a new tab for comparison


***

We will now convert all the below steps from the previously created freestyle project into a Pipeline script - 

1. Set Build node as slave1 

2. Checkout from git repository - https://github.com/hub-kubernetes/jenkins-cicd.git

3. Run maven build with clean, compile, test and package

4. Archive the file at location maven_integration_demo/spring-boot-samples/spring-boot-angular/target/*.jar


***

### Set Build Node as slave1 

In the pipeline syntax page - 

* Select sample step as **node: Allocate node** 

* set the label as **slave1** 

* Click **Generate pipeline script**

![image](https://user-images.githubusercontent.com/44743158/63224771-699c4a80-c1e6-11e9-9e06-5328d10ad999.png)

* Copy the output to the Pipeline section 


***

### Checkout the git repository

* Go back to Pipeline syntax page 

* Select the sample step as **git: Git** 

* In the **Repository URL** stage enter your URL - https://github.com/hub-kubernetes/jenkins-cicd.git

* Click **Generate pipeline script**

![image](https://user-images.githubusercontent.com/44743158/63224822-43c37580-c1e7-11e9-8853-aa457d22a08b.png)

* Copy this output and place it inside the **node** block in the Pipeline page

![image](https://user-images.githubusercontent.com/44743158/63224835-8be29800-c1e7-11e9-93ec-8df1f51aacc5.png)


***

### Run Maven Build as Shell script 

**STEP 1** - change directory to maven_integration_demo/spring-boot-samples/spring-boot-angular

* Go back to Pipeline syntax page 

* Select the sample step as **dir: Change current directory** and enter the **PATH** as `maven_integration_demo/spring-boot-samples/spring-boot-angular`

* Click **Generate Pipeline Script** 

![image](https://user-images.githubusercontent.com/44743158/63225248-5d66bc00-c1eb-11e9-87bf-4f0e5c3336d7.png)

* Copy this output and place it inside the **node** block in the Pipeline page

![image](https://user-images.githubusercontent.com/44743158/63225288-c0585300-c1eb-11e9-936b-6a2ceb5e80a0.png)


**STEP 2** - Execute maven build 

* Go back to Pipeline syntax page 

* Select the sample step **sh: Shell Script** 

* Enter the shell script as `mvn clean compile test package` 

* Click **Generate Pipeline Script** 

![image](https://user-images.githubusercontent.com/44743158/63225334-3bba0480-c1ec-11e9-8614-44090224cc93.png)

* Copy this output and place it inside the **dir** block in the Pipeline page

![image](https://user-images.githubusercontent.com/44743158/63225339-57bda600-c1ec-11e9-9dcd-bac79b5308b4.png)


***

### Archive the artifact 

* Go back to Pipeline syntax page 

* Select the sample step **step: General Build Step** 

* Select Build Step as **Archive the Artifact** 

* Enter Files to archive as the relative path `target/*.jar`

* Click Generate Pipeline Script 

![image](https://user-images.githubusercontent.com/44743158/63225432-97d15880-c1ed-11e9-9e33-8469ab388329.png)

* Copy this output and place it inside the **dir** block in the Pipeline page


***

### Divide your Pipeline into stages 

* Jenkins Pipeline allows you to create stages as a part of pipeline. Each stage can be have one or more steps of the pipeline. 

* A stage in Jenkins Pipeline is defined as a part of its own block and is represented as below - 

~~~
stage('checkout') {
    // some block
}
~~~

* We will divide our code into 3 stages - 

**1. Stage Checkout -**

~~~
stage('checkout') {
git 'https://github.com/hub-kubernetes/jenkins-cicd.git'
}
~~~

**2. Stage Build -***

~~~
stage('build') {
sh label: '', script: 'mvn clean compile test package'
}
~~~

**3. Stage Artifact -**

~~~
stage('artifact') {
archiveArtifacts 'target/*.jar'
}
~~~

The final Pipeline will look like the below - 

```
node('slave1') {
    
    stage('checkout') {
        git 'https://github.com/hub-kubernetes/jenkins-cicd.git'
    }
    
    dir('maven_integration_demo/spring-boot-samples/spring-boot-angular') {
        
    stage('build') {  
        sh label: '', script: 'mvn clean compile test package'
    }
    
    stage('artifact') {
        archiveArtifacts 'target/*.jar'
    }
}
}

```

![image](https://user-images.githubusercontent.com/44743158/63225608-3ca06580-c1ef-11e9-851c-04fc0631f136.png)

Click on Save and then trigger the build 

You will now be able to see all stages of your build in the status view 

![image](https://user-images.githubusercontent.com/44743158/63225635-aae52800-c1ef-11e9-9e7b-67c95603a773.png)












