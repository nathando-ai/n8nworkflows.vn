---
title: "📊 Tự Động Hóa Báo Cáo Rủi Ro Tài Chính Từ Phỏng Vấn ElevenLabs Với AI (OpenAI + Gmail) - Không Cần Code"
description: "Workflow này tự động chuyển đổi file âm thanh phỏng vấn từ ElevenLabs thành báo cáo rủi ro tài chính chi tiết, gửi trực tiếp qua email. Giúp các sếp tiết kiệm 10+ giờ/tháng phân tích thủ công, giảm sai sót và nâng cao hiệu quả quyết định."
slug: "tu-dong-hoa-bao-cao-rui-ro-tai-chinh-tu-phong-van-elevenlabs"
tags: [n8n, automation, no-code, ai-summarization, financial-analysis, elevenlabs, openai, gmail]
keywords: [tự động hóa báo cáo tài chính, n8n workflow elevenlabs, ai phân tích rủi ro, gửi báo cáo email tự động, openai gpt-5-mini, google drive upload audio]
---

# 🚀 **Tự Động Hóa Báo Cáo Rủi Ro Tài Chính Từ Phỏng Vấn ElevenLabs Với AI (OpenAI + Gmail)**

### **Giải pháp cho vấn đề gì?**
Các sếp thường phải:
- **Nghe và ghi chép** hàng giờ âm thanh phỏng vấn từ khách hàng/đối tác.
- **Phân tích thủ công** thông tin tài chính trong cuộc hội thoại để đánh giá rủi ro.
- **Tạo báo cáo** và gửi qua email, dễ bị lỗi hoặc mất thời gian.

