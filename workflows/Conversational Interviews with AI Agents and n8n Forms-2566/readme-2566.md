---
title: "🤖 Tự Động Hóa Phỏng Vấn AI Tự Động Với n8n Forms & Agent: Giải Pháp Phỏng Vấn Không Cần Code"
description: "Workflow này tự động hóa quy trình phỏng vấn AI thông minh bằng n8n Forms và AI Agent, ghi lại tất cả câu hỏi và trả lời vào Google Sheets, giúp tiết kiệm thời gian và cải thiện chất lượng phân tích. Đặc biệt phù hợp cho nghiên cứu thị trường, feedback sản phẩm hoặc phỏng vấn khách hàng."
slug: "tieu-dong-hoa-phong-van-ai-voi-n8n-forms"
tags: [n8n, automation, ai-agent, no-code, google-sheets, redis, langchain]
keywords: [n8n workflow phỏng vấn AI, tự động hóa phỏng vấn, AI Agent n8n, lưu trữ phỏng vấn vào Google Sheets, tự động hóa nghiên cứu thị trường]
---

# 🚀 **Tự Động Hóa Phỏng Vấn AI Tự Động Với n8n Forms & Agent: Giải Pháp Không Cần Code**

### **Giải pháp cho những ai đang gặp khó khăn trong:**
- **Phỏng vấn khách hàng/người dùng:** Tốn thời gian chuẩn bị, điều phối và ghi chép.
- **Nghiên cứu thị trường:** Khó khăn trong việc thu thập và phân tích phản hồi.
- **Feedback sản phẩm:** Cần nhiều nguồn dữ liệu để đánh giá khách quan.

Workflow này **tự động hóa toàn bộ quy trình phỏng vấn** bằng AI Agent thông minh, ghi lại tất cả câu hỏi và trả lời vào **Google Sheets**, giúp bạn **tiết kiệm thời gian, tăng chính xác và cá nhân hóa** mỗi cuộc phỏng vấn.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Không cần điều phối viên phỏng vấn, AI tự động hỏi và ghi lại.
✅ **Chất lượng cao:** AI Agent đặt câu hỏi mở và theo dõi logic, giúp thu thập thông tin sâu sắc.
✅ **Lưu trữ tự động:** Tất cả dữ liệu được ghi vào **Google Sheets** cho phân tích dễ dàng.
✅ **Hoạt động 24/7:** Khách hàng có thể trả lời bất kỳ lúc nào, không giới hạn thời gian.
✅ **Cá nhân hóa:** AI thích ứng với từng người dùng, tạo trải nghiệm phỏng vấn tốt hơn.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
- **Tài khoản n8n Self-hosted** (không dùng n8n Cloud vì cần Redis và Webhook riêng).
- **Tài khoản Google Sheets** (để lưu trữ kết quả phỏng vấn).
- **API Key Groq** (để sử dụng mô hình AI `llama-3.2-90b-text-preview`).
- **Redis (Upstash hoặc Redis tự host)** để lưu trữ phiên phỏng vấn.
- **Domain hoặc URL riêng** (để tạo Webhook và trang hoàn thành phỏng vấn).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2566) hoặc copy toàn bộ JSON từ [GitHub](https://github.com/n8n-io/workflows/tree/main/workflows/2566).
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các bước cấu hình BẮT BUỘC**
Workflow này có **30 node**, nhưng chỉ cần chú ý đến các node quan trọng sau:

#### **🔹 Node 1: Cấu hình Redis (Upstash/Redis tự host)**
- **Tại node `Create Session` và `Update Session`:**
  - Đăng ký tài khoản **Upstash Redis** (miễn phí) hoặc tự host Redis.
  - Thêm **credentials Redis** trong **n8n Credentials Manager** (Settings → Credentials → Add → Redis).
  - Điền **URL Redis** và **Password** (nếu có).

#### **🔹 Node 2: Cấu hình Groq API**
- **Tại node `Groq Chat Model`:**
  - Đăng ký tài khoản **Groq** và lấy **API Key**.
  - Thêm **credentials `groqApi`** trong n8n (Settings → Credentials → Add → API → Groq).
  - Điền **API Key** và chọn mô hình `llama-3.2-90b-text-preview`.

#### **🔹 Node 3: Cấu hình Google Sheets**
- **Tại node `Save to Google Sheet`:**
  - Tạo một **Google Sheet mới** và chia sẻ cho tài khoản n8n (nếu dùng OAuth2).
  - Thêm **credentials `googleSheetsOAuth2Api`** trong n8n (Settings → Credentials → Add → Google Sheets).
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).

#### **🔹 Node 4: Cấu hình Webhook (để hiển thị kết quả phỏng vấn)**
- **Tại node `Webhook`:**
  - Nếu dùng **n8n Self-hosted**, Webhook URL sẽ tự động tạo (ví dụ: `https://tên-domain.com/ai-interview-transcripts/:session_id`).
  - **Lưu ý:** Cần **domain riêng** để Webhook hoạt động (không dùng n8n Cloud).
  - **Để hiển thị trang kết quả:**
    - Sau khi phỏng vấn kết thúc, người dùng sẽ được chuyển đến URL Webhook này.
    - Node `Show Transcript` sẽ hiển thị toàn bộ cuộc phỏng vấn.

#### **🔹 Node 5: Cấu hình Form Trigger (để bắt đầu phỏng vấn)**
- **Tại node `Start Interview`:**
  - Thêm **credentials `formTrigger`** (nếu cần).
  - Cấu hình **form fields** (ví dụ: yêu cầu người dùng nhập **tên** trước khi bắt đầu).

---
### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Nhấn **Run Workflow** với dữ liệu mẫu (ví dụ: nhập tên `Test User`).
   - Kiểm tra **Google Sheets** xem liệu dữ liệu có được ghi lại không.
   - Kiểm tra **Redis** xem liệu phiên có được lưu trữ không.

2. **Bật Active:**
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi báo cáo tự động:** Sau khi phỏng vấn kết thúc, gửi email hoặc Slack thông báo kết quả.
- **Lưu log vào Google Drive:** Thay vì chỉ lưu vào Sheets, có thể lưu toàn bộ phiên vào Google Drive.
- **Kết hợp với CRM:** Gửi dữ liệu phỏng vấn vào **HubSpot, Salesforce** hoặc **Notion**.
- **Tích hợp với AI Chatbot:** Cho phép người dùng bắt đầu phỏng vấn qua **Slack/Telegram**.
- **Phân tích tự động:** Sử dụng **Google Apps Script** để phân tích dữ liệu trong Sheets.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc phỏng vấn thủ công**, giúp **tự động hóa toàn bộ quy trình** từ đặt câu hỏi đến lưu trữ dữ liệu. Đặc biệt phù hợp cho:
✔ **Nhà nghiên cứu thị trường** (thu thập feedback nhanh chóng).
✔ **Doanh nghiệp sản phẩm** (phân tích phản hồi khách hàng).
✔ **Nhóm phát triển sản phẩm** (hiểu rõ nhu cầu người dùng).

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho đội ngũ của bạn!**

---
### **🔗 Tài liệu tham khảo**
- [Bài viết chi tiết trên n8n Community](https://community.n8n.io/t/build-your-own-ai-interview-agents-with-n8n-forms/62312)
- [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1wKjVdm7HeufJkHrUJn_bW9bFI_blm0laoI_jgXKDe0Q/edit?usp=sharing)
- [Upstash Redis (miễn phí)](https://upstash.com/)

---
### **🎁 Đăng ký VPS cho n8n Self-hosted**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Happy Automating!** 🤖💻