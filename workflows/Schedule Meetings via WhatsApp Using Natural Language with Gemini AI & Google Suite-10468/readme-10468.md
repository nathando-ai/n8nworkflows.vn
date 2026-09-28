---
title: "🤖 **Tự Động Hóa Lịch Hẹn Qua WhatsApp Với AI Gemini & Google Suite – Không Cần Code!**"
description: "Workflow này chuyển đổi tin nhắn WhatsApp thành trợ lý lịch hẹn thông minh, tự động hiểu yêu cầu người dùng (ví dụ: 'hẹn cuộc họp với John vào 10h sáng mai'), tra cứu thông tin liên lạc từ Google Sheets, kiểm tra lịch trùng lặp trên Google Calendar, và thực hiện tạo/sửa/xóa lịch một cách hoàn toàn tự động. Giúp tiết kiệm thời gian lên đến 80% cho việc quản lý lịch hẹn."
slug: "tu-dong-hoa-lich-hen-whatsapp-ai-gemini-google-suite"
tags: [n8n, automation, ai-chatbot, google-calendar, google-sheets, whatsapp-business, no-code]
keywords: [tự động hóa lịch hẹn WhatsApp, AI Gemini n8n, tự động hóa Google Calendar, chatbot lịch hẹn tự động, tự động hóa WhatsApp Business, tự động hóa quản lý cuộc họp]
---

# 🚀 **Trợ Lý Lịch Hẹn AI Qua WhatsApp – Tự Động Hóa 100% Với n8n**

### **Nỗi Đau Của Các Sếp Khi Quản Lý Lịch Hẹn**
Hàng ngày, các sếp và nhân viên phải mất **giờ đồng hồ** để:
- **Trao đổi qua WhatsApp** để xác nhận thời gian, địa điểm, và danh sách người tham gia.
- **Sửa đổi lịch** khi có yêu cầu mới, dẫn đến rủi ro **trùng lịch** và mất thời gian theo dõi.
- **Gửi thông báo nhắc nhở** thủ công, dễ bị quên hoặc trễ.
- **Tra cứu thông tin liên lạc** của đối tác, khách hàng từ nhiều nguồn khác nhau.

**Kết quả?** Lịch hẹn trở thành **nỗi ám ảnh**, làm gián đoạn công việc chính và gây mất hiệu quả.

