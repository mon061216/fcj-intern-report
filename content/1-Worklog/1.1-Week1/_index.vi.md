---
title: "Worklog Tuần 1"
date: 2026-09-21
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:
- Kết nối, làm quen với các thành viên trong nhóm thực tập First Cloud AI Journey (FCAJ) và nắm rõ nội quy, quy trình báo cáo tiến độ.
- Hiểu sâu bản chất giao tiếp mạng trên nền tảng Web: cách Client gửi yêu cầu, cách Backend xử lý logic, giao tiếp với Database và phản hồi dữ liệu thông qua giao thức HTTP/HTTPS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tham gia buổi định hướng (Onboarding) từ ngày 20/09, làm quen với mentor và các thành viên trong team <br> - Đọc kỹ quy định thực tập, cách thức viết worklog trên nền tảng Hugo và quy tắc quản lý source code trên GitHub | 21/09/2026 | 21/09/2026 | Tài liệu nội bộ FCAJ |
| 3 | - Phân tích kiến trúc 3 tầng: Frontend (Presentation), Backend (Business Logic) và Database (Data Storage) <br> - Tìm hiểu cấu trúc chi tiết của một **HTTP Request** (Request Line, Headers, Body) và **HTTP Response** (Status Line, Headers, Body) <br> - Nghiên cứu cấu trúc dữ liệu **JSON** (Key-Value, Array, Nested Object) dùng để trao đổi dữ liệu giữa các dịch vụ | 22/09/2026 | 22/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Nghiên cứu chuẩn thiết kế **RESTful API** và quy tắc đặt tên **Endpoint** theo tài nguyên (Resource-based URL) <br> - Phân biệt rõ ngữ nghĩa và tính chất Idempotent của các HTTP Methods: `GET` (truy vấn), `POST` (tạo mới), `PUT` (cập nhật toàn bộ), `PATCH` (cập nhật một phần), `DELETE` (xóa) <br> - Hệ thống hóa các nhóm **HTTP Status Code**: `2xx` (`200 OK`, `201 Created`, `204 No Content`), `4xx` (`400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`), `5xx` (`500 Internal Server Error`, `502 Bad Gateway`) <br> - Tìm hiểu cơ chế thương lượng nội dung qua cặp header `Content-Type` và `Accept` | 23/09/2026 | 23/09/2026 | MDN Web Docs |
| 5 | - Phân biệt địa chỉ **IP** (định danh thiết bị trên mạng), **Domain Name** (tên miền thân thiện thông qua hệ thống phân giải DNS), **Port** (cổng định danh tiến trình ứng dụng) và dải địa chỉ nội bộ `localhost` (`127.0.0.1`) <br> - So sánh sự khác biệt giữa **HTTP** (truyền văn bản thuần - plaintext, port 80) và **HTTPS** (mã hóa đường truyền bằng chứng chỉ SSL/TLS, port 443) | 24/09/2026 | 24/09/2026 | MDN Web Docs |
| 6 | - Tìm hiểu nguyên lý bảo mật **12-Factor App** về việc tách biệt cấu hình khỏi mã nguồn bằng **Environment Variables** (biến môi trường) <br> - **Thực hành:** Sử dụng Postman và công cụ dòng lệnh `curl` để gửi các request CRUD tới một REST API mẫu, quan sát chi tiết Request/Response Headers, Payload JSON và vẽ sơ đồ luồng đi của dữ liệu từ trình duyệt xuống Database | 25/09/2026 | 25/09/2026 | Thực hành cá nhân |

### Kết quả đạt được tuần 1:
- Hòa nhập tốt với môi trường làm việc tại FCAJ, nắm rõ lộ trình 12 tuần và tiêu chuẩn trình bày tài liệu kỹ thuật.
- Giải thích được tường tận hành trình của một gói tin: từ lúc người dùng bấm nút trên Frontend -> phân giải DNS ra IP -> mở kết nối HTTPS tới Port của Backend -> Backend đọc biến môi trường để kết nối Database -> truy vấn dữ liệu và đóng gói JSON trả về kèm Status Code tương ứng.
- Sử dụng thành thạo Postman và `curl` để kiểm thử API và đọc lỗi dựa trên mã trạng thái HTTP.