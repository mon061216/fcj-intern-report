---
title: "Worklog Tuần 8"
date: 2026-11-09
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:
- Làm chủ công nghệ đóng gói ứng dụng bằng **Docker** để giải quyết triệt để vấn đề sai khác môi trường giữa máy lập trình và máy chủ thực tế.
- Đóng gói ASP.NET Core Web API thành Docker Image tối ưu và vận hành ứng dụng dưới dạng Container trên EC2.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu kiến trúc Docker: phân biệt bản thiết kế tĩnh (**Docker Image** với cấu trúc các lớp layer) và thực thể đang chạy (**Docker Container**), vai trò của Docker Daemon và Docker Registry | 09/11/2026 | 09/11/2026 | Docker Documentation |
| 3 | - Viết `Dockerfile` áp dụng kỹ thuật **Multi-stage Build** (sử dụng image `mcr.microsoft.com/dotnet/sdk` để build code và chỉ copy thành phẩm sang image `mcr.microsoft.com/dotnet/aspnet` gọn nhẹ để chạy) <br> - Thực hành lệnh `docker build -t todo-api:v1 .` và chạy kiểm thử container bằng `docker run` ở máy cá nhân | 10/11/2026 | 10/11/2026 | Microsoft .NET Docker Docs |
| 4 | - Thực hành các kỹ thuật quản lý container nâng cao: ánh xạ cổng kết nối (**Port mapping** `-p 8080:8080`), gắn kết dữ liệu bền vững (**Volume** `-v`) và truyền cấu hình nhạy cảm qua **Environment Variables** (`-e` hoặc `--env-file`) | 11/11/2026 | 11/11/2026 | Docker Documentation |
| 5 | - Tạo tệp `docker-compose.yml` để khai báo tường minh cấu hình dịch vụ, mạng nội bộ, chính sách tự khởi động lại (`restart: unless-stopped`) và các biến môi trường kết nối RDS/S3 | 12/11/2026 | 12/11/2026 | Docker Compose Docs |
| 6 | - Cài đặt Docker Engine và Docker Compose plugin trên máy chủ **EC2 Ubuntu** <br> - Đưa mã nguồn/image lên EC2, khởi chạy hệ thống bằng lệnh `docker compose up -d`, kiểm tra log qua `docker logs -f` và xác nhận API hoạt động ổn định thay thế hoàn toàn cách cài đặt thủ công trước đây | 13/11/2026 | 13/11/2026 | Thực hành cá nhân |

### Kết quả đạt được tuần 8:
- Nắm vững kỹ thuật viết `Dockerfile` chuẩn xác và tối ưu dung lượng image thông qua multi-stage build.
- Chuyển đổi thành công quy trình triển khai Backend trên EC2 sang dạng container hóa, giúp việc nâng cấp phiên bản hoặc khôi phục ứng dụng chỉ mất vài giây với một câu lệnh duy nhất.