---
title: "Worklog Tuần 6"
date: 2026-10-26
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:
- Nắm vững quy trình đóng gói (Publish) và triển khai một ứng dụng Backend thực tế viết bằng **ASP.NET Core Web API** lên máy chủ Linux trên AWS.
- Cấu hình ứng dụng chạy bền bỉ dưới dạng Linux `systemd` service và mở kết nối truy cập tài liệu API (Swagger UI) từ Internet.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Xây dựng ứng dụng **Todo API** cơ bản bằng ASP.NET Core (hỗ trợ đầy đủ các endpoint `GET`, `POST`, `PUT`, `DELETE` và tích hợp Swagger UI) <br> - Chạy kiểm thử ứng dụng trên máy cá nhân, sau đó chạy lệnh `dotnet publish -c Release -o ./publish` để xuất ra gói tệp thực thi tối ưu | 26/10/2026 | 26/10/2026 | Microsoft .NET Docs |
| 3 | - Khởi tạo máy chủ **EC2 Ubuntu** mới trên AWS và kết nối SSH <br> - Cài đặt **ASP.NET Core Runtime** phù hợp với phiên bản .NET của dự án trên Ubuntu server và kiểm tra bằng lệnh `dotnet --info` | 27/10/2026 | 27/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Sử dụng lệnh `scp` để truyền toàn bộ thư mục `./publish` từ máy cá nhân lên thư mục `/var/www/todoapi` trên EC2 <br> - Chạy thử ứng dụng ở chế độ **Foreground** (`dotnet TodoApi.dll --urls "http://0.0.0.0:5000"`) để quan sát trực tiếp log khởi động và kiểm tra các lỗi thiếu thư viện (nếu có) | 28/10/2026 | 28/10/2026 | Thực hành cá nhân |
| 5 | - Tạo tệp cấu hình dịch vụ `/etc/systemd/system/todoapi.service` với các tham số `WorkingDirectory`, `ExecStart`, `Restart=always`, `User=www-data` <br> - Kích hoạt dịch vụ bằng `sudo systemctl daemon-reload`, `sudo systemctl enable todoapi` và `sudo systemctl start todoapi` để API chạy ngầm ổn định | 29/10/2026 | 29/10/2026 | Linux Systemd Docs |
| 6 | - Cấu hình **Security Group** của EC2 mở Inbound Rule cho cổng ứng dụng (Custom TCP Port 5000) <br> - Mở trình duyệt trên máy cá nhân, truy cập `http://<EC2-Public-IP>:5000/swagger` và thực hiện gọi thử các API tạo/xem/xóa dữ liệu thành công | 30/10/2026 | 30/10/2026 | Thực hành cá nhân |

### Kết quả đạt được tuần 6:
- Triển khai thành công ứng dụng ASP.NET Core Web API từ môi trường phát triển cá nhân lên hoạt động thực tế trên hạ tầng AWS EC2.
- Ứng dụng tự động khởi chạy cùng hệ điều hành và tự động phục hồi nếu gặp sự cố nhờ quản lý qua `systemd` service.
- Nắm vững cách gỡ lỗi (debug) kết nối mạng giữa cấu hình lắng nghe địa chỉ IP của ứng dụng (`0.0.0.0` thay vì chỉ `localhost`) và luật mở cổng của AWS Security Group.