---
title : "How to enhance frontend"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---


In this step, will learn how to use amplify to enhance the end user's experience
Open the cmd in you front end location and use this command `npm install -g @aws-amplify-cli`
![Spring boot security error](/images/4.frontendenhancement/01.png)
Then run the command `amplify init` to start the configuration.
![Spring boot security error](/images/4.frontendenhancement/02.png)
Then  when it ask if you want to accept the defult configuration remember to said no
Then please config as follow
- Name of the environment `dev` 
- Default editor `Android Studio`
- Type of app `.android`
- Res directory  `app\src\main\res\`
![Spring boot security error](/images/4.frontendenhancement/03.png)
When it ask for your AWS access key you need to provide the key you have save
* ***Note:*** if you don't have your key please check 
![Spring boot security error](/images/4.frontendenhancement/04.png)
After that it finish, you will see some thing like this
![Spring boot security error](/images/4.frontendenhancement/05.png)
You can go back the folder where you have the frontend, now you will see that it has created an amplify file
![Spring boot security error](/images/4.frontendenhancement/06.png)
Inside it is an amplify and an aws configuration
![Spring boot security error](/images/4.frontendenhancement/07.png)
Now open the termminal in android studio and run this
`amplify add auth`
![Spring boot security error](/images/4.frontendenhancement/09.png)
Then after it finished run this command  `amplify push`
![Spring boot security error](/images/4.frontendenhancement/10.png)
After it finished, it will return something like this
![Spring boot security error](/images/4.frontendenhancement/11.png)
Open the build.gradle in the app/ folder and add these in the dependencies
- `implementation "com.amplifyframework:core:2.23.0"`
- `implementation "com.amplifyframework:aws-auth-cognito:2.23.0"`
- `implementation "com.amplifyframework:aws-api:2.23.0"`
- `coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:2.0.4'`
![Spring boot security error](/images/4.frontendenhancement/12.png)
Create a new `MyApplication.java` file in the same folder as `MainActivity`:
```java
package com.example.musicapp;

import android.app.Application;
import android.util.Log;

import com.amplifyframework.AmplifyException;
import com.amplifyframework.core.Amplify;
import com.amplifyframework.auth.cognito.AWSCognitoAuthPlugin;

public class MyApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        try {
            Amplify.addPlugin(new AWSCognitoAuthPlugin());
            Amplify.configure(getApplicationContext());
            Log.i("MyAmplifyApp", "Initialized Amplify v2");
        } catch (AmplifyException e) {
            Log.e("MyAmplifyApp", "Could not initialize Amplify", e);
        }
    }
}
```

![Spring boot security error](/images/4.frontendenhancement/13.png)
After that, open the AndroidManifest and add this `android:name=".MyApplication"`
![Spring boot security error](/images/4.frontendenhancement/14.png)
Now go back to the build.gradle and add this in compileOptions of android
- `coreLibraryDesugaringEnabled true`
![Spring boot security error](/images/4.frontendenhancement/15.png)
And scroll up to the top manifset and add these
- `<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />`
![Spring boot security error](/images/4.frontendenhancement/16.png)
After that open the terminal again and run `./gradlew clean build --refresh-dependencies` 
![Spring boot security error](/images/4.frontendenhancement/17.png)
Finally just change the base url in the RetrofitService in the  ultis and change the link to your domain
![Spring boot security error](/images/4.frontendenhancement/18.png)

