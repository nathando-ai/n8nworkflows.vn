---
title: "🚀 Tự Động Lấy Tất Cả Email Từ Nhiều Tài Khoản Gmail & Gửi Báo Cáo Trên Discord (Không Cần Code)"
description: "Workflow này tự động quét, lưu trữ và báo cáo tất cả email mới từ nhiều tài khoản Gmail vào một bảng dữ liệu thống nhất, đồng thời gửi thông báo tổng hợp lên Discord. Giúp các sếp tiết kiệm 10+ giờ/ngày và tránh bỏ lỡ tin nhắn quan trọng."
slug: "tu-dong-lay-email-gmail-va-gui-bao-cao-discord"
tags: [n8n, tự động hóa email, quản lý ticket, Gmail API, Discord notification, data table, no-code]
keywords: [n8n workflow Gmail, tự động lấy email từ nhiều tài khoản, báo cáo email Discord, lưu trữ email thống nhất, tự động hóa quản lý email]
---

# 🚀 **Tự Động Lấy Email Từ Nhiều Tài Khoản Gmail & Gửi Báo Cáo Trên Discord**

### **📌 Nỗi Đau Của Các Sếp Hiện Nay**
- **Bỏ lỡ email quan trọng** vì phải kiểm tra từng tài khoản Gmail thủ công hàng giờ.
- **Làm mất thời gian** khi phải sao chép email từ nhiều tài khoản vào một bảng Excel hoặc Google Sheets.
- **Không biết có bao nhiêu email mới** trong ngày, dẫn đến quản lý rối loạn.
- **Không có báo cáo tự động** để báo cáo cho team hoặc khách hàng.

