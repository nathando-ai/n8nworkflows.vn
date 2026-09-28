---
title: "🤖 Hệ Thống Email Lạnh Tự Động Hóa Cá Nhân Hóa với Google Gemini + Xác Nhận Telegram & Google Sheets"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp tạo và gửi email lạnh cá nhân hóa, nhận phản hồi qua Telegram, và tự động cập nhật trạng thái trên Google Sheets. Giảm thời gian làm thủ công từ 30 phút/lần xuống 0, đồng thời tăng tỷ lệ phản hồi từ khách hàng."
slug: "he-thong-email-lanh-tu-dong-hoa-google-gemini-telegram"
tags: [n8n, automation, no-code, cold email, google-gemini, telegram, google-sheets, smtp]
keywords: [n8n workflow email lạnh, tự động hóa email cá nhân hóa, google gemini api, telegram approval, google sheets tracking]
---

# 🚀 **Hệ Thống Email Lạnh Tự Động Hóa Cá Nhân Hóa với AI Google Gemini + Xác Nhận Telegram**

## **🔥 Nỗi Đau Của Các Sếp Khi Gửi Email Lạnh Thủ Công**
Gửi email lạnh là một trong những công việc **tốn thời gian nhất** trong sales và marketing. Các sếp phải:
- **Tìm kiếm và lọc leads** từ Google Sheets (hoặc CRM) một cách thủ công.
- **Tạo nội dung email cá nhân hóa** cho từng khách hàng, tránh bị spam và tăng tỷ lệ mở.
- **Chờ đợi phản hồi** và **cập nhật trạng thái** sau mỗi lần gửi, dễ bị quên hoặc sai sót.
- **Tốn trung bình 30-60 phút/lần** cho mỗi batch email, khiến hiệu suất rơi vào tình trạng **chậm và không nhất quán**.

**Workflow này giải quyết tất cả vấn đề trên bằng AI + tự động hóa 100% không code!**

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Từ 30 phút/lần xuống **0 phút** (AI tự động tạo email, gửi và cập nhật).
✅ **Cá nhân hóa cao**: Google Gemini phân tích dữ liệu khách hàng và tạo **nội dung email độc quyền** cho từng lead.
✅ **Xác nhận trước khi gửi**: Trước khi email được gửi, các sếp **xác nhận qua Telegram** (✅/❌), tránh gửi sai hoặc không mong muốn.
✅ **Tracking toàn diện**: Tất cả trạng thái (Filtered Leads, Sent Leads, Emails Sent) được **cập nhật tự động** trên Google Sheets.
✅ **Tăng tỷ lệ phản hồi**: Email được tối ưu hóa bởi AI, tăng **tỷ lệ mở và click** lên đến 30% so với email thủ công.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Google Sheets** với **3 tab** (cấu trúc chi tiết dưới đây):
   - **Filtered Leads** (Danh sách leads sẵn sàng gửi)
   - **Sent Leads** (Danh sách leads đã gửi)
   - **Emails Sent** (Danh sách email đã gửi thành công)
