---
title: "Blog 1"
date: 2026-11-26
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# KIỂM THỬ SERVERLESS & EVENT-DRIVEN TRÊN LOCAL VỚI LOCALSTACK VÀ JAVA 21

Khi phát triển các ứng dụng Serverless hướng sự kiện (Event-Driven) trên AWS—chẳng hạn nhận sự kiện từ webhook đưa vào **Amazon SQS**, xử lý bất đồng bộ qua **AWS Lambda (Java 21)**, lưu trạng thái vào **Amazon DynamoDB**, đọc tham số từ **SSM Parameter Store** và đẩy các bản tin lỗi sang **SQS Dead-Letter Queue (DLQ)**—việc deploy trực tiếp lên cloud cho mỗi lần sửa lỗi nhỏ thường mất nhiều thời gian và dễ phát sinh chi phí ngoài ý muốn.

Bài viết này chia sẻ quy trình kiểm thử **Local-First** kết hợp **LocalStack** và **Java 21 (AWS SDK v2)** để kiểm tra trọn vẹn cả luồng xử lý chuẩn lẫn luồng lỗi/DLQ ngay trên máy cá nhân trước khi triển khai lên AWS bằng **AWS SAM**.

Các nội dung chính trong bài viết:

- **Tách biệt endpoint theo môi trường trong AWS SDK v2:** Chỉ ghi đè endpoint (`endpointOverride`) trỏ tới LocalStack (`http://localhost:4566`) khi chạy ở chế độ local (`isLocal = true`), và giữ nguyên endpoint mặc định khi chạy trên AWS Cloud.
- **Giả lập đồng bộ hạ tầng Event-Driven bằng Docker:** Khởi chạy SQS, DLQ, DynamoDB, SSM Parameter Store, S3, IAM và Lambda trên local thông qua cấu hình `docker-compose.yml` gọn nhẹ tại region `ap-southeast-1`.
- **Kiểm thử cả luồng hợp lệ lẫn luồng lỗi DLQ:** Gửi payload chuẩn để xác nhận việc ghi dữ liệu vào DynamoDB và xóa bản tin khỏi hàng đợi chính, đồng thời gửi payload lỗi cố ý để kiểm chứng cơ chế retry và định tuyến tự động sang **SQS DLQ**.
- **Triển khai AWS SAM an toàn và tiết kiệm hơn:** Phát hiện sớm các lỗi thiếu tham số, lỗi xử lý ngoại lệ hoặc sai cấu hình hàng đợi với chi phí `$0` trên local trước khi đóng gói và deploy lên AWS Cloud.

![Sơ đồ kiến trúc kiểm thử Local-First Serverless](images/blog1-localstack-architecture.png)

- **Link bài viết trên Facebook:** [Link bài viết Blog 1 trên AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj)
- **Cấu hình & Mã nguồn minh họa:** Bao gồm file `docker-compose.yml` khởi chạy LocalStack (`:4566`) và đoạn mã cấu hình endpoint cho `SqsClient` trong Java 21.