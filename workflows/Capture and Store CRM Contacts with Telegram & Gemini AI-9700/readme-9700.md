---
title: "🤖 **Tự Động Hóa CRM Từ Telegram + Gemini AI: Nhập Liêu Tín Thông Tin Khách Hàng Mới Với Chatbot 24/7**"
description: "Workflow này tự động hóa việc thu thập, phân tích và lưu trữ thông tin khách hàng từ Telegram (text, voice, ảnh business card) vào Google Sheets (hoặc CRM thực tế) với sự trợ giúp của Gemini AI. Giúp các sếp tiết kiệm 10+ giờ/ngày so với cách làm thủ công."
slug: "tieu-dong-hoa-crm-tu-telegram-voi-gemini-ai"
tags: [n8n, automation, crm, ai-agent, telegram-bot, google-sheets, gemini-ai]
keywords: [tự động hóa CRM Telegram, chatbot thu thập khách hàng, Gemini AI n8n, lưu trữ thông tin khách hàng tự động, workflow n8n CRM]
---

# 🚀 **Chatbot Telegram + Gemini AI: Thu Thập & Lưu Trữ CRM Khách Hàng Mới 100% Tự Động**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Ghi chép thủ công** thông tin khách hàng từ cuộc gọi, tin nhắn, hoặc ảnh business card.
- **Tìm kiếm trùng lặp** thông tin khách hàng trong CRM, tốn thời gian và dễ bỏ sót.
- **Phân tích dữ liệu** từ voice note hoặc ảnh để trích xuất thông tin chính xác.
- **Cập nhật CRM** sau mỗi cuộc gặp, dẫn đến sai sót và mất mát cơ hội.

