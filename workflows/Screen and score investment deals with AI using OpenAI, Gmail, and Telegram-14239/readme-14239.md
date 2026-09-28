---
title: "🚀 Tự Động Học Đánh Giá & Lọc Giao Dịch Đầu Tư AI với OpenAI, Gmail & Telegram (N8N)"
description: "Workflow tự động hóa 100% không code để nhận, phân tích và đánh giá giao dịch đầu tư từ email hoặc webhook bằng trí tuệ nhân tạo, gửi kết quả qua Telegram và lưu vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/ngày trong việc sàng lọc lead đầu tư."
slug: "tieu-dong-hoa-danh-gia-giao-dich-dau-tu-ai"
tags: [n8n, automation, ai-summarization, lead-generation, openai, google-sheets, telegram-bot]
keywords: [n8n workflow đầu tư, tự động hóa sàng lọc giao dịch, AI đánh giá lead, OpenAI trong n8n, Telegram alert đầu tư]
---

# 🚀 **Tự Động Học Đánh Giá & Lọc Giao Dịch Đầu Tư với AI (N8N)**

### **Giải pháp cho các sếp đầu tư:**
Hàng ngày, các sếp phải mất **10+ giờ** để đọc email, đánh giá giao dịch đầu tư từ các lead, và quyết định xem liệu đó có phù hợp với chiến lược hay không. **Workflow này tự động hóa toàn bộ quy trình:**
- Nhận giao dịch từ **email** hoặc **form webhook**
- **Trích xuất thông tin chi tiết** bằng OpenAI (GPT-4o-mini)
- **Đánh giá theo 5 tiêu chí trọng lượng** (phù hợp ngành, doanh thu, tăng trưởng, đội ngũ, rõ ràng)
- **Phân loại tự động** (PASS, REVIEW, REJECT) và gửi **báo cáo Telegram** ngay lập tức
- **Lưu tất cả lịch sử** vào Google Sheets để theo dõi

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/ngày** trong việc sàng lọc lead thủ công
✅ **Đánh giá khách quan** dựa trên 5 tiêu chí AI (không bị ảnh hưởng cảm xúc)
✅ **Phân loại tự động** (PASS/REVIEW/REJECT) với độ chính xác cao
✅ **Báo cáo Telegram thực thời** để các sếp quyết định nhanh chóng
✅ **Lưu trữ lịch sử** trên Google Sheets để phân tích dài hạn
✅ **Hoàn toàn không cần code** – chỉ cần cấu hình các node
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Key:**
   - **Gmail** (để nhận email đầu tư)
   - **OpenAI API Key** (để sử dụng GPT-4o-mini)
   - **Telegram Bot Token** + **Chat ID** (để gửi báo cáo)
   - **Google Sheets** (để lưu lịch sử giao dịch)
   - **Header Auth** (nếu sử dụng webhook từ API/form)