2. **Bot Telegram** + **Chat ID** của các sếp để xác nhận email.
3. **Google Gemini API Key** (đăng ký tại [Google AI Studio](https://aistudio.google.com/)).
4. **SMTP Email** (cấu hình Gmail hoặc dịch vụ SMTP khác như SendGrid).
5. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/9267](https://n8n.io/workflows/9267) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/9267](https://n8n.io/workflows/9267).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán vào.
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **28 node**, nhưng chỉ **5 node quan trọng** cần cấu hình kỹ lưỡng:

#### **📌 Node 1: "Get Lead from Google Sheet" (googleSheets)**
- **Cấu hình:**
  - **Credentials**: Thêm **Google Sheets API** (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
  - **Sheet Name**: Chọn tab **Filtered Leads**.
  - **Range**: `Filtered Leads!A2:D` (giả sử cột A: Email, B: Tên, C: Công ty, D: Trạng thái).
  - **Limit Sheets Get Function**: Đặt **3 leads/lần** (để không quá tải API).

#### **📌 Node 2: "Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Cấu hình:**
  - **API Key**: Điền **Google Gemini API Key** (tạo tại [Google AI Studio](https://aistudio.google.com/)).
  - **Prompt Template**: Sử dụng **prompt mặc định** của workflow (AI sẽ tự động tạo email dựa trên dữ liệu lead).
  - **Model**: Chọn **gemini-pro** (mô hình mạnh nhất hiện tại).

#### **📌 Node 3: "Send message and wait for response" (telegram)**
- **Cấu hình:**
  - **Bot Token**: Thêm **Bot Token Telegram** (tạo tại [@BotFather](https://t.me/BotFather)).
  - **Chat ID**: Nhập **Chat ID của Telegram** (cách lấy: Gửi tin nhắn cho bot, sau đó check [API Telegram](https://api.telegram.org/bot<BOT_TOKEN>/getUpdates)).
  - **Message**: AI sẽ tự động gửi **gợi ý email** cho xác nhận.

#### **📌 Node 4: "Send email" (emailSend)**
- **Cấu hình:**
  - **Credentials**: Thêm **SMTP Email** (ví dụ: Gmail).
  - **From Email**: Điền địa chỉ email gửi (ví dụ: `sales@doanhnghiep.com`).
  - **Subject & Body**: Sử dụng **dữ liệu từ AI** (node "Google Gemini Chat Model").
  - **SMTP Settings**: Cấu hình đúng **host, port, username, password**.

#### **📌 Node 5: "Filtered Leads Update" & "Sent Leads Append" (googleSheetsTool)**
- **Cấu hình:**
  - **Credentials**: Sử dụng cùng **Google Sheets API** như node "Get Lead".
  - **Range**:
    - **Filtered Leads Update**: `Filtered Leads!D2` (cập nhật trạng thái).
    - **Sent Leads Append**: `Sent Leads!A2:D` (thêm lead mới vào danh sách đã gửi).
    - **Emails Sent Append**: `Emails Sent!A2:D` (lưu email đã gửi thành công).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 lead mẫu**:
   - Chọn **Manual Trigger** → Nhấn **Execute**.
   - Kiểm tra **Telegram** để xác nhận email.
   - Sau khi xác nhận, email sẽ được gửi và **cập nhật trạng thái** trên Google Sheets.
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tối Ưu Hóa Telegram Approval**
- **Tự động phản hồi "✅" cho email chất lượng cao**:
  - Sử dụng **node "Switch"** để phân loại email (ví dụ: nếu subject dài > 20 ký tự, tự động xác nhận).
- **Gửi thông báo khi email bị từ chối**:
  - Kết nối với **Slack/Email** để báo cáo lý do từ chối (ví dụ: "Khách hàng không phù hợp").

### **🔹 Lưu Log & Báo Cáo Định Kỳ**
- **Tạo tab "Logs" mới** trên Google Sheets để lưu:
  - Thời gian gửi.
  - Trạng thái (Gửi thành công/Thất bại).
  - Lý do từ chối (nếu có).
- **Gửi báo cáo hàng tuần** qua **Email/Telegram** bằng:
  - Node **emailSend** + **dateTime** để lọc dữ liệu trong tuần.

### **🔹 Kết Hợp với CRM**
- Nếu dùng **HubSpot/Zoho CRM**, thay thế **Google Sheets** bằng **CRM API** để tự động cập nhật trạng thái lead.

### **🔹 Cập Nhật AI với Dữ Liệu Mới**
- **Tăng chất lượng email** bằng cách:
  - Thêm **node "memoryBufferWindow"** để AI nhớ **lịch sử tương tác** với khách hàng.
  - Sử dụng **prompt động** dựa trên **trạng thái trước đó** (ví dụ: nếu khách hàng đã phản hồi trước, AI sẽ nhắc lại).

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **quan hệ khách hàng** thay vì làm thủ công. Với **Google Gemini**, email được tạo **cá nhân hóa và chuyên nghiệp**, trong khi **Telegram Approval** đảm bảo **không gửi sai**.

**🚀 Hãy áp dụng ngay và tăng hiệu suất email lạnh của doanh nghiệp!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Cần hỗ trợ thêm?** Đăng ký [hỗ trợ kỹ thuật n8n](https://n8n.io/community) hoặc liên hệ admin để tối ưu workflow!