**Giải pháp?** Một **chatbot Telegram + Gemini AI** tự động:
✅ **Trích xuất** thông tin từ text, voice, hoặc ảnh business card.
✅ **Xác minh trùng lặp** khách hàng dựa trên email/phone.
✅ **Cập nhật CRM** (Google Sheets hoặc CRM thực tế) một cách chính xác.
✅ **Hỏi lại** nếu thiếu thông tin quan trọng.
✅ **Lưu trữ** lịch sử cuộc hội thoại để tiếp tục sau.

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/ngày** so với cách làm thủ công.
- **Chính xác 100%** với AI Gemini phân tích text/voice/ảnh.
- **Không trùng lặp** khách hàng nhờ kiểm tra email/phone.
- **Hoạt động liên tục** 24/7, không cần can thiệp.
- **Dễ dàng mở rộng** sang CRM thực tế (HubSpot, Pipedrive...).
- **Tích hợp Telegram** để thu thập dữ liệu từ mọi nơi.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                          | **Hướng Dẫn**                                                                 |
|---------------------------|--------------------------------------------------|-------------------------------------------------------------------------------|
| **Telegram Bot**          | Token Bot (tạo từ [@BotFather](https://t.me/BotFather)) | [Hướng dẫn tạo bot Telegram](https://docs.n8n.io/integrations/builtin/credentials/telegram/) |
| **Google Gemini API**      | API Key (tạo từ [Google Cloud](https://aistudio.google.com/)) | [Cài đặt API Key Gemini](https://developers.generativeai.google/)              |
| **Google Sheets**         | File Google Sheets với cột: **Full name, Email, Phone, Company, Job title, Meeting notes** | [Tạo file mẫu](https://docs.google.com/spreadsheets/d/1...) (sẽ được hướng dẫn chi tiết) |
| **VPS (n8n Self-hosted)** | Máy chủ 2GB+ RAM (gợi ý VPS TinoHost/Xeon)       | [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/self-hosted/)               |

### **2. Cấu Hình Trước Khi Import**
- **Tạo bot Telegram** và lấy **Token**.
- **Tạo file Google Sheets** với cấu trúc cột chuẩn.
- **Cấu hình credentials** trong n8n:
  - `telegramApi` (dùng cho Telegram Trigger & Send Message).
  - `googleApi` (dùng cho Google Sheets).
  - `googlePalmApi` (dùng cho Gemini AI).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/9700](https://n8n.io/workflows/9700) (chọn **Export JSON**).
2. **Mở n8n Editor** → **Import** → Chọn file JSON vừa tải.
3. **Xác nhận import** và workflow sẽ hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → **Create Workflow** → **Import from JSON**.
3. **Dán JSON** và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **22 node** phức tạp, các sếp cần **cấu hình chính xác** các node sau:

#### **🔹 Node "Telegram Trigger" (Bắt đầu workflow)**
- **Credentials**: Chọn `telegramApi` (đã cấu hình Token).
- **Webhook URL**: Sau khi import, **copy URL** từ node này và **set webhook** cho bot Telegram:
  ```bash
  curl -X POST "https://api.telegram.org/bot{TOKEN}/setWebhook?url={WEBHOOK_URL}"
  ```
  *(Thay `{TOKEN}` và `{WEBHOOK_URL}` bằng giá trị thực tế.)*

#### **🔹 Node "parameters" (Cấu hình Google Sheets)**
- **Spreadsheet ID**: Lấy từ **URL Google Sheets** (phần sau `/d/`).
  Ví dụ: `https://docs.google.com/spreadsheets/d/1ABC123.../edit` → **ID = `1ABC123...`**.
- **Sheet Name**: Tên sheet (mặc định là `Sheet1`).

#### **🔹 Node "Search for contact" (Kiểm tra trùng lặp)**
- **Query**: Cấu hình để tìm kiếm theo **email** hoặc **phone**.
  *(N8n sẽ tự động cập nhật logic này khi import.)*

#### **🔹 Node "AI Agent" (Gemini AI)**
- **Credentials**: Chọn `googlePalmApi` (API Key Gemini).
- **Prompt**: Workflow đã cấu hình sẵn, **không cần chỉnh sửa** trừ khi cần tùy biến.

#### **🔹 Node "Create new contact" & "Update existing contact"**
- **Credentials**: Chọn `googleApi` (Google Sheets).
- **Operation**:
  - `Create new contact` → **Append** (thêm mới).
  - `Update existing contact` → **AppendOrUpdate** (cập nhật).

#### **🔹 Node "Transcribe audio" & "Analyze image"**
- **Credentials**: Chọn `googlePalmApi`.
- **Resource**:
  - **Audio**: Chọn file voice note từ Telegram.
  - **Image**: Chọn ảnh business card từ Telegram.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn **text**, **voice**, hoặc **ảnh business card** đến bot Telegram.
   - Bot sẽ **trích xuất thông tin**, **hỏi lại nếu thiếu**, và **hiển thị kết quả**.
2. **Bật Active**:
   - Nhấn **Active** trên canvas n8n.
   - **Kiểm tra log** để đảm bảo workflow chạy bình thường.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp CRM Thực Tế**
- Thay thế **Google Sheets** bằng **HubSpot, Pipedrive, Monday** bằng cách:
  - Thêm node **HubSpot API** hoặc **Pipedrive API**.
  - Cấu hình **credentials** tương ứng.

### **2. Lưu Log & Báo Cáo**
- Thêm node **Google Drive** hoặc **Email** để lưu **log hoạt động** của bot.
- **Ví dụ**:
  - Sau khi lưu CRM thành công, bot gửi **email báo cáo** cho team.

### **3. Tùy Chỉnh Prompt AI**
- Nếu muốn **Gemini AI** phân tích chi tiết hơn, chỉnh sửa **prompt** trong node `AI Agent`:
  ```json
  {
    "prompt": "Extract full name, email, phone, company, and job title from the following text: {input}"
  }
  ```

### **4. Tích Hợp Slack/Telegram Cảnh Báo**
- Thêm node **Slack** hoặc **Telegram** để **cảnh báo** khi có khách hàng mới được lưu.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng chính xác** với AI Gemini, và **mở rộng khả năng** với CRM thực tế. **Chỉ cần 30 phút setup**, bot sẽ **hoạt động tự động** 24/7!

**🚀 Hành động ngay:**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình Telegram + Google Sheets** theo yêu cầu.
3. **Test với dữ liệu mẫu** và **bật Active**.
4. **Tích hợp CRM** nếu cần nâng cao.

**💡 Lưu ý cuối cùng:**
- Nếu gặp vấn đề, **check log** trong n8n và **cập nhật credentials**.
- **Tùy biến prompt** để phù hợp với ngành nghề của doanh nghiệp.

**Chúc các sếp thành công!** 🎉