**Workflow này tự động hóa toàn bộ quy trình:**
1. Nhận file âm thanh từ ElevenLabs → **Chuyển thành báo cáo rủi ro chi tiết**.
2. **Trích xuất dữ liệu** về tình hình tài chính, điểm mạnh/điểm yếu.
3. **Đánh giá rủi ro** bằng AI (OpenAI GPT-5 Mini) và tạo **báo cáo HTML sẵn sàng gửi**.
4. **Gửi tự động** qua Gmail cho các stakeholder.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần nghe lại âm thanh hoặc ghi chép thủ công.
- **Chính xác 100%**: AI trích xuất và phân tích dữ liệu với độ chính xác cao hơn con người.
- **Báo cáo cá nhân hóa**: Mỗi cuộc phỏng vấn đều được xử lý riêng, với đánh giá rủi ro cụ thể.
- **Hoạt động liên tục**: Nhận và xử lý âm thanh ngay khi ElevenLabs gửi webhook (không cần can thiệp).
- **Gửi tự động**: Báo cáo được gửi qua email ngay sau khi hoàn thành, không quên hay trì hoãn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản ElevenLabs**:
   - Đăng ký tại [ElevenLabs](https://try.elevenlabs.io/) và lấy **API Key**.
   - Cấu hình **webhook endpoint** trong ElevenLabs để gửi dữ liệu âm thanh và phiên bản dịch sau cuộc gọi.
   - **Path Webhook**: `0a1e32dd-fb2d-450f-a9bd-e69c43bfdecf` (không thay đổi).

2. **Tài khoản OpenAI**:
   - Lấy **API Key** từ [OpenAI](https://platform.openai.com/) và thêm vào n8n dưới tên `openAiApi`.
   - Chọn model: `gpt-5-mini` (đã được cấu hình sẵn trong workflow).

3. **Tài khoản Google Drive**:
   - Cấu hình **OAuth2** trong n8n với tên `googleDriveOAuth2`.
   - Chọn **folder đích** để lưu file âm thanh (thay đổi trong node "Upload audio").

4. **Tài khoản Gmail**:
   - Cấu hình **OAuth2** trong n8n với tên `gmailOAuth2`.
   - Thiết lập **người nhận** (placeholder `recipient@example.com`) và **chủ đề email** (placeholder `Financial Risk Report for {companyName}`).

5. **Node bổ sung (nếu cần)**:
   - Nếu muốn lưu log hoặc gửi báo cáo qua Slack/Telegram, các sếp có thể thêm node tương ứng sau node "Send report".

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14546](https://n8n.io/workflows/14546) (nút "Download").
- Trong n8n Editor:
  - Nhấn **"Import"** → Chọn file JSON vừa tải.
  - Hoặc **copy/paste** JSON từ file vào ô "Import Workflow" và nhấn "Import".

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **15 node** với các bước quan trọng sau. Các sếp **phải** kiểm tra và điều chỉnh:

##### **A. Webhook (Nhận dữ liệu từ ElevenLabs)**
- **Không cần thay đổi** `path` hoặc `httpMethod` (POST).
- **Kiểm tra** trong ElevenLabs:
  - Đăng ký endpoint `https://<tên-domain-n8n>/webhook/0a1e32dd-fb2d-450f-a9bd-e69c43bfdecf` để nhận:
    - File âm thanh (base64) sau cuộc gọi.
    - Phiên bản dịch (transcript) của cuộc gọi.

##### **B. Upload audio → Google Drive**
- Node **"Upload audio"** sử dụng `googleDriveOAuth2`.
- **Thay đổi folder đích**:
  - Mở node → Tab "Credentials" → Chọn folder Google Drive phù hợp.
  - **Lưu ý**: File âm thanh sẽ được lưu với tên tự động (ví dụ: `interview_<timestamp>.mp3`).

##### **C. Trích xuất và phân tích AI**
- **Node "Information Extractor"**:
  - Trích xuất dữ liệu **cấu trúc** (ví dụ: tên công ty, doanh thu, nợ phải trả, điểm mạnh/điểm yếu).
  - **Không cần chỉnh** nếu dữ liệu trong transcript phù hợp với cấu trúc mặc định.
  - **Nếu cần thay đổi**: Mở node → Tab "Configuration" → Sửa `prompt` trong `informationExtractor`.

- **Node "Calculate Rating"**:
  - Đánh giá **rủi ro tài chính** (score từ 1-10) và lý do.
  - **Không cần chỉnh** nếu sử dụng cấu trúc mặc định.
  - **Nếu muốn thay đổi**: Mở node → Tab "Configuration" → Sửa `prompt` trong `chainLlm`.

- **Node "Financial Report Generator"**:
  - Tạo **báo cáo HTML** từ dữ liệu trích xuất và đánh giá rủi ro.
  - **Không cần chỉnh** nếu muốn giữ mẫu mặc định.
  - **Nếu muốn cá nhân hóa**: Mở node → Tab "Configuration" → Sửa `prompt` trong `chainLlm`.

##### **D. Gửi báo cáo qua Gmail**
- Node **"Send report"** sử dụng `gmailOAuth2`.
- **Thay đổi người nhận**:
  - Mở node → Tab "Credentials" → Sửa `to` từ `recipient@example.com` thành email thực tế.
- **Thay đổi chủ đề email**:
  - Mở node → Tab "Configuration" → Sửa `subject` từ `Financial Risk Report for {companyName}` thành mẫu phù hợp (ví dụ: `Báo cáo Rủi Ro Tài Chính - {Tên Công Ty}`).

##### **E. Các node khác (không cần chỉnh)**
- **"Switch"**: Chuyển hướng dữ liệu từ ElevenLabs (âm thanh hoặc transcript).
- **"Merge"**: Gộp kết quả từ các node AI.
- **"Code" nodes**: Chuyển đổi base64 → MP3 (không cần chỉnh).

---

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Nhấn nút **"Execute"** trên node Webhook.
   - Gửi một **file âm thanh mẫu** từ ElevenLabs (hoặc sử dụng file test).
   - Kiểm tra kết quả ở node cuối cùng ("Send report") để đảm bảo:
     - File âm thanh được upload Google Drive thành công.
     - Transcript được trích xuất và phân tích AI.
     - Báo cáo HTML được tạo và gửi email.

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **"Inactive"** sang **"Active"**.
   - **Lưu ý**: N8n sẽ tự động nhận webhook từ ElevenLabs và xử lý tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log cho audit**:
   - Thêm node **Google Sheets** sau node "Send report" để ghi lại lịch sử báo cáo.
   - Cấu hình node Sheets với `googleSheetsOAuth2` và sheet phù hợp.

2. **Gửi báo cáo qua Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node "Send report" để thông báo khi báo cáo được tạo.

3. **Tự động lưu bản sao báo cáo**:
   - Thêm node **Google Drive (Create File)** sau node "Financial Report Generator" để lưu bản HTML của báo cáo.

4. **Cập nhật mô hình AI**:
   - Nếu muốn sử dụng mô hình mới (ví dụ: `gpt-4`), mở node `lmChatOpenAi` → Tab "Configuration" → Thay đổi `model` từ `gpt-5-mini` sang `gpt-4`.

5. **Tự động xóa file âm thanh sau xử lý**:
   - Thêm node **Google Drive (Delete File)** sau node "Upload audio" để xóa file sau khi xử lý xong.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc phân tích thủ công, đồng thời **nâng cao độ chính xác** và **tính chuyên nghiệp** của báo cáo tài chính. Với chỉ **5 phút setup**, các sếp có thể tự động hóa toàn bộ quy trình từ âm thanh phỏng vấn đến báo cáo email sẵn sàng gửi.

**Hành động ngay**:
1. **Import workflow** và cấu hình tài khoản.
2. **Test với một cuộc phỏng vấn mẫu**.
3. **Bật Active** và để AI làm việc 24/7!

---
**🔗 Tài liệu tham khảo**:
- [ElevenLabs Webhook Documentation](https://docs.elevenlabs.io/docs/webhooks)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
- [n8n Google Drive Nodes](https://docs.n8n.io/integrations/builtins/google-drive/)

**🎥 Học thêm từ tác giả**:
👉 [YouTube Channel của Davide Boizza](https://youtube.com/@n3witalia) (có nhiều **template miễn phí** cho n8n!).