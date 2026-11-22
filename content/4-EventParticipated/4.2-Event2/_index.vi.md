---
title: "Sự kiện 2"
date: 2026-09-29
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Báo cáo tóm tắt: “AWS Cloud and AI Day Hanoi 2026 - HCMC Watch Party”

### Mục tiêu sự kiện

- Cập nhật chiến lược ứng dụng Cloud/AI quy mô quốc gia, doanh nghiệp và xu hướng hạ tầng số
- Tìm hiểu kiến trúc nền tảng đằng sau các dịch vụ đám mây tin cậy ("invisible engineering")
- Nắm vững quy trình kiểm chứng chất lượng, giám sát (observability) và bảo mật cho phần mềm có sự hỗ trợ của AI
- Kết nối cùng cộng đồng AWS tại điểm cầu Watch Party TP. Hồ Chí Minh ở tòa nhà Bitexco Financial Tower[cite: 2]

### Diễn giả

- **Hoàng Minh** – Thứ trưởng Bộ Khoa học và Công nghệ
- **Jennifer Wicks** – Đại sứ Hoa Kỳ tại Việt Nam
- **Eric Yeo** – Tổng Giám đốc AWS khu vực Malaysia, Việt Nam và Đông Dương
- **TS. Jens Lottner** – Tổng Giám đốc (CEO), Techcombank
- **TS. Werner Vogels** – Giám đốc Công nghệ (CTO), Amazon.com
- **Mai Le** – Giám đốc Quản lý Sản phẩm, Katalon

### Nội dung nổi bật

#### Hạ tầng số và hệ sinh thái Cloud/AI

- Nhấn mạnh sự phát triển của AI gắn liền với năng lực hạ tầng tính toán, đội ngũ nhân lực kỹ thuật và sự hợp tác giữa doanh nghiệp, cơ quan quản lý và trường đại học.
- Minh họa cách nền tảng đám mây thúc đẩy chuyển đổi số trong nhiều lĩnh vực như phân tích dữ liệu y tế, giám sát bán lẻ và nông nghiệp.

#### Xuất phát từ bài toán của khách hàng

- Nhấn mạnh nguyên tắc xác định rõ bài toán nghiệp vụ, dữ liệu sẵn có và kết quả đo lường được trước khi lựa chọn dịch vụ AWS hay mô hình AI.
- Phân tích các ví dụ triển khai thực tế cho thấy việc khoanh vùng bài toán đúng giúp tránh thiết kế dư thừa.

#### Tích hợp AI vào quy trình vận hành doanh nghiệp

- Chia sẻ kinh nghiệm từ Techcombank về việc đưa AI xuyên suốt quy trình phát triển và vận hành thay vì chỉ dùng như một công cụ độc lập.
- Đề cập đến việc gắn kết yêu cầu phần mềm với phát triển và kiểm thử, hỗ trợ xử lý sự cố, quản trị quyền truy cập và đào tạo đội ngũ.

#### Kỹ thuật vận hành ẩn (Invisible Engineering) và hệ thống phân tán

- **TS. Werner Vogels** phân tích các quyết định kỹ thuật nền tảng phía sau dịch vụ đám mây: thấu hiểu mẫu truy cập dữ liệu và cân bằng giữa hiệu năng, tính cô lập (isolation) và độ tin cậy.
- Giới thiệu **AWS Nitro System**, **AWS Lambda** và **Firecracker** như các lớp hạ tầng ẩn giúp vận hành Serverless an toàn, cùng **Amazon Time Sync Service** và **ClockBound** để xử lý đồng bộ thời gian trong hệ thống phân tán.

#### Kiểm chứng phần mềm AI và quản lý "Nợ kiểm chứng" (Validation Debt)

- Diễn giả **Mai Le** (Katalon) chỉ ra khái niệm **validation debt** — khối lượng kiểm chứng bị dồn ứ khi AI tạo mã nguồn nhanh hơn tốc độ kiểm thử của đội ngũ.
- Nhấn mạnh sự cần thiết của việc liên kết chặt chẽ từ yêu cầu, thay đổi mã nguồn, ca kiểm thử tự động đến dữ liệu giám sát thực tế (telemetry) để đưa ra quyết định phát hành dựa trên bằng chứng.

#### Bảo mật ứng dụng chủ động và hàng rào kiểm soát (Guardrails)

- Giới thiệu hướng tiếp cận bảo mật chủ động xuyên suốt vòng đời phát triển phần mềm (như AWS Security Agent) nhằm thu hẹp khoảng cách giữa tốc độ lập trình và kiểm thử an toàn thông tin.
- Củng cố tầm quan trọng của các lớp kiểm soát (guardrails), phân quyền chặt chẽ và giám sát liên tục trong hệ thống doanh nghiệp.

### Bài học cốt lõi

#### Tư duy kiến trúc và thiết kế

- **Lấy bài toán làm trung tâm**: Xác định rõ người dùng mục tiêu, dữ liệu và chỉ số thành công trước khi chọn dịch vụ hay mô hình AI.
- **Nền tảng kỹ thuật vững chắc**: Đánh giá đồng thời hiệu năng, tính cô lập, độ tin cậy và mô hình truy cập dữ liệu khi thiết kế hệ thống.

#### Chất lượng kỹ thuật và kiểm chứng

- **Kiểm soát nợ kiểm chứng**: Kết hợp tốc độ phát triển với kiểm thử tự động có thể truy vết, log có cấu trúc và dữ liệu đo lường thực nghiệm[cite: 2].
- **Truy vết đầu cuối**: Gắn kết trực tiếp yêu cầu nghiệp vụ với bằng chứng kiểm thử trước khi đưa tính năng lên môi trường vận hành.

