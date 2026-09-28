---
title: "🤖 Tự Động Hóa Onboarding Khách Hàng với Form, Google Sheets & Trả Lời AI Cá Nhân Hóa (OpenRouter)"
description: "Workflow tự động hóa 100% không code giúp doanh nghiệp thu thập dữ liệu khách hàng từ form, lưu trữ trên Google Sheets, và tự động tạo phản hồi AI cá nhân hóa qua email/Telegram. Giảm thời gian triệt để 90% trong quá trình onboarding mới."
slug: "tieu-dong-hoa-onboarding-khach-hang-form-google-sheets-ai"
tags: [n8n, automation, no-code, ai-chatbot, google-sheets, openrouter, langchain]
keywords: [tự động hóa onboarding khách hàng, n8n workflow, form tự động, ai cá nhân hóa email, google sheets tự động, openrouter api, langchain agent]
---

# 🚀 **Tự Động Hóa Onboarding Khách Hàng với Form, Google Sheets & Trả Lời AI Cá Nhân Hóa**

## **Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Lặp đi lặp lại** việc nhập liệu dữ liệu khách hàng mới từ form vào Google Sheets?
- **Mất thời gian** viết email chào mừng cho từng khách hàng mới, không thể cá nhân hóa?
- **Không biết** cách xử lý nhanh chóng các yêu cầu khác nhau từ khách hàng mới?
- **Lo lắng** về việc mất khách hàng do phản hồi chậm trễ?

Workflow này **giải quyết tất cả** bằng cách tự động hóa **tất cả quá trình onboarding** từ khi khách hàng gửi form đến khi nhận phản hồi cá nhân hóa qua email hoặc Telegram.

---
:::info[Gurey AI Partnership Form & Client Triage Workflow]
**Đây là phiên bản tiếng Việt của workflow "Client Onboarding with Form, Google Sheets and AI-Generated Responses" của Abdullahi Ahmed, được tối ưu hóa cho doanh nghiệp Việt Nam.**
👉 [Xem workflow gốc](https://n8n.io/workflows/8977) (n8n.io)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** trong quá trình onboarding mới.
- **Cá nhân hóa hoàn toàn** email chào mừng dựa trên dữ liệu khách hàng.
- **Lưu trữ dữ liệu an toàn** trên Google Sheets với lịch sử đầy đủ.
- **Phản hồi AI 24/7** qua Telegram hoặc email, không cần nhân viên trực tiếp.
- **Tăng tỷ lệ chuyển đổi** nhờ phản hồi nhanh chóng và chuyên nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets và Gmail).
2. **API Key OpenRouter** (để sử dụng mô hình AI Claude 3.5).
3. **API Key Pinecone** (nếu muốn lưu trữ vector cho AI).
4. **API Key OpenAI** (để tạo embedding cho dữ liệu).
5. **Tài khoản Telegram** (để gửi thông báo tự động).
6. **Google Sheet** đã chuẩn bị sẵn (cấu trúc 2 sheet: `Client Data` và `AI Summaries`).

