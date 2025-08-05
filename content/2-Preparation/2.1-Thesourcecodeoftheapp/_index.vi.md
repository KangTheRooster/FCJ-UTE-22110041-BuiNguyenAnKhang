---
title : "Chuẩn bị Backend và Frontend"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

### Công nghệ cho Backend và Frontend

#### Frontend
- **Java (Android)**  
  - Java được chọn vì là một trong những ngôn ngữ ổn định và được sử dụng rộng rãi nhất trong phát triển ứng dụng Android.  
  - **Retrofit** để giao tiếp với API và **Amplify SDK** để tích hợp AWS.  
  - Sử dụng XML layouts để xây dựng giao diện người dùng (UI) linh hoạt và phản hồi tốt.  
  - Có sự hỗ trợ lâu dài và cộng đồng lập trình viên lớn, khiến Java trở thành một lựa chọn đáng tin cậy.  

- **XML (Thiết kế giao diện)**  
  - Cung cấp một cách có cấu trúc và linh hoạt để thiết kế các thành phần UI.  
  - Tách biệt phần thiết kế khỏi logic, giúp ứng dụng dễ bảo trì và mở rộng.  
  - Tích hợp tốt với hệ thống xem trước (preview) của Android Studio.  

---

#### Backend
- **Spring Boot (Java)**  
  - Được chọn vì sự đơn giản và hệ sinh thái mạnh mẽ trong việc xây dựng RESTful APIs.  
  - Hỗ trợ phát triển nhanh chóng với các máy chủ nhúng như Tomcat.  
  - Rất phù hợp cho triển khai trên đám mây (Elastic Beanstalk).  
  - Tích hợp sẵn với JPA/Hibernate cho các thao tác cơ sở dữ liệu.  

- **Maven (Quản lý Build & Dependency)**  
  - Tự động hóa việc build dự án, quản lý thư viện (dependencies), và đóng gói thành tệp `.jar`.  
  - Đảm bảo tính nhất quán giữa các môi trường và đơn giản hóa việc triển khai lên AWS Elastic Beanstalk.  
