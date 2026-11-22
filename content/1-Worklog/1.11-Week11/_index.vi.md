---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:
- Kiểm thử toàn diện độ chính xác và độ ổn định của hệ thống **Ask First** với nhiều định dạng đầu vào và kịch bản lừa đảo thực tế.
- Tối ưu hóa độ trễ (Cold Start) của Java Lambda, xử lý các tình huống lỗi hàng đợi SQS và rà soát bài toán chi phí Serverless.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Thực hiện kiểm thử đầu cuối (End-to-End Testing) trên Telegram với các kịch bản lừa đảo phổ biến: tin nhắn giả danh công an/ngân hàng, hình ảnh chuyển khoản giả mạo, file lạ và tin nhắn thoại (voice message) yêu cầu chuyển tiền | 30/11/2026 | 30/11/2026 | Thực hành dự án |
| 3 | - **Tối ưu hiệu năng & Xử lý lỗi (Troubleshooting):** <br>&emsp; + Giảm thời gian Cold Start của **Java 21 Lambda** bằng cách tối ưu kích thước gói JAR/dependencies và cấu hình tier-1 compilation (`JAVA_TOOL_OPTIONS`) <br>&emsp; + Kiểm thử cơ chế **Dead Letter Queue (DLQ)** trên SQS khi xảy ra lỗi gọi API Bedrock hoặc file âm thanh/hình ảnh quá dung lượng cho phép, theo dõi trace lỗi qua **CloudWatch Logs** | 01/12/2026 | 01/12/2026 | AWS Lambda Java Best Practices |
| 4 | - Rà soát bảo mật và quyền riêng tư dữ liệu người dùng: kiểm tra chính sách tự động xóa tệp media trên **S3 Bucket** (S3 Lifecycle Expiration), đảm bảo dữ liệu DynamoDB được mã hóa và các Lambda Function chỉ có quyền truy cập tối thiểu vào đúng tài nguyên được chỉ định | 02/12/2026 | 02/12/2026 | AWS Well-Architected Framework |
| 5 | - Phân tích chi phí vận hành của kiến trúc Serverless thông qua **AWS Cost Explorer** (so sánh chi phí trả theo lượt gọi của API Gateway, Lambda, SQS, DynamoDB On-Demand và token của Amazon Bedrock so với việc duy trì máy chủ EC2/RDS chạy 24/7) | 03/12/2026 | 03/12/2026 | AWS Pricing & Cost Explorer |
| 6 | - Thiết lập **CloudWatch Alarm** giám sát sức khỏe hệ thống: cảnh báo ngay khi có message rơi vào Dead Letter Queue (DLQ), khi tỷ lệ lỗi Lambda vượt ngưỡng hoặc chi phí gọi Bedrock tăng đột biến | 04/12/2026 | 04/12/2026 | Thực hành dự án |

### Kết quả đạt được tuần 11:
- Nâng cao độ tin cậy và tốc độ phản hồi của bot trên Telegram; xử lý triệt để các trường hợp ngoại lệ như tệp tin lỗi định dạng hoặc quá tải hàng đợi.
- Chứng minh được tính hiệu quả vượt trội về mặt chi phí của kiến trúc Serverless cho bài toán thực tế: chi phí gần như bằng 0 khi không có người dùng tương tác nhưng sẵn sàng mở rộng tức thì khi có nhiều tin nhắn gửi đến cùng lúc.