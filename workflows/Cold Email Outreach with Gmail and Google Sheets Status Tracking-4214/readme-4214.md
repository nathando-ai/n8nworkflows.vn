---
title: "🚀 Tự Động Hóa Email Lạnh (Cold Email) với Gmail + Google Sheets - Theo Dõi Trạng Thái Tự Động"
description: "Giải pháp tự động hóa email lạnh 24/7 giúp các sếp tiết kiệm thời gian, tăng tỷ lệ phản hồi và theo dõi trạng thái gửi email trên Google Sheets. Không cần code, chỉ cần cấu hình đơn giản!"
slug: "tu-dong-hoa-email-lanh-gmail-google-sheets"
tags: [n8n, automation, cold-email, marketing-automation, google-sheets]
keywords: [n8n workflow cold email, tự động hóa email lạnh, gửi email tự động Gmail, theo dõi trạng thái email, marketing automation]
---

# 🚀 **Tự Động Hóa Email Lạnh (Cold Email) với Gmail + Google Sheets - Theo Dõi Trạng Thái Tự Động**

### **Nỗi Đau Của Các Sếp Khi Gửi Email Lạnh Thủ Công**
Gửi email lạnh là một trong những công việc tốn thời gian nhất trong marketing và bán hàng. Các sếp phải:
- **Tìm kiếm và cập nhật danh sách leads** trên Google Sheets.
- **Gửi email cá nhân hóa** cho từng khách hàng, đảm bảo nội dung phù hợp.
- **Theo dõi trạng thái gửi** (đã gửi, chưa gửi, đã phản hồi) để tránh trùng lặp.
- **Tốn thời gian** để làm việc này hàng ngày, trong khi có thể tự động hóa hoàn toàn.

**Workflow này giải quyết tất cả những vấn đề trên!** Nó sẽ:
✅ **Tự động lấy leads** từ Google Sheets (chỉ những người chưa nhận email).
✅ **Gửi email cá nhân hóa** qua Gmail (cấu hình 1 lần, chạy tự động hàng ngày).
✅ **Cập nhật trạng thái** trên Google Sheets ngay khi email được gửi.
✅ **Chạy 24/7** mà không cần can thiệp của bạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gửi email thủ công hàng ngày.
- **Tăng tỷ lệ phản hồi**: Email cá nhân hóa và tự động hóa giúp tăng engagement.
- **Tránh trùng lặp**: Theo dõi trạng thái trên Google Sheets, không gửi email cho cùng một người nhiều lần.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày vào thời gian đã thiết lập (2 PM).
- **Dễ dàng mở rộng**: Thêm nhiều leads hoặc thay đổi nội dung email một cách đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n).
2. **Google Sheets** với:
   - **Danh sách leads** (cột `Email`, `Name`, `Company`, `Status`).
   - **Cột `Is Email Sent`** để theo dõi trạng thái (giá trị ban đầu là `no`).
