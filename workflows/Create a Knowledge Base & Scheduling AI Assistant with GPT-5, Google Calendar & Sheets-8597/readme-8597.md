---
title: "🤖 Tự Động Hóa Trợ Lý AI Tích Hợp GPT-5, Lịch Google & Google Sheets – Giải Pháp Chatbot Khôn Năng Cho Doanh Nghiệp"
description: "Workflow này tự động hóa quá trình trả lời câu hỏi khách hàng, kiểm tra sẵn sàng lịch và xác nhận lịch hẹn thông qua chatbot AI, tiết kiệm thời gian lên đến 80% và giảm thiểu lỗi thủ công. Sử dụng GPT-5, Google Sheets làm knowledge base và Google Calendar để quản lý lịch hẹn."
slug: "tieu-dong-hoa-tro-ly-ai-gpt5-google-calendar-sheets"
tags: [n8n, automation, ai-chatbot, google-sheets, google-calendar, gmail, langchain, no-code]
keywords: [n8n workflow tự động hóa, chatbot AI GPT-5, quản lý lịch hẹn tự động, knowledge base Google Sheets, tự động hóa doanh nghiệp]
---

# 🚀 **Tự Động Hóa Trợ Lý AI Tích Hợp GPT-5, Lịch & Email – Giải Pháp Chatbot Khôn Năng Cho Doanh Nghiệp**

## **🔥 Giới Thiệu: Tự Động Hóa Quá Trình Trả Lời Câu Hỏi & Lịch Hẹn**
Hiện nay, việc trả lời câu hỏi khách hàng, kiểm tra sẵn sàng lịch và xác nhận lịch hẹn thủ công không chỉ tốn thời gian mà còn dễ gây lỗi. **Workflow này tự động hóa toàn bộ quá trình** bằng cách kết hợp:
✅ **Trợ lý AI GPT-5** trả lời câu hỏi từ knowledge base (Google Sheets)
✅ **Kiểm tra sẵn sàng lịch** trên Google Calendar (theo múi giờ Paris)
✅ **Xác nhận & tạo lịch hẹn** tự động
✅ **Gửi email xác nhận** với chi tiết cuộc họp

