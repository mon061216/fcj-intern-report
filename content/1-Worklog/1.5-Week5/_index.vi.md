---
title: "Worklog Tuần 5"
date: 2026-10-19
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
- Thiết lập tài khoản AWS cá nhân tuân thủ nghiêm ngặt các nguyên tắc bảo mật và kiểm soát tài chính.
- Thực hành thao tác trực tiếp trên AWS Console để khởi tạo S3 Bucket, triển khai máy chủ ảo EC2 Linux, cài đặt Web Server Nginx và dọn dẹp tài nguyên đúng quy trình.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Khởi tạo tài khoản AWS và kích hoạt xác thực đa yếu tố **MFA** (Virtual MFA app) cho tài khoản **Root User** <br> - Tạo **IAM User** quản trị riêng (gắn policy `AdministratorAccess`) để sử dụng làm việc hằng ngày, tuyệt đối không dùng Root User cho các tác vụ thông thường | 19/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Truy cập AWS Billing & Cost Management để thiết lập **AWS Budgets** (tạo Zero-Spend Budget và ngưỡng cảnh báo qua email khi chi phí chạm mốc dự kiến) <br> - Chọn **AWS Region** tối ưu về độ trễ cho khu vực Việt Nam (`ap-southeast-1` - Singapore) | 20/10/2026 | 20/10/2026 | AWS Billing Console |
| 4 | - **Thực hành Amazon S3:** <br>&emsp; + Tạo S3 Bucket với tên duy nhất toàn cầu, cấu hình tùy chọn Block All Public Access <br>&emsp; + Thực hiện upload tệp tin (ảnh, tài liệu), kiểm tra thuộc tính Object URL, tải tệp về và thử nghiệm tính năng tạo Presigned URL để chia sẻ tệp tạm thời an toàn | 21/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - **Thực hành Amazon EC2:** <br>&emsp; + Khởi tạo EC2 instance sử dụng Ubuntu/Amazon Linux AMI (`t2.micro`/`t3.micro`), tạo mới Key Pair (`.pem`) <br>&emsp; + Cấu hình Security Group mở cổng SSH (Port 22) giới hạn theo địa chỉ IP cá nhân (`My IP`) <br>&emsp; + Thực hiện kết nối SSH từ Terminal máy cá nhân vào EC2 instance thành công | 22/10/2026 | 22/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **Triển khai Web Server & Dọn dẹp tài nguyên:** <br>&emsp; + Cập nhật hệ thống (`sudo apt update`) và cài đặt **Nginx** trên EC2 <br>&emsp; + Chỉnh sửa Security Group bổ sung Inbound Rule cho phép giao thức HTTP (Port 80) từ mọi nơi (`0.0.0.0/0`), truy cập trang chào mừng của Nginx thành công bằng Public IP trên trình duyệt <br>&emsp; + Thực hiện **Terminate EC2 instance** và xóa S3 Bucket thử nghiệm để đảm bảo không phát sinh chi phí ngầm | 23/10/2026 | 23/10/2026 | Thực hành cá nhân |

### Kết quả đạt được tuần 5:
- Hoàn tất thiết lập môi trường thực hành AWS an toàn, có hàng rào cảnh báo chi phí tự động.
- Lần đầu tiên tự tay khởi tạo máy chủ đám mây, kết nối điều khiển từ xa qua SSH và phục vụ trang web công khai trên Internet qua Nginx.
- Rèn luyện thói quen kiểm tra kỹ bảng điều khiển (EC2, EBS, S3) và dọn dẹp sạch sẽ tài nguyên sau khi hoàn thành bài lab.