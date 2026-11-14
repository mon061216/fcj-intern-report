---
title: "Worklog Tuần 4"
date: 2026-10-12
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
- Nắm vững kiến trúc, các khái niệm thành phần và cơ chế vận hành của 6 dịch vụ nền tảng trên AWS: **EC2, S3, RDS, VPC, IAM và CloudWatch**.
- Có khả năng đọc hiểu một bản vẽ kiến trúc AWS hoàn chỉnh và giải thích được chức năng của từng khối dịch vụ trong hệ thống.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu **Amazon EC2 (Elastic Compute Cloud)**: <br>&emsp; + Cấu hình phần cứng qua **Instance Type** (dòng `t2.micro`, `t3.small`...) và hệ điều hành qua **AMI** (Amazon Machine Image) <br>&emsp; + Bảo mật kết nối bằng **Key Pair** và tường lửa ảo **Security Group** (Stateful firewall) <br>&emsp; + Lưu trữ bền vững với **EBS** (Elastic Block Store) và sự khác biệt về dữ liệu/chi phí giữa các trạng thái **Stop**, **Start** và **Terminate** | 12/10/2026 | 12/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Nghiên cứu **Amazon S3 (Simple Storage Service)**: <br>&emsp; + Cấu trúc lưu trữ phẳng gồm **Bucket** (tên duy nhất toàn cầu) và **Object** (dữ liệu + metadata + key) <br>&emsp; + Cơ chế phân quyền qua Block Public Access, Bucket Policy và Presigned URL <br>&emsp; + Quản lý vòng đời dữ liệu với **Versioning** (lưu nhiều phiên bản chống xóa nhầm) và **Lifecycle Rules** (tự động chuyển sang lớp lưu trữ rẻ hơn như S3 Glacier hoặc xóa file cũ) | 13/10/2026 | 13/10/2026 | AWS Documentation |
| 4 | - Nghiên cứu **Amazon RDS (Relational Database Service)**: <br>&emsp; + Lợi ích của dịch vụ cơ sở dữ liệu được AWS quản lý (tự động vá lỗi OS, sao lưu định kỳ) với engine **PostgreSQL** <br>&emsp; + Cách thức ứng dụng kết nối qua DNS **Endpoint** và cổng mặc định **Port 5432** <br>&emsp; + Cơ chế **Automated Backups**, Manual Snapshots và tầm quan trọng của việc tắt **Public Access** để cô lập database | 14/10/2026 | 14/10/2026 | AWS Documentation |
| 5 | - Nghiên cứu **Amazon VPC (Virtual Private Cloud)**: <br>&emsp; + Thiết kế dải mạng riêng ảo bằng **CIDR block** (ví dụ `10.0.0.0/16`) <br>&emsp; + Phân chia **Public Subnet** (có route trỏ ra **Internet Gateway - IGW**, dành cho Web Server/Load Balancer) và **Private Subnet** (không mở trực tiếp ra Internet, dành cho Database/Backend nội bộ) <br>&emsp; + Cách cấu hình **Route Table** và phối hợp giữa **Security Group** (cấp độ instance) với NACL (cấp độ subnet) | 15/10/2026 | 15/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - Nghiên cứu **AWS IAM**: phân biệt **Root User** (quyền tối cao, chỉ dùng khi thiết lập ban đầu), **IAM User** (dành cho con người), **IAM Group** (nhóm quyền), **IAM Role** (cấp quyền tạm thời cho dịch vụ AWS như EC2 truy cập S3 mà không cần lưu khóa cứng), **Policy** (tài liệu JSON định nghĩa quyền `Allow`/`Deny`), nguyên tắc **Least Privilege** và bảo mật 2 lớp **MFA** <br> - Nghiên cứu **Amazon CloudWatch**: thu thập **Logs** (nhật ký ứng dụng), theo dõi **Metrics** (chỉ số CPU, RAM, Network) và thiết lập **Alarms** (cảnh báo tự động) | 16/10/2026 | 16/10/2026 | AWS Skill Builder |

### Kết quả đạt được tuần 4:
- Hệ thống hóa đầy đủ kiến thức lý thuyết của 6 dịch vụ xương sống trong hệ sinh thái AWS.
- Hiểu rõ cách kết hợp VPC + Security Group + IAM Role để xây dựng lớp phòng thủ nhiều tầng (Defense in Depth) cho ứng dụng.
- Tự tin đọc hiểu bất kỳ sơ đồ kiến trúc AWS cơ bản nào và chỉ ra được đường đi của dữ liệu cũng như cơ chế bảo mật giữa các thành phần.