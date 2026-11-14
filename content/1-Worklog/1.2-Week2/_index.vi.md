---
title: "Worklog Tuần 2"
date: 2026-09-28
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:
- Làm chủ môi trường dòng lệnh Linux (CLI) – nền tảng vận hành của hơn 90% máy chủ Cloud hiện nay.
- Hiểu cách thức quản lý tiến trình (Process), dịch vụ nền (Service), phân quyền hệ thống và cấu hình mạng (IP, Port, Firewall, SSH) để đưa một ứng dụng lên chạy trên máy chủ từ xa.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - So sánh sự khác biệt cốt lõi giữa Windows Server và Linux (kiến trúc nhân, giao diện dòng lệnh, cơ chế phân quyền, hiệu năng và chi phí bản quyền) <br> - Tìm hiểu khái niệm **Terminal**, **Shell** (Bash/Zsh) và cấu trúc hệ thống tệp tin chuẩn FHS trên Linux (`/etc` chứa file cấu hình, `/var/log` chứa log, `/home` chứa dữ liệu người dùng, `/usr/bin` chứa chương trình) | 28/09/2026 | 28/09/2026 | Linux Journey |
| 3 | - **Thực hành thao tác CLI:** <br>&emsp; + Quản lý thư mục và tệp tin: `ls -la`, `cd`, `pwd`, `mkdir -p`, `cp -r`, `mv`, `rm -rf` <br>&emsp; + Đọc và lọc nội dung file: `cat`, `less`, `head`, `tail -f`, `grep` <br>&emsp; + Phân quyền truy cập file và thư mục bằng `chmod` (dạng số như `755`, `644`, `400` và dạng ký tự `u+x`) và chuyển quyền sở hữu bằng `chown` | 29/09/2026 | 29/09/2026 | Ubuntu Documentation |
| 4 | - Phân biệt **Program** (tệp thực thi nằm trên ổ đĩa), **Process** (tiến trình đang nạp trên RAM có PID riêng) và **Service** (tiến trình chạy ngầm được quản lý bởi `systemd`) <br> - Thực hành kiểm tra tài nguyên với `ps aux`, `top`/`htop`, `kill -9` và quản lý service qua `systemctl status/start/stop/enable` <br> - Phân biệt chế độ chạy **Foreground** (chiếm dụng terminal, in log trực tiếp) và **Background** (chạy ngầm, ghi log ra file hoặc `journalctl`) | 30/09/2026 | 30/09/2026 | Linux Journey |
| 5 | - Nghiên cứu kiến trúc mạng máy chủ: <br>&emsp; + Sự khác nhau giữa **Public IP** (định tuyến trên Internet) và **Private IP** (dải mạng nội bộ theo chuẩn RFC 1918 như `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`) <br>&emsp; + Cách tính toán số lượng địa chỉ IP khả dụng từ ký hiệu **CIDR** (ví dụ `/16`, `/24`), vai trò của **Subnet** và **Default Gateway** <br>&emsp; + Cơ chế lọc gói tin của **Firewall** (`ufw` / `iptables`) dựa trên địa chỉ IP nguồn, giao thức (TCP/UDP) và Port đích | 01/10/2026 | 01/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - Nghiên cứu cơ chế mã hóa bất đối xứng của giao thức **SSH** (Port 22) sử dụng cặp khóa **Public Key** (lưu trên server tại `~/.ssh/authorized_keys`) và **Private Key** (giữ bí mật ở máy client) <br> - **Thực hành:** Dùng lệnh `ssh-keygen` tạo cặp khóa RSA/Ed25519, phân quyền `chmod 400` cho Private Key và thực hiện kết nối SSH vào máy ảo Linux thành công | 02/10/2026 | 02/10/2026 | Thực hành cá nhân |

### Kết quả đạt được tuần 2:
- Thành thạo bộ lệnh Linux thiết yếu phục vụ việc quản trị file, tìm kiếm log lỗi và phân quyền bảo mật trên server.
- Hiểu rõ vòng đời của một ứng dụng trên Linux: từ lúc khởi chạy thủ công dưới dạng Process đến khi đóng gói thành Service tự động phục hồi khi server khởi động lại.
- Nắm vững điều kiện tiên quyết để một client kết nối được tới ứng dụng trên server: Server phải có Public IP, ứng dụng phải lắng nghe trên đúng Port và Firewall phải mở luật (Inbound Rule) cho Port đó.