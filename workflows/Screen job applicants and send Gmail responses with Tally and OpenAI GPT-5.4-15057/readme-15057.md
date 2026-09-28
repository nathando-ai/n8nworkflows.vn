---
title: "🤖 Tự Động Xếp Hạng Ứng Viên Và Gửi Email Trả Lời Nhờ AI GPT-5.4 + TallyForms (N8n)"
description: "Workflow tự động hóa tuyển dụng giúp các sếp đánh giá ứng viên qua AI, gửi email mời phỏng vấn hoặc từ chối tự động, tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tuyen-dung-tu-dong-voi-gpt-5-4-tallyforms"
tags: [n8n, automation, hr, ai-summarization, openai, tallyforms, google-sheets]
keywords: [tự động hóa tuyển dụng n8n, ai đánh giá ứng viên, gpt-5.4 tuyển dụng, workflow tuyển dụng tự động, tallyforms + gmail + google sheets]
---

# 🚀 **Tự Động Xếp Hạng Ứng Viên & Gửi Email Trả Lời Nhờ AI GPT-5.4 + TallyForms**

### **Giải pháp AI tự động hóa tuyển dụng cho các sếp bận rộn**
Hiện nay, việc tuyển dụng thủ công thường tốn thời gian và dễ bị chủ quan. Các sếp phải:
- Đọc hàng chục hồ sơ ứng viên mỗi ngày.
- Đánh giá từng ứng viên theo tiêu chí nhất định.
- Gửi email trả lời (mời phỏng vấn hoặc từ chối) một cách cá nhân hóa.
- Theo dõi trạng thái ứng viên trong bảng Excel.

**Workflow này giúp các sếp:**
✅ **Tự động hóa 100% quy trình tuyển dụng** từ nhận hồ sơ đến gửi email trả lời.
✅ **Sử dụng AI GPT-5.4** để đánh giá ứng viên theo tiêu chí cụ thể của công ty.
✅ **Gửi email cá nhân hóa** (mời phỏng vấn hoặc từ chối) tự động.
✅ **Lưu tất cả dữ liệu vào Google Sheets** để theo dõi dễ dàng.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian đánh giá hồ sơ và gửi email.
- **Đánh giá khách quan**: AI GPT-5.4 đánh giá ứng viên theo tiêu chí chính xác, không bị chủ quan.
- **Email cá nhân hóa**: Mỗi ứng viên nhận được email phù hợp với tình trạng (mời phỏng vấn hoặc từ chối).
- **Theo dõi dễ dàng**: Tất cả dữ liệu được lưu vào Google Sheets với trạng thái, điểm số và đánh giá chi tiết.
- **Hoạt động 24/7**: Workflow chạy tự động ngay cả khi các sếp nghỉ ngơi.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản TallyForms** để tạo form nhận hồ sơ ứng viên.
2. **API Key OpenAI** (để sử dụng GPT-5.4).
3. **Tài khoản Gmail** (để gửi email trả lời).
4. **Tài khoản Google Sheets** (để lưu dữ liệu ứng viên).
5. **Bảng Google Sheets** với tab tên **"applications"** và các cột:
   - `timestamp`, `name`, `email`, `role`, `score`, `grade`, `evaluation`, `status`.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấp vào **"Create"** → **"Import"** và chọn file JSON.
   *Hoặc* copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15057) và paste vào **"Import from JSON"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình TallyForms**
- **Node: Tally Trigger**
  - Đăng nhập vào tài khoản TallyForms và chọn **form ứng viên** đã tạo.
  - Các trường bắt buộc trong form:
    - Full Name (Tên đầy đủ)
    - Email (Email)
    - Role Applied For (Vị trí ứng tuyển)
    - Years of Experience (Số năm kinh nghiệm)
    - Experience Summary (Tóm tắt kinh nghiệm)
    - Why do you want this role? (Lý do ứng tuyển)

