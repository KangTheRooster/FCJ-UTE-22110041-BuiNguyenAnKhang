---
title : "Deploy the backend on Elastic Beanstalk"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.3 </b> "
---
# To setup backend you will have to follow these steps
## Set up all the environment variable
### 1st Step:  Create a clean package
Locate to the backend file and run this command
`mvn clean package` to create a musicapp-0.0.1-SNAPSHOT.jar
![Build the jar file](/images/3.backenddeployment/3.3.ebdeploy/01.png)
![Build the jar file](/images/3.backenddeployment/3.3.ebdeploy/02.png)
### 2nd Step: Clone the elasticbeanstalk and install virtualenz
Clone the repository through this link [Github](https://github.com/aws/aws-elastic-beanstalk-cli-setup.git)
Then remember to install virtualenv using this command `pip install virtualenv`
![Install virtualenv](/images/3.backenddeployment/3.3.ebdeploy/03.png)
After that you need to set the environmental variables for it
### 3rd step: Set the environmental variable for the virtualenv
My path is this but your path maybe different so remember to check it 1st **C:\Users\MyUserName\AppData\Roaming\Python\Python311\Scripts**
.Open **Edit Environment Variables** then click on **Environment Variables** 
![Environmental Variables](/images/3.backenddeployment/3.3.ebdeploy/04.png)
After that choose **Path** in **User Variables** and click **Edit**
![Environmental Variables](/images/3.backenddeployment/3.3.ebdeploy/05.png)
Click new and paste the path of your virtualenv and click ok to save it
![Environmental Variables](/images/3.backenddeployment/3.3.ebdeploy/06.png)
### 4th step: Set up the eb
After complete those steps open a new cmd/powercell and run this
`virtualenv --version` to check if it is working or not
cd to the place you clone the repository at
mine is  cd **C:\h\aws-elastic-beanstalk-cli-setup\scripts**
after that run `python ebcli_installer.py`
![Check if the virtualenv is correct or not](/images/3.backenddeployment/3.3.ebdeploy/07.png)
![Set up eb](/images/3.backenddeployment/3.3.ebdeploy/08.png)
Then run the command as it guides
- `CMD Prompt: cmd.exe /c "C:\Users\AnKhang\.ebcli-virtual-env\executables\path_exporter.bat"`
- `PowerShell: & "C:\Users\AnKhang\.ebcli-virtual-env\executables\path_exporter.vbs"`
### 5th step : Remember to check Internet Informtation Services
Thats right for eb to work you will need to turn on the Internet Information Services
Go to **Control Panel/Programs** then click on the **Turn Window features on or off**
![Where to go to check](/images/3.backenddeployment/3.3.ebdeploy/09.png)
If it is on you are okay to continue but if it is off you must turn it on
![Turn on the IIS](/images/3.backenddeployment/3.3.ebdeploy/10.png)
Now lets head back to the **powershell** or **cmd** and `run eb --version`
![Check eb version](/images/3.backenddeployment/3.3.ebdeploy/11.png)
If you get the result like the picture, congratulation you have finised the set up step. If not, try again.
### 6th step: Create a procfile
Go to the the folder where you have the proc file and open **cmd/powershell**
![Target file location](/images/3.backenddeployment/3.3.ebdeploy/12a.png)
Then create a Procfile in that folder
![Proc file](/images/3.backenddeployment/3.3.ebdeploy/13a.png)
After that go into the Procfile and write this content
`web: java -jar MusicApp-0.0.1-SNAPSHOT.jar`
![Proc file content](/images/3.backenddeployment/3.3.ebdeploy/14.png)
* ***Note***: You can create a Procfile.txt with that content then rename it and delete the txt part
### 7th step: Create a key pair
We will need to create a key pair
,go to **EC2** in the network and security tabs select **Keyparis**
![Key Pair Location](/images/3.backenddeployment/3.3.ebdeploy/15.png)
After that select create keypair
name it like you like and select the format for it is **.pem**      
![Key Pair Location](/images/3.backenddeployment/3.3.ebdeploy/16.png)
Then click create
After that open cmd again and run aws configure
![Key Pair Location](/images/3.backenddeployment/3.3.ebdeploy/39.png)
Enter your access key id and secret access [key]({{< relref "5-createawskey.md" >}})
* For how to create it visit here
## Starting to deploy
# Step 1: go to the target folder and open a cmd or powercell
Run the `eb init` command to start config the elastic beanstalk
![Start create the env](/images/3.backenddeployment/3.3.ebdeploy/17.png)
Cause I am currently in VietNam so I will choose the region 8
![Region selection](/images/3.backenddeployment/3.3.ebdeploy/18.png)
Here because I already create an application so I just need to choose it and if you don't have you can go with option 2
![Create an application](/images/3.backenddeployment/3.3.ebdeploy/19.png)
The backend we are using is java springboot so we will go with option 5
![Programing Language Option](/images/3.backenddeployment/3.3.ebdeploy/20.png)
Our java version is 21 so we will go with option 1
![Java Version](/images/3.backenddeployment/3.3.ebdeploy/21.png)
Here I will go with Y for SSH because it is useful for debugging logs, installing tools,etc. but you don't have to follow me on this
![SSH](/images/3.backenddeployment/3.3.ebdeploy/22.png)
* ***Note:*** that in before this section there can be a option for code commit remember to choose option no(n)

After that it will ask for your keypair just input the keypair you created
![Key Pair Input](/images/3.backenddeployment/3.3.ebdeploy/23.png)
* The passphrase is optional but if you want to improve the security you can input it

Run the command eb create [your env name] to create the env
![Create the env](/images/3.backenddeployment/3.3.ebdeploy/24.png)
* ***Note:*** that if there is a error like this that means you have deleted the default vpc and need to go to vpc and click create default vpc

After it successfully deploy it will return something like this
![Successful deploy](/images/3.backenddeployment/3.3.ebdeploy/25.png)

* ***Note:*** if you see this error it is because you have not config aws
 
Now if you visit it domain it will return a 502 error
![Domain link](/images/3.backenddeployment/3.3.ebdeploy/37.png)
![502 error](/images/3.backenddeployment/3.3.ebdeploy/34.png)

This is because we have not set up our environment variables
Now we need to copy the domain link and save it in a note
![Configuration](/images/3.backenddeployment/3.3.ebdeploy/33.png)
Now go to the configuration and scroll down to Updates Monitoring and and logging
And select edit
Then add 6 more variable like this
![Environmental values](/images/3.backenddeployment/3.3.ebdeploy/36.png)
Now if we reload the domain it will return the error of 401
![Spring boot security error](/images/3.backenddeployment/3.3.ebdeploy/38.png)
This is because the spring boot security in the backend so don't worry now  we just need to edit the front end
