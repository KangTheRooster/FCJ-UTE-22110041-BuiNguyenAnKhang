---
title : "Triển khai dữ liệu bài hát"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

## Bước 1:
Chúng ta sẽ cần tạo một **S3 bucket**  
Trong menu chính, tìm kiếm **S3** và nhấp vào nó  
![Search for S3](/images/3.backenddeployment/3.1.s3deploy/001.png)  
Trong giao diện chính của S3, nhấn **Create bucket**  
![Console of S3](/images/3.backenddeployment/3.1.s3deploy/002.png)  
![Create bucket button](/images/3.backenddeployment/3.1.s3deploy/003.png)  

## Bước 2:
### Cấu hình bucket
Chúng ta cần đặt tên cho bucket và đảm bảo tên là duy nhất. Ở đây tôi sẽ đặt tên bucket là `music-app-audio-files`  
![General Configuration](/images/3.backenddeployment/3.1.s3deploy/004.png)  

Trong phần **Block Public Access settings for this bucket**  
Bỏ chọn ô **Block all public access** rồi xác nhận cảnh báo  
![Block Public Access settings for this bucket](/images/3.backenddeployment/3.1.s3deploy/005.png)  

Sau đó cuộn xuống cuối và chọn **Create bucket**  
* ***Lưu ý:*** ghi nhớ tên bucket và khu vực (region) của nó  
![Create bucket button](/images/3.backenddeployment/3.1.s3deploy/006.png)  

## Bước 3:
### Triển khai dữ liệu lên bucket
Sau khi AWS tạo bucket, nhấp vào bucket vừa tạo  
![Your bucket](/images/3.backenddeployment/3.1.s3deploy/007.png)  

Chọn nút **Upload**  
![Upload section](/images/3.backenddeployment/3.1.s3deploy/008.png)  

Sau đó chọn **Add folder**  
![Add folder button](/images/3.backenddeployment/3.1.s3deploy/009.png)  

Xác định vị trí thư mục chứa bài hát của bạn  
![Locates where you store your songs folder](/images/3.backenddeployment/3.1.s3deploy/010.png)  

* Bạn có thể tải thư mục bài hát của tôi tại đây: [Songs link](https://drive.google.com/file/d/1SeIgQEcaohhNQzAQo4sL0Efhty97k6hs/view?usp=sharing)  
* Cấu trúc thư mục bài hát của tôi như sau:  
![Structure song folder](/images/3.backenddeployment/3.1.s3deploy/022.png)  

Bây giờ chọn **Upload**  
![Upload board now change](/images/3.backenddeployment/3.1.s3deploy/011.png)  

Chờ cho đến khi tải xong toàn bộ  
![Upload status](/images/3.backenddeployment/3.1.s3deploy/012.png)  

## Bước 4:
### Cấu hình quyền truy cập
Sau khi tải xong, bạn có thể kiểm tra cấu trúc giống như hình minh họa.  

Bây giờ chọn một thư mục bất kỳ, ở đây tôi chọn bài hát **The Riot**  
![Songs folder is now on S3](/images/3.backenddeployment/3.1.s3deploy/013.png)  

Bạn có thể chọn một vài thuộc tính của nó, nhưng tôi khuyên nên chọn ảnh (image) để khi kiểm tra lại thì không bị tải nhạc về máy tính.  
![The selected song](/images/3.backenddeployment/3.1.s3deploy/014.png)  
![Song's image](/images/3.backenddeployment/3.1.s3deploy/015.png)  

Sau khi nhấp vào ảnh, bạn sẽ thấy phần thuộc tính (properties)  
![Image's properties](/images/3.backenddeployment/3.1.s3deploy/016.png)  

Copy Object URL và dán vào tab mới → sẽ hiển thị **Access Denied**  
![Access Denied](/images/3.backenddeployment/3.1.s3deploy/017.png)  

Điều này là do chúng ta mới bật public cho bucket chứ chưa cho nội dung của nó. Để xem được nội dung, ta cần thêm **Bucket Policy**.  

Quay lại bucket `music-app-audio-files` và chọn tab **Permissions**  
![Permission tab](/images/3.backenddeployment/3.1.s3deploy/018.png)  

Tại đây bạn sẽ thấy bucket policy đang trống và đang cho phép public access.  
Chọn nút **Edit** trong phần bucket policy và dán đoạn sau:  
```
json
{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "AllowPublicRead",
"Effect": "Allow",
"Principal": "",
"Action": "s3:GetObject",
"Resource": "arn:aws:s3:::music-app-audio-files/"
}
]
}
```
![Add new policy](/images/3.backenddeployment/3.1.s3deploy/019.png)  
![The policy](/images/3.backenddeployment/3.1.s3deploy/020.png)  

Sau khi chọn **Save changes**, quay lại tab cũ và reload → bạn sẽ thấy ảnh được hiển thị.  
* Nhớ thay đổi tên bucket trong `Resource` thành tên bucket của bạn.  
![Load image success](/images/3.backenddeployment/3.1.s3deploy/021.png)  

* Ở bước này bạn cũng có thể sử dụng **pre-signed URLs** trong code (Java backend, Python, …). Tuy nhiên, các URL này sẽ hết hạn sau một thời gian ngắn nhưng an toàn cho truy cập giới hạn.  