👉 [Hướng dẫn lấy API Key OpenRouter](https://openrouter.ai/keys)
👉 [Hướng dẫn lấy API Key Pinecone](https://www.pinecone.io/)
👉 [Hướng dẫn lấy API Key OpenAI](https://platform.openai.com/api-keys)

---
:::info[CHUẨN BỊ HÀNH TRÌNH]
- **N8n Self-hosted** (khuyến nghị sử dụng VPS để workflow hoạt động 24/7).
- **N8n Nodes bổ sung**:
  - `@n8n/n8n-nodes-langchain` (để sử dụng AI Agent).
  - `n8n-nodes-base.googleSheets`, `n8n-nodes-base.gmail`, `n8n-nodes-base.telegram`.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/8977](https://n8n.io/workflows/8977) (chọn **Export**).
2. **Mở n8n Editor** trên máy chủ của bạn.
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải workflow** từ link trên và copy toàn bộ JSON.
2. **Mở n8n Editor** → **Nhấp vào "Import"** → **Chọn "Paste JSON"** → **Dán và import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: On Form Submission (Form Trigger)**
- **Không cần cấu hình** (n8n sẽ tự tạo URL form).
- **Customize form** bằng cách chỉnh sửa HTML/CSS trong node này (nếu muốn thay đổi giao diện).
- **Dữ liệu thu thập**:
  - Tên, email, vai trò, công ty, doanh thu, mục tiêu dự án, và các thông tin khác.

#### **🔹 Node 2 & 3: Log Client Data (Google Sheets)**
- **Chọn credentials**:
  - **Google Sheets OAuth2 API** (đã cấu hình trước khi import).
  - **Sheet Name**: Đảm bảo sheet có tên chính xác (`Client Data`).
  - **Operation**: Đặt là `appendOrUpdate` (n8n sẽ tự động cập nhật).
- **Cột cần có trong sheet**:
  - `Date`, `Name`, `Email`, `Role`, `Company Size`, `Revenue`, `Project Goals`, `Form Submission Data`.

#### **🔹 Node 4-6: AI Agent & OpenRouter Chat Model**
- **Cấu hình AI Agent**:
  - **Model**: Sử dụng `anthropic/claude-3.5-sonnet` (đã được chỉ định trong node `OpenRouter Chat Model1`).
  - **Prompt**: N8n tự động tạo prompt dựa trên dữ liệu form.
  - **Output Parser**: Đảm bảo kết quả là JSON (ví dụ: `{"client_summary": "..."}`).
- **Credentials**:
  - **OpenRouter API Key** (điền vào `openRouterApi`).
  - **Pinecone API Key** (nếu muốn lưu trữ vector, điền vào `pineconeApi`).
  - **OpenAI API Key** (để tạo embedding, điền vào `openAiApi`).

#### **🔹 Node 7-9: Welcome Email AI Agent**
- **Cấu hình email**:
  - **Subject**: AI sẽ tự động tạo tiêu đề cá nhân hóa (ví dụ: *"Chào [Tên], Chúng Tôi Sẵn Sàng Hỗ Trợ Dự Án [Mục Tiêu]!"*).
  - **Body**: Nội dung email sẽ kết hợp dữ liệu form + tóm tắt AI.
- **Node Send Email (Gmail)**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **Điền địa chỉ email** của khách hàng từ dữ liệu form.

#### **🔹 Node 10-11: Send Telegram Notification (Tùy Chọn)**
- **Cấu hình Telegram**:
  - **Credentials**: Điền `telegramApi` (API Key Telegram Bot).
  - **Chat ID**: Điền ID chat của bot Telegram (có thể lấy từ [@BotFather](https://t.me/BotFather)).
  - **Message**: AI sẽ tự động tạo tin nhắn tóm tắt cho quản lý.

#### **🔹 Node 12-13: Log Summary (Google Sheets)**
- **Cập nhật sheet `AI Summaries`**:
  - N8n sẽ ghi lại tóm tắt AI vào sheet riêng để theo dõi.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **Run Workflow** và gửi dữ liệu mẫu qua form.
   - Kiểm tra:
     - Dữ liệu có được lưu vào Google Sheets không?
     - Email/Telegram có được gửi không?
     - AI có tạo tóm tắt và email cá nhân hóa không?
2. **Bật Active**:
   - Sau khi test thành công, **bật switch "Active"** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối với Slack (Thông Báo Cho Đội Ngũ)**
- **Thêm node Slack** sau node `Send a text message` để thông báo cho team khi có khách hàng mới.
- **Cài đặt**:
  - **Credentials**: `slackApi` (API Key từ Slack App).
  - **Channel**: Chọn channel cần thông báo (ví dụ: `#new-leads`).

### **2. Lưu Log Hoạt Động (Google Sheets)**
- **Thêm node `stickyNote`** để ghi lại lịch sử hoạt động của workflow (giúp debug dễ dàng).

### **3. Gửi Báo Cáo Định Kỳ (Email/Telegram)**
- **Sử dụng node `Set Interval`** để gửi báo cáo tổng hợp khách hàng mới hàng tuần.
- **Ví dụ**:
  - Tóm tắt số lượng khách hàng mới.
  - Dự án phổ biến nhất.
  - Kết quả chuyển đổi.

### **4. Cải Tiến AI Agent**
- **Tùy chỉnh prompt** trong node `AI Agent` để AI trả lời chính xác hơn.
- **Ví dụ**:
  ```json
  {
    "instruction": "Tóm tắt thông tin khách hàng dưới dạng JSON với các trường: name, company, project_goals, priority_level, next_steps."
  }
  ```

### **5. Sử Dụng Mô Hình AI Khác**
- **Thay đổi model** trong node `OpenRouter Chat Model` từ `anthropic/claude-3.5-sonnet` sang mô hình khác (ví dụ: `mistral/mistral-7b`).
- **Lưu ý**: Cần kiểm tra lại API Key và tài nguyên của OpenRouter.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào chiến lược kinh doanh thay vì công việc lặp lại. Bằng cách tự động hóa **tất cả quá trình onboarding**, doanh nghiệp sẽ:
✅ **Tăng tốc độ phản hồi** với khách hàng.
✅ **Cá nhân hóa trải nghiệm** một cách chuyên nghiệp.
✅ **Giảm thiểu lỗi** nhờ AI xử lý dữ liệu chính xác.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình credentials** theo hướng dẫn.
3. **Test và bật workflow** để bắt đầu tự động hóa onboarding.

👉 **Cần hỗ trợ thêm?** Liên hệ với Abdullahi Ahmed qua [Calendly](https://calendly.com/gureyosman2008/30min) để tư vấn custom workflow!

---
:::note[CHÚ Ý]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow hoạt động 24/7.
- **Đăng ký VPS** với mã giảm giá **VPSN8N** để tiết kiệm chi phí:
  👉 [TinoHost](https://tino.vn/vps-n8n?affid=388) (Giảm 39%)
  👉 [BNIX](https://my.bnix.one/aff.php?aff=172) (Xeon 4GB chỉ 50k/tháng)
:::

---
**🎬 Theo dõi Abdullahi Osman trên YouTube** để cập nhật các workflow mới:
[@gureyosman06](https://www.youtube.com/@gureyosman06)