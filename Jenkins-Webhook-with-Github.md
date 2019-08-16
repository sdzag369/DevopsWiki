# Creating a Webhook between Jenkins and Github

### Why use webhook ? 

> Till now we have seen how to trigger a build using SCM. However one major flaw in this approach is that you have to trigger these builds manually. We need a mechanism (automation) to ensure that whenever your code is committed to any selected branch on SCM(usually master), jenkins should trigger the build automatically. In order to achieve that, we will use Github as our primary Git repository and create a webhook from Jenkins to Github. Jenkins will automatically track all changes made on the Github repository and will trigger a new build whenever you merge your code to master. 

## Configurations for webhook 

* Go to Jenkins Dashboard by clicking the jenkins icon on the top left 

![image](https://user-images.githubusercontent.com/44743158/63161808-9a418000-c03e-11e9-9027-dfb50b483083.png)

* Click **Manage Jenkins**

![image](https://user-images.githubusercontent.com/44743158/63161890-d07eff80-c03e-11e9-9daf-fdae452121a3.png)

* Select **Configure System** 

* Scroll down to the **Github** section 

* Click **Add Github Server** and click **Github Server** 

![image](https://user-images.githubusercontent.com/44743158/63162022-28b60180-c03f-11e9-8cec-e63dbbe4ffcc.png)

* Open a new tab and go to your github.com repository

* Log in to your github account 

* On the top right corner click on your profile icon and then click **Settings**

![image](https://user-images.githubusercontent.com/44743158/63162230-a11cc280-c03f-11e9-8e43-2f639577a368.png)

* In the Settings page, on the left Panel, click **Developer Setting** 

![image](https://user-images.githubusercontent.com/44743158/63162328-e17c4080-c03f-11e9-91a9-f27cd754bea8.png)


* In the **Developer Setting** page, click **Personal Access Token** 

* Click **Generate New Token** 

![image](https://user-images.githubusercontent.com/44743158/63162471-391aac00-c040-11e9-8eab-806736353d38.png)

* In the **OAUTH** page, check **repo** to provide access to only the repos 

![image](https://user-images.githubusercontent.com/44743158/63163211-6d8f6780-c042-11e9-9dfd-3a3e2b758a5e.png)

* In the **Note** tab put the value **webhook**

* Click **Generate Token**

* Your token will now be generated 

* Store the webhook PAT securely in your KMS as this token has access to your repo 

* Go back to your Jenkins tab and now we will configure this token

* Give any name in the **name** field 

* Keep **API URL** as **https://api.github.com**

* In Credentials Field click **Add** -> **Jenkins** 

![image](https://user-images.githubusercontent.com/44743158/63163625-8a786a80-c043-11e9-9422-68539e5ae935.png)

* Change the **Kind** as **Secret Text** 

![image](https://user-images.githubusercontent.com/44743158/63163700-cf9c9c80-c043-11e9-9e65-cab4803eb9b0.png)

* **Secret** field will have the **PAT** generated from **Github** 

* **ID** field can be kept as any name. We will keep **webhook**

* Click **Add** 

* In **Credentials** drop down select **webhook** as the credential provider

* Click **Test Connection**

![image](https://user-images.githubusercontent.com/44743158/63163902-56517980-c044-11e9-9b4c-e48fab3138ec.png)

* Ensure successful connection 

* Check **Manage Hooks** 

* Click **Save** 

![image](https://user-images.githubusercontent.com/44743158/63163995-a03a5f80-c044-11e9-8cf5-3bcaf3dd5848.png)


> Github now has a webhook set up with Jenkins. In order to test the functionality, we will use an existing job, **scmdemo** in our folder **MyFirstFolder**

* In Jenkins go inside your folder **MyFirstFolder** 

* Click on the Job **scmdemo** 

* On the left Panel select **configure**

* The configure option let you edit the previous configurations 

* In the **General** tab check **GitHub project** 

* Provide the base URL of your github repository 

* In my case the base url is `https://github.com/hub-kubernetes/jenkinscode`

![image](https://user-images.githubusercontent.com/44743158/63164286-96fdc280-c045-11e9-9d75-c8f3c127da3c.png)

* In the **Build Trigger** section  select **GitHub hook trigger for GITScm polling**

![image](https://user-images.githubusercontent.com/44743158/63164326-bac10880-c045-11e9-9b06-019a15eac94d.png)

* Click Save

> Now that we have the job configured, make any changes in your github master repository. You should see that the webhook will launch automatically and a new build will be kicked off. 