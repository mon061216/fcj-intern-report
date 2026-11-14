---
title: "Worklog Tuần 3"
date: 2026-10-05
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
- Nắm vững tư duy chuyển dịch từ hạ tầng vật lý (On-premises) lên điện toán đám mây (Cloud Computing).
- Hiểu rõ kiến trúc hạ tầng toàn cầu của AWS, mô hình chia sẻ trách nhiệm bảo mật, cơ chế quản lý quyền hạn cơ bản và nguyên lý tính phí.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - So sánh chi tiết **On-premises** và **Cloud Computing** trên các khía cạnh: chi phí đầu tư ban đầu (CapEx vs OpEx), thời gian triển khai, khả năng mở rộng và bảo trì phần cứng <br> - Phân loại 4 trụ cột tài nguyên trên Cloud: **Compute** (năng lực tính toán), **Storage** (lưu trữ dữ liệu phi cấu trúc/khối), **Database** (cơ sở dữ liệu có cấu trúc) và **Networking** (hạ tầng kết nối mạng) | 05/10/2026 | 05/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Phân tích ranh giới quản lý giữa 3 mô hình dịch vụ: **IaaS** (Infrastructure as a Service - ví dụ EC2), **PaaS** (Platform as a Service - ví dụ Elastic Beanstalk, RDS) và **SaaS** (Software as a Service) <br> - Tìm hiểu đặc điểm và kịch bản áp dụng của **Public Cloud**, **Private Cloud** và **Hybrid Cloud** | 06/10/2026 | 06/10/2026 | AWS Skill Builder |
| 4 | - Phân biệt các khái niệm thiết kế hệ thống phân tán: <br>&emsp; + **Scalability** (khả năng nâng cấp tài nguyên theo chiều dọc Vertical Scaling hoặc mở rộng số lượng node theo chiều ngang Horizontal Scaling) vs **Elasticity** (khả năng tự động co giãn tài nguyên linh hoạt theo lưu lượng thực tế) <br>&emsp; + **High Availability** (tính sẵn sàng cao, giảm thiểu downtime) vs **Fault Tolerance** (khả năng chịu lỗi, hệ thống vẫn hoạt động liên tục không gián đoạn ngay cả khi có thành phần bị sập) | 07/10/2026 | 07/10/2026 | AWS Documentation |
| 5 | - Nghiên cứu cấu trúc hạ tầng toàn cầu của AWS: **AWS Region** (cụm trung tâm dữ liệu độc lập về địa lý), **Availability Zone - AZ** (mỗi Region gồm nhiều AZ cách biệt vật lý nhưng kết nối qua mạng cáp quang tốc độ cực cao để dự phòng thảm họa) và **Edge Location** (điểm biên phục vụ CloudFront CDN và Route 53 giúp giảm độ trễ cho người dùng cuối) <br> - Phân tích **Shared Responsibility Model**: AWS chịu trách nhiệm bảo mật *của* đám mây (phần cứng, hạ tầng vật lý, lớp ảo hóa), khách hàng chịu trách nhiệm bảo mật *trong* đám mây (dữ liệu, mã nguồn, cấu hình mạng, IAM, hệ điều hành khách) | 08/10/2026 | 08/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - Tìm hiểu tổng quan dịch vụ **AWS IAM** (Identity and Access Management) dùng để kiểm soát xác thực (Authentication) và phân quyền (Authorization) <br> - Nghiên cứu các yếu tố cấu thành chi phí trên AWS: Compute time (giờ/giây chạy), Storage volume (GB/tháng), Data Transfer Out (lưu lượng truyền ra Internet) và chính sách **AWS Free Tier** | 09/10/2026 | 09/10/2026 | AWS Pricing Calculator |

### Kết quả đạt được tuần 3:
- Hình thành tư duy thiết kế kiến trúc Cloud: biết cách triển khai tài nguyên trên nhiều Availability Zone (Multi-AZ) để đạt High Availability.
- Xác định rõ trách nhiệm bảo mật của bản thân khi triển khai ứng dụng trên AWS nhằm tránh các lỗ hổng cấu hình phổ biến.
- Hiểu cách ước tính chi phí cơ bản và nắm được nguyên tắc tối ưu hóa hóa đơn AWS (tắt tài nguyên không dùng, tận dụng Free Tier, hạn chế Data Transfer Out không cần thiết).