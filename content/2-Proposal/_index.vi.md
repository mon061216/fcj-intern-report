---
title: "Bản đề xuất"
date: 2026-10-19
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Ask First — Trợ lý "Hỏi Trước Khi Chuyển"
## Giải pháp AWS Serverless kết hợp AI lai (Hybrid Local-First) phòng chống lừa đảo trực tuyến cho người cao tuổi

### 1. Tóm tắt điều hành
**Ask First ("Hỏi Trước")** được thiết kế bởi nhóm sinh viên thực tập *Null Name* tại TP. Hồ Chí Minh nhằm bảo vệ người cao tuổi và gia đình trước các chiêu trò lừa đảo trực tuyến ngày càng tinh vi[cite: 1]. Nền tảng hoạt động trực tiếp trên ứng dụng nhắn tin quen thuộc (**Telegram**, thiết kế mở rộng sang **Zalo Bot Platform**)[cite: 1], đóng vai trò như một **"người thứ ba" số hóa** xen vào thời điểm vàng trước khi nạn nhân thực hiện chuyển khoản hoặc cung cấp mã OTP[cite: 1]. 

Hệ thống áp dụng kiến trúc **AWS Serverless** hướng sự kiện tại vùng `ap-southeast-1` (Singapore) kết hợp mô hình suy luận ngôn ngữ mở trên **Amazon Bedrock** tại `ap-southeast-2` (Sydney)[cite: 1]. Áp dụng chiến lược **Hybrid Local-First**, các tác vụ trích xuất văn bản từ ảnh (OCR), tính toán vector nhúng (Embedding), ẩn danh thông tin cá nhân (Mask PII) và kiểm tra luật cứng đều chạy trực tiếp trên CPU bên trong AWS Lambda, đảm bảo hình ảnh gốc không rời khỏi hệ thống và tối ưu hóa chi phí vận hành xuống mức chỉ khoảng **3,00 – 6,50 USD/tháng** cho quy mô 3.000 lượt kiểm tra[cite: 1].

---

### 2. Tuyên bố vấn đề

*Vấn đề hiện tại*
Theo thống kê của Bộ Công an, thiệt hại do lừa đảo trực tuyến tại Việt Nam năm 2025 ước tính vượt mức **8.000 tỷ đồng**, nhưng chỉ khoảng **32,12%** nạn nhân thực hiện trình báo (theo khảo sát của Hiệp hội An ninh mạng Quốc gia - NCA)[cite: 1]. Thủ đoạn phổ biến nhất là mạo danh cơ quan công an, viện kiểm sát hoặc giả mạo cổng dịch vụ công, nhắm mạnh vào **người cao tuổi**[cite: 1]. Điểm chung của các vụ việc là kẻ gian dùng áp lực tâm lý để **cô lập nạn nhân** (*"không được trao đổi với bất kỳ ai"*)[cite: 1]. Trong khi các hệ thống như SIMO của Ngân hàng Nhà nước hay tính năng cảnh báo trên Android đã hỗ trợ chặn ở tầng hạ tầng tài khoản và cuộc gọi, vẫn còn một khoảng trống lớn ở **tầng nội dung hội thoại** và **sự kết nối với người thân** ngay tại nhà trước khi tiền rời khỏi tài khoản[cite: 1].

*Giải pháp*
Ask First cung cấp một trợ lý ảo ngay trong khung chat để người cao tuổi có thể chuyển tiếp tin nhắn, dán đường dẫn (link) hoặc gửi ảnh chụp màn hình đáng ngờ[cite: 1]. Hệ thống sử dụng **AWS Lambda** (Java 21 và Python 3.12) kết hợp **Amazon SQS** để xử lý bất đồng bộ, **Amazon DynamoDB** để quản lý trạng thái và bộ nhớ đệm, cùng **Amazon Bedrock** (Qwen3 32B & Guardrails) để phân tích ngữ cảnh và giải thích dấu hiệu lừa đảo bằng ngôn ngữ dễ hiểu[cite: 1]. Nếu phát hiện mức độ *Nguy hiểm* kèm hành động rủi ro (chuyển tiền, đọc OTP, cài tệp `.apk`), hệ thống tự động gửi cảnh báo đồng thời tới người thân đã được liên kết qua cơ chế đồng thuận hai chiều (double opt-in)[cite: 1].

