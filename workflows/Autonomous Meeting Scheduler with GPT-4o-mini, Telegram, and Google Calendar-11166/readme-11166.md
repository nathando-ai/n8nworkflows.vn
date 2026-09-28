---
title: "🤖 Thư Viện AI Tự Động Hẹn Lịch Học Tập - GPT-4o-mini + Telegram + Google Calendar (100% Không Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp hẹn lịch họp, cuộc họp, hoặc học tập chỉ bằng cách nhắn tin Telegram - AI tự tìm kiếm thông tin, kiểm tra sẵn sàng lịch, và tạo sự kiện tự động trên Google Calendar. Giảm thời gian thủ công 90%!"
slug: "thu-vien-ai-tu-dong-hen-lich-gpt-4o-mini-telegram-google-calendar"
tags: [n8n, automation, ai-agent, telegram-bot, google-calendar, no-code, google-sheets, openai-gpt-4o-mini]
keywords: [n8n workflow tự động hóa, AI tự động hẹn lịch, Telegram bot tự động, Google Calendar API, tự động hóa cuộc họp, GPT-4o-mini cho doanh nghiệp, tự động hóa không code]
---

# 🚀 **AI Tự Động Hẹn Lịch - Thư Viện Tự Động Hóa Cuộc Học Tập & Hợp Tác**

### **📌 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- Nhắn tin với đồng nghiệp/khách hàng để hẹn lịch.
- Tra cứu thông tin liên lạc trong Google Sheets.
- Kiểm tra sẵn sàng lịch trên Google Calendar.
- Gửi email xác nhận và gửi link cuộc họp.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi AI có thể **giải quyết tất cả trong vài giây** chỉ bằng một tin nhắn!

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** trong việc hẹn lịch.
- **Tự động hóa hoàn toàn** từ nhận tin nhắn đến tạo sự kiện.
- **Tối ưu hóa lịch** bằng AI đề xuất thời gian phù hợp nhất.
- **Gửi email tự động** xác nhận cuộc họp cho cả hai bên.
- **Cập nhật liên tục** thông tin CRM từ Google Sheets.
- **Mở rộng khả năng** để tự động hóa các công việc khác (tư vấn, báo cáo, quản lý khách hàng...).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản Telegram** (để nhận tin nhắn từ người dùng).
2. **API Key OpenAI** (để sử dụng GPT-4o-mini).
3. **Google Sheets** (để lưu trữ danh sách CRM với cột: **Tên | Email | Số điện thoại**).
4. **Google Calendar** (để tạo sự kiện tự động).
5. **Tài khoản Gmail** (để gửi email xác nhận).
6. **VPS n8n** (để chạy workflow 24/7).

