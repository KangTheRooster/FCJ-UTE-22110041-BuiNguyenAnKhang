---
title : "Mục đích của ứng dụng"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1.1 </b> "
---

### Giới thiệu

Trong bối cảnh sự phát triển nhanh chóng của công nghệ số, âm nhạc đã trở thành một phần không thể thiếu trong đời sống hàng ngày của con người. Việc tạo ra một ứng dụng phát nhạc trực tuyến không chỉ đáp ứng nhu cầu giải trí mà còn kết nối người dùng với một thế giới âm nhạc đa dạng và phong phú. Với sự phổ biến của các nền tảng như **Spotify**, việc phát triển một ứng dụng tương tự và tích hợp các tính năng hiện đại, thân thiện với người dùng là một giải pháp hiệu quả để nâng cao trải nghiệm nghe nhạc và thu hút người dùng.

Dự án này tập trung vào việc xây dựng một ứng dụng phát nhạc trực tuyến dựa trên **Java Spring Boot**, lấy cảm hứng từ Spotify. Hệ thống được thiết kế với các tính năng chính như:
- Phát nhạc trực tuyến  
- Tạo và quản lý danh sách phát  
- Tìm kiếm và gợi ý bài hát dựa trên sở thích của người dùng  
- Quản lý tài khoản người dùng  
- Hỗ trợ tải nhạc ngoại tuyến để tiện lợi và linh hoạt hơn  

Quy trình phát triển áp dụng các nguyên lý cốt lõi của **Kỹ thuật phần mềm**, bao gồm:
- Phân tích yêu cầu (SRS)  
- Thiết kế hệ thống với **biểu đồ Use Case**, **biểu đồ lớp (Class diagrams)**, **biểu đồ tuần tự (Sequence diagrams)**, và **biểu đồ cộng tác (Collaboration diagrams)**  
- Xây dựng kiến trúc hệ thống hướng đối tượng  
- Tích hợp API để mang lại trải nghiệm phát nhạc mượt mà và chất lượng cao  

Thông qua quá trình triển khai dự án, nhóm đã có cơ hội áp dụng kiến thức lý thuyết vào thực tiễn, bao gồm phân tích yêu cầu, thiết kế hệ thống, triển khai và kiểm thử. Quá trình này không chỉ giúp nhóm hiểu sâu hơn về **vòng đời phát triển phần mềm** mà còn rèn luyện **kỹ năng lập trình, giải quyết vấn đề và làm việc nhóm**.

Tuy nhiên, do hạn chế về thời gian và kinh nghiệm, quá trình phát triển khó tránh khỏi những thách thức — từ **thiết kế giao diện chưa tối ưu** cho đến **giới hạn về hiệu suất hệ thống**. Những thiếu sót này trở thành bài học quý giá, và nhóm luôn sẵn sàng đón nhận những đóng góp, phản hồi để tiếp tục hoàn thiện ứng dụng trong tương lai.

Để đảm bảo **khả năng mở rộng, bảo mật và độ tin cậy**, hệ thống được **triển khai trên AWS**. Ứng dụng sử dụng **Elastic Beanstalk** để triển khai backend, **RDS (Aurora MySQL)** cho quản lý cơ sở dữ liệu, **S3** để lưu trữ dữ liệu đa phương tiện, và **Amplify (Cognito)** cho xác thực và tích hợp frontend. Kiến trúc dựa trên điện toán đám mây này đảm bảo ứng dụng có thể phát triển theo nhu cầu của người dùng đồng thời duy trì hiệu suất và tính sẵn sàng cao.
