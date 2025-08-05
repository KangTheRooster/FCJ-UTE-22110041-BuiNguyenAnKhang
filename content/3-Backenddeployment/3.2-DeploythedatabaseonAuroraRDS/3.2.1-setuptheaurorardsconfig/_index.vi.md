---
title : "Cấu hình Aurora và RDS"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2.1 </b> "
---

Mở bảng điều khiển **Aurora và RDS** sau đó chọn **Create database**  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/01.png)  

Chọn **MySQL** và mẫu **Free Tier** (bạn có thể chọn tier khác nếu muốn)  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/02.png)  

Cuộn xuống phần **Settings**, đặt tên DB instance theo ý muốn, ở đây tôi đặt là `musicapp-db`, username là `admin`, mật khẩu tự đặt  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/03.png)  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/04.png)  

Trong phần **Connectivity**, đổi **Public access** thành **Yes** và giữ nguyên các thiết lập mặc định khác  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/05.png)  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/06.png)  

Cuộn xuống phần **Additional Configuration**, đổi tên database thành `music_app`  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/07.png)  

Sau đó chọn **Create database** và mở database vừa tạo để xem chi tiết thuộc tính  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/09.png)  

* Nhớ copy lại **endpoint** để sử dụng sau này.  

---

Bây giờ vào **EC2 Security Group**, chọn security group liên quan  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/10.png)  

Chọn **Edit inbound rule**  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/11.png)  

Thêm một rule mới:  
- Type: **MySQL/Aurora**  
- Source: **MyIP**  

* ***Lưu ý:*** bạn có thể đặt source là **Anywhere (IPv4)** để dễ dàng truy cập hơn.  
![a](/images/3.backenddeployment/3.2.aurorardsdeploy/3.2.1.setuprds/12.png)  
