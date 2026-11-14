---
title: "Worklog Tuần 9"
date: 2026-11-16
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:
- Làm chủ tư duy kiến trúc **Serverless hướng sự kiện (Event-Driven)** trên AWS, hiểu rõ sự khác biệt giữa mô hình máy chủ truyền thống (EC2/ECS) và mô hình phi máy chủ (AWS Lambda).
- Thành thạo công cụ **AWS SAM (Serverless Application Model)** để định nghĩa hạ tầng dưới dạng mã (Infrastructure as Code - IaC), chạy giả lập trên **LocalStack** và tích hợp dịch vụ AI tạo sinh **Amazon Bedrock**.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu sâu kiến trúc **AWS Lambda** (vòng đời thực thi, hiện tượng *Cold Start* với Java 21, cơ chế quản lý bộ nhớ/timeout, concurrency) và **Amazon API Gateway** (HTTP API vs REST API, tiếp nhận Webhook từ bên thứ ba) <br> - Tìm hiểu dịch vụ hàng đợi tin nhắn **Amazon SQS** (Standard vs FIFO Queue, Visibility Timeout, Dead Letter Queue - DLQ) để xử lý bất đồng bộ | 16/11/2026 | 16/11/2026 | AWS Serverless Docs |
| 3 | - Nghiên cứu cơ sở dữ liệu NoSQL **Amazon DynamoDB** (Partition Key, Sort Key, GSI, mô hình On-Demand capacity tối ưu chi phí cho ứng dụng ít truy cập) <br> - Tìm hiểu **AWS SAM CLI**: cấu trúc tệp `template.yaml`, định nghĩa các tài nguyên Lambda, API Gateway, SQS, DynamoDB và phân quyền IAM Policy trực tiếp trong template | 17/11/2026 | 17/11/2026 | AWS SAM Documentation |
| 4 | - **Thực hành LocalStack:** Cài đặt và cấu hình **LocalStack** kết hợp với `sam local` để chạy kiểm thử các hàm Lambda, hàng đợi SQS và bảng DynamoDB ngay trên máy cá nhân mà không cần deploy liên tục lên AWS thật | 18/11/2026 | 18/11/2026 | LocalStack Documentation |
| 5 | - Nghiên cứu **Amazon Bedrock**: cơ chế gọi các mô hình nền tảng (Foundation Models như Claude/Nova) thông qua Bedrock Runtime API <br> - Tìm hiểu khả năng xử lý đa phương thức (**Multimodal**: phân tích văn bản, đọc nội dung từ hình ảnh và trích xuất thông tin tệp tin) phục vụ bài toán nhận diện dấu hiệu lừa đảo | 19/11/2026 | 19/11/2026 | Amazon Bedrock Docs |
| 6 | - Phân tích bài toán thực tế và chốt kiến trúc cho dự án **Ask First (ScamProtection)**: tại sao phải tách luồng nhận Webhook từ Telegram (trả về `200 OK` tức thì trong dưới 3 giây) và luồng xử lý AI nặng thông qua hàng đợi SQS | 20/11/2026 | 20/11/2026 | Tài liệu thiết kế dự án |

### Kết quả đạt được tuần 9:
- Nắm vững quy trình phát triển ứng dụng Serverless hiện đại với **Java 21** và **AWS SAM**, tự tin khai báo toàn bộ hạ tầng bằng mã nguồn (`template.yaml`).
- Thiết lập thành công môi trường phát triển cục bộ với **LocalStack**, giúp rút ngắn thời gian kiểm thử và tránh phát sinh chi phí trong quá trình lập trình.
- Hiểu rõ cách kết nối **Amazon Bedrock** để phân tích ngữ cảnh hội thoại và nội dung đa phương thức nhằm phát hiện kịch bản lừa đảo.