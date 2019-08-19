## Create a new Folder for your project 

* Click **Create new Job**

* Enter the name: **MyFirstFolder**

* Select Type as **Folder**

* Click OK

![image](https://user-images.githubusercontent.com/44743158/63156905-614fde00-c033-11e9-803f-f508e2742aa0.png)

* Fill in the details as below and click **Save**

![image](https://user-images.githubusercontent.com/44743158/63157019-a96f0080-c033-11e9-9e2e-9387c0b981e7.png)


***


## Create your First Job/Project inside **MyFirstFolder** folder

> You should be inside the folder. You can verify the current folder as below - 

![image](https://user-images.githubusercontent.com/44743158/63157250-28fccf80-c034-11e9-9e72-1983aad95c53.png)

* Click **Create new Job**

* Give the job name - myfirstjob

* Select **FreeStyle Project** 

* Click **OK**

![image](https://user-images.githubusercontent.com/44743158/63157367-682b2080-c034-11e9-8f8f-61924359a3b4.png)



***

## Configure your first Jenkins Job

* Provide any **Description** of your choice 

* Tick **Restrict where this project can be run**

* Set the label as **slave1** to make sure the job runs slave node

* **Source Code Management** is set as none

![image](https://user-images.githubusercontent.com/44743158/63157622-fe5f4680-c034-11e9-9e19-7f54bf9e66fc.png)

* **Build Triggers** and **Build Environment** are kept blank

* In **Build** Step click **Add build step** and Select **Execute Shell**

![image](https://user-images.githubusercontent.com/44743158/63157807-6d3c9f80-c035-11e9-9a20-fc8d91e6670a.png)

* In the **Command** section enter the below shell script 

~~~
echo "Hello World" 

echo "This folder is inside the workspace on slave node at location $(pwd)"
~~~

* Click Save

![image](https://user-images.githubusercontent.com/44743158/63157931-c4db0b00-c035-11e9-93b6-c86a50002763.png)

* On the left panel click **Build Now** 

* Check the **Build History** 

![image](https://user-images.githubusercontent.com/44743158/63158014-f8b63080-c035-11e9-9fee-6539145ccec7.png)

* Select the build number to get more details 

* Click on **Console Output** 

![image](https://user-images.githubusercontent.com/44743158/63158112-2f8c4680-c036-11e9-80b4-0c528bc5f895.png)


***

## Create a parameterized job

* Go back to the folder **myFirstFolder**

* On the left panel select **New Item** 

* Enter the **name** as **ParameterizedJob** and select **Freestyle Project** 

* Click **OK**

![image](https://user-images.githubusercontent.com/44743158/63158455-e8528580-c036-11e9-8a2c-497b4c040a14.png)

* In the **General** section check **This project is parameterized** 

* **Add Parameter** -> **String Parameter** 

* Give variable name as **name**

* Give Default Value as **defaultName** 

![image](https://user-images.githubusercontent.com/44743158/63158583-2f407b00-c037-11e9-8a8c-0f6bb6549e5a.png)

* Keep **Source Code Management**, **Build Triggers** and **Build Environment** intact

* **Build** -> **Add Build Step** -> **Execute Shell** 

![image](https://user-images.githubusercontent.com/44743158/63158676-69118180-c037-11e9-86b9-9375b921f0b5.png)

* Provide the below **command** 

```
echo "The value of the variable name is $name" 
```

![image](https://user-images.githubusercontent.com/44743158/63158774-a4ac4b80-c037-11e9-8cd7-004eebd4762d.png)

* Add a new post Build Step 

* Select **Add Post Build Action** and select **Delete workspace when build is done**

![image](https://user-images.githubusercontent.com/44743158/63158912-edfc9b00-c037-11e9-96de-bb5911d708b7.png)

* Click **Save** 

* On the left Panel select **Build with Parameters** 

![image](https://user-images.githubusercontent.com/44743158/63159039-3916ae00-c038-11e9-9812-a607270fb363.png)

* You may keep the default parameter or change the parameter 

* Click **Build** 

* Check the **Build History** and then **Console Output** 

![image](https://user-images.githubusercontent.com/44743158/63159143-6ebb9700-c038-11e9-94df-0c38192ad3b3.png)


***

## Working with SCM (Github) - First Job

> All the demos for jenkins with SCM is kept at https://github.com/hub-kubernetes/jenkinscode. We will use this repository to perform all subsequent demos related to SCM. 

> For this demo we will work with a small parameterized shell script - https://github.com/hub-kubernetes/jenkinscode/blob/master/number.sh. This script adds two numbers and takes it from the parameters.

* Go to the folder **MyFirstFolder** and create a new freestyle job with the name **scmdemo**

* In the **General** section check **Discard Old Builds** to always get a fresh build

![image](https://user-images.githubusercontent.com/44743158/63160825-59e10280-c03c-11e9-8a94-7a6848d90092.png)

* In the **General** Section check **This project is parameterized**

* **Add Parameter** -> **String Parameter** 

* **Name**: **num1** and **Default Value**: **10**

* Add a new Parameter

* **Name**: **num2** and **Default Value**: **5**

![image](https://user-images.githubusercontent.com/44743158/63160451-6f096180-c03b-11e9-947b-5ad09e7c152c.png)

* In **Source Code Management** section select **Git**

* Enter the **URL** as **https://github.com/hub-kubernetes/jenkinscode**

* **Credentials** are set as **None** because this is a public repository

* **Branches to build** will be set as **master**

![image](https://user-images.githubusercontent.com/44743158/63160613-ce677180-c03b-11e9-91e6-44a3a45818c1.png)

* Keep **Build Triggers** and **Build Environment** as default 

* In the **Build** step, select **Add Build** and **Execute Shell**

* Enter the commands as below - 

~~~
chmod +x ./number.sh
./number.sh
~~~

![image](https://user-images.githubusercontent.com/44743158/63160736-230aec80-c03c-11e9-8496-80bb2bbb5945.png)

* Click **Save** 

* On the Left Panel click **Build with Parameters**

![image](https://user-images.githubusercontent.com/44743158/63160955-9dd40780-c03c-11e9-9d65-bf1d45897e1a.png)

* Feel free to change the numeric values for num1 and num2 parameters

* Click **Build** 

* Check the Build History and **Console Output** 

![image](https://user-images.githubusercontent.com/44743158/63161218-281c6b80-c03d-11e9-9939-e91af57f451e.png)







 

