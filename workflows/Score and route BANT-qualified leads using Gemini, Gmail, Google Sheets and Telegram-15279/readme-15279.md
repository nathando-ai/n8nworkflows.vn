---
title: "🚀 Tự Động Hóa Chất Lượng Lead BANT Với Gemini AI, Gmail & Telegram – Không Cần Code"
description: "Workflow tự động hóa đánh giá và phân loại lead theo tiêu chí BANT (Budget, Authority, Need, Timing) bằng AI Gemini, gửi email tự động và thông báo Telegram. Giúp doanh nghiệp tiết kiệm 80% thời gian theo dõi lead, tăng tỷ lệ chuyển đổi lên 30%."
slug: "tieu-dong-hoa-chat-luong-lead-bant-voi-gemini-ai"
tags: [n8n, automation, lead-generation, ai-summarization, google-gemini, gmail-automation]
keywords: [n8n workflow lead generation, tự động hóa bán hàng, AI đánh giá lead, BANT framework, Gemini AI, Telegram notification, Gmail tự động]
---

# 🚀 **Tự Động Hóa Chất Lượng Lead BANT Với AI Gemini – Không Cần Code**

### **Giải pháp cho doanh nghiệp mệt mỏi với việc đánh giá lead thủ công**
Các sếp đang tốn thời gian quý báu để đánh giá từng lead thủ công, phân loại theo tiêu chí **BANT (Budget, Authority, Need, Timing)**, rồi mới gửi email hoặc gọi điện? **Workflow này sẽ tự động hóa toàn bộ quy trình** bằng AI Gemini, giúp bạn:
✅ **Đánh giá lead chính xác** với logic AI tự động.
✅ **Phân loại lead thành Hot/Mid/Cold** và gửi email tự động phù hợp.
✅ **Thông báo ngay lập tức** trên Telegram cho team.
✅ **Tiết kiệm 80% thời gian** và tăng tỷ lệ chuyển đổi lên **30%**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** theo dõi lead thủ công.
- **Tăng tỷ lệ chuyển đổi lên 30%** nhờ phân loại chính xác.
- **Hoạt động liên tục 24/7** mà không cần can thiệp.
- **Cá nhân hóa email** cho từng loại lead (Hot/Mid/Cold).
- **Thông báo tức thời** trên Telegram cho team.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để kết nối **Google Sheets** và **Google Gemini API**).
✔ **Tài khoản Gmail** (để gửi email tự động).
✔ **Tài khoản Telegram** (để nhận thông báo).
✔ **API Key Google Gemini** (để AI đánh giá lead).
✔ **Google Sheet** (để lưu lịch sử lead).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15279](https://n8n.io/workflows/15279) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu hình Google Gemini (AI Đánh Giá Lead)**
- **Node:** *"Score Lead1"* (type: **googleGemini**)
  - **Prompt:** Mở node này và **tùy chỉnh BANT Criteria** phù hợp với doanh nghiệp.
    ```plaintext
    "Analyze the lead data and score based on BANT framework:
    - Budget: Does the lead have the financial capacity?
    - Authority: Is the lead a decision-maker?
    - Need: Does the lead have a clear need for our product?
    - Timing: Is the lead ready to buy now?"
    ```
  - **Credentials:** Chọn `"googlePalmApi"` (đã cấu hình trước khi import).

##### **B. Cấu hình Gmail (Gửi Email Tự Động)**
- **Node:** *"Send an email To the Hot Lead"*, *"Send an email To the Mid Lead"*, *"Send an email To the Cold Lead"* (type: **gmail**)
  - **Credentials:** Chọn `"gmailOAuth2"` (đã cấu hình trước).
  - **Nội dung email:** Tùy chỉnh theo từng loại lead:
    - **Hot Lead:** Gửi **link đặt lịch hẹn**.
    - **Mid Lead:** Gửi **link WhatsApp pre-filled**.
    - **Cold Lead:** Gửi **email nurturing** với tài liệu hữu ích.

##### **C. Cấu hình Telegram (Thông Báo Team)**
- **Node:** *"Send a notification to the team"* (type: **telegram**)
  - **Credentials:** Chọn `"telegramApi"` (đã cấu hình trước).
  - **Thông báo mẫu:**
    ```plaintext
    "🚨 New Lead Alert: [Lead Name] - Score: [Hot/Mid/Cold]"
    ```

##### **D. Cấu hình Google Sheets (Lưu Lịch Sử)**
- **Node:** *"Log client data"* (type: **googleSheets**)
  - **Credentials:** Chọn `"googleSheetsOAuth2Api"`.
  - **Sheet Name:** Đảm bảo sheet đã tồn tại và có **cột phù hợp** (Lead Name, Score, Email, etc.).

#### **3. Kích hoạt ⚡️**
- **Test Run:** Nhấn **"Run Workflow"** với dữ liệu mẫu để kiểm tra.
- **Active Workflow:** Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack:** Thay vì Telegram, các sếp có thể gửi thông báo trên **Slack** bằng node `slack`.
2. **Lưu log hoạt động:** Sử dụng node `stickyNote` để ghi lại lịch sử lead và phân tích sau này.
3. **Gửi báo cáo định kỳ:** Tạo một workflow phụ để **tổng hợp và gửi báo cáo hàng tuần** về chất lượng lead.
4. **Tùy chỉnh email động:** Sử dụng **template email động** (n8n-nodes-base.email) để cá nhân hóa hơn.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **tăng doanh thu** thay vì làm việc thủ công. **Hãy áp dụng ngay** và xem cách AI Gemini giúp bạn **tự động hóa lead generation** một cách thông minh!

👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow từ n8n.io](https://n8n.io/workflows/15279)

---
**Cần hỗ trợ?** Liên hệ với tác giả:
📧 [gureyai2006@gmail.com](mailto:gureyai2006@gmail.com)
🌐 [Gurey AI](https://gurey-ai.vercel.app/)