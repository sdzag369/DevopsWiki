## Create a new Folder for your project 

* Click **Create new Job**

* Enter the name: **MyFirstFolder**

* Select Type as **Folder**

* Click OK

![image](https://user-images.githubusercontent.com/44743158/63156905-614fde00-c033-11e9-803f-f508e2742aa0.png)

* Fill in the details as below and click **Save**

![image](https://user-images.githubusercontent.com/44743158/63157019-a96f0080-c033-11e9-9e2e-9387c0b981e7.png)


## Create your First Job/Project inside **MyFirstFolder** folder

> You should be inside the folder. You can verify the current folder as below - 

![image](https://user-images.githubusercontent.com/44743158/63157250-28fccf80-c034-11e9-9e72-1983aad95c53.png)

* Click **Create new Job**

* Give the job name - myfirstjob

* Select **FreeStyle Project** 

* Click **OK**

![image](https://user-images.githubusercontent.com/44743158/63157367-682b2080-c034-11e9-8f8f-61924359a3b4.png)


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