**Workflow này giải quyết tất cả!** Nó sẽ:
✅ **Quét tự động** tất cả email mới từ nhiều tài khoản Gmail (dùng OAuth2).
✅ **Lưu trữ thống nhất** vào một bảng dữ liệu (Data Table) tránh trùng lặp.
✅ **Cập nhật thời gian quét cuối cùng** để không lấy lại email cũ.
✅ **Gửi báo cáo Discord** với số lượng email mới mỗi lần chạy (ví dụ: *"15 email mới từ 3 tài khoản"*).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo an toàn và không bị giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** không phải kiểm tra email thủ công.
- **Không bỏ lỡ email** nhờ việc quét tự động theo lịch.
- **Dữ liệu thống nhất** trên một bảng Data Table, dễ dàng phân tích.
- **Báo cáo tự động** trên Discord, giúp team biết tình hình ngay lập tức.
- **Không cần code** – chỉ cần cấu hình OAuth2 và thiết lập bảng dữ liệu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (cần kích hoạt **Gmail API** và tạo **OAuth2 Credentials**).
   - [Hướng dẫn kích hoạt Gmail API](https://developers.google.com/gmail/api/quickstart/python)
   - [Tạo OAuth2 Client ID](https://console.cloud.google.com/apis/credentials)
2. **Bảng dữ liệu Data Table** (trên n8n) với 2 bảng:
   - `cold_email_accounts` (để lưu danh sách email + `last_polled` – thời gian quét cuối cùng).
   - `all_emails` (để lưu tất cả email mới).
3. **Bot Discord** (để gửi thông báo):
   - Tạo bot trên [Discord Developer Portal](https://discord.com/developers/applications).
   - Thêm bot vào channel cần báo cáo.
4. **n8n Self-hosted** (không dùng n8n.cloud để tránh giới hạn).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11721) hoặc copy JSON từ canvas.
- Vào **n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc** copy JSON vào ô **Import Workflow** và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **15 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình Bảng Dữ liệu Data Table**
- **Bảng `cold_email_accounts`** (lưu thông tin tài khoản Gmail):
  - Cột cần thiết:
    - `email` (địa chỉ email).
    - `last_polled` (thời gian quét cuối cùng, định dạng **Epoch**).
    - `oauth2_credentials_id` (ID của OAuth2 Credentials trong n8n).
  - **Ví dụ dữ liệu:**
    ```json
    [
      {"email": "account1@gmail.com", "last_polled": 1712345678, "oauth2_credentials_id": "cred123"},
      {"email": "account2@gmail.com", "last_polled": 1712345678, "oauth2_credentials_id": "cred456"}
    ]
    ```

- **Bảng `all_emails`** (lưu tất cả email mới):
  - Cột cần thiết:
    - `email` (địa chỉ email nguồn).
    - `subject` (tiêu đề email).
    - `body` (nội dung email).
    - `date` (thời gian nhận).
    - `id` (ID duy nhất của email trong Gmail).

##### **B. Cấu Hình OAuth2 Credentials**
- Trong node **"Run Node With Credentials X"**, chọn:
  - **Credentials ID** = `{{$node["Get All Email Accounts"].json[].oauth2_credentials_id}}` (đọc từ bảng `cold_email_accounts`).
  - **Gmail API Key** = Khóa OAuth2 từ Google Cloud Console.

##### **C. Cấu Hình Schedule Trigger**
- Node **"Schedule Trigger"** chạy **mỗi giờ** (hoặc tùy chỉnh).
- Thiết lập trong **Settings** của workflow:
  - **Frequency**: `Every hour`.
  - **Timezone**: Chọn theo khu vực của bạn.

##### **D. Cấu Hình Discord Notification**
- Node **"Send a message"** (Discord):
  - **Credentials**: Chọn `discordBotApi` (đã cấu hình bot Discord trước).
  - **Channel ID**: ID của channel Discord muốn gửi báo cáo.
  - **Message Format**: Sử dụng template:
    ```json
    {
      "content": `📧 **New Emails Report**\nTotal new emails: **{{$node["Limit"].json[0].length}}**\nTime: **{{$node["Schedule Trigger"].json["$nodeTime"]}}**`
    }
    ```

##### **E. Cấu Hình Code Nodes**
- Node **"Polling Time Calculator"** (Code):
  - Cập nhật logic tính `after` và `before` (thời gian quét):
    ```javascript
    // Ví dụ: Quét email từ last_polled + 1 giờ đến hiện tại
    const after = new Date($node["Get All Email Accounts"].json[].last_polled * 1000).toISOString();
    const before = new Date().toISOString();
    return { after, before };
    ```
- Node **"Email Normalization"** (Code):
  - Sử dụng để **lọc và định dạng email** (ví dụ: loại bỏ spam, giữ lại email quan trọng).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **Manual Trigger** để kiểm tra workflow.
   - Kiểm tra **bảng `all_emails`** có thêm email mới không.
   - Kiểm tra **Discord** có nhận được báo cáo không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Email**:
   - Thay vì Discord, có thể gửi báo cáo lên **Slack** hoặc **Email** bằng node `n8n-nodes-base.email`.
   - **Ví dụ**:
     ```json
     {
       "to": "team@example.com",
       "subject": "Daily Email Report",
       "text": `Total new emails: **{{$node["Limit"].json[0].length}}**`
     }
     ```

2. **Lưu Log Chi Tiết**:
   - Thêm node **Sticky Note** (`n8n-nodes-base.stickyNote`) để ghi lại lỗi hoặc thông tin debug.
   - **Ví dụ**:
     ```json
     {
       "note": `Email account: **{{$node["Get All Email Accounts"].json[].email}}**\nStatus: **{{$node["If new email found"].json["$nodeStatus"]}}**`
     }
     ```

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **Schedule Trigger** để gửi báo cáo **hàng ngày/lần 1 tuần** thay vì mỗi giờ.
   - **Ví dụ**:
     ```json
     {
       "cron": "0 0 * * *", // Gửi lúc 0h hàng ngày
       "timezone": "Asia/Ho_Chi_Minh"
     }
     ```

4. **Lọc Email Quan Trọng**:
   - Trong node **Code (Email Normalization)**, thêm logic lọc email từ **những người gửi cụ thể** hoặc có từ khóa nhất định.
   - **Ví dụ**:
     ```javascript
     const importantEmails = $node["Get new emails if any"].json.filter(email =>
       email.subject.includes("urgent") ||
       email.from.includes("client@example.com")
     );
     return { emails: importantEmails };
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc kiểm tra email thủ công, đồng thời **tự động hóa toàn bộ quy trình** từ lấy email đến báo cáo. **Chỉ cần 30 phút cấu hình**, bạn sẽ có một hệ thống **tự động, chính xác và hiệu quả**!

**Hành động ngay hôm nay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để tránh giới hạn).
2. **Import workflow** và cấu hình OAuth2, bảng dữ liệu.
3. **Test và bật Active** để bắt đầu tự động hóa!

**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ với tôi để hỗ trợ chi tiết! 🚀