#### Quản trị và trách nhiệm con người

- **Bảo mật ngay từ thiết kế**: Tích hợp quản trị quyền truy cập tối thiểu và bộ lọc an toàn ngay trong luồng xử lý AI[cite: 2].
- **Trách nhiệm giám sát của con người**: Luôn duy trì vai trò đánh giá rủi ro và phê duyệt của con người khi ứng dụng AI vào thực tế[cite: 2].

### Áp dụng vào công việc

- **Áp dụng IAM Least Privilege & Guardrails cho dự án Ask First**: Tách biệt IAM Role cho từng hàm Lambda (`webhook`, `worker`, `ai`), kết hợp ẩn danh thông tin cá nhân cục bộ (Mask PII) với Amazon Bedrock Guardrails và vô hiệu hóa (defang) các đường dẫn nghi ngờ[cite: 1].
- **Ngăn ngừa validation debt bằng kiểm thử tự động**: Xây dựng bộ dữ liệu đánh giá chuẩn và kiểm thử hợp đồng (`AiContractTest`) trong CI/CD để đo lường độ phủ phát hiện lừa đảo, tỷ lệ báo nhầm và tính đúng đắn của JSON Schema[cite: 1].
- **Tăng cường giám sát hệ thống (Observability)**: Thiết lập log có cấu trúc và cảnh báo CloudWatch để theo dõi độ trễ đầu cuối, giới hạn gọi Bedrock và cơ chế dự phòng[cite: 1].
- **Duy trì yếu tố con người trong vòng lặp (Human-in-the-loop)**: Thiết kế cơ chế liên kết đồng thuận hai chiều (double opt-in) để người thân nhận cảnh báo kịp thời và chủ động gọi điện xác minh cho người cao tuổi[cite: 1].

### Trải nghiệm tại sự kiện

Tham dự chương trình **“AWS Cloud and AI Day Hanoi 2026 - HCMC Watch Party”** vào ngày 29/09/2026 tại tầng 26 tòa nhà Bitexco Financial Tower mang lại cho tôi góc nhìn toàn diện về cách xây dựng và vận hành hệ thống Cloud/AI an toàn, có kiểm chứng[cite: 2]. Những trải nghiệm nổi bật bao gồm:

#### Học hỏi từ các diễn giả hàng đầu
- Tiếp thu những chia sẻ sâu sắc từ **TS. Werner Vogels** về cách các công nghệ nền tảng như Nitro, Firecracker và ClockBound đảm bảo tính cô lập và độ tin cậy ở quy mô lớn.
- Học hỏi kinh nghiệm thực tiễn từ **TS. Jens Lottner** và **Mai Le** về quản trị AI trong doanh nghiệp và cách giải quyết bài toán validation debt.

#### Tiếp cận góc nhìn kiến trúc và kỹ thuật
- Hiểu rõ hơn các đánh đổi kỹ thuật xoay quanh môi trường thực thi Serverless, đồng bộ thời gian phân tán và bảo mật chủ động (Proactive AppSec).
- Nắm vững cách kết hợp test tự động, log và telemetry làm bằng chứng đánh giá các thành phần AI[cite: 2].

#### Khai thác công cụ hiện đại
- Tìm hiểu cách các công cụ AI hỗ trợ phát triển phần mềm và kiểm tra bảo mật tự động giúp tăng năng suất khi đi kèm quy trình kiểm soát chặt chẽ.

#### Giao lưu và thảo luận
- Trao đổi trực tiếp cùng các bạn thực tập sinh First Cloud AI Journey tại điểm cầu TP. Hồ Chí Minh về nội dung các phiên keynote và hướng áp dụng vào dự án nhóm[cite: 2].

#### Bài học rút ra
- Tốc độ phát triển nhanh nhưng thiếu kiểm chứng sẽ tạo ra nợ kỹ thuật; kiểm thử, log và metrics phải là bằng chứng bắt buộc trước khi phát hành[cite: 2].
- Hệ thống AI đáng tin cậy đòi hỏi quản trị quyền truy cập chặt chẽ, bảo vệ dữ liệu riêng tư và trách nhiệm giám sát rõ ràng của con người[cite: 2].

#### Một số hình ảnh tại sự kiện
- ![Không gian Watch Party tại Bitexco](/images/4-Events/event2-venue.jpg)
  *Không gian sự kiện AWS Cloud and AI Day Watch Party tại tầng 26, tòa nhà Bitexco Financial Tower.*
- ![Thẻ tham dự và khu vực giao lưu](/images/4-Events/event2-badge.jpg)
  *Thẻ tham dự sự kiện và khu vực giao lưu kết nối.*
- ![Phiên phát biểu chính của Eric Yeo và TS. Werner Vogels](/images/4-Events/event2-keynote.jpg)
  *Theo dõi phiên phát biểu chính được truyền hình trực tiếp từ Hà Nội.*
- ![Phiên chia sẻ về bảo mật chủ động và kiểm chứng phần mềm](/images/4-Events/event2-appsec.jpg)
  *Nội dung chia sẻ về bảo mật chủ động và hàng rào kiểm soát doanh nghiệp.*

> Nhìn chung, sự kiện đã kết nối chiến lược ứng dụng Cloud/AI với các nguyên lý kỹ thuật hệ thống cốt lõi, định hướng trực tiếp cho cách tôi thiết kế bảo mật, kiểm thử và giám sát trong phần việc Backend của mình.