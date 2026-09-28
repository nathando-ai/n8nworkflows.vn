---
title: "🚀 Tự Động Hóa Bài Đăng Facebook Tuần Kế Hoạch Từ Google Sheets - Chỉ Cần 1 Lần Cài Đặt!"
description: "Giải pháp hoàn hảo cho các sếp marketing tự động hóa việc lên lịch bài đăng Facebook hàng tuần từ Google Sheets, tiết kiệm thời gian lên tới 16h/tháng và đảm bảo nội dung được đăng đúng thời gian, không bỏ lỡ ngày nào."
slug: "tu-dong-hoa-bai-dang-facebook-tu-google-sheets"
tags: [n8n, automation, social-media, google-sheets, facebook-posting]
keywords: [tự động hóa bài đăng facebook, google sheets facebook, n8n workflow tự động, lên lịch bài đăng tự động, marketing tự động hóa]
---

# 🚀 **Tự Động Hóa Bài Đăng Facebook Tuần Kế Hoạch Từ Google Sheets - Không Cần Code!**

### **💡 Nỗi Đau Của Các Sếp Marketing Hàng Ngày**
Các sếp marketing phải mất **tối thiểu 4h/tuần** để:
- Chọn nội dung từ Google Sheets.
- Lên lịch bài đăng trên Facebook.
- Kiểm tra lại lịch trình để tránh trùng lặp hoặc quên đăng.
- Đối mặt với rủi ro **bài đăng bị lỡ thời gian** do quên hoặc quên nhắc nhở.

**Kết quả?** Nội dung không được đăng đúng thời gian, hiệu quả marketing bị giảm, và thời gian quý giá bị "chôn vùi" trong công việc lặp đi lặp lại.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
- **Tiết kiệm 16h/tháng** (4h/tuần) cho việc lên lịch bài đăng.
- **Đảm bảo bài đăng được đăng đúng thời gian** (không bỏ lỡ ngày nào).
- **Tự động hóa hoàn toàn** - không cần nhắc nhở hay can thiệp thủ công.
- **Tăng cường hiệu quả marketing** với nội dung được lên lịch chính xác.
- **Dễ dàng mở rộng** cho nhiều nền tảng khác (Instagram, LinkedIn) sau này.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ danh sách bài đăng).
2. **Tài khoản Facebook Business Manager** (để đăng bài tự động).
3. **Tài khoản Telegram** (để nhận thông báo nếu có lỗi).
4. **API Key của n8n** (nếu tự host trên VPS).
5. **Dữ liệu mẫu trong Google Sheets** (cấu trúc bao gồm: **Ngày đăng, Nội dung, Link, Thời gian**).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/7977) hoặc sao chép JSON từ đây.
- **Bước 2:** Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON hoặc tải file.
- **Bước 3:** Chọn **Workflow Name** là **"Schedule Weekly Facebook Posts"** và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này được thiết kế để **chạy tự động hàng tuần** (thứ 7) và **đăng bài từ Google Sheets**. Dưới đây là các bước cấu hình quan trọng:

##### **🔹 Node "Daily at 9 AM" (ScheduleTrigger)**
- **Cấu hình:** Đặt lịch chạy **mỗi thứ 7 lúc 9h sáng** (hoặc thời gian phù hợp với các sếp).
- **Lưu ý:** Nếu muốn chạy vào thời gian khác, chỉnh **cron expression** trong node này (ví dụ: `0 9 * * 0` cho thứ 7 lúc 9h).

##### **🔹 Node "Query Notion Database" (HTTP Request)**
- **Thay đổi thành "Query Google Sheets"** (do workflow gốc dùng Notion, nhưng các sếp nên sử dụng Google Sheets).
- **Cấu hình:**
  - **Method:** `GET`
  - **URL:** `https://sheets.googleapis.com/v4/spreadsheets/[ID_SHEET]/values/[TÊN_TRANG_CHỨA_DỮ_LIỆU]!A:Z`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer [API_KEY_GOOGLE_SHEETS]"
    }
    ```
  - **API Key:** Lấy từ [Google Cloud Console](https://console.cloud.google.com/).
  - **ID Sheet & Sheet Name:** Lấy từ liên kết Google Sheets (ví dụ: `https://docs.google.com/spreadsheets/d/[ID_SHEET]/edit` → `[ID_SHEET]` là phần sau `/edit`).

##### **🔹 Node "Get Today's Date" (Code)**
- **Lưu ý:** Node này lấy ngày hiện tại để so sánh với ngày trong Google Sheets.
- **Không cần chỉnh sửa** nếu các sếp muốn sử dụng ngày hệ thống.

