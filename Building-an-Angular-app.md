The below angular project will act as a frontend application for the spring boot application we deployed as pipeline. 

The angular project now needs to know the location of the backend server. The file `jenkins-cicd/maven_integration_demo/spring-boot-samples/spring-boot-angular/angularclient/src/app/service/user.service.ts` holds this information. There are two variables that needs to be parameterized `SPRING_BACKEND` and `SPRING_PORT`. we will also write a script to replace these variables. 

This build will be triggered only after successful completion of **spring_pipeline** job. 

### Create a Freestyle job for Angular build

* New Item -> Freestyle Project. 

* Give the name as **angularbuild** and click **OK** 

![image](https://user-images.githubusercontent.com/44743158/63498323-48d43d80-c4e3-11e9-92e7-095fe4c8edb0.png)


***

In the General section - 

* Check Github Project - and give the Project URL 

* Check **This project is parameterized** and add 2 parameters of the type **string parameter**

* Parameters are - **spring_server** and **spring_port**. The default values are **localhost** and **8888* respectively. 

![image](https://user-images.githubusercontent.com/44743158/63498670-ff382280-c4e3-11e9-806c-1837349ebc14.png)


***

In the Source Code Management section - 

* Check **Git**

* Add the repository URL 

* Keep everything else default. There would be no credentials because the repository is public

![image](https://user-images.githubusercontent.com/44743158/63498953-82f20f00-c4e4-11e9-816d-7ada60b463d1.png)


***

In the Build Trigger Section 

* Check **Build after other projects are built** 

* Give the name of the spring build. In my case, its **spring_pipeline** 

* Ensure **Trigger only if build is stable** is selected. 


![image](https://user-images.githubusercontent.com/44743158/63499467-8934bb00-c4e5-11e9-8466-f231a478295c.png)


***


In the Build environment section - 

* Select **Delete workspace before build starts**

![image](https://user-images.githubusercontent.com/44743158/63499598-c5681b80-c4e5-11e9-89aa-904ef979a15d.png)


***

In the Build section - 

* Select **Execute Shell** 

![image](https://user-images.githubusercontent.com/44743158/63499686-f8aaaa80-c4e5-11e9-9aff-0c96726747f1.png)

We will now write a build script in shell to replace the placeholders in the `user.service.ts` file and then we will execute `npm install` to build the project. 

Your build script will look like below 

```
cd maven_integration_demo/spring-boot-samples/spring-boot-angular/angularclient/src/app/service

# Replace Placeholders with the parameters provided 

sed -i "s/SPRING_BACKEND/${spring_server}/g" user.service.ts

sed -i "s/SPRING_PORT/${spring_port}/g" user.service.ts

#Go back to Build directory to execute npm install

cd ../../../

# Install angular Build

npm i rxjs-compat

npm install

npm run build

```

![image](https://user-images.githubusercontent.com/44743158/63500159-fa28a280-c4e6-11e9-9e15-ad8153753578.png)


***

In the post build action - 

* Select Archive Artifact

* Put the location for archiving as `maven_integration_demo/spring-boot-samples/spring-boot-angular/angularclient/dist/angularclient/*`

Click Save

