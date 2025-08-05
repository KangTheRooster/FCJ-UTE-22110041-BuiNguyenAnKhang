---
title : "Dọn dẹp tài nguyên"
date : 2022
weight : 6
chapter : false
pre : "<b>6. </b>"
---

Vào Aurora RDS và chọn database, trong phần **Action** chọn **Delete**  
![Delete Aurora RDS](/images/6.clean/00.png)  
* ***Lưu ý:*** không cần tạo bản sao lưu (bạn có thể làm nếu muốn, nhưng tôi không khuyến nghị).  

Vào S3 và chọn bucket **music-app-audio-files**  
![De](/images/6.clean/01.png)  
Bạn sẽ cần làm trống nội dung của nó trước khi xóa  
![Empty the bucket](/images/6.clean/02.png)  

Chọn tất cả nội dung trong bucket và chọn **Delete**  
![Empty the bucket](/images/6.clean/03.png)  

Xác nhận và xóa  
![Empty the bucket](/images/6.clean/04.png)  

Bây giờ quay lại bucket S3, bạn có thể xóa nó  
![Spring boot security error](/images/6.clean/05.png)  
![Spring boot security error](/images/6.clean/06.png)  
![Spring boot security error](/images/6.clean/07.png)  

* ***Lưu ý:*** nếu bạn không thể xóa, hãy vào tab **Permission** của bucket và kiểm tra **Bucket Policy** để đảm bảo nó cho phép xóa.  
![Spring boot security error](/images/6.clean/07-a.png)  

Đổi `Deny` thành `Allow` và bạn sẽ có thể xóa bucket.  

Vào **Elastic Beanstalk → Environment**  
![Spring boot security error](/images/6.clean/08.png)  

Chọn environment và chọn action **Terminate**  
![Spring boot security error](/images/6.clean/09.png)  

Sau đó vào **VPC → Your VPC** và xóa toàn bộ VPC  
![Spring boot security error](/images/6.clean/10.png)  
