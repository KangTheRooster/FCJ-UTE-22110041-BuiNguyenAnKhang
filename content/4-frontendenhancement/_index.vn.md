---
title : "Cách nâng cao frontend"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

Trong bước này, chúng ta sẽ học cách sử dụng amplify để nâng cao trải nghiệm của người dùng cuối.  
Mở cmd trong thư mục frontend của bạn và chạy lệnh `npm install -g @aws-amplify-cli`  
![Spring boot security error](/images/4.frontendenhancement/01.png)  

Sau đó chạy lệnh `amplify init` để bắt đầu cấu hình.  
![Spring boot security error](/images/4.frontendenhancement/02.png)  

Khi được hỏi có muốn chấp nhận cấu hình mặc định hay không, hãy chọn No.  
Sau đó cấu hình như sau:  
- Tên môi trường `dev`  
- Trình soạn thảo mặc định `Android Studio`  
- Loại ứng dụng `.android`  
- Thư mục Res `app\src\main\res\`  
![Spring boot security error](/images/4.frontendenhancement/03.png)  

Khi được hỏi về AWS access key, bạn cần nhập key đã lưu.  
* ***Lưu ý:*** nếu bạn chưa có key, vui lòng kiểm tra.  
![Spring boot security error](/images/4.frontendenhancement/04.png)  

Sau khi hoàn tất, bạn sẽ thấy kết quả như sau:  
![Spring boot security error](/images/4.frontendenhancement/05.png)  

Quay lại thư mục frontend, bạn sẽ thấy đã xuất hiện một thư mục amplify.  
![Spring boot security error](/images/4.frontendenhancement/06.png)  

Bên trong có amplify và aws configuration.  
![Spring boot security error](/images/4.frontendenhancement/07.png)  

Bây giờ mở terminal trong Android Studio và chạy:  
`amplify add auth`  
![Spring boot security error](/images/4.frontendenhancement/09.png)  

Sau khi hoàn tất, chạy tiếp lệnh `amplify push`  
![Spring boot security error](/images/4.frontendenhancement/10.png)  

Khi xong, nó sẽ trả về kết quả như sau:  
![Spring boot security error](/images/4.frontendenhancement/11.png)  

Mở file build.gradle trong thư mục app/ và thêm các dependencies sau:  
- `implementation "com.amplifyframework:core:2.23.0"`  
- `implementation "com.amplifyframework:aws-auth-cognito:2.23.0"`  
- `implementation "com.amplifyframework:aws-api:2.23.0"`  
- `coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:2.0.4'`  
![Spring boot security error](/images/4.frontendenhancement/12.png)  

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


Tạo file mới `MyApplication.java` cùng thư mục với `MainActivity`:  
![Spring boot security error](/images/4.frontendenhancement/13.png)  

Sau đó mở AndroidManifest và thêm dòng sau:  
`android:name=".MyApplication"`  
![Spring boot security error](/images/4.frontendenhancement/14.png)  

Quay lại build.gradle và thêm dòng này trong compileOptions của android:  
- `coreLibraryDesugaringEnabled true`  
![Spring boot security error](/images/4.frontendenhancement/15.png)  

Kéo lên đầu file manifest và thêm:  
- `<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />`  
![Spring boot security error](/images/4.frontendenhancement/16.png)  

Sau đó mở lại terminal và chạy:  
`./gradlew clean build --refresh-dependencies`  
![Spring boot security error](/images/4.frontendenhancement/17.png)  

Cuối cùng, thay đổi base url trong RetrofitService trong thư mục ultis và đổi sang domain của bạn.  
![Spring boot security error](/images/4.frontendenhancement/18.png)  
