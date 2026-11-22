---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:
- Phát triển hoàn chỉnh các dịch vụ Backend bằng **Java 21** và triển khai hạ tầng Serverless trên AWS cho dự án **Ask First (ScamProtection)**.
- Hoàn thiện luồng xử lý tin nhắn đa phương thức (văn bản, hình ảnh, tệp tin, âm thanh) từ Telegram Bot và tính năng liên kết, gửi cảnh báo khẩn cấp tới người thân.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Khởi tạo cấu trúc dự án **Ask First** với Maven, Java 21 và AWS SAM (`template.yaml`) <br> - Thiết kế schema bảng **Amazon DynamoDB** để lưu trữ thông tin người dùng cao tuổi, mã liên kết gia đình (Family Link), lịch sử phiên kiểm tra nguy cơ và trạng thái cảnh báo | 23/11/2026 | 23/11/2026 | Thực hành dự án |
| 3 | - Phát triển **Webhook Receiver Lambda** kết nối với **API Gateway**: tiếp nhận sự kiện từ **Telegram Bot API** (hỗ trợ kiểm thử cục bộ qua ngrok và webhook thật trên AWS), xác thực token bí mật, đẩy payload vào **Amazon SQS** và phản hồi trạng thái `200 OK` ngay lập tức để tránh Telegram gửi lặp tin nhắn | 24/11/2026 | 24/11/2026 | Telegram Bot API Docs |
| 4 | - Phát triển **Multimodal Worker Lambda** lắng nghe sự kiện từ SQS: <br>&emsp; + Xử lý tải tệp phương tiện (hình ảnh biên lai/tin nhắn chụp màn hình, file đính kèm, tệp âm thanh/voice note) từ máy chủ Telegram và lưu trữ an toàn vào **Amazon S3** (cấu hình Lifecycle tự động xóa sau thời gian ngắn để bảo vệ quyền riêng tư) <br>&emsp; + Chuyển đổi âm thanh sang văn bản (Speech-to-Text) và gửi dữ liệu đa phương thức sang **Amazon Bedrock** kèm Prompt chuyên biệt để đánh giá mức độ rủi ro lừa đảo | 25/11/2026 | 25/11/2026 | Amazon Bedrock & S3 Docs |
| 5 | - Phát triển luồng **Liên kết người thân & Cảnh báo tự động**: <br>&emsp; + Xây dựng chức năng tạo mã kết nối giữa tài khoản Telegram của người cao tuổi và người thân giám hộ <br>&emsp; + Khi Bedrock đánh giá mức độ nguy cơ cao, hệ thống tự động định dạng lời khuyên dễ hiểu gửi lại cho người cao tuổi, đồng thời bắn thông báo cảnh báo chi tiết kèm bằng chứng tới Telegram của người thân | 26/11/2026 | 26/11/2026 | Thực hành dự án |
| 6 | - Triển khai toàn bộ stack lên AWS thông qua lệnh `sam build` và `sam deploy` <br> - Cấu hình **Environment Variables** / AWS Systems Manager Parameter Store để quản lý Telegram Bot Token, cấu hình IAM Role cho từng Lambda theo nguyên tắc Least Privilege và kiểm tra log tập trung trên **CloudWatch** | 27/11/2026 | 27/11/2026 | AWS SAM Deployment |

### Kết quả đạt được tuần 10:
- Hoàn thiện hệ thống Backend Serverless **Ask First** chạy thực tế trên AWS, tích hợp mượt mà với Telegram Bot.
- Người cao tuổi có thể gửi trực tiếp tin nhắn văn bản, ảnh chụp màn hình, tệp tin hoặc ghi âm giọng nói để bot phân tích nguy cơ lừa đảo và nhận phản hồi trực quan, dễ hiểu.
- Cơ chế cảnh báo đa tầng hoạt động chính xác: vừa trấn an và hướng dẫn người cao tuổi phòng tránh, vừa kịp thời báo động cho người thân can thiệp.