*Lợi ích và hoàn vốn đầu tư (ROI)*
Giải pháp giúp phá vỡ sự cô lập tâm lý của nạn nhân nhờ sự can thiệp kịp thời của con cháu[cite: 1], đồng thời tuân thủ nghiêm ngặt **Luật Bảo vệ dữ liệu cá nhân (91/2025/QH15)** và **Nghị định 356/2025/NĐ-CP** thông qua cơ chế đồng ý tách bạch theo mục đích, ẩn danh dữ liệu nhạy cảm cục bộ và tự động xóa dữ liệu theo vòng đời (TTL)[cite: 1]. Về mặt tài chính, dự án tận dụng hoàn toàn thiết bị di động sẵn có của người dùng mà không tốn chi phí đầu tư phần cứng hay thuê máy chủ GPU đắt đỏ[cite: 1]. Với chi phí hạ tầng AWS ước tính chỉ **3,00 – 6,50 USD/tháng** (khoảng **36 – 78 USD/năm**)[cite: 1], giải pháp mang lại hiệu quả xã hội và kinh tế vượt trội ngay từ tháng đầu tiên vận hành nhờ ngăn chặn được các rủi ro thiệt hại tài chính lên tới hàng chục hoặc hàng trăm triệu đồng cho mỗi hộ gia đình[cite: 1].

---

### 3. Kiến trúc giải pháp

Nền tảng áp dụng kiến trúc Serverless tách biệt hai luồng xử lý: luồng phản hồi nhanh (webhook xác thực, chống trùng lặp, quản lý người dùng) và luồng xử lý AI bất đồng bộ thông qua hàng đợi[cite: 1]. Mọi tương tác giao diện diễn ra trực tiếp trong khung chat Telegram thông qua các nút bấm trực quan, giúp người cao tuổi sử dụng dễ dàng mà không cần cài đặt thêm ứng dụng mới[cite: 1].

![Ask First System Architecture](/images/2-Proposal/system_architecture.png)

*Dịch vụ AWS sử dụng*
- **AWS Lambda (3 Functions)**: 
  - `webhook` (Java 21 + SnapStart): Tiếp nhận sự kiện từ Telegram qua Function URL, xác thực token, chống trùng lặp và điều phối lệnh nhanh[cite: 1].
  - `worker` (Java 21 + SnapStart): Điều phối luồng kiểm tra tin, gom cụm tin nhắn liên tiếp (debounce), gửi cảnh báo người thân và đẩy chỉ số vận hành[cite: 1].
  - `ai` (Python 3.12 Container Image): Thực thi toàn bộ pipeline AI (OCR cục bộ, ẩn danh PII, kiểm tra luật, truy xuất RAG, gọi LLM và tạo câu trả lời)[cite: 1].
- **Amazon SQS (+ Dead-Letter Queue)**: Hàng đợi trung gian giúp webhook phản hồi dưới 1 giây, điều tiết lưu lượng gọi AI, hỗ trợ trì hoãn 3 giây để gom tin nhắn và 900 giây (15 phút) để nhắc lại cảnh báo[cite: 1].
- **Amazon DynamoDB**: Bảng đơn (Single-table design) lưu hồ sơ người dùng, bằng chứng đồng ý, liên kết người thân, kết quả kiểm tra (chỉ metadata), bộ nhớ đệm kết quả và tự động xóa dữ liệu bằng TTL[cite: 1].
- **Amazon Bedrock & Guardrails (tại `ap-southeast-2`)**: Cung cấp mô hình suy luận ngôn ngữ mở **Qwen3 32B** (kèm dự phòng **gpt-oss-120b**) để phân loại kịch bản và **Bedrock Guardrails** để phát hiện tấn công chèn lệnh (prompt injection) tiếng Việt[cite: 1].
- **Amazon S3 & ECR**: S3 lưu trữ trọng số mô hình AI cục bộ (ONNX), kho tri thức cảnh báo chính thức (RAG index) và bộ dữ liệu đánh giá; ECR lưu trữ container image của hàm `ai`[cite: 1].
- **Dịch vụ vận hành & bảo mật**: AWS SSM Parameter Store (lưu trữ khóa bí mật), Amazon CloudWatch (log và dashboard), Amazon SNS (nhận cảnh báo sự cố qua email) và AWS Budgets[cite: 1].

