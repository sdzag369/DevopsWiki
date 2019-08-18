# Jenkins Pipeline Project

## Why Jenkins Pipeline ?????

1. Jenkins provides a way to automate your builds process. 

2. You as a Pipeline integration engineer can login to the UI and create a bunch of jobs by configuring them on the UI. 

3. Lets take an example as below where we have configured 1000 backend jobs and 1000 frontend jobs - 

![image](https://user-images.githubusercontent.com/44743158/63221139-3cce4000-c1b2-11e9-98b4-ba2ca5bcdb36.png)

4. Here we are using **maven** as the primary build tool for Java and **npm v4** for creating our UI angular project. 

5. As and when time progresses, you are now upgrading from **maven** to **gradle** and **npm v4** to **npm v6**

6. Below would be the new changes 

![image](https://user-images.githubusercontent.com/44743158/63221211-4e641780-c1b3-11e9-917c-14dbc8213383.png)

7. So how do we make changes thousand of jobs manually? 

8. You can manually go to each job and make these changes. This is time consuming and will require a lot of manual work. 

9. A second option would be to go to jenkins workspace and find the XML file that represents these jobs and make the corresponding changes. This again tends to be a time consuming task as this involves you searching for the correct file and modifying them with precision. 

10. A third option can be to use plugins, however a bunch of free plugins available dont provide an accurate way of making these changes specially when there are dependency involved. 


***

### Enter Jenkins Pipeline Plugin 

> After you have worked with Jenkins for sometime you realize that the jenkins jobs arent linear most of the times. A linear pipeline would probably look like this 

![image](https://user-images.githubusercontent.com/44743158/63221365-9f750b00-c1b5-11e9-870f-7c4358b32e0e.png)

> In a complete integrated & automated scenario, specially on production environments your pipeline would most probably look like below - 

![image](https://user-images.githubusercontent.com/44743158/63221375-cb908c00-c1b5-11e9-9a9f-2a72ee55b25d.png)

> In order to manage these dependencies we now need a way to even treat our **jobs as code**. Jenkins Pipelines helps you deliver your entire pipeline as a code and enables you to store the job definitions at one centralized repository on your SCM. 


***

### Jenkins Pipeline & JenkinsFile 

> Jenkins Pipeline (or simply "Pipeline" with a capital "P") is a suite of plugins which supports implementing and integrating continuous delivery pipelines into Jenkins.

> A continuous delivery (CD) pipeline is an automated expression of your process for getting software from version control right through to your users and customers. Every change to your software (committed in source control) goes through a complex process on its way to being released. This process involves building the software in a reliable and repeatable manner, as well as progressing the built software (called a "build") through multiple stages of testing and deployment.

> Pipeline provides an extensible set of tools for modeling simple-to-complex delivery pipelines "as code" via the Pipeline domain-specific language (DSL) syntax.

> Creating a Jenkinsfile and committing it to source control provides a number of immediate benefits:

* Automatically creates a Pipeline build process for all branches and pull requests.

* Code review/iteration on the Pipeline (along with the remaining source code).

* Audit trail for the Pipeline.

* Single source of truth for the Pipeline, which can be viewed and edited by multiple members of the project.

You can find the syntax of the pipeline at [Pipeline Syntax Page](https://jenkins.io/doc/book/pipeline/#pipeline-syntax-overview)