2. **Google Sheets:**
   - Tạo một **bảng mới** với **tab "Deal Pipeline"** và các cột sau:
     ```
     Deal ID | Sender Email | Source | Timestamp | Company | Industry | Stage | Revenue | Ask (USD) | Team Size | Score | Verdict | Highlights | Red Flags
     ```

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14239](https://n8n.io/workflows/14239) hoặc copy/paste JSON từ trang này.
- Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Credentials (Bắt buộc)**
| Node | Tham số cần thay đổi | Ghi chú |
|------|----------------------|---------|
| **New Email Received** | Gmail | Chọn **Gmail** trong **Credentials** và cấp quyền cho n8n |
| **Deal Submission Webhook** | Header Auth | Thêm **Authorization Header** (nếu sử dụng API/form) |
| **Extract Deal Info - OpenAI** | OpenAI API Key | Điền **API Key** từ tài khoản OpenAI |
| **Score Deal - OpenAI** | OpenAI API Key | Cùng API Key như trên |
| **Telegram - PASS/REVIEW/REJECT** | Telegram Bot Token + Chat ID | Thay `YOUR_TELEGRAM_CHAT_ID` bằng **Chat ID** của bạn (tìm bằng `@username_to_chatbot` trên Telegram) |
| **Log Deal to Pipeline Sheet** | Google Sheets ID | Thay `YOUR_GOOGLE_SHEET_ID` bằng **ID Sheet** (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`) |

##### **B. Cấu hình Node Quá Trình**
1. **Normalize Email Data / Webhook Data**
   - Đảm bảo **các trường dữ liệu** (Company, Industry, Revenue, etc.) được trích xuất chính xác từ email/webhook.

2. **Build Deal Text**
   - Node **Code** này kết hợp tất cả thông tin thành **1 chuỗi text** cho AI xử lý. **Không cần chỉnh sửa** nếu dữ liệu đầu vào đầy đủ.

3. **Has Deal Content?**
   - Nếu **email/webhook trống**, workflow sẽ **dừng và báo lỗi** (node `Stop - No Deal Content`).

4. **Extract Deal Info - OpenAI**
   - **Prompt AI** đã được tối ưu để trích xuất:
     - Tên công ty, ngành nghề, giai đoạn, doanh thu, yêu cầu đầu tư, đội ngũ, điểm mạnh/điểm yếu.
   - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

5. **Score Deal - OpenAI**
   - **Prompt AI** đánh giá theo **5 tiêu chí trọng lượng**:
     - **Phù hợp ngành (30%)**
     - **Doanh thu (20%)**
     - **Tăng trưởng (20%)**
     - **Đội ngũ (15%)**
     - **Rõ ràng (15%)**
   - **Để PASS = 7.5+**, **REVIEW = 5-7.4**, **REJECT = <5**.
   - **Nếu muốn thay đổi tiêu chí**, chỉnh sửa **node `Score Deal`** (đi vào **Code** và sửa prompt).

6. **Telegram Alerts**
   - **Thay `YOUR_TELEGRAM_CHAT_ID`** trong **3 node Telegram** bằng **Chat ID** của bạn (tìm bằng cách gửi tin nhắn cho bot và lấy ID từ URL).

7. **Log Deal to Pipeline Sheet**
   - **Đảm bảo Sheet có đúng cột** (như mô tả ở trên).
   - **Operation = Append** để thêm mới mỗi giao dịch.

#### **3. Kích hoạt ⚡️**
- **Test Run** với **1 email mẫu** hoặc **gửi POST request** đến webhook để kiểm tra:
  ```json
  {
    "email": "test@example.com",
    "subject": "Investment Opportunity",
    "body": "Công ty ABC, ngành Tech, doanh thu 5M/year, yêu cầu 1M USD..."
  }
  ```
- Nếu **không lỗi**, bật **Active** workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thay Telegram bằng Slack/Email**
   - Thay node **Telegram** bằng **Slack Webhook** hoặc **Gmail Send Email** (n8n có node hỗ trợ).

2. **Lưu log chi tiết hơn**
   - Thêm **node `Set`** sau **Log Deal** để lưu **file đính kèm** (nếu có) vào Google Drive.

3. **Tích hợp với CRM**
   - Thay **Google Sheets** bằng **HubSpot, Salesforce** hoặc **Notion** (n8n có node hỗ trợ).

4. **Tự động gửi báo cáo hàng tuần**
   - Sử dụng **node `Schedule`** để gửi **báo cáo tổng hợp** qua Telegram/Email định kỳ.

5. **Cải thiện prompt AI**
   - Nếu muốn **AI đánh giá khác**, chỉnh sửa **prompt** trong node `Score Deal` (ví dụ: thêm tiêu chí mới như "sự bền vững").

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp đầu tư để tập trung vào **quyết định chiến lược** thay vì làm việc thủ công. **Chỉ cần 30 phút setup**, workflow sẽ **hoạt động tự động 24/7**, giúp:
✔ **Nhận và đánh giá giao dịch** ngay lập tức
✔ **Phân loại tự động** (PASS/REVIEW/REJECT)
✔ **Lưu trữ lịch sử** để phân tích dài hạn
✔ **Gửi báo cáo Telegram** để các sếp quyết định nhanh chóng

**🚀 Hãy import ngay và bắt đầu tự động hóa đầu tư của mình!**
Nếu có vấn đề, **liên hệ Devon Toh** qua [Calendly](https://cal.com/devon-toh-vrmdab/30min) để hỗ trợ chi tiết.

---
**#TựĐộngHóaĐầuTư #N8N #AIĐánhGiáLead #OpenAITrongN8N**