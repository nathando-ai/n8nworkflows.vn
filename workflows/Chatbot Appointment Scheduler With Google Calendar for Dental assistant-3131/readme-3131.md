---
title: "🦷 Tự Động Hóa Lịch Hẹn Khám Răng Cho Nhân Viên Y Tế Với Chatbot & Google Calendar (N8n + AI)"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp nhân viên y tế (dental assistant) nhận lịch hẹn từ khách hàng qua chatbot, kiểm tra sẵn sàng lịch trên Google Calendar và tự động cập nhật vào Google Sheets. Tiết kiệm 80% thời gian quản lý lịch!"
slug: "tieu-dong-hoa-lich-hem-kham-rang-voi-chatbot-google-calendar"
tags: [n8n, automation, ai, google-calendar, google-sheets, dental-assistant]
keywords: [tự động hóa lịch hẹn khám răng, chatbot n8n, google calendar tự động, tự động hóa y tế, n8n workflow ai]
---

# 🦷 **Tự Động Hóa Lịch Hẹn Khám Răng Cho Nhân Viên Y Tế Với Chatbot & Google Calendar**

### 📌 **Nỗi Đau Của Nhân Viên Y Tế**
Hàng ngày, nhân viên y tế (dental assistant) phải:
- **Nhận hàng chục tin nhắn** từ khách hàng muốn đặt lịch khám răng qua Facebook, Telegram hay Zalo.
- **Tra cứu sẵn sàng lịch** trên Google Calendar để tránh trùng lịch.
- **Ghi chép thủ công** thông tin lịch vào Google Sheets hoặc Excel.
- **Gọi điện xác nhận** với khách hàng, tốn thời gian và dễ lỡ lịch.

**Kết quả?** Thời gian quản lý lịch chiếm **30-50% thời gian làm việc**, dẫn đến **sự chậm trễ, sai sót và mất hài lòng khách hàng**.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quá trình đặt lịch**: Khách hàng chỉ cần chat với bot, hệ thống tự xử lý.
- **Kiểm tra sẵn sàng lịch ngay lập tức**: Không cần gọi điện xác nhận, tránh trùng lịch.
- **Cập nhật tự động vào Google Sheets**: Dữ liệu lịch được ghi chép chính xác, không mất thời gian nhập liệu.
- **Hoạt động 24/7**: Khách hàng có thể đặt lịch bất kỳ thời gian nào, kể cả đêm.
- **Tiết kiệm thời gian**: Giảm **80% công việc quản lý lịch**, tăng hiệu suất làm việc.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (đã kết nối với OAuth 2.0).
2. **Tài khoản Google Sheets** (bảng dữ liệu để lưu lịch hẹn).
3. **API Key OpenAI** (để sử dụng mô hình AI `gpt-4o-mini`).
4. **Dịch vụ chatbot** (Facebook Messenger, Telegram, Zalo, hoặc Webhook tùy chọn).
5. **Session ID** (để lưu trữ lịch sử chat giữa bot và khách hàng).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3131) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô nhập.
  3. Chọn **Create Workflow** để tạo mới.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **7 node** chính. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **🔹 Node 1: When Chat Message Received (chatTrigger)**
- **Chức năng**: Nhận tin nhắn từ khách hàng qua chatbot (Facebook, Telegram, Zalo, hoặc Webhook).
- **Cấu hình**:
  - Chọn **Source** (nguồn chatbot) phù hợp (ví dụ: Facebook Messenger).
  - **Lưu ý**: Nếu sử dụng Webhook, cần cài đặt URL Webhook trong dịch vụ chatbot.

##### **🔹 Node 2: AI Agent (agent)**
- **Chức năng**: Xử lý logic chatbot dựa trên **Prompt** đã định sẵn.
- **Cấu hình**:
  - **Prompt mặc định** đã được thiết lập, chỉ cần **điền thông điệp của khách hàng** vào biến `{{$json.message}}`.
  - **Ví dụ Prompt**:
    ```
    Bạn là một trợ lý y tế chuyên nghiệp. Hãy giúp khách hàng đặt lịch khám răng.
    - Nếu khách hàng muốn đặt lịch: Hỏi ngày giờ ưa thích và kiểm tra sẵn sàng lịch.
    - Nếu khách hàng muốn hủy lịch: Xóa lịch trong Google Calendar và Google Sheets.
    - Hãy trả lời bằng tiếng Việt và giữ thái độ thân thiện.
    ```