##### **🔹 Node "Is Day 7?" (If)**
- **Điều kiện:** Kiểm tra xem ngày trong Google Sheets có phải là **thứ 7** không.
- **Lưu ý:** Nếu muốn đăng bài vào ngày khác, chỉnh **câu điều kiện** trong node này (ví dụ: `{{ $json["day"] === "Monday" }}`).

##### **🔹 Node "Send Day 7 Email" (EmailSend)**
- **Cấu hình:**
  - **From Email:** Địa chỉ email của các sếp.
  - **To Email:** Địa chỉ email cần thông báo (ví dụ: email của team marketing).
  - **Subject:** `"Bài đăng Facebook cho ngày {{ $json["date"] }} đã được lên lịch!"`
  - **Body:** `"Xin chào, bài đăng đã được tự động lên lịch thành công. Chi tiết: {{ $json["content"] }}"`.
- **Lưu ý:** Nếu không muốn gửi email, có thể xóa node này và chuyển sang **Telegram Notification** thay thế.

##### **🔹 Node "Notify via Telegram" (Telegram)**
- **Cấu hình:**
  - **Chat ID:** Lấy từ [@BotFather](https://t.me/BotFather) (tạo bot Telegram và lấy chat ID).
  - **Message:** `"📢 Bài đăng Facebook đã được lên lịch tự động! Ngày: {{ $json["date"] }} - Nội dung: {{ $json["content"] }}"`.
- **Lưu ý:** Nếu muốn nhận thông báo lỗi, thêm node này vào **error handling** của workflow.

##### **🔹 Node "Respond to Webhook" (RespondToWebhook)**
- **Không cần chỉnh sửa** nếu các sếp không sử dụng webhook.

---
#### **3. Kích Hoạt ⚡️ Workflow**
- **Bước 1:** Nhấn **Test Run** để kiểm tra workflow với dữ liệu mẫu.
- **Bước 2:** Nếu test thành công, bật **Active** để workflow chạy tự động hàng tuần.
- **Bước 3:** Kiểm tra **Google Sheets** và **Facebook Page** để xác nhận bài đăng được đăng đúng.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **📌 Thêm Log Lịch Sử:**
   - Sử dụng **Sticky Note** để ghi lại lịch sử bài đăng (ví dụ: ngày đăng, trạng thái thành công/thất bại).
   - **Cách làm:** Thêm node **StickyNote** sau node **EmailSend** và cấu hình lưu dữ liệu vào.

2. **📌 Kết Nối Với Facebook API:**
   - Thay vì dùng **Email Notification**, các sếp có thể **đăng bài trực tiếp trên Facebook** bằng node **Facebook API**.
   - **Cách làm:** Thêm node **HTTP Request** với URL:
     ```
     https://graph.facebook.com/v12.0/[PAGE_ID]/feed?access_token=[ACCESS_TOKEN]
     ```
   - **Headers:**
     ```json
     {
       "Content-Type": "application/json"
     }
     ```
   - **Body:**
     ```json
     {
       "message": "{{ $json["content"] }}",
       "link": "{{ $json["link"] }}"
     }
     ```

3. **📌 Gửi Báo Cáo Tuần Kế:**
   - Thêm node **Google Calendar** để **lên lịch báo cáo tuần kế** cho team.
   - **Cách làm:** Sử dụng node **Google Calendar** với API Key và cấu hình:
     - **Event Title:** `"Báo cáo bài đăng Facebook - Tuần {{ $json["week"] }}"`
     - **Start Time:** `{{ $json["next_week_date"] }}T09:00:00Z`

4. **📌 Tự Động Xóa Bài Đăng Sau 1 Tuần:**
   - Thêm node **If** để kiểm tra **tuổi bài đăng** và xóa nếu quá 7 ngày.
   - **Cách làm:** Sử dụng node **Facebook API Delete Post** với URL:
     ```
     https://graph.facebook.com/v12.0/[POST_ID]?access_token=[ACCESS_TOKEN]
     ```

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing khỏi công việc lặp đi lặp lại, đồng thời **đảm bảo bài đăng được đăng đúng thời gian** mà không cần can thiệp thủ công.

**🚀 Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Google Sheets** và **API Keys**.
3. **Bật Active** và để workflow làm việc cho các sếp!

**💡 Nếu cần hỗ trợ:**
- **Dùng VPS TinoHost** để host n8n 24/7 (mã giảm giá **VPSN8N**).
- **Trao đổi trên cộng đồng n8n** hoặc liên hệ với tác giả [Shelly-Ann Davy](https://n8n.io/workflows/7977).

**🎁 Bonus:** Các sếp có thể **mở rộng workflow** để tự động hóa bài đăng trên **Instagram, LinkedIn, hoặc TikTok** sau này!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔥 Chúc các sếp thành công với việc tự động hóa marketing!** 🚀