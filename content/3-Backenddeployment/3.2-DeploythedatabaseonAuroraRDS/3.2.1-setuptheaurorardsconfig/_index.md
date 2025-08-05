---
title : "Set up the config for Aurora and RDS"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2.1 </b> "
---

Open the Aurora and RDS dashboard then select create a database
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/01.png)
Choose my SQL and template as Free Tier (You can choose different tier if you like)
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/02.png)
Scroll down to the setting option, set the DB instance as you want, here I will set it as musicapp-db and username is admin, set the password as you want
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/03.png)
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/04.png)
In connectivity option, change public access to yes and let everything as defult
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/05.png)
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/06.png)\
Scroll down to the Additional Configuration, change the name to music_app
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/07.png)
Then select create and database and go to the database you just created to see it properties
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/09.png)
* Remember to copy the endpoint so we can use it later
- Now go to EC2 Security Group select the security group
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/10.png)
Select **Edit inbound rule**
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/11.png)
Add new rule
- Type **MySQL/Aurora**
- Source **MyIP**
* ***Note*** you can set source as **Any where ipV4** to be easier to access
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/12.png)