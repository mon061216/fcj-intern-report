---
title: "Worklog Tuần 12"
date: 2026-12-07
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:
- Hoàn thiện trọn vẹn bộ tài liệu kỹ thuật, sơ đồ kiến trúc Event-Driven Serverless cho dự án **Ask First (ScamProtection)**.
- Tổng kết toàn bộ quá trình 12 tuần thực tập tại First Cloud AI Journey, bảo vệ kết quả dự án và bàn giao tài nguyên.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Vẽ sơ đồ kiến trúc chi tiết của hệ thống **Ask First** (thể hiện rõ luồng dữ liệu từ Telegram -> API Gateway -> Webhook Lambda -> SQS -> Worker Lambda -> S3 / DynamoDB / Amazon Bedrock -> Telegram Alert tới người thân) | 07/12/2026 | 07/12/2026 | Draw.io / Mermaid |
| 3 | - Biên soạn tệp `README.md` hoàn chỉnh cho repository dự án: mô tả bài toán bảo vệ người cao tuổi, giải thích kiến trúc hướng sự kiện, hướng dẫn chạy local với LocalStack/ngrok, quy trình deploy bằng `sam deploy` và bảng phân tích chi phí từng dịch vụ AWS | 08/12/2026 | 08/12/2026 | GitHub Repository |
| 4 | - Rà soát, chuẩn hóa định dạng và hoàn thiện toàn bộ hệ thống Worklog 12 tuần trên trang báo cáo thực tập cá nhân | 09/12/2026 | 09/12/2026 | Tài liệu báo cáo FCAJ |
| 5 | - Chuẩn bị slide thuyết trình và kịch bản demo trực tiếp trên điện thoại/Telegram: thử nghiệm gửi tin nhắn văn bản, hình ảnh, tệp tin và ghi âm lừa đảo để minh họa khả năng phát hiện rủi ro và bắn thông báo sang tài khoản người thân | 10/12/2026 | 10/12/2026 | Thực hành cá nhân |
| 6 | - Tham gia buổi báo cáo tổng kết cuối kỳ thực tập với mentor, giải trình kiến trúc hệ thống (luồng đi của request, vai trò từng dịch vụ, điểm phát sinh lỗi/chi phí), tiếp thu đánh giá và hoàn tất dọn dẹp các tài nguyên thử nghiệm không cần thiết | 11/12/2026 | 11/12/2026 | Tổng kết FCAJ |

### Kết quả đạt được tuần 12:
- Hoàn thành xuất sắc dự án **Ask First (ScamProtection)** cùng bộ tài liệu kỹ thuật và sơ đồ kiến trúc chuyên nghiệp.
- Nắm vững toàn diện cả hai mảng kiến thức: hạ tầng máy chủ truyền thống (EC2, VPC, RDS, Docker) và kiến trúc đám mây hiện đại (Serverless, Event-Driven, IaC với AWS SAM, GenAI với Amazon Bedrock).
- Tự tin giải thích sâu sắc mọi khía cạnh kỹ thuật, bảo mật, xử lý sự cố và tối ưu chi phí của hệ thống trong buổi bảo vệ tổng kết thực tập First Cloud AI Journey.
