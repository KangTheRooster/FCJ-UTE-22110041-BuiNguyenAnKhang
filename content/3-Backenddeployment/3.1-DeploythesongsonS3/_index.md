---
title : "Deploy for the songs' data"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---
## Step 1:
We will need to create an **S3 bucket**
In your home menu, search **S3** and click on it
![Search for S3](/images/3.backenddeployment/3.1.s3deploy/001.png)
In the main console for S3 click **Create bucket**
![Console of S3](/images/3.backenddeployment/3.1.s3deploy/002.png)
![Create bucket button](/images/3.backenddeployment/3.1.s3deploy/003.png)
## Step 2:
### Now we need to set the configuration for the bucket
We need to set a name for the bucket and set it a unique name, here i will call my bucket `music-app-audio-files`
![General Configuration](/images/3.backenddeployment/3.1.s3deploy/004.png)
In the **Block Public Access settings for this bucket** section
Deselect the **Block all public access** box then click the Warning box
![Block Public Access settings for this bucket](/images/3.backenddeployment/3.1.s3deploy/005.png)
After that scroll down to the bottom and select the create bucket
* ***Note:*** remember your bucket name and its region
![Create bucket button](/images/3.backenddeployment/3.1.s3deploy/006.png)
## Step 3
### After AWS create our bucket we will need to deploy our data
Click on the bucket we just created
![Your bucket](/images/3.backenddeployment/3.1.s3deploy/007.png)
Then select the upload button
![Upload section](/images/3.backenddeployment/3.1.s3deploy/008.png)
After that we will select the **Add folder**
![Add folder button](/images/3.backenddeployment/3.1.s3deploy/009.png)
Then locate the place where we will store our songs
![Locates where you store your songs folder](/images/3.backenddeployment/3.1.s3deploy/010.png)
* You can download my song folder here: [Songs link](https://drive.google.com/file/d/1SeIgQEcaohhNQzAQo4sL0Efhty97k6hs/view?usp=sharing)
* My structure for the song folder is 
![Structure song folder](/images/3.backenddeployment/3.1.s3deploy/022.png)
Now we will select the **upload option**
![Upload board now change](/images/3.backenddeployment/3.1.s3deploy/011.png)
Wait until it finished all the upload
![Upload status](/images/3.backenddeployment/3.1.s3deploy/012.png)
## Step 4:
### Set up the permission
After we upload every thing you can go and check it structure just as my structure
Now select a random folder and click on it here i will choose the song called **The Riot**
![Songs folder is now on S3](/images/3.backenddeployment/3.1.s3deploy/013.png)
You can choose 1 or 3 of it attributes but I will recommand choosing the picture so when we finish and test it again it will not download the song to your computer
![The selected song](/images/3.backenddeployment/3.1.s3deploy/014.png)
![Song's image](/images/3.backenddeployment/3.1.s3deploy/015.png)
After click on the song image you will see its properties
![Image's properties](/images/3.backenddeployment/3.1.s3deploy/016.png)
Copy in the Object URL and paste it in another tab it will return access denied
![Access Denied](/images/3.backenddeployment/3.1.s3deploy/017.png)
This is due to we are only set public for the bucket not its content so to view its content we will need to add a new bucket policy
Head back to the `music_app_audio_files` and select the permission tab
![Permission tab](/images/3.backenddeployment/3.1.s3deploy/018.png)
Here we can see the policy of the bucket is empty and it is currently allow public access
Now select the "Edit" button in the bucket policy setting and paste this in
```
json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowPublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::music-app-audio-files/*"
    }
  ]
}
```
![Add new policy](/images/3.backenddeployment/3.1.s3deploy/019.png)
![The policy](/images/3.backenddeployment/3.1.s3deploy/020.png)
After select the **save changes** option, head back to the other tab and reload you should be able to load the image
* Remember to change the resource bucket's name into your bucket name
![Load image success](/images/3.backenddeployment/3.1.s3deploy/021.png)
* In this step you can go with pre-signed URLs in code(backend Java, Python, etc) however these URLs will expire after a short time but are safe for limited access.