👉 **🎁 Mã giảm giá VPS n8n:**
👉 [Đăng ký VPS TinoHost (Mã: **VPSN8N** - giảm 39%)](https://tino.vn/vps-n8n?affid=388)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải workflow** từ [n8n.io/workflows/11166](https://n8n.io/workflows/11166).
- **Import vào n8n Editor** bằng cách:
  - Nhấn **Import** → Chọn file JSON.
  - Hoặc **copy/paste** JSON từ trang workflow vào Editor.

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**
Workflow này gồm **11 node** chính, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node 1: Telegram Trigger (n8n-nodes-base.telegramTrigger)**
- **Cấu hình:**
  - **Bot Token:** Lấy từ [@BotFather](https://t.me/BotFather) trên Telegram.
  - **Chat ID:** Để test, các sếp có thể gửi tin nhắn cho bot và sao chép `chat_id` từ URL khi nhấn vào tin nhắn.
  - **Trigger:** Chọn **"Message"** để bắt đầu workflow khi nhận tin nhắn.

#### **🔹 Node 2: Prepare Data (n8n-nodes-base.set)**
- **Không cần cấu hình thêm**, node này chỉ **tách dữ liệu** từ tin nhắn Telegram (text, chat_id, user_name).

#### **🔹 Node 3: Load CRM Data (n8n-nodes-base.googleSheets)**
- **Cấu hình:**
  - **Credentials:** Thêm **Google Sheets** vào n8n (cài đặt từ **Credentials → Add → Google Sheets**).
  - **Sheet Name:** Đặt tên là **"CRM"** (hoặc tên phù hợp).
  - **Range:** Chọn toàn bộ bảng (`"Sheet1!A:D"`).
  - **Format:** Đảm bảo cột **Tên, Email, Số điện thoại** được định dạng chính xác.

#### **🔹 Node 4: AI Agent (n8n-nodes-langchain.agent)**
- **Không cần cấu hình**, node này **tự động xử lý logic** dựa trên **system prompt** được cài đặt sẵn.
- **Lưu ý:** Nếu muốn **tùy chỉnh AI**, các sếp có thể chỉnh sửa **system prompt** trong node này để phù hợp với nhu cầu riêng.

#### **🔹 Node 5: OpenAI Model (n8n-nodes-langchain.lmChatOpenAi)**
- **Cấu hình:**
  - **API Key:** Điền **API Key OpenAI** (mua tại [openai.com](https://openai.com/)).
  - **Model:** Đặt là **`gpt-4o-mini`** (mô hình miễn phí, hiệu suất cao).
  - **Temperature:** Giữ mặc định (`0.7`) để AI không quá ngẫu nhiên.

#### **🔹 Node 6: Google Calendar Tool (n8n-nodes-base.googleCalendarTool)**
- **Cấu hình:**
  - **Credentials:** Thêm **Google Calendar** vào n8n (cài đặt từ **Credentials → Add → Google Calendar**).
  - **Authorization:** Đăng nhập và cấp quyền cho n8n truy cập.

#### **🔹 Node 7: CRM Search Tool (n8n-nodes-base.googleSheetsTool)**
- **Cấu hình:**
  - **Credentials:** Sử dụng cùng **Google Sheets** như Node 3.
  - **Range:** Chọn cùng **Sheet "CRM"** và cột tương ứng.

#### **🔹 Node 8: Send Response (n8n-nodes-base.telegram)**
- **Cấu hình:**
  - **Bot Token:** Điền lại **Bot Token** từ Node 1.
  - **Chat ID:** Sử dụng **`{{ $node["Prepare Data"].json["chatId"] }}`** để tự động trả lời tin nhắn.

#### **🔹 Node 9: Should Create Event? (n8n-nodes-base.if)**
- **Không cần cấu hình**, node này **kiểm tra điều kiện** để tạo sự kiện nếu AI xác nhận.

#### **🔹 Node 10: Create Calendar Event (n8n-nodes-base.googleCalendar)**
- **Cấu hình:**
  - **Credentials:** Sử dụng **Google Calendar** như Node 6.
  - **Summary:** Đặt tên sự kiện (ví dụ: **"Cuộc họp với {{ $node["AI Agent"].json["contactName"] }}"**).
  - **Start Time & End Time:** AI sẽ tự động đề xuất thời gian.

#### **🔹 Node 11: Send Confirmation Email (n8n-nodes-base.gmail)**
- **Cấu hình:**
  - **Credentials:** Thêm **Gmail** vào n8n (cài đặt từ **Credentials → Add → Gmail**).
  - **To:** Điền **`{{ $node["AI Agent"].json["attendeeEmail"] }}`** (email của người tham gia).
  - **Subject:** **"Xác nhận cuộc họp với {{ $node["AI Agent"].json["contactName"] }}"**.
  - **Body:** Thể hiện nội dung email tự động (có thể tùy chỉnh).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với tin nhắn mẫu:
   - Gửi tin nhắn Telegram: **"Hẹn lịch họp với Anna vào thứ Sáu"**.
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active** workflow để nó hoạt động liên tục.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH MỞ RỘNG TỐI ĐA]
1. **Thêm Slack/Telegram Notifications:**
   - Sử dụng **node Slack** hoặc **Telegram** để gửi thông báo khi AI tạo sự kiện thành công.

2. **Lưu Log Tất Cả Cuộc Hẹn:**
   - Thêm **node Google Sheets** để ghi lại lịch sử cuộc họp (ngày, giờ, người tham gia, trạng thái).

3. **Gửi Báo Cáo Tuần/Tháng:**
   - Sử dụng **node Google Sheets** + **node Gmail** để tự động gửi báo cáo tổng hợp lịch họp.

4. **Tùy Chỉnh AI Cho Nhiều Dịch Vụ:**
   - Chỉnh sửa **system prompt** trong **AI Agent** để AI có thể:
     - **Tự động tạo hóa đơn** từ Google Sheets.
     - **Trả lời tin nhắn khách hàng** tự động.
     - **Tổng hợp báo cáo** từ nhiều nguồn dữ liệu.

5. **Sử Dụng GPT-4o (Nếu Có Ngân Sách):**
   - Thay thế **gpt-4o-mini** bằng **gpt-4o** để AI hiểu và xử lý logic phức tạp hơn.
:::

---
## **📌 Kết Luận**
Workflow này không chỉ **giải phóng thời gian** cho các sếp mà còn **mở ra vô số khả năng tự động hóa** cho doanh nghiệp. Từ **hẹn lịch** đến **quản lý khách hàng**, **tự động hóa cuộc họp**, **tư vấn AI**, tất cả đều có thể được thực hiện **chỉ bằng một tin nhắn**.

**🚀 Hành động ngay:**
1. **Cài đặt VPS n8n** (đăng ký với mã **VPSN8N** để giảm chi phí).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với tin nhắn mẫu** và bắt đầu tự động hóa!

**💡 Lưu ý:** Nếu muốn **tùy chỉnh AI** để phù hợp với ngành nghề riêng, các sếp có thể chỉnh sửa **system prompt** trong **AI Agent** để AI hiểu rõ hơn về **ngôn ngữ và quy trình** của doanh nghiệp.

---
**🔥 Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa công việc!** 🚀