*Thiết kế thành phần*
- **Lớp tiếp nhận & gom tin (Channel Adapter & Debounce)**: Tách biệt giao thức Telegram để sẵn sàng mở rộng sang Zalo Bot; tự động gom các tin nhắn hoặc album ảnh gửi liên tiếp trong 3 giây thành một phiên phân tích duy nhất[cite: 1].
- **Tiền xử lý & Ẩn danh cục bộ (Local Extract & Masking)**: Sử dụng mô hình OCR chạy trên CPU của Lambda để đọc chữ từ ảnh chụp màn hình, sau đó che toàn bộ số điện thoại, số tài khoản, CCCD và mã OTP trước khi gửi văn bản ra ngoài[cite: 1].
- **Hệ thống phân tích lai (Hybrid AI Pipeline)**: Kết hợp tầng luật cứng (nhận diện từ khóa đòi OTP, cài tệp `.apk`, kiểm tra tên miền giả mạo/typosquatting), truy xuất ngữ cảnh từ kho cảnh báo công an (RAG cục bộ bằng mô hình nhúng e5-small) và suy luận của LLM để đưa ra kết luận 4 mức độ rõ ràng[cite: 1].
- **Cơ chế bảo vệ gia đình (Double Opt-in Guardian Alert)**: Liên kết người thân qua mã mời dùng một lần; tự động gửi cảnh báo song song kèm mức độ chia sẻ tùy chọn (Mức 1–3) và xác nhận đã liên hệ (ACK)[cite: 1].

---

### 4. Triển khai kỹ thuật

*Các giai đoạn triển khai (Lộ trình 6 tuần Bootcamp)*
Dự án được chia thành 4 giai đoạn kỹ thuật bám sát nguyên tắc *Contract-First* và tích hợp theo lát cắt dọc[cite: 1]:
1. **Giai đoạn P0 — Khởi tạo & Thử nghiệm giảm rủi ro (Tuần 1–2)**: Thiết lập tài khoản AWS, cấu trúc monorepo, chốt hợp đồng dữ liệu JSON Schema giữa Java và Python, đo hiệu năng gọi Bedrock (Qwen3 32B) và đánh giá độ chính xác của mô hình OCR tiếng Việt cục bộ[cite: 1].
2. **Giai đoạn P1 — Luồng kiểm tra văn bản & liên kết (Tuần 2–3)**: Hoàn thiện pipeline nhận diện văn bản, kiểm tra tên miền giả mạo (`U_TEXT_LINK_MISMATCH`, typosquatting), tích hợp luật cứng, LLM Judge và cơ chế đồng ý tách bạch theo mục đích[cite: 1].
3. **Giai đoạn P2 — Nhận diện ảnh & Cảnh báo người thân (Tuần 3–4)**: Đóng gói mô hình OCR vào container image Lambda `ai`, triển khai bộ nhớ đệm theo mã băm nội dung và hoàn thiện luồng liên kết, cảnh báo song song tới người thân[cite: 1].
4. **Giai đoạn P3 & P4 — Tích hợp RAG, Đánh giá & Cứng hóa (Tuần 5–6)**: Tích hợp kho tri thức 100 cảnh báo chính thức, hiệu chỉnh ngưỡng phân loại trên bộ 300 mẫu kiểm thử tự động trong CI/CD, thiết lập kill-switch, giám sát CloudWatch và kiểm thử nội bộ[cite: 1].

