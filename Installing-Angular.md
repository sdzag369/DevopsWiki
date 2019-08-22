# Angular JS installation 

AngularJS lets you extend HTML with HTML attributes called directives. AngularJS directives offers functionality to HTML applications. 

### Installing Angular on your master and slave nodes

> Below are the steps to install angujarJS on your system. In order to install Angular, you must also install nodeJS and npm applications 

` curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -` 

` sudo apt-get install -y nodejs` 

***

### Check version of nodeJS and npm

```
node --version
v12.8.1

npm --version
6.10.2
```

***

### Install angular CLI 

` npm install -g @angular/cli` 

You might get a prompt as below - 

~~~
Would you like to share anonymous usage data with the Angular Team at Google under
Google’s Privacy Policy at https://policies.google.com/privacy? For more details and
how to change this setting, see http://angular.io/analytics. (y/N)
~~~

You may either enter y or N. The choice is yours. 


***

### Check Angular Version

~~~
ng --version

     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/
    

Angular CLI: 8.2.2
Node: 12.8.1
OS: linux x64
Angular: 
~~~
