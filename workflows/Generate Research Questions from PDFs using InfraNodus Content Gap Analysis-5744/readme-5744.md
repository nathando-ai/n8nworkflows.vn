---
title: "🚀 Tự Động Tạo Câu Hỏi Nghiên Cứu Từ File PDF Với InfraNodus Content Gap Analysis"
description: "Khám phá cách tự động trích dụng tài liệu PDF, phân tích khoảng trống nội dung (content gap) bằng InfraNodus GraphRAG và tạo câu hỏi nghiên cứu đột phá trong n8n."
slug: "tao-cau-hoi-nghien-cuu-tu-pdf-voi-infranodus-n8n"
tags: [n8n, automation, infranodus, ai-rag, pdf-extraction, graphrag]
keywords: [n8n workflow, infranodus, content gap analysis, tạo câu hỏi nghiên cứu, ai text network analysis, trích xuất pdf n8n]
---

# 🚀 Tự Động Tạo Câu Hỏi Nghiên Cứu Từ File PDF Với InfraNodus Content Gap Analysis

Các sếp có bao giờ cảm thấy việc đọc hàng đống tài liệu PDF, tổng hợp thông tin và tìm ra một hướng đi mới (research question) cho đề tài của mình mất quá nhiều thời gian nhưng kết quả từ AI lại hay bị chung chung, rập khuôn? 

Bài toán này xuất hiện ở mọi nơi: từ các nhà nghiên cứu khoa học, đội ngũ R&D sản phẩm, cho đến các chuyên gia nội dung cần tìm góc nhìn độc bản. Thay vì làm thủ công, workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình: **Nhận file PDF tải lên -> Trích xuất văn bản chuẩn xác -> Phân tích mạng lưới cấu trúc (Knowledge Graph) bằng InfraNodus -> Tìm khoảng trống tri thức (Content Gap) -> Tạo câu hỏi nghiên cứu đột phá.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Người dùng chỉ cần upload file PDF qua giao diện Form, phần còn lại hệ thống lo.
- **Tránh thiên kiến AI (AI Bias):** Sử dụng công nghệ *GraphRAG* và *Text Network Analysis* của InfraNodus để tìm ra những khoảng trống nội dung mà con người hoặc LLM thông thường dễ bỏ sót.
- **Góc nhìn mới lạ:** Tạo ra các câu hỏi/prompt kết nối các chủ đề tưởng chừng không liên quan trong tài liệu lại với nhau.
- **Giao diện thân thiện:** Trả kết quả trực tiếp ngay trên form tương tác cho người dùng cuối.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản & API Key InfraNodus:** Đăng ký tài khoản tại [InfraNodus](https://infranodus.com) để lấy API Key xác thực cho HTTP Request node.
- **Tùy chọn nâng cao (ConvertAPI):** Nếu muốn giữ nguyên định dạng layout của PDF phức tạp, chuẩn bị tài khoản tại [ConvertAPI](https://convertapi.com?ref=4l54n).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> Dán (Paste) toàn bộ cấu trúc vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính được bố trí theo các bước sau:

1. **On form submission (`formTrigger`):**
   - Đây là điểm khởi đầu cho phép người dùng upload file PDF thông qua một web form công khai. Các sếp có thể chia sẻ URL này cho đồng nghiệp hoặc tổ chức.
2. **Convert binary files to PDF (`code`):**
   - Xử lý các định dạng dữ liệu nhị phân tải lên để đảm bảo chúng sẵn sàng chuyển đổi thành tệp PDF chuẩn.
3. **Extract text from PDF files (`extractFromFile`):**
   - Node mặc định dùng để bóc tách văn bản từ PDF. 
   - *Lưu ý nâng cao:* Nếu file PDF của các sếp có bố cục phức tạp (nhiều cột, bảng biểu), hãy thay thế node này bằng HTTP Request gọi tới **ConvertAPI** (đã được gợi ý sẵn trên canvas của workflow) để giữ nguyên vẹn cấu trúc văn bản.
4. **Prepare for InfraNodus (`code`):**
   - Gom toàn bộ văn bản đã trích xuất thành một chuỗi (string) duy nhất và cấu hình độ sâu khoảng trống (*gap depth*) mà InfraNodus sẽ sử dụng để phân tích.
5. **InfraNodus GraphRAG Question Generator (`httpRequest`):**
   - Node cốt lõi gọi API của InfraNodus.
   - **BẮT BUỘC:** Các sếp cần cấu hình **Credentials** (`httpBearerAuth`) với API Key cá nhân lấy từ tài khoản InfraNodus của mình.
6. **Display on the Form to the User (`form`):**
   - Hiển thị kết quả câu hỏi nghiên cứu/prompt được tạo ra trực tiếp trên giao diện form trả về cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form, upload một file PDF mẫu.
- Kiểm tra kết quả trả về trên màn hình form.
- Khi mọi thứ mượt mà, bật công tắc **Active** góc trên bên phải để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook / App riêng:** Thay vì hiển thị qua form mặc định của n8n, các sếp có thể đẩy kết quả qua webhook đểúng dụng vào web app riêng thông qua `iframe`.
- **Lưu trữ tri thức:** Kết nối thêm node Google Sheets hoặc Notion để lưu lại lịch sử các câu hỏi nghiên cứu đã tạo ra cho từng dự án.
- **Bổ sung thông báo:** Gắn thêm node Slack hoặc Telegram để bắn tin nhắn thông báo ngay khi có ai đó hoàn thành việc phân tích tài liệu PDF mới.

---

### 📌 Kết luận
Việc kết hợp n8n với InfraNodus GraphRAG mở ra một hướng đi cực kỳ mạnh mẽ để khai thác tài liệu chuyên sâu mà không tốn sức. Triển khai ngay workflow này để nâng tầm chất lượng nghiên cứu và sáng tạo nội dung của các sếp lên một nấc thang mới!