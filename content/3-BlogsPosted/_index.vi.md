---
title: "Các bài blogs đã đăng"
date: 2026-11-26
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Dưới đây là danh sách các bài viết kỹ thuật chuyên sâu được biên soạn và chia sẻ trên cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) trong suốt quá trình thực tập:

### [Blog 1 - KIỂM THỬ SERVERLESS & EVENT-DRIVEN TRÊN LOCAL VỚI LOCALSTACK VÀ JAVA 21](3.1-blog1/)
Chia sẻ quy trình kiểm thử Local-First kết hợp LocalStack, Docker và Java 21 (AWS SDK v2) để kiểm chứng trọn vẹn luồng xử lý và cơ chế định tuyến lỗi Dead-Letter Queue (DLQ) trước khi triển khai lên đám mây với chi phí $0 bằng AWS SAM.

### [Blog 2 - LAMBDA + EVENTBRIDGE: TỰ ĐỘNG CẬP NHẬT DỮ LIỆU HẰNG NGÀY VỚI EVENT-DRIVEN ARCHITECTURE](3.2-blog2/)
Hướng dẫn xây dựng kiến trúc Serverless hướng sự kiện trên AWS kết nối Amazon EventBridge Scheduler, AWS Lambda và Amazon S3/CloudFront để tự động tổng hợp và cập nhật dữ liệu đa nguồn độc lập theo thời gian thực.

### [Blog 3 - THIẾT KẾ LUỒNG DỮ LIỆU IOT (MQTT → AWS IOT CORE → GLUE → S3) TỐI ƯU CHI PHÍ CHO ĐỒ ÁN QUY MÔ NHỎ](3.3-blog3/)
Chia sẻ giải pháp giải quyết "cơn ác mộng small files" trong các dự án IoT trên AWS: kết hợp IoT Core Rule Engine, S3 Lifecycle và AWS Glue ETL để nén hàng triệu file JSON thành Apache Parquet, tiết kiệm ~85% dung lượng lưu trữ và ~98% chi phí truy vấn Athena.