---
### **🎯 Kết Quả Các Sếp Nhận Được Khi Sử Dụng Workflow Này**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết Kiệm 80% Thời Gian** – Không cần trao đổi lại qua lại, AI tự động hiểu và thực hiện yêu cầu.
✅ **Tránh Trùng Lịch & Lỗi Sửa Đổi** – Kiểm tra lịch Google Calendar trước khi tạo sự kiện mới.
✅ **Cá Nhân Hóa & Dễ Dàng** – AI hiểu ngôn ngữ tự nhiên (ví dụ: *"Hẹn lại cuộc họp với team vào thứ 4 tuần sau"*).
✅ **Hoạt Động 24/7** – Không cần người hỗ trợ, tự động gửi xác nhận qua WhatsApp và email.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tài Khoản WhatsApp Business API** (đăng ký tại [Meta Developer Portal](https://developers.facebook.com/)).
- **Tài Khoản Google** (để kết nối với **Google Calendar** và **Google Sheets**).
- **Google Sheets** chứa danh sách liên lạc (cấu trúc chi tiết sau).
- **API Key của Google Gemini** (miễn phí, đăng ký tại [Google AI Studio](https://aistudio.google/)).
- **n8n Self-hosted** (để chạy 24/7, không phụ thuộc vào phiên bản cloud).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/10468](https://n8n.io/workflows/10468) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create a new workflow** và nhấn **Import**.

#### **Phương Pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/10468](https://n8n.io/workflows/10468) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán mã.
3. Chọn **Create a new workflow** và nhấn **Import**.

---
### **2. Các Bước Cấu Hình BẮT BUỘC (Không Thể Bỏ Qua!)**

#### **📌 Node 1: WhatsApp Trigger (n8n-nodes-base.whatsAppTrigger)**
- **Cấu hình:**
  - **Webhook URL**: Điền URL Webhook từ WhatsApp Business API (thường là `https://<your-n8n-server>/whatsapp/webhook`).
  - **Phone Number ID**: ID của số điện thoại WhatsApp đã đăng ký (tìm trong **Meta Developer Portal**).
  - **Test**: Gửi tin nhắn mẫu (ví dụ: *"Hẹn cuộc họp với Ali vào 10h sáng mai"*) để kiểm tra.

#### **📌 Node 2: Contacts Data (n8n-nodes-base.googleSheetsTool)**
- **Cấu hình:**
  - **Google Sheets ID**: ID của bảng Google Sheets chứa danh sách liên lạc (tìm trong URL của sheet, ví dụ: `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/` → **1AbCdEfGhIjKlMnOpQrStUvWxYz**).
  - **Tab Name**: Tên tab chứa dữ liệu (ví dụ: `Contacts`).
  - **Range**: `Sheet1!A:D` (giả sử cột A: Tên, B: Email, C: Loại, D: Số điện thoại).
  - **Mẫu dữ liệu:**
    | **Name**       | **Email**               | **Type**   | **Phone**       |
    |----------------|-------------------------|------------|-----------------|
    | Ali Zubair     | ali@example.com         | Client     | 0123456789      |
    | John Doe       | john@example.com        | Partner    | 0987654321      |

#### **📌 Node 3: Google Calendar (n8n-nodes-base.googleCalendarTool)**
- **Cấu hình:**
  - **Google Account**: Kết nối tài khoản Google đã đăng ký.
  - **Calendar ID**: Chọn **Calendar chính** (ví dụ: `primary` hoặc email của bạn).
  - **Test**: Kiểm tra node **Get_Events** có lấy được lịch hiện tại không.

#### **📌 Node 4: Google Gemini Chat Model (n8n-nodes-langchain.lmChatGoogleGemini)**
- **Cấu hình:**
  - **API Key**: Điền **API Key** từ Google AI Studio.
  - **Model**: Chọn `gemini-pro` (mô hình miễn phí).
  - **Test**: Gửi yêu cầu mẫu (ví dụ: *"Hãy hiểu yêu cầu: 'Hẹn lại cuộc họp với John vào thứ 4 tuần sau'"*) để kiểm tra AI có phản hồi chính xác không.

#### **📌 Node 5: Các Agent AI (n8n-nodes-langchain.agent)**
- **Cấu hình chung:**
  - **System Prompt**: Các sếp có thể chỉnh sửa **system message** trong mỗi agent (Intent Agent, Correction Agent, Calendar Agent) để phù hợp với ngữ cảnh công việc.
  - **Ví dụ chỉnh sửa:**
    ```json
    {
      "role": "system",
      "content": "Bạn là trợ lý lịch hẹn chuyên nghiệp. Hãy hiểu yêu cầu người dùng và trả lời bằng tiếng Việt chính xác."
    }
    ```

#### **📌 Node 6: WhatsApp Send & Wait (n8n-nodes-base.whatsApp)**
- **Cấu hình:**
  - **Phone Number ID**: Điền ID số điện thoại WhatsApp (giống như ở **WhatsApp Trigger**).
  - **Test**: Gửi tin nhắn mẫu để kiểm tra AI có phản hồi tự động không.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với tin nhắn mẫu:
   - Gửi tin nhắn: *"Hẹn cuộc họp với Ali vào 10h sáng mai"*.
   - Kiểm tra:
     - AI có hiểu yêu cầu không?
     - Lịch có được tạo trên Google Calendar không?
     - Tin nhắn xác nhận có được gửi về WhatsApp không?
2. **Bật Active**: Sau khi test thành công, nhấn **Active** để workflow chạy liên tục.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Slack/Telegram**
- **Cách làm:**
  - Thêm node **Slack** hoặc **Telegram Bot** vào workflow để gửi thông báo về kênh nhóm.
  - **Lợi ích:** Giúp team theo dõi lịch hẹn một cách dễ dàng.

### **2. Lưu Log & Báo Cáo Định Kỳ**
- **Cách làm:**
  - Thêm node **Google Sheets** hoặc **Google Drive** để lưu lịch sử cuộc họp.
  - **Lợi ích:** Dễ dàng tra cứu và báo cáo cho quản lý.

### **3. Chuyển Đổi Thời Gian Giờ**
- **Cách làm:**
  - Sử dụng node **Code** để chuyển đổi giờ từ UTC sang giờ địa phương của khách hàng.
  - **Lợi ích:** Tránh nhầm lẫn về thời gian giữa các khu vực khác nhau.

### **4. Hỗ Trợ Cuộc Họp Lặp Lại**
- **Cách làm:**
  - Chỉnh sửa **system prompt** của **Calendar Agent** để hỗ trợ lịch hẹn định kỳ (ví dụ: *"Họp hàng tuần thứ 2"*).
  - **Lợi ích:** Tiết kiệm thời gian cho các cuộc họp định kỳ.

---
## **📌 Kết Luận: Tự Động Hóa Lịch Hẹn – Không Cần Code!**

Workflow này **giải phóng thời gian** cho các sếp và nhân viên khỏi công việc nhắc nhở, sửa đổi lịch, và tra cứu liên lạc. **AI Gemini** hiểu ngôn ngữ tự nhiên, **Google Calendar** tránh trùng lịch, và **WhatsApp** giữ mọi người đồng bộ.

**👉 Hãy áp dụng ngay để:**
✔ **Tiết kiệm 80% thời gian** quản lý lịch.
✔ **Tránh lỗi trùng lịch** và mất thời gian theo dõi.
✔ **Cung cấp trải nghiệm cá nhân hóa** cho khách hàng và đối tác.

---
### **🔗 Tài Nguyên Tham Khảo**
- [Đăng ký WhatsApp Business API](https://developers.facebook.com/)
- [Google AI Studio (Gemini API)](https://aistudio.google/)
- [TinoHost VPS cho n8n Self-hosted](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N**)

**🚀 Bắt đầu tự động hóa ngay hôm nay!**