*Yêu cầu kỹ thuật*
- **Backend & Hạ tầng**: Java 21 (Maven, AWS SDK v2, Powertools for AWS Lambda) tối ưu hóa khởi động lạnh bằng SnapStart; triển khai 100% bằng Infrastructure as Code với **AWS SAM** và tự động hóa qua GitHub Actions (OIDC)[cite: 1].
- **AI & Dữ liệu**: Python 3.12, Pydantic v2, ONNX Runtime (chạy OCR và embedding trên CPU mà không cần GPU), Amazon Bedrock Converse API[cite: 1]. Hệ thống đạt mục tiêu độ trễ **p95 ≤ 15 giây** cho văn bản/ảnh, tỷ lệ phát hiện lừa đảo (**Recall ≥ 90%**) và tỷ lệ báo nhầm trên tin nhắn hợp lệ nhạy cảm (**≤ 10%**)[cite: 1].

---

### 5. Lộ trình & Mốc triển khai
- **Tuần 1 (19/10 – 25/10/2026)**: Chốt kiến trúc, hợp đồng dữ liệu BE–AI (Gate G0), thiết lập hạ tầng cơ bản và kích hoạt quyền truy cập Bedrock[cite: 1].
- **Tuần 2 (26/10 – 01/11/2026)**: Chốt mô hình LLM (Gate G1) và giải pháp OCR cục bộ (Gate G2); hoàn thiện khung xử lý webhook và hàng đợi SQS[cite: 1].
- **Tuần 3 (02/11 – 08/11/2026)**: Hoàn thành luồng kiểm tra văn bản và đường dẫn giả mạo đầu cuối (Mốc M1: Text E2E) cùng quy trình đăng ký đồng ý[cite: 1].
- **Tuần 4 (09/11 – 15/11/2026)**: Tích hợp nhận diện ảnh chụp màn hình và tính năng cảnh báo người thân tự động (Mốc M2)[cite: 1].
- **Tuần 5 (16/11 – 22/11/2026)**: Tích hợp RAG trích dẫn nguồn chính thức (Mốc M3), hiệu chỉnh ngưỡng trên 300 mẫu kiểm thử và đóng băng tính năng (Mốc M4: MVP Freeze)[cite: 1].
- **Tuần 6 (23/11 – 29/11/2026)**: Kiểm thử nội bộ cùng các thành viên gia đình (Mốc M5), hoàn thiện hệ thống cảnh báo vận hành, tài liệu và thuyết trình tổng kết (Mốc M6)[cite: 1].

---

### 6. Ước tính ngân sách

Giả định mức tải vận hành thử nghiệm là **3.000 lượt kiểm tra/tháng** (60% văn bản, 30% ảnh chụp màn hình, 10% tin thoại dự phòng; 25% lượt đi qua nhánh luật nhanh hoặc trúng bộ nhớ đệm mà không cần gọi LLM)[cite: 1]:

*Chi phí hạ tầng AWS (Ước tính)*
- **Amazon Bedrock (Qwen3 32B tại `ap-southeast-2`)**: ~1,30 USD/tháng (2.250 lượt gọi chính, ~2.500 token đầu vào và 300 token đầu ra mỗi lượt)[cite: 1].
- **Amazon Bedrock (gpt-oss-120b dự phòng/leo thang)**: ~0,15 USD/tháng (ước tính 10% số lượt cần phân tích sâu)[cite: 1].
- **Amazon Bedrock Guardrails**: ~0,50 USD/tháng (bộ lọc chống tấn công chèn lệnh tiếng Việt)[cite: 1].
- **Xử lý AI cục bộ (OCR & Embedding trên Lambda CPU)**: 0,00 USD phí token; chi phí tính toán Lambda (`webhook`, `worker`, `ai`) ước tính **0,00 – 1,30 USD/tháng** (nằm trong hạn mức miễn phí 400.000 GB-giây/tháng của AWS Free Tier)[cite: 1].
- **Amazon SQS, DynamoDB, CloudWatch Logs (TTL/Retention 7–30 ngày)**: 0,50 – 2,00 USD/tháng[cite: 1].
- **Amazon S3 & Amazon ECR**: ~0,20 USD/tháng (lưu trữ container image ~1,5 GB và trọng số mô hình ~0,5 GB)[cite: 1].

*Tổng chi phí vận hành*: **~3,00 – 6,50 USD/tháng** (tương đương **36,00 – 78,00 USD/12 tháng**)[cite: 1].  
*Chi phí phần cứng*: **0,00 USD** (tận dụng điện thoại thông minh và ứng dụng nhắn tin sẵn có của người dùng)[cite: 1].

