---
title : "Clean up resources"
date : 2022
weight : 6
chapter : false
pre : "<b>6. </b>"
---
Go to Aurora RDS and choose the database and in the **Action** choose **Delete**
![Delete Aurora RDS](/images/6.clean/00.png)  
* ***Note*** do not create any backup (you can do it if you want but i would not reccomand it)

Go to S3 and select the bucket **music-app-audio-files**
![De](/images/6.clean/01.png) 
You will need to empty it content before deleting it 
![Empty the bucket](/images/6.clean/02.png)  
Select all the content in the bucket and select delete
![Empty the bucket](/images/6.clean/03.png) 
Confirm and delete it    
![Empty the bucket](/images/6.clean/04.png)  
Now go back to the S3 bucket, you can delete it now
![Spring boot security error](/images/6.clean/05.png)  
![Spring boot security error](/images/6.clean/06.png)  
![Spring boot security error](/images/6.clean/07.png)
* ***Note*** if you can not delete it remember to go to the **Permission** tab of the bucket and check the bucket pollicy to make sure it allow delete
![Spring boot security error](/images/6.clean/07-a.png)  
Change the deny to allow and you are good to delete it
Go to the **Elastic Beanstalk->Environment** 
![Spring boot security error](/images/6.clean/08.png)  
Then select the environment and choose action **Terminate**
![Spring boot security error](/images/6.clean/09.png)  
Now go to the **VPC-> Your VPC** and delete all the vpc
![Spring boot security error](/images/6.clean/10.png)    