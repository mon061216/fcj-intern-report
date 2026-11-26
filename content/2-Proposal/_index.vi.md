---
title: "Bản đề xuất"
date: 2026-11-25
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Ask First ("Hỏi Trước") — Trợ lý "Hỏi Trước Khi Chuyển"
## Giải pháp AWS Serverless kết hợp AI lai (Hybrid Local-First) giúp người cao tuổi phòng chống lừa đảo trực tuyến

### 1. Tóm tắt điều hành & Tổng quan

**Ask First ("Hỏi Trước")** được nghiên cứu và phát triển bởi nhóm sinh viên thực tập **Null Name** tại TP. Hồ Chí Minh trong khuôn khổ chương trình đào tạo *Workforce Bootcamp – First Cloud AI Journey (FCAJ) 2026*. Dự án hướng tới mục tiêu giải quyết vấn đề nhức nhối trong xã hội: bảo vệ người cao tuổi và các gia đình Việt Nam trước làn sóng lừa đảo trực tuyến ngày càng tinh vi và nguy hiểm.

Nền tảng hoạt động trực tiếp trên ứng dụng nhắn tin quen thuộc (**Telegram Bot**, thiết kế kiến trúc sẵn sàng mở rộng sang **Zalo Bot Platform**), đóng vai trò như một **"người thứ ba" số hóa** can thiệp kịp thời vào "thời điểm vàng" trước khi nạn nhân thực hiện chuyển khoản hoặc cung cấp mã OTP cho kẻ xấu. Khi nhận được tin nhắn, đường dẫn (link) hay ảnh chụp màn hình đáng ngờ, người cao tuổi chỉ cần chuyển tiếp trực tiếp vào khung chat. Trợ lý sẽ phân tích và phản hồi bằng ngôn ngữ tiếng Việt giản dị, rõ ràng:

- Phân loại rõ ràng vào một trong **4 mức rủi ro**: `DANGEROUS` (Nguy hiểm), `SUSPICIOUS` (Đáng ngờ), `UNSURE` (Chưa chắc chắn), `LOW_RISK` (Rủi ro thấp) — **cố ý không thiết lập mức "AN TOÀN"** nhằm triệt tiêu tâm lý chủ quan của người dùng.
- Chỉ rõ kịch bản lừa đảo nhận diện, các dấu hiệu trích xuất trực tiếp từ tin nhắn, danh sách hành động cần làm ngay và cung cấp đường dây nóng (hotline) chính thức đã được xác thực (thông qua RAG).
- **Cảnh báo tự động tới người thân** (thông qua cơ chế liên kết đồng thuận hai chiều - *double opt-in*) khi phát hiện tin nhắn có mức độ rủi ro cao hoặc kèm hành vi nguy hại.

Toàn bộ hệ thống được xây dựng 100% trên nền tảng **AWS Serverless**: các hàm AWS Lambda (Java 21) đảm nhiệm việc tiếp nhận Webhook từ Telegram và điều phối nghiệp vụ; một hàm AWS Lambda chuyên biệt (Python 3.12, Container Image) thực thi toàn bộ pipeline AI cục bộ (OCR, che thông tin cá nhân PII, kiểm tra luật cứng, tìm kiếm RAG nội bộ); và chỉ duy nhất bước đánh giá phân loại (*LLM Judge*) cuối cùng mới gọi tới mô hình ngôn ngữ mở trên **Amazon Bedrock** với **văn bản đã được ẩn danh tuyệt đối**.

| Tiêu chí | Thông số chi tiết |
|---|---|
| **Đội ngũ phát triển** | Nhóm sinh viên thực tập **Null Name** (4 thành viên: 2 Backend Java 21, 2 AI Python 3.12) |
| **Thời gian thực hiện** | 6 tuần (19/10/2026 – 29/11/2026), thuộc khuôn khổ Bootcamp FCAJ |
| **Khu vực triển khai (Region)** | Hạ tầng tính toán tại `ap-southeast-1` (Singapore); Amazon Bedrock tại `ap-southeast-2` (Sydney) |
| **Kênh tương tác** | Telegram Bot API (Webhook thông qua AWS Lambda Function URL) |
| **Chi phí vận hành ước tính** | ≈ 6,16 USD/tháng cho 3.000 lượt kiểm tra (không tính Free Tier); ≈ 2,40 USD/tháng nếu tận dụng mức Always-Free Tier của AWS |

---

### 2. Tuyên bố vấn đề & Đối tượng người dùng