##### **🔹 Node 3: OpenAI Chat Model (lmChatOpenAi)**
- **Chức năng**: Sử dụng mô hình AI `gpt-4o-mini` để trả lời khách hàng.
- **Cấu hình**:
  - **Thêm API Key OpenAI**:
    1. Vào **Credentials** → Tạo mới **OpenAI API**.
    2. Điền **API Key** từ tài khoản OpenAI của bạn.
  - **Model**: Đã chọn `gpt-4o-mini` (mô hình nhanh và hiệu quả).

##### **🔹 Node 4: Window Buffer Memory (memoryBufferWindow)**
- **Chức năng**: Lưu trữ **lịch sử chat** giữa bot và khách hàng để AI hiểu ngữ cảnh.
- **Cấu hình**:
  - **Thêm Session ID**:
    1. Vào **Credentials** → Tạo mới **Memory Buffer**.
    2. Điền **Session ID** (có thể là `{{$json.userId}}` nếu chatbot hỗ trợ).

##### **🔹 Node 5 & 6: Check Availability & Create Event (googleCalendarTool)**
- **Chức năng**:
  - **Check Availability**: Kiểm tra lịch sẵn sàng trên Google Calendar.
  - **Create Event**: Tạo sự kiện mới nếu lịch trống.
- **Cấu hình**:
  - **Kết nối Google Calendar**:
    1. Vào **Credentials** → Tạo mới **Google Calendar OAuth2**.
    2. Nhấn **Connect** và đăng nhập tài khoản Google Calendar.
  - **Cấu hình Node**:
    - **Check Availability**:
      - Tham số `resource`: `calendar`.
      - Tham số `timeZone`: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
    - **Create Event**:
      - Tham số `summary`: `Lịch hẹn khám răng - {{$json.name}}`.
      - Tham số `start` và `end`: Đặt theo định dạng `YYYY-MM-DDTHH:MM:SSZ`.

##### **🔹 Node 7: Add Data (googleSheetsTool)**
- **Chức năng**: Cập nhật thông tin lịch vào Google Sheets.
- **Cấu hình**:
  - **Kết nối Google Sheets**:
    1. Vào **Credentials** → Tạo mới **Google Sheets OAuth2**.
    2. Nhấn **Connect** và chọn bảng dữ liệu (Sheet) muốn lưu.
  - **Tham số**:
    - **Operation**: `append` (thêm dữ liệu mới).
    - **Range**: `Sheet1!A1` (đường dẫn ô bắt đầu ghi dữ liệu).
    - **Values**: Điền các cột như `Tên Khách Hàng`, `Ngày Lịch`, `Giờ Lịch`, `Số Điện Thoại`.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo lịch hẹn cho nhân viên.
   - **Cách làm**:
     - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
     - Gửi thông báo khi lịch được tạo thành công.

2. **Lưu Log Lịch Hẹn**:
   - Thêm node **Google Drive** hoặc **Firebase** để lưu lịch sử chat và lịch hẹn.
   - **Ưu điểm**: Dễ dàng theo dõi và phân tích dữ liệu.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp lịch hẹn hàng tuần/tháng.
   - **Cách làm**:
     - Tạo một workflow mới với node **Google Sheets** và **Email** (ví dụ: Gmail).
     - Chọn **Schedule** để chạy hàng tuần.

4. **Cá Nhân Hóa Trải Nghiệm**:
   - Thêm **AI Prompt** để bot hỏi thêm thông tin chi tiết (ví dụ: lý do khám răng, triệu chứng).
   - **Ví dụ Prompt**:
     ```
     Nếu khách hàng muốn đặt lịch khám răng, hãy hỏi thêm:
     - Bạn muốn khám răng ở phòng nào? (Phòng 1, Phòng 2, Phòng 3)
     - Bạn có triệu chứng nào cần chú ý không? (Nha chu, viêm nướu, đau răng...)
     ```

---
### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của nhân viên y tế khỏi công việc quản lý lịch hẹn thủ công. Với **AI + Google Calendar + Google Sheets**, các sếp có thể:
✅ **Tiết kiệm 80% thời gian** quản lý lịch.
✅ **Tránh sai sót và trùng lịch**.
✅ **Cung cấp trải nghiệm khách hàng chuyên nghiệp**.
✅ **Hoạt động 24/7** mà không cần nhân viên trực ca.

**🚀 Hãy áp dụng ngay và tự động hóa quy trình của bạn!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::