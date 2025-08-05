---
title : "Các dịch vụ AWS trong Lab"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

## Backend
### Elastic Beanstalk
- Lưu trữ **ứng dụng backend Spring Boot** (`MusicApp.jar`) được build bằng **Java 21 + Maven**.  
- Quy trình triển khai:  
  1. Code → `mvn clean package` → tạo file `.jar` trong thư mục `target/`.  
  2. `Procfile` chạy file `.jar` trên các instance của EB.  
  3. `eb deploy` tải lên và triển khai ứng dụng.  
- Các biến môi trường (`DB_URL`, `DB_USER`, `DB_PASS`, thông tin Gmail SMTP, …) được thiết lập qua `eb setenv`.  
- Cung cấp **load balancing + auto-scaling** giúp backend tự động mở rộng theo nhu cầu người dùng.  

### S3
- Tạo bucket để **lưu trữ tệp** (sẽ sử dụng trong ứng dụng nhạc sau này).  
- Các trường hợp sử dụng dự kiến:  
  - Lưu **file nhạc** do nghệ sĩ tải lên.  
  - Lưu **ảnh bìa album / ảnh hồ sơ**.  
  - Phục vụ file trực tiếp cho frontend thông qua **pre-signed URLs** (tải xuống an toàn).  
- Backend có thể tạo pre-signed URLs từ S3 để kiểm soát quyền truy cập.  

### Aurora và RDS
- Hiện tại sử dụng **Amazon RDS (MySQL 8.0)** tại `ap-southeast-2`.  
  - Ví dụ cấu hình kết nối:  
    ```
    spring.datasource.url=jdbc:mysql://musicapp-db.c7a64kgsc9iz.ap-southeast-2.rds.amazonaws.com:3306/music_app
    spring.datasource.username=admin
    spring.datasource.password=******
    ```
- Lưu trữ:  
  - **Tài khoản người dùng** (id, email, username, password hash).  
  - **Hồ sơ cá nhân** (họ tên, số điện thoại, …).  
  - **Mã đặt lại mật khẩu & token**.  


---

## Frontend

### Amplify
- Tích hợp vào **frontend Android (Java)** với **Amplify Android v2.23.0**.  
- **Các plugin Amplify trong `MyApplication`:**  
  - `Auth` → Cognito User Pools cho **đăng ký / đăng nhập / làm mới token**.  
  - `API` (đã cấu hình, nhưng backend vẫn sử dụng Retrofit cho REST).  
- **Cách hoạt động trong ứng dụng hiện tại:**  
  1. Người dùng đăng nhập qua Amplify → Cognito cấp **ID + access tokens**.  
  2. Retrofit sử dụng các token này (JWT) để gọi API backend trên Elastic Beanstalk.  
  3. Backend xác thực token, xử lý yêu cầu và truy vấn RDS.  
- Amplify cũng quản lý **duy trì phiên đăng nhập** (người dùng vẫn đăng nhập khi mở lại ứng dụng).  

---

## Tóm tắt luồng hoạt động
- **Ứng dụng Android (Amplify Cognito)** → Xác thực người dùng.  
- **Ứng dụng sử dụng Retrofit APIs** → Gọi backend Spring Boot trên **Elastic Beanstalk**.  
- **Backend giao tiếp với RDS** (dữ liệu người dùng + dữ liệu ứng dụng) và **S3** (lưu trữ media).  

