---
title: "Worklog Tuần 7"
date: 2026-11-02
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:
- Nâng cấp kiến trúc ứng dụng từ lưu trữ cục bộ sang mô hình Cloud chuẩn mực: tách biệt tầng dữ liệu sang **Amazon RDS** và tệp tin sang **Amazon S3**.
- Áp dụng thực hành bảo mật tốt nhất: sử dụng **IAM Role** thay cho Access Key cứng, truyền thông tin nhạy cảm qua biến môi trường và giám sát log tập trung bằng **Amazon CloudWatch**.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Khởi tạo instance cơ sở dữ liệu **PostgreSQL** trên **Amazon RDS** (chọn chế độ *No* tại mục Public Access để đảm bảo database không lộ ra Internet) <br> - Cấu hình **Security Group chaining**: thiết lập Inbound Rule của RDS chỉ cho phép lưu lượng TCP tại **Port 5432** có nguồn (Source) đến từ **Security Group ID của EC2** | 02/11/2026 | 02/11/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Cấu hình chuỗi kết nối (Connection String gồm RDS Endpoint, Database Name, Username, Password) thông qua **Environment Variables** trong file cấu hình `systemd` của EC2 <br> - Cập nhật mã nguồn ASP.NET Core sử dụng Entity Framework Core / Npgsql, chạy database migration và xác nhận dữ liệu được lưu trữ bền vững trên PostgreSQL RDS | 03/11/2026 | 03/11/2026 | Microsoft EF Core Docs |
| 4 | - Tạo **IAM Policy** cấp quyền tối thiểu (cho phép `s3:PutObject`, `s3:GetObject` trên đúng Bucket của dự án và quyền ghi log `logs:CreateLogStream`, `logs:PutLogEvents` lên CloudWatch) <br> - Tạo **IAM Role** gắn Policy trên và thực hiện *Modify IAM Role* để gắn trực tiếp vào EC2 instance (tuyệt đối không lưu `AWS_ACCESS_KEY_ID` trong code hay file cấu hình) | 04/11/2026 | 04/11/2026 | AWS IAM Best Practices |
| 5 | - Tích hợp thư viện `AWSSDK.S3` vào Web API, viết endpoint cho phép người dùng tải tệp đính kèm lên **Amazon S3** và trả về đường dẫn/key lưu trong RDS | 05/11/2026 | 05/11/2026 | AWS SDK for .NET Docs |
| 6 | - Tích hợp thư viện logging (`AWS.Logger.AspNetCore` hoặc CloudWatch Agent) để đẩy toàn bộ application log từ EC2 về **Amazon CloudWatch Logs** <br> - Kiểm thử luồng dữ liệu khép kín: Client gọi API trên EC2 -> ghi metadata vào RDS -> lưu file vào S3 -> kiểm tra log giao dịch hiển thị tức thì trên CloudWatch | 06/11/2026 | 06/11/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 7:
- Hoàn thiện kiến trúc đa dịch vụ chuẩn chỉnh trên AWS, loại bỏ hoàn toàn tình trạng dữ liệu bị mất khi thay thế máy chủ EC2.
- Nâng cao mức độ bảo mật hệ thống: Database nằm hoàn toàn trong vùng an toàn không tiếp xúc Internet, và ứng dụng xác thực với các dịch vụ AWS hoàn toàn tự động thông qua cơ chế cấp phát token tạm thời của IAM Role.
- Dễ dàng theo dõi, tìm kiếm và chẩn đoán hành vi ứng dụng thông qua giao diện tập trung của CloudWatch Logs mà không cần SSH vào từng máy chủ để đọc file text.