---

### 7. Đánh giá rủi ro

*Ma trận rủi ro*
- **Mô hình LLM suy luận chậm, gặp lỗi định dạng JSON hoặc bị giới hạn hạn mức (throttling)**: Ảnh hưởng cao, xác suất trung bình[cite: 1].
- **Kẻ gian chèn lệnh độc hại (Prompt Injection) vào tin nhắn/ảnh để đánh lừa AI**: Ảnh hưởng cao, xác suất trung bình[cite: 1].
- **Phát sinh chi phí đột biến do spam hoặc tấn công từ chối dịch vụ**: Ảnh hưởng trung bình, xác suất thấp[cite: 1].
- **Người thân chặn bot hoặc không nhận được tin cảnh báo khẩn cấp**: Ảnh hưởng cao, xác suất thấp[cite: 1].

*Chiến lược giảm thiểu*
- **Hiệu năng & Độ tin cậy AI**: Áp dụng cơ chế phân tầng (Cascade) từ luật cứng sang Qwen3 32B và mô hình dự phòng gpt-oss-120b; kiểm tra cấu trúc đầu ra bằng Pydantic; làm nóng hàm Lambda trước các phiên trình diễn[cite: 1].
- **An toàn & Bảo mật**: Chạy tầng luật cứng độc lập với điểm số tối đa (`max(luật, LLM)`), kích hoạt Bedrock Guardrails, làm vô hiệu hóa (defang) mọi đường dẫn nghi ngờ (`hxxps://...[.]...`) và ẩn danh dữ liệu cá nhân cục bộ[cite: 1].
- **Kiểm soát chi phí**: Giới hạn tần suất sử dụng theo từng người dùng (30 lượt/giờ, 100 lượt/ngày), giới hạn đồng thời SQS ở mức 5, thiết lập cảnh báo ngân sách AWS Budgets (10/25/50 USD) và công tắc ngắt nhanh (**Kill Switch**) tắt LLM không cần triển khai lại[cite: 1].

*Kế hoạch dự phòng*
- Khi dịch vụ Bedrock gặp sự cố hoặc kích hoạt Kill Switch, hệ thống tự động chuyển sang **chế độ suy giảm (Rules-Only)** để tiếp tục cảnh báo dựa trên bộ luật cứng và hướng dẫn người dùng gọi điện xác minh trực tiếp với người thân hoặc đường dây nóng chính thức[cite: 1].
- Nếu việc gửi cảnh báo qua Telegram tới người thân thất bại (do bị chặn), bot thông báo trung thực trạng thái cho người cao tuổi và cung cấp danh thiếp (`sendContact`) để gọi điện thoại trực tiếp[cite: 1].

---

### 8. Kết quả kỳ vọng

*Cải tiến kỹ thuật*
Xây dựng thành công một trợ lý phòng chống lừa đảo thời gian thực hoạt động mượt mà trên nền tảng nhắn tin phổ biến, đạt tốc độ phản hồi dưới 15 giây cho văn bản/ảnh chụp màn hình và độ chính xác nhận diện lừa đảo trên 90%[cite: 1]. Kiến trúc Serverless kết hợp AI cục bộ chứng minh khả năng xử lý đa phương thức an toàn, bảo mật dữ liệu nhạy cảm ngay tại biên tính toán với chi phí vận hành dưới 0,005 USD mỗi lượt kiểm tra[cite: 1].

*Giá trị dài hạn*
Tạo ra một giải pháp bảo vệ kỹ thuật số thiết thực, dễ tiếp cận cho người cao tuổi Việt Nam mà không tạo rào cản công nghệ[cite: 1]. Nhờ thiết kế mô-đun hóa với lớp **Channel Adapter** và cấu trúc tách biệt miền tri thức, nền tảng có thể dễ dàng tích hợp lên **Zalo Bot Platform** và mở rộng sang **Giai đoạn 2 (Kho tri thức sống)** — tự động thu thập, tổng hợp các thủ đoạn lừa đảo mới từ cổng thông tin của Bộ Công an để cảnh báo sớm cho cộng đồng[cite: 1].