3. **API Key và Credentials**:
   - **Gmail OAuth2** (cấu hình trong n8n).
   - **Google Sheets OAuth2 API** (cấu hình trong n8n).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4214](https://n8n.io/workflows/4214) hoặc copy toàn bộ JSON từ canvas.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- Workflow sẽ hiển thị với **5 nodes** như sau:
  ```
  Schedule Trigger → Fetch Leads → Batch Processing → Send Email → Update Status
  ```

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Node "Schedule Trigger"**
- **Thiết lập thời gian chạy**: Mặc định là **2 PM hàng ngày**, nhưng các sếp có thể thay đổi theo nhu cầu.
- **Lưu ý**: Nếu muốn chạy nhiều lần trong ngày, cần điều chỉnh hoặc chia nhỏ batch.

##### **B. Node "Fetch Leads" (Google Sheets)**
- **Chọn Sheet và Range**:
  - **Sheet Name**: Tên của file Google Sheets chứa leads.
  - **Range**: Phần dữ liệu cần lấy (ví dụ: `Sheet1!A:E`).
- **Lọc leads chưa gửi email**:
  - Trong **Filter**, thêm điều kiện:
    ```json
    {
      "column": "Is Email Sent",
      "operator": "is",
      "value": "no"
    }
    ```
  - Nếu không có filter, workflow sẽ lấy tất cả leads và gửi email trùng lặp.

##### **C. Node "Batch Processing" (Split in Batches)**
- **Thiết lập batch size**:
  - Mặc định là **10 leads/batch**, nhưng các sếp có thể tăng/giờm tùy vào tốc độ Gmail.
  - **Lưu ý**: Nếu Gmail bị chặn, giảm batch size xuống **5 leads/batch**.

##### **D. Node "Send Personalized Email" (Gmail)**
- **Cấu hình email mẫu**:
  - Trong **Subject** và **Body**, các sếp có thể sử dụng **template động** bằng cách trích xuất dữ liệu từ Google Sheets (ví dụ: `{{ $node["Fetch Leads"].json["email"] }}`).
  - **Ví dụ email cá nhân hóa**:
    ```
    Subject: Hi {{ $node["Fetch Leads"].json["name"] }} - Let's Talk!
    Body: Hi {{ $node["Fetch Leads"].json["name"] }},
    I saw your work at {{ $node["Fetch Leads"].json["company"] }} and think we could collaborate. Let me know if you're interested!
    ```
- **Kiểm tra Gmail OAuth2**:
  - Đảm bảo **gmailOAuth2** đã được cấu hình trong **Credentials** của n8n.

##### **E. Node "Update Lead Status" (Google Sheets)**
- **Cập nhật cột `Is Email Sent`**:
  - **Operation**: Chọn `update`.
  - **Range**: Cùng với node `Fetch Leads`.
  - **Data**: Sử dụng **JSON Path** để cập nhật giá trị:
    ```json
    {
      "Is Email Sent": "yes"
    }
    ```
  - **Lưu ý**: Nếu cột `Is Email Sent` không tồn tại, workflow sẽ báo lỗi.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một batch nhỏ (ví dụ: 2-3 leads) để kiểm tra:
   - Email có được gửi thành công không?
   - Trạng thái trên Google Sheets có được cập nhật không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi email được gửi thành công/bất thành công.
   - **Cách làm**:
     - Thêm node **Slack Webhook** sau node **Send Email**.
     - Gửi tin nhắn động như:
       ```
       Email sent to {{ $node["Fetch Leads"].json["name"] }}!
       ```

2. **Lưu Log Lịch Sử**:
   - Thêm node **StickyNote** để ghi lại lịch sử gửi email (ví dụ: ngày gửi, trạng thái).
   - **Cách làm**:
     - Sau node **Send Email**, thêm node **StickyNote** với nội dung:
       ```json
       {
         "Email": "{{ $node["Fetch Leads"].json["email"] }}",
         "Status": "Sent",
         "Date": "{{ $node["Schedule Trigger"].json["date"] }}"
       }
       ```

3. **Gửi Email Định Kỳ Theo Ngày**:
   - Nếu muốn gửi email vào ngày cụ thể (ví dụ: thứ 2 hàng tuần), thay đổi **Schedule Trigger** thành:
     ```
     0 14 * * 1  # Chạy vào 2 PM thứ 2 hàng tuần
     ```

4. **Kết hợp với CRM**:
   - Nếu sử dụng **HubSpot** hoặc **Salesforce**, thay thế Google Sheets bằng API của CRM để quản lý leads.

---

### 📌 **Kết Luận**
Workflow **Cold Email Outreach** này là giải pháp **tự động hóa hoàn toàn** cho email lạnh, giúp các sếp:
✔ **Tiết kiệm thời gian** (không cần gửi email thủ công).
✔ **Tăng tỷ lệ phản hồi** (email cá nhân hóa).
✔ **Theo dõi hiệu quả** (trạng thái gửi trên Google Sheets).
✔ **Chạy 24/7** (không cần can thiệp).

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Google Sheets và Gmail** theo hướng dẫn.
3. **Bật workflow** và để nó làm việc cho bạn!

Nếu có bất kỳ vấn đề, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng **n8n** trên [Discord](https://discord.gg/n8n). **Chúc các sếp thành công!** 🚀