Kết quả? **Tiết kiệm 80% thời gian, giảm thiểu sai sót và cải thiện trải nghiệm khách hàng!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động trả lời câu hỏi** từ knowledge base (FAQ, chính sách, sản phẩm) **không cần can thiệp thủ công**.
- **Kiểm tra sẵn sàng lịch** và đề xuất 3 slot thời gian thay thế nếu lịch đã bận.
- **Tạo lịch hẹn tự động** (1 giờ) và gửi email xác nhận chi tiết.
- **Hoạt động 24/7** mà không cần người dùng phải can thiệp.
- **Cá nhân hóa trải nghiệm** với AI hiểu ngữ cảnh và lịch sử chat.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản OpenAI** (API Key cho GPT-5) – [Đăng ký tại đây](https://platform.openai.com/api-keys)
✔ **Google Sheets** với knowledge base (cấu trúc mẫu [đây](https://docs.google.com/spreadsheets/d/1TIaqkiVRr-Z3VLC-mvXW2Ak1zO0becK1-wqcgVeop0E/copy))
✔ **Google Calendar** (để kiểm tra sẵn sàng lịch)
✔ **Gmail** (để gửi email xác nhận)
✔ **n8n Self-hosted** (để chạy workflow 24/7)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8597](https://n8n.io/workflows/8597) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấp vào "Import"** và chọn file JSON đã tải.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **9 node** chính, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🔹 Node 1: Chat with Your Data (chatTrigger)**
- **Chức năng**: Khởi động cuộc chat với AI.
- **Lưu ý**:
  - Đảm bảo **credentials** của node này được kết nối với **Google Sheets** (dùng `googleSheetsOAuth2Api`).
  - **Test run** bằng câu hỏi mẫu: *"Hỏi về dịch vụ đào tạo của công ty"*.

#### **🔹 Node 2: OpenAI GPT-5 Model (lmChatOpenAi)**
- **Chức năng**: Sử dụng mô hình GPT-5 để trả lời.
- **Cấu hình**:
  - Điền **API Key OpenAI** vào `openAiApi` (tạo trong **Credentials** của n8n).
  - Chọn mô hình: `gpt-5-mini` (nếu có).
  - **Test run** với câu hỏi: *"Làm thế nào để đăng ký khóa học?"*.

#### **🔹 Node 3: Knowledgebase Lookup (googleSheetsTool)**
- **Chức năng**: Tra cứu câu trả lời trong Google Sheets.
- **Cấu hình**:
  - Chọn **Sheet Name** (tên bảng chứa knowledge base).
  - **Range**: `Sheet1!A1:D100` (hoặc điều chỉnh theo cấu trúc mẫu).
  - **Test run** với câu hỏi: *"Công ty có hỗ trợ trả góp không?"*.

#### **🔹 Node 4: Calendar: Check Availability (googleCalendarTool)**
- **Chức năng**: Kiểm tra sẵn sàng lịch (theo múi giờ Paris).
- **Cấu hình**:
  - Chọn **credentials**: `googleCalendarOAuth2Api`.
  - **Time Zone**: `Europe/Paris`.
  - **Test run** với yêu cầu: *"Kiểm tra sẵn sàng lịch vào 10h sáng ngày mai"*.

#### **🔹 Node 5: Calendar: Create Appointment (googleCalendarTool)**
- **Chức năng**: Tạo lịch hẹn nếu khách hàng đồng ý.
- **Cấu hình**:
  - Chọn **credentials**: `googleCalendarOAuth2Api`.
  - **Duration**: `1h` (hoặc điều chỉnh).
  - **Test run** với yêu cầu: *"Tạo lịch hẹn vào 11h sáng"*.

#### **🔹 Node 6: Send Booking Confirmation (gmailTool)**
- **Chức năng**: Gửi email xác nhận chi tiết cuộc họp.
- **Cấu hình**:
  - Chọn **credentials**: `gmailOAuth2`.
  - **Template email**: Sử dụng mẫu đã chuẩn bị (có thể tùy chỉnh).
  - **Test run** với nội dung email mẫu.

#### **🔹 Node 7: AI Agent Support (agent) & Memory (memoryBufferWindow)**
- **Chức năng**: Quản lý logic chat và lưu trữ lịch sử.
- **Lưu ý**:
  - Node này tự động kết nối với các node khác, **không cần cấu hình thêm**.
  - **Test run** với cuộc chat mẫu để kiểm tra logic.

---
### **3. Kích Hoạt Workflow ⚡️**
- **Bật "Active"** trong n8n Editor.
- **Test run** với dữ liệu mẫu:
  1. Gửi câu hỏi: *"Hỏi về khóa học marketing"*.
  2. AI trả lời từ knowledge base.
  3. Nếu cần lịch hẹn, hệ thống sẽ tự động kiểm tra sẵn sàng và gửi email xác nhận.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết nối Slack/Telegram**: Thêm node `webhook` để nhận tin nhắn từ Slack/Telegram và chuyển sang AI.
- **Lưu log hoạt động**: Sử dụng node `stickyNote` để ghi lại lịch sử chat và lịch hẹn.
- **Báo cáo định kỳ**: Tạo workflow riêng gửi báo cáo tổng hợp lịch hẹn hàng tháng qua email.
- **Tích hợp CRM**: Kết nối với HubSpot/Zoho để lưu thông tin khách hàng vào hệ thống.
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại như trả lời FAQ, kiểm tra lịch và xác nhận hẹn. **Với AI GPT-5 và Google Sheets làm knowledge base**, hệ thống không chỉ nhanh chóng mà còn **cải thiện trải nghiệm khách hàng** một cách đáng kể.

**🚀 Hãy áp dụng ngay và tự động hóa doanh nghiệp của mình!**

---
### **🎁 Đăng ký VPS để chạy n8n 24/7**
:::info[HƯỚNG DẪN CÀI ĐẶT]
Để workflow hoạt động liên tục, các sếp nên **self-host n8n** trên VPS. Dưới đây là một số dịch vụ ưu đãi:
👉 **[TinoHost](https://tino.vn/vps-n8n?affid=388)** (Mã giảm giá: **VPSN8N** – giảm tới 39%)
👉 **[BNIX](https://my.bnix.one/aff.php?aff=172)** (VPS Xeon 4GB chỉ **50k/tháng**)
:::

---
### **📚 Tài Liệu Tham Khảo**
- [Tutorial chi tiết trên Notion](https://automatisation.notion.site/Build-Your-First-AI-Agent-with-ChatGPT-5-By-Dr-Firas-26f3d6550fd9801eb00dc0c578fc5f2c)
- [Mẫu knowledge base Google Sheets](https://docs.google.com/spreadsheets/d/1TIaqkiVRr-Z3VLC-mvXW2Ak1zO0becK1-wqcgVeop0E/copy)
- [Hướng dẫn cấu hình credentials](https://youtu.be/fDzVmdw7bNU)