#### Thực trạng lừa đảo trực tuyến tại Việt Nam
Tội phạm lừa đảo trên không gian mạng tại Việt Nam đang diễn biến phức tạp với quy mô thiệt hại tài chính đặc biệt nghiêm trọng:
- Theo thống kê của Bộ Công an, tổng thiệt hại do lừa đảo trực tuyến trong năm 2025 ước tính vượt mức **8.000 tỷ đồng** ([VOV](https://vov.vn/phap-luat/thiet-hai-tu-lua-dao-truc-tuyen-len-toi-8000-ty-dong-trong-nam-2025-post1286479.vov)).
- Báo cáo khảo sát năm 2025 của Hiệp hội An ninh mạng Quốc gia (NCA) chỉ ra rằng thủ đoạn mạo danh cơ quan công an, viện kiểm sát hoặc cổng dịch vụ công là hình thức phổ biến nhất, và chỉ có **32,12%** nạn nhân thực hiện trình báo cơ quan chức năng ([Báo Hải Phòng](https://baohaiphong.vn/cac-hinh-thuc-lua-dao-truc-tuyen-nao-pho-bien-nhat-nam-2025-532711.html), [Công Lý](https://doanhnhan.congly.vn/lua-dao-truc-tuyen-nam-2025-gay-thiet-hai-tren-6-000-ty-dong.html)).
- Điển hình tại các địa phương như Thái Nguyên, cơ quan công an ghi nhận nạn nhân của các vụ mạo danh lực lượng chức năng *"chủ yếu là người cao tuổi, người hưu trí và người dân sinh sống tại khu vực nông thôn, vùng sâu vùng xa"* do hạn chế về khả năng cập nhật thông tin và công nghệ ([Bộ Công an](https://www.bocongan.gov.vn/bai-viet/kip-thoi-ngan-chan-vu-viec-gia-danh-luc-luong-cong-an-lua-dao-chiem-doat-tai-san-1782987242)).

#### Khoảng trống giải pháp (The Gap)
Hiện nay, các ngân hàng và nhà mạng viễn thông đã triển khai nhiều giải pháp kỹ thuật như cảnh báo sinh trắc học (SIMO) hay chặn cuộc gọi rác. Tuy nhiên, đòn thao túng tâm lý mang tính quyết định luôn xảy ra **rất sớm trong các cuộc trò chuyện riêng tư**, nơi kẻ gian gây áp lực để **cô lập nạn nhân** (*"đây là chuyên án bí mật, tuyệt đối không được tiết lộ cho gia đình, bạn bè"*). 

Trong thực tế, hầu hết các vụ lừa đảo được ngăn chặn thành công đều nhờ sự xuất hiện kịp thời của **"người thứ ba"** (giao dịch viên ngân hàng cảnh giác, nhân viên bưu điện hoặc công an xã khuyên can). Dẫu vậy, con cháu không thể ở bên cạnh cha mẹ 24/7, và người cao tuổi cũng chưa có trong tay một công cụ thuận tiện để **chuyển tiếp ảnh chụp hoặc đường dẫn và nhận ngay lời giải thích cặn kẽ, dễ hiểu**.

#### Đối tượng người dùng mục tiêu (User Personas)

| Nhóm người dùng | Nhu cầu & Hành vi cốt lõi |
|---|---|
| **Người cao tuổi (Chính)** | Chỉ cần chuyển tiếp tin nhắn, gửi ảnh chụp màn hình hoặc dán link đáng ngờ; nhận phản hồi ngắn gọn, dễ hiểu trong vài giây mà không cần cài đặt thêm ứng dụng lạ hay thao tác phức tạp. |
| **Người thân / Con cháu (Phụ)** | Nhận thông báo tự động ngay khi người cao tuổi nhận phải tin nhắn rủi ro cao; có sẵn nút bấm xác nhận *"Tôi đã liên hệ"* để phối hợp can thiệp kịp thời. |

#### Lợi ích xã hội & Hoàn vốn đầu tư (ROI)
- **Về mặt xã hội**: Phá vỡ thế cô lập tâm lý của kẻ gian, tạo sợi dây liên kết bảo vệ gia đình chủ động. Thiết kế tuân thủ chặt chẽ **Luật Bảo vệ dữ liệu cá nhân (91/2025/QH15)** và **Nghị định 356/2025/NĐ-CP** thông qua nguyên tắc đồng ý tách bạch theo mục đích, ẩn danh cục bộ và vòng đời dữ liệu tự động (TTL).
- **Về mặt kinh tế**: Dự án tận dụng hoàn toàn hạ tầng nhắn tin và thiết bị sẵn có của người dân (chi phí phần cứng **0 USD**). Với ngân sách hạ tầng AWS chỉ khoảng **3,00 – 6,50 USD/tháng** (tương đương **36 – 78 USD/năm**), hệ thống mang lại tỷ suất hoàn vốn xã hội vô cùng to lớn khi giúp ngăn chặn các vụ lừa đảo có thể cướp đi tài sản tích lũy cả đời từ hàng chục đến hàng trăm triệu đồng của mỗi gia đình.

---

### 3. Mục tiêu, Tiêu chí thành công & Phạm vi triển khai

#### Tiêu chí thành công kỹ thuật (Pre-defined Gates & Metrics)

| Tiêu chí | Mục tiêu cam kết | Kết quả kiểm thử thực tế (Sprint W6) |
|---|---|---|
| **Độ phủ tin lừa đảo (Recall)** | ≥ 90% | **100%** (Đạt tuyệt đối trên 90 mẫu kịch bản lừa đảo thực tế) |
| **Báo nhầm tin lành tính (False Positive)** | ≤ 10% | **5%** (1/20 mẫu tin nhắn lành tính nhưng có yếu tố nhạy cảm) |
| **Độ trễ đầu-cuối (Warm Latency)** | p95 ≤ 15 giây (văn bản & ảnh) | Văn bản đạt **p95 = 3,5s**; Ảnh chụp đạt **p95 = 17,0s** (chấp nhận được theo thực tế) |
| **Chi phí vận hành** | ≤ 0,005 USD/lượt; ≤ 50 USD/tháng | **≈ 0,000792 USD/lượt** (tiền token LLM); tổng hóa đơn dev **3,93 USD** |
| **Bảo vệ quyền riêng tư** | Tuyệt đối không rò rỉ dữ liệu nhạy cảm | Ảnh chỉ nằm trong RAM của Lambda; PII được che trước khi ra LLM; TTL 30 ngày |

#### Trong phạm vi triển khai (MVP - 6 tuần)
- **Đa dạng dữ liệu đầu vào**: Xử lý văn bản, đường dẫn (bao gồm cả link ẩn sau text), ảnh chụp màn hình đơn lẻ và album ảnh, tin nhắn chuyển tiếp; hỗ trợ cơ chế gom tin liên tiếp (Debounce) trong 3 giây thành một phiên kiểm tra duy nhất.
- **Phản hồi trực quan 4 mức**: Cung cấp phân tích chi tiết gồm mức độ rủi ro, tên kịch bản lừa đảo, trích xuất bằng chứng từ tin nhắn, danh sách việc cần làm ngay, hotline chính thức và trích nguồn tin cậy (RAG).
- **Quyền riêng tư & Quản lý dữ liệu**: Quy trình đồng ý chủ động (Consent), hỗ trợ rút đồng ý (`/rutdongy`) và xóa sạch dữ liệu cá nhân (`/xoadulieu`).
- **Bảo vệ gia đình (Family Shield)**: Liên kết người thân qua mã mời dùng một lần (Double opt-in), tự động gửi cảnh báo song song, nhắc nhở sau 15 phút nếu chưa xác nhận, nút bấm *"Tôi đã liên hệ"*.
- **Tiện ích chat & Ứng cứu khẩn cấp**: Bộ lệnh quản lý `/nguoithan`, `/lichsu`, `/caidat`; cẩm nang hướng dẫn hành động trong 30 phút đầu khi nghi ngờ đã bị lừa tiền (`/bilua`).
- **Cơ chế vận hành an toàn**: Nút phản hồi *"Bot báo sai"* để thu thập feedback; công tắc ngắt khẩn cấp (**Kill Switch**) chuyển sang chế độ chỉ chạy luật cứng mà không cần triển khai lại code; xử lý thông báo thân thiện đối với tệp không hỗ trợ (video, sticker, file `.apk`).

#### Các phần đã cắt giảm khỏi kế hoạch ban đầu (Scope Cuts)
Để hoàn thiện sản phẩm đạt chất lượng cao nhất trong thời gian 6 tuần (kế hoạch ban đầu là 12 tuần), nhóm đã chủ động cắt giảm các tính năng sau:

| Hạng mục cắt giảm / Hoãn lại | Lý do điều chỉnh |
|---|---|
| **Tin nhắn thoại & Nhận dạng giọng nói (ASR)** | Không đủ thời gian tối ưu mô hình âm thanh tiếng Việt trên CPU Lambda; bot phản hồi hướng dẫn chuyển sang văn bản/ảnh. |
| **Mô hình thị giác lớn (VLM Fallback)** | Nhận diện ảnh qua mô hình OCR cục bộ đã vượt qua bài kiểm tra chất lượng (Gate G2), không cần dùng VLM đắt đỏ. |
| **Hội thoại nhiều lượt (Multi-turn Chat)** | Tập trung tối ưu hóa độ chính xác và tốc độ phản hồi cho một lượt kiểm tra duy nhất thay vì trò chuyện lan man. |
| **Telegram Mini App (Giao diện Web)** | Toàn bộ trải nghiệm người dùng được tối ưu hóa trực tiếp trong khung chat Telegram thông qua bàn phím và nút bấm inline. |
| **Giai đoạn 2: Kho tri thức sống tự động cập nhật** | Tạm hoãn sang giai đoạn sau; kho tri thức hiện tại sử dụng 100 kịch bản cảnh báo chính thức đã chuẩn hóa. |
| **Thử nghiệm diện rộng (Pilot 10–20 hộ gia đình)** | Thay thế bằng thử nghiệm nội bộ trong nhóm và người thân trong gia đình để đảm bảo an toàn tuyệt đối. |

**Cố ý không làm (Anti-Goals / Out of Scope)**: Không can thiệp chặn cuộc gọi viễn thông hay can thiệp ứng dụng ngân hàng; không xây dựng danh sách đen công khai số điện thoại/số tài khoản (tránh rủi ro pháp lý); không phân tích deepfake video thời gian thực; không gửi tin nhắn SMS viễn thông; không ghi âm cuộc gọi.

---

### 4. Kiến trúc giải pháp kỹ thuật

![Kiến trúc Ask First trên AWS](/images/2-Proposal/system_architecture.png)

#### Bốn nguyên tắc thiết kế cốt lõi
1. **Serverless, Event-Driven, không VPC, không NAT Gateway**: Tận dụng tối đa mô hình trả tiền theo dung lượng thực tế, loại bỏ hoàn toàn chi phí cố định của NAT Gateway (~32 USD/tháng) và máy chủ chạy ngầm.
2. **AI lai cục bộ trước (Hybrid Local-First)**: Toàn bộ các công đoạn nặng như OCR, nhận diện và che thông tin cá nhân (PII Masking), kiểm tra tập luật cứng và tính toán vector embedding đều chạy trực tiếp trên CPU của AWS Lambda. Chỉ bước Judge cuối cùng mới gọi Bedrock trên văn bản đã ẩn danh.
3. **Quy trình có kiểm soát (Deterministic Workflow, không dùng Autonomous Agent)**: Pipeline xử lý tuần tự qua 8 bước chặt chẽ: `Normalize → Extract → Mask PII → Signals (Luật + URL) → Retrieve (RAG) → Guard → Judge → Fuse → Respond`. Hệ thống đảm bảo luôn trả về kết quả từ tầng luật cứng ngay cả khi LLM gặp sự cố gián đoạn.
4. **Không lưu trữ nội dung gốc**: Tuyệt đối không lưu trữ tin nhắn hoặc hình ảnh gốc của người dùng. Hệ thống chỉ ghi nhận kết quả phân loại, mã dấu hiệu và mã băm (hash) với thời gian tự động xóa (TTL) 30 ngày.

#### Dịch vụ AWS sử dụng và Lý do lựa chọn

| Dịch vụ AWS | Vai trò trong hệ thống | Lý do lựa chọn |
|---|---|---|
| **AWS Lambda: `webhook`, `worker`, `worker-dlq`** (Java 21, Zip) | Tiếp nhận sự kiện Telegram qua **Function URL**, điều phối phiên kiểm tra, gửi phản hồi và kích hoạt cảnh báo người thân. | Khởi động nhanh, tối ưu hóa chi phí theo lượt gọi; Function URL cung cấp endpoint HTTPS bảo mật mà không cần API Gateway. |
| **AWS Lambda: `ai`** (Python 3.12, Container Image 3008 MB) | Thực thi toàn bộ pipeline AI cục bộ (mô hình OCR, thư viện embedding, bộ luật). | Định dạng Container Image cho phép đóng gói các thư viện học máy và mô hình ONNX vượt giới hạn 250 MB của file Zip; xử lý ảnh trực tiếp trong RAM. |
| **Amazon SQS & Dead-Letter Queue (DLQ)** | Hàng đợi đệm bất đồng bộ giữa `webhook` và `worker`. | Giúp Webhook phản hồi người dùng trong < 1 giây; giới hạn concurrency để kiểm soát hạn mức Bedrock; tận dụng `DelaySeconds` để gom tin nhắn (3s) và kích hoạt nhắc nhở (15 phút) mà không cần cron job. |
| **Amazon DynamoDB** (On-demand, Single-table) | Quản lý hồ sơ người dùng, bằng chứng đồng ý, liên kết gia đình, metadata lượt kiểm tra, cache kết quả và cờ tính năng (Feature Flags). | Cơ chế truy xuất Key-Value tốc độ cao, hỗ trợ **TTL** tự động xóa dữ liệu tuân thủ quyền riêng tư, Conditional Writes đảm bảo tính bất biến (Idempotency). |
| **Amazon Bedrock: Qwen3 32B** (Judge chính) & **gpt-oss-120b** (Dự phòng) | Đánh giá ngữ cảnh chuyên sâu và phân loại kịch bản trên văn bản đã che PII. | Mô hình Serverless trả phí theo token thực tế, không tốn chi phí thuê GPU. Cung cấp mô hình mã nguồn mở chất lượng cao có sẵn tại khu vực Sydney (`ap-southeast-2`). |
| **Amazon Bedrock Guardrails** | Bộ lọc bảo vệ ngăn chặn tấn công chèn lệnh (`PROMPT_ATTACK`). | Nhận diện và vô hiệu hóa các nỗ lực Jailbreak hoặc chèn lệnh độc hại ẩn bên trong tin nhắn lừa đảo được chuyển tiếp. |
| **Amazon S3** | Lưu trữ trọng số mô hình ONNX cục bộ, chỉ mục vector RAG, tập dữ liệu đánh giá và các mẫu đóng góp ẩn danh. | Chi phí lưu trữ cực rẻ; cho phép cập nhật tri thức hoặc đổi mô hình mà không cần build lại Docker image; bảo mật với Block Public Access và mã hóa SSE. |
| **Amazon ECR** | Lưu trữ container image của Lambda hàm `ai`. | Bắt buộc đối với các hàm Lambda khởi chạy từ Docker image. |
| **AWS SSM Parameter Store** (SecureString) | Quản lý tập trung Bot Token Telegram, Webhook Secret và các tham số stack. | Đảm bảo không lộ thông tin bí mật trong mã nguồn hoặc biến môi trường. |
| **Amazon CloudWatch & SNS** | Ghi log JSON có gắn `trace_id` thống nhất, giám sát chỉ số, kích hoạt cảnh báo DLQ gửi email tới đội ngũ phát triển. | Cung cấp khả năng quan sát tập trung; SNS đóng vai trò cổng thông báo nội bộ cho nhóm kỹ thuật khi có sự cố hạ tầng. |
| **AWS IAM & GitHub Actions (OIDC)** | Phân quyền tối thiểu (Least Privilege); tự động hóa CI/CD không cần lưu Access Key dài hạn. | Tiêu chuẩn bảo mật nghiêm ngặt cấp doanh nghiệp. |

#### Cố ý không sử dụng (Architectural Trade-offs)
- **Không dùng Amazon API Gateway**: Tính năng Lambda Function URL đã cung cấp đầy đủ endpoint HTTPS bảo mật với chi phí 0 USD, loại bỏ hoàn toàn độ trễ và chi phí trung gian của API Gateway.
- **Không dùng AWS Step Functions**: Luồng xử lý của hệ thống là tuyến tính và hoàn tất dưới 30 giây; việc điều phối trực tiếp qua SQS và Lambda giúp giảm thiểu độ phức tạp và chi phí.
- **Không dùng Amazon OpenSearch / Vector DB chuyên dụng**: Kho tri thức RAG gồm 100 kịch bản chuẩn có kích thước nhỏ gọn; việc tính toán độ tương đồng Cosine trực tiếp trong bộ nhớ RAM của Lambda chỉ mất **45 ms (p95)**, tiết kiệm hàng chục USD tiền cụm tìm kiếm mỗi tháng.
- **Không dùng Amazon EC2 / SageMaker Endpoint có GPU**: Chi phí duy trì GPU chạy liên tục (tối thiểu 50–100 USD/tháng) hoàn toàn không khả thi ở quy mô dự án nhỏ; mô hình Serverless trả theo token của Bedrock là lựa chọn tối ưu nhất.
- **Không dùng Amazon Transcribe, Textract, Bedrock Agents, VPC/NAT**.

#### Luồng dữ liệu đầu-cuối (End-to-End Workflow)
1. Người cao tuổi chuyển tiếp tin nhắn hoặc ảnh; Telegram gửi HTTP POST cập nhật tới Function URL của hàm `webhook` kèm mã `secret_token` (xác thực bằng thuật toán so sánh thời gian không đổi - constant-time).
2. Hàm `webhook` kiểm tra chống trùng lặp `update_id`, xác minh trạng thái đồng ý người dùng, gom tin nhắn vào bộ đệm `BUFFER#`, gửi tin nhắn tạm thời *"⏳ Đang kiểm tra..."* và đẩy tác vụ vào Amazon SQS với độ trễ 3 giây. Telegram nhận mã phản hồi 200 trong vòng chưa đầy 1 giây.
3. Hàm `worker` lấy tác vụ từ hàng đợi, đọc dữ liệu bộ đệm và trạng thái Kill Switch, sau đó kích hoạt hàm `ai` theo phương thức đồng bộ với `op=analyze` (chỉ truyền metadata và `file_id`, tuyệt đối không truyền mảng byte ảnh qua mạng).
4. Hàm `ai` tải ảnh trực tiếp vào bộ nhớ RAM, chạy mô hình OCR cục bộ, ẩn danh thông tin nhạy cảm (số điện thoại, số tài khoản, CCCD, mã OTP, email), áp dụng bộ luật cứng, kiểm tra tên miền độc hại và truy xuất ngữ cảnh từ kho tri thức RAG.
5. Hàm `ai` kiểm tra an toàn qua Bedrock Guardrails, gọi mô hình LLM Judge (Qwen3 32B; tự động leo thang sang gpt-oss-120b nếu độ tin cậy thấp), tổng hợp điểm số giữa luật và AI (*Fuse*), sau đó định dạng câu trả lời tiếng Việt từ mẫu câu chuẩn.
6. Nếu kết luận ở mức `DANGEROUS` kèm hành vi rủi ro, hàm `worker` lập tức kích hoạt gửi tin nhắn cảnh báo song song tới toàn bộ người thân đã được liên kết; trạng thái "đã cảnh báo" chỉ được xác nhận khi Telegram trả về `message_id`.
7. Hàm `worker` chỉnh sửa tin nhắn tạm *"⏳"* thành câu trả lời phân tích hoàn chỉnh và ghi nhận siêu dữ liệu phiên kiểm tra `CHECK#` (kèm TTL 30 ngày); tự động lên lịch nhắc nhở sau 15 phút nếu người thân chưa xác nhận xử lý.
8. Trường hợp tác vụ gặp lỗi 5 lần liên tiếp sẽ được chuyển vào Dead-Letter Queue (DLQ): hàm `worker-dlq` gửi thông báo xin lỗi người dùng vì hệ thống bận, đồng thời CloudWatch Alarm kích hoạt gửi email cảnh báo sự cố tới nhóm qua SNS.

{{% notice note %}}
**Thông số cấu hình thực tế trên stack Dev (`infra/template.yaml`)**: Mức xử lý đồng thời tối đa (Maximum Concurrency) với SQS được thiết lập là **5** cho hàm `worker` và **2** cho hàm `worker-dlq`. Tính năng SnapStart hiện đang **tắt theo mặc định** để phục vụ việc đo đạc chỉ số khởi động lạnh (ADR-008). Mô hình OCR sử dụng kiến trúc lai kết hợp giữa **RapidOCR PP-OCRv6 small** và **VietOCR** nhằm tối ưu độ chính xác tiếng Việt.
{{% /notice %}}

---

### 5. Kế hoạch & Tiến độ triển khai thực tế

Quy trình phát triển diễn ra trong 6 Sprint hàng tuần với 3 nhánh công việc song song (Backend, AI, Hạ tầng & Tích hợp), kết nối chặt chẽ thông qua bản hợp đồng dữ liệu chuẩn JSON Schema.

| Tuần | Mốc kiểm soát (Gate/Milestone) | Nội dung công việc | Tình trạng thực tế (Theo Git Repository) |
|---|---|---|---|
| **Tuần 1** (19–25/10) | **Gate G0: Hợp đồng dữ liệu** | Xây dựng JSON Schema giao tiếp Backend ↔ AI, tạo bộ dữ liệu mẫu (fixtures) và tích hợp Contract Test vào CI. | **Hoàn thành**: Hợp đồng được sáp nhập ngày 23/10 ([PR #89](https://github.com/ask-first-fcaj/ask-first/pull/89)), Backend đóng Gate G0 ngày 28/10 ([Issue #2](https://github.com/ask-first-fcaj/ask-first/issues/2)); bộ test Java tích hợp vào CI ngày 11/11 ([PR #104](https://github.com/ask-first-fcaj/ask-first/pull/104)). |
| **Tuần 2** (26/10–01/11) | **Gate G1: Chọn LLM**<br>**Gate G2: Chọn OCR** | Benchmark mô hình Judge; đánh giá so sánh các giải pháp OCR trên tập 50 ảnh chụp thực tế. | **Gate G2 đạt** ngày 30/10 (chọn RapidOCR, độ nhận diện URL đạt 94%). **Gate G1 chốt trễ** vào ngày 11/11 (chọn Qwen3 32B theo tài liệu kiến trúc ADR-002). |
| **Tuần 3** (02–08/11) | **Mốc M1: Text E2E Pipeline** | Hoàn thiện luồng kiểm tra văn bản đầu-cuối (kết hợp luật cứng và mô hình Qwen3). | **Hoàn thành muộn hơn dự kiến**: Pipeline văn bản hoàn tất 03/11, tích hợp Bedrock thật 11/11 ([PR #132](https://github.com/ask-first-fcaj/ask-first/pull/132)), Lambda `ai` kết nối hạ tầng 23/11 ([PR #173](https://github.com/ask-first-fcaj/ask-first/pull/173)), chính thức đóng mốc INT-01 ngày 25/11 ([Issue #56](https://github.com/ask-first-fcaj/ask-first/issues/56)). |
| **Tuần 4** (09–15/11) | **Mốc M2: Ảnh & Cảnh báo người thân** | Hoàn thiện luồng xử lý ảnh chụp màn hình qua OCR cục bộ; kích hoạt cảnh báo người thân. | Đo kiểm hiệu năng luồng ảnh trực tiếp trên môi trường AWS Lambda vào ngày 25/11 (xem chi tiết mục 7). |
| **Tuần 5** (16–22/11) | **Mốc M3: Tích hợp RAG**<br>**Mốc M4: MVP Freeze** | Tích hợp nguồn tri thức cảnh báo chính thức; đánh giá toàn diện trên bộ dữ liệu kiểm thử. | Báo cáo đánh giá M4 hoàn thành ngày 17/11; độ trễ RAG trên Lambda đạt p95 = 45 ms. |
| **Tuần 6** (23–29/11) | **Mốc M5: Thử nghiệm nội bộ**<br>**Mốc M6: Báo cáo tổng kết**<br>**Mốc M7: Nộp Workshop** | Thử nghiệm nội bộ cùng gia đình, chốt bảng dự toán chi phí thực tế, đánh giá rủi ro và đóng gói tài liệu. | Đánh giá kiểm thử cuối kỳ hoàn tất ngày 24/11; đối chiếu hóa đơn AWS Cost Explorer ngày 25/11. |

Sau cột mốc M4 (MVP Freeze), nhóm tuân thủ kỷ luật kỹ thuật: chỉ tập trung khắc phục lỗi, tinh chỉnh prompt và hiệu chỉnh ngưỡng điểm thông qua hệ thống kiểm thử tự động (Eval Gate).

---

### 6. Dự toán ngân sách & Đối chiếu chi phí thực tế

Mô hình tính toán dựa trên mức tải thử nghiệm **3.000 lượt kiểm tra/tháng** (bao gồm văn bản và ảnh chụp, không bao gồm tin thoại). Các dịch vụ hạ tầng AWS được tính toán thông qua công cụ **[AWS Pricing Calculator](https://calculator.aws/#/estimate?id=073f413f6ac370de48bf3bff0ba10a7b870ae807)** (tạo ngày 24/11/2026, khu vực `ap-southeast-1`, tùy chọn *"Without Free Tier"*). Chi phí Amazon Bedrock được tính toán trực tiếp dựa trên số lượng token đo đạc từ pipeline thực tế.

#### Bảng dự toán chi phí vận hành hàng tháng

| Dịch vụ AWS | Phương pháp tính toán | Chi phí không tính Free Tier (USD/tháng) | Chi phí thực hưởng Always-Free (USD/tháng) |
|---|---|---|---|
| **Amazon Bedrock: LLM** (Qwen3 32B + dự phòng gpt-oss-120b) | 2.250 lượt gọi LLM × 0,000792 USD (đo đạc thực tế, đã bao gồm tỷ lệ leo thang) | 1,78 | 1,78 |
| **Amazon Bedrock Guardrails** | 2.250 lượt × 0,15 USD / 1.000 text units | 0,34 | 0,34 |
| **AWS Lambda `ai`** (3008 MB) | Tính theo AWS Pricing Calculator | 0,73 | 0,00 |
| **AWS Lambda `worker`** (512 MB) | Tính theo AWS Pricing Calculator | 0,13 | 0,00 |
| **AWS Lambda `webhook`** (512 MB) | Tính theo AWS Pricing Calculator | 0,03 | 0,00 |
| **Amazon SQS** (Hàng đợi chính + DLQ) | Tính theo AWS Pricing Calculator | 0,28 | 0,00 |
| **Amazon DynamoDB** (On-demand) | Tính theo AWS Pricing Calculator | 0,29 | < 0,05 |
| **Amazon S3** (Lưu trữ model, index, eval) | Tính theo AWS Pricing Calculator | 0,03 | 0,03 |
| **Amazon ECR** (Lưu trữ container image hàm `ai`) | Tính theo AWS Pricing Calculator | 0,20 | 0,20 |
| **Amazon CloudWatch** (Logs, Metrics, Alarms, Dashboard) | Tính theo AWS Pricing Calculator | 2,35 | 0,00 |
| **Amazon SNS & SSM Parameter Store** | Thuộc hạn mức sử dụng cơ bản | ≈ 0,00 | 0,00 |
| **Tổng cộng** | | **≈ 6,16 USD/tháng** | **≈ 2,40 USD/tháng** |

- **Chi phí trung bình mỗi lượt kiểm tra (Token LLM)**: Chỉ khoảng **0,000792 USD (~20 VNĐ)**, thấp hơn rất nhiều so với hạn mức mục tiêu ban đầu là 0,005 USD.
- Con số 2.250 lượt gọi LLM dựa trên giả định 25% lượt kiểm tra được xử lý nhanh bởi tập luật cứng (Fast Path) hoặc trúng bộ nhớ đệm (Cache). Ngay cả trong kịch bản xấu nhất khi 100% lượt đều phải gọi tới LLM, chi phí Bedrock cũng chỉ ở mức ~2,70 USD/tháng.

#### Đối chiếu số liệu thực tế trên tài khoản AWS của nhóm (Ngày 25/11/2026)
- **Tận dụng AWS Free Tier**: Tài khoản của nhóm duy trì trong hạn mức Always-Free. Trong tháng 11 (tính đến ngày 25/11): Lambda tiêu thụ ≈ 8.200 / 400.000 GB-giây và 273 / 1.000.000 requests; Amazon SQS tiêu thụ ≈ 178.000 / 1.000.000 requests; CloudWatch duy trì dưới hạn mức 10 alarms miễn phí. Do đó, cột *"Chi phí thực hưởng Always-Free"* phản ánh chính xác chi phí nhóm phải chi trả.
- **Thời gian thực thi của Lambda (CloudWatch Duration qua 14 ngày test)**: 
  - Hàm `ai` (248 lượt gọi): Thời gian trung bình 2,7s; **p95 = 9,7s**.
  - Hàm `worker` (73 lượt gọi): Thời gian trung bình 4,6s; **p95 = 14,2s**.
  - Hàm `webhook` (50 lượt gọi): Thời gian trung bình 1,0s; **p95 = 3,0s**.
- **Chi phí thực tế theo AWS Budgets & Cost Explorer (01–25/11/2026)**:
  - Tài khoản hạ tầng Dev: AWS Budgets ghi nhận **≈ 0,09 USD** (dự báo cả tháng ≈ 0,10 USD, không bao gồm Bedrock).
  - Tài khoản chạy Bedrock (Sydney): Tổng chi phí thực tế là **3,93 USD** (bao gồm 3,57 USD phí dịch vụ và 0,36 USD thuế VAT 10%):
    - *Qwen3 32B*: Tiêu thụ 11,8 triệu token đầu vào, 0,94 triệu token đầu ra = **2,40 USD**.
    - *gpt-oss-120b* (dự phòng): Tiêu thụ 2,5 triệu token đầu vào, 0,44 triệu token đầu ra = **0,66 USD**.
    - *Bedrock Guardrails*: Tiêu thụ 3.266 text units (`ContentPolicyUnitsConsumed`) = **0,49 USD**.
    - *Gemma 3 12B* (chạy đánh giá Benchmark G1): **0,02 USD**.

#### Chiến lược tối ưu hóa chi phí (Cost Optimization Best Practices)
1. **Kiến trúc không chi phí cố định**: Loại bỏ hoàn toàn VPC/NAT Gateway, API Gateway và máy chủ GPU, đảm bảo hóa đơn bám sát 100% lưu lượng sử dụng thực tế.
2. **Chiến lược AI lai (Local-First)**: Đẩy toàn bộ tác vụ OCR, nhúng vector và kiểm tra luật vào CPU của Lambda, loại bỏ hoàn toàn phí token cho các bước tiền xử lý.
3. **Đường dẫn nhanh (Fast Path) & Bộ nhớ đệm (Cache)**: Tiết kiệm ngay ≈ 0,00094 USD cho mỗi lượt kiểm tra không cần gọi tới Bedrock.
4. **Cơ chế Kill Switch & Rate Limiting**: Cho phép ngắt gọi LLM tức thì khi phát hiện dấu hiệu spam bất thường mà không cần triển khai lại mã nguồn.
5. **Chính sách vòng đời dữ liệu (Lifecycle & Retention)**: Dữ liệu mẫu đóng góp trên S3 tự động xóa sau 30 ngày; cấu hình thời gian lưu trữ CloudWatch Logs trong 7 ngày và gắn chính sách ECR Lifecycle Policy chỉ giữ lại 5 bản build mới nhất.

---

### 7. Đánh giá rủi ro & Chiến lược giảm thiểu

Bảng theo dõi và xử lý rủi ro được cập nhật dựa trên kết quả kiểm thử thực tế tại mốc Sprint W6:

| Rủi ro tiềm ẩn | Mức độ ảnh hưởng | Giải pháp giảm thiểu | Tình trạng nghiệm thu thực tế (W6) |
|---|---|---|---|
| **Bỏ sót tin lừa đảo (False Negative)** | Cực kỳ nghiêm trọng (Người dùng mất tiền) | Tầng luật cứng có điểm sàn độc lập với LLM; không bao giờ đưa ra kết luận "An toàn"; áp dụng bài test tự động (Eval Gate) với yêu cầu Recall ≥ 90%. | **Đạt tuyệt đối**: Tỷ lệ Recall đạt **100%** trên tập 90 mẫu kịch bản lừa đảo thực tế. |
| **Báo nhầm tin nhắn bình thường (False Positive)** | Nghiêm trọng (Mất niềm tin của người dùng) | Tinh chỉnh bộ trọng số dung hợp (*Fusion Thresholds*: 70/60/25 theo ADR-005); thiết lập trần tỷ lệ báo nhầm ≤ 10%. | **Đạt xuất sắc**: Tỷ lệ báo nhầm chỉ ở mức **5%** (1/20) trên tập dữ liệu lành tính có từ khóa nhạy cảm. |
| **Tập dữ liệu kiểm thử nhỏ, thiên lệch** | Trung bình | Công khai minh bạch hạn chế của tập mẫu; xây dựng tính năng cho phép người dùng tự nguyện đóng góp mẫu đã ẩn danh. | Tập kiểm thử đạt **134 mẫu chuẩn hóa** (chưa đạt mục tiêu lý tưởng 300 mẫu ban đầu do thời gian 6 tuần hạn hẹp). |
| **LLM gặp lỗi, bị nghẽn (Throttle) hoặc cạn Quota** | Nghiêm trọng (Dịch vụ gián đoạn) | Xây dựng kiến trúc đa tầng (Cascade): chuyển sang mô hình dự phòng gpt-oss-120b; nếu lỗi toàn bộ sẽ kích hoạt chế độ chỉ chạy luật cứng (Rules-Only). | Đã tích hợp và kiểm thử tự động chuyển tầng thành công trong mã nguồn. |
| **Tấn công chèn lệnh (Prompt Injection) trong tin nhắn** | Nghiêm trọng (AI bị thao túng kết luận) | Kích hoạt Bedrock Guardrails (`PROMPT_ATTACK`); tự động gán mức tối thiểu là `UNSURE` nếu phát hiện injection; câu trả lời xuất ra qua template định sẵn. | Đã triển khai và vượt qua các kịch bản kiểm thử tấn công chèn lệnh. |
| **Độ trễ phản hồi và hiện tượng khởi động lạnh (Cold Start)** | Trung bình (Trải nghiệm chậm) | Gom tin trên SQS; nạp sẵn trọng số mô hình ở giai đoạn INIT của Lambda; làm nóng hệ thống (warm-up) trước các phiên trình diễn. | Văn bản đạt **p95 = 3,5s**. **Ảnh chụp đạt p95 = 17,0s** (vượt chỉ tiêu 15s ban đầu nhưng nằm trong ngưỡng chấp nhận 30s của Lead AI); thời gian Init Cold Start của hàm `ai` là 6,2s (p50). |
| **Chi phí gia tăng đột biến do bị tấn công Spam** | Trung bình (Vượt ngân sách) | Giới hạn tần suất gọi theo người dùng; thiết lập hạn mức Concurrency trên SQS; kích hoạt Kill Switch; theo dõi qua AWS Budgets. | Thiết lập ngân sách AWS Budgets 50 USD/tháng với các mốc cảnh báo tự động gửi email tại 10, 25, 40 và 50 USD. |
| **Rủi ro rò rỉ dữ liệu cá nhân & Tuân thủ pháp lý** | Cực kỳ nghiêm trọng (Vi phạm pháp luật) | Thực hiện ẩn danh PII cục bộ trước khi dữ liệu rời khỏi RAM; tuyệt đối không lưu nội dung gốc; thiết lập TTL 30 ngày. | **Tuân thủ chuẩn mực**: Đối chiếu trực tiếp với **Luật Bảo vệ dữ liệu cá nhân số 91/2025/QH15** và **Nghị định 356/2025/NĐ-CP** (ghi chú: đây là ánh xạ kỹ thuật, không thay thế tư vấn pháp lý). |
| **Mô hình Bedrock không khả dụng tại Region** | Nghiêm trọng (Judge không hoạt động) | Sử dụng mô hình có sẵn in-region tại Sydney (`ap-southeast-2`); dự phòng khu vực Jakarta (`ap-southeast-3`); thay đổi cấu hình qua `ai/config/models.yaml`. | Hệ thống hoạt động ổn định trên vùng Sydney, chưa cần kích hoạt chuyển vùng. |
| **Thiếu hụt nguồn lực thời gian (Khung thời gian 6 tuần)** | Cao (Trễ tiến độ dự án) | Phân chia nhân sự theo cặp (2 Backend, 2 AI); chủ động cắt giảm phạm vi nghiệp vụ sớm (Voice, VLM, Mini App) từ Sprint W3. | Đã kiểm soát tiến độ và đóng các cột mốc quan trọng đúng hạn theo kế hoạch điều chỉnh v3. |

---

### 8. Kết quả kỳ vọng & Giá trị dự án

#### Đóng góp về mặt kỹ thuật
- Chứng minh tính khả thi và hiệu quả vượt trội của kiến trúc **AI lai (Hybrid Local-First) trên nền tảng AWS Serverless**: kết hợp hài hòa giữa xử lý CPU biên (chi phí 0 đồng) và năng lực suy luận sâu của LLM trên đám mây.
- Đạt được các chỉ số vận hành ấn tượng: độ chính xác phát hiện lừa đảo **Recall 100%**, phản hồi văn bản dưới 4 giây và chi phí token chỉ vỏn vẹn **~20 đồng mỗi lượt kiểm tra**.
- Thiết lập quy trình phát triển chuẩn mực công nghiệp (*Contract-First* với JSON Schema, CI/CD tự động hóa qua GitHub Actions OIDC và quản trị hạ tầng hoàn toàn bằng AWS SAM).

#### Giá trị nhân văn và Tác động xã hội dài hạn
- Mang lại một công cụ bảo vệ số hóa gần gũi, thiết thực và hoàn toàn miễn phí cho người cao tuổi Việt Nam, giúp thu hẹp khoảng cách thế hệ và bảo vệ thành quả lao động của các gia đình trước tội phạm công nghệ cao.
- Với cấu trúc mô-đun hóa độc lập của lớp **Channel Adapter**, hệ thống sẵn sàng mở rộng sang **Zalo Bot Platform** trong tương lai để tiếp cận hàng chục triệu người dùng phổ thông tại Việt Nam, đồng thời tạo tiền đề cho việc xây dựng **Kho tri thức cảnh báo lừa đảo cộng đồng** liên tục được cập nhật.