##### **B. Cấu hình OpenAI (GPT-5.4)**
- **Node: GPT-5.4 Model** và **GPT-5.4 Model 2**
  - Đi đến **Credentials** → **Add Credential** → Chọn **OpenAI**.
  - Nhập **API Key** từ tài khoản OpenAI.
  - **Lưu ý quan trọng**:
    - Mở node **"Score Candidate"** (Agent) và **cập nhật system prompt** với **tiêu chí tuyển dụng cụ thể** của công ty.
    - Ví dụ:
      ```plaintext
      You are an HR assistant evaluating candidates for the role of [Vị trí]. Score candidates from 1-10 based on:
      - Years of experience (minimum [số năm])
      - Relevance of experience to the role
      - Quality of motivation letter
      Provide a 2-sentence evaluation.
      ```

##### **C. Cấu hình Gmail**
- **Node: Send Interview Invitation** và **Send Rejection Email**
  - Đi đến **Credentials** → **Add Credential** → Chọn **Gmail OAuth2**.
  - Chọn tài khoản Gmail sẽ gửi email.
  - **Lưu ý**:
    - Các email mẫu đã được thiết lập trong workflow, nhưng các sếp có thể chỉnh sửa nội dung trong **node Gmail**.

##### **D. Cấu hình Google Sheets**
- **Node: Log to Applications Sheet**
  - Đi đến **Credentials** → **Add Credential** → Chọn **Google Sheets OAuth2**.
  - Chọn tài khoản Google Sheets.
  - Nhập **Sheet ID** của bảng **"applications"** (có thể lấy từ liên kết bảng).
  - **Cấu trúc cột bắt buộc**:
    ```
    timestamp | name | email | role | score | grade | evaluation | status
    ```

##### **E. Cấu hình Node "Set Status"**
- **Node: Set Status Shortlisted** và **Set Status Rejected**
  - Các node này sẽ tự động cập nhật trạng thái ứng viên trong Google Sheets.
  - **Không cần chỉnh sửa** nếu đã cấu hình đúng các node trên.

#### **3. Kích hoạt ⚡️**
1. **Test run** với một hồ sơ mẫu:
   - Điền thông tin vào form TallyForms và gửi.
   - Kiểm tra email và Google Sheets để đảm bảo workflow hoạt động.
2. **Bật Active workflow**:
   - Nhấp vào nút **"Active"** ở góc trên bên phải của canvas.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả tuyển dụng ngay khi có ứng viên mới.
2. **Lưu log chi tiết**:
   - Sử dụng node **StickyNote** để ghi chú thêm thông tin về ứng viên (ví dụ: cuộc gọi phỏng vấn, quyết định cuối cùng).
3. **Báo cáo định kỳ**:
   - Tạo một workflow riêng để gửi báo cáo tổng hợp về số lượng ứng viên, điểm số trung bình, và tỷ lệ chấp nhận/reject.
4. **Cập nhật tiêu chí tuyển dụng**:
   - Khi có thay đổi trong yêu cầu tuyển dụng, chỉ cần chỉnh sửa **system prompt** trong node **"Score Candidate"** là xong.
5. **Tích hợp với CRM**:
   - Nếu công ty sử dụng **HubSpot** hoặc **Salesforce**, có thể thêm node **HTTP Request** để đồng bộ dữ liệu ứng viên vào CRM.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình tuyển dụng một cách **khách quan, nhanh chóng và hiệu quả**. Bằng cách kết hợp **TallyForms, AI GPT-5.4, Gmail và Google Sheets**, các sếp không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng tuyển dụng.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với một hồ sơ mẫu** và bắt đầu tự động hóa tuyển dụng!

👉 **Đăng ký VPS TinoHost** (mã giảm giá **VPSN8N**) để tự host n8n:
[🔗 TinoHost](https://tino.vn/vps-n8n?affid=388)

👉 **Hoặc chọn VPS Xeon 4GB chỉ 50k/tháng**:
[🔗 BNIX](https://my.bnix.one/aff.php?aff=172)

---
**Chia sẻ và đặt câu hỏi về workflow trên LinkedIn của tác giả Yaron Been:**
[🔗 LinkedIn](https://www.linkedin.com/in/yaronbeen/) | [📺 YouTube](https://www.youtube.com/@YaronBeen/videos)