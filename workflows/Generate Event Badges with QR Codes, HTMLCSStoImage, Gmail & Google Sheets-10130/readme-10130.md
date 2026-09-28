---
title: "🎟️ Tự Động Hóa Sáng Tạo Thẻ Hẹn Hò Sự Kiện Với QR Code & Email - N8n Workflow Miễn Phí"
description: "Workflow này tự động tạo thẻ hẹn hò sự kiện cá nhân hóa với QR Code, chuyển đổi HTML thành ảnh PNG, gửi email tự động và ghi log vào Google Sheets - tiết kiệm 90% thời gian so với thủ công. Phù hợp cho các sự kiện đại học, hội nghị doanh nghiệp và hội thảo chuyên ngành."
slug: "tự-dộng-hoa-tao-the-he-hon-su-kien"
tags: [n8n, automation, no-code, google-sheets, gmail, qr-code, html-to-image]
keywords: [n8n workflow tự động hóa, tạo thẻ sự kiện với QR code, chuyển đổi HTML thành ảnh, tự động hóa email, Google Sheets API, HTMLCSStoImage API]
---

# 🚀 **Tự Động Hóa Sáng Tạo Thẻ Hẹn Hò Sự Kiện Với QR Code, Email & Google Sheets**

### **Giải pháp hoàn hảo cho các sếp quản lý sự kiện**
Hãy tưởng tượng một tình huống: Bạn đang chuẩn bị cho một **hội nghị lớn, hội thảo doanh nghiệp, hoặc sự kiện đại học** với hàng trăm người tham dự. Thẻ hẹn hò thủ công không chỉ tốn thời gian mà còn dễ gây lỗi (như sai tên, thiếu QR Code, hoặc thiết kế không thống nhất). **Workflow này tự động hóa toàn bộ quy trình**, từ nhận dữ liệu đăng ký đến gửi email thẻ hẹn hò với QR Code, chỉ trong **5-8 giây/người**!

Không cần viết code, không cần kiến thức kỹ thuật, chỉ cần **n8n + một số API miễn phí**, bạn đã có một hệ thống tự động hóa chuyên nghiệp.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thiết kế thẻ thủ công, chỉ cần nhập dữ liệu đăng ký.
- **Chính xác 100%**: Tự động kiểm tra email, tên, và tạo ID duy nhất cho từng người tham dự.
- **Thẻ cá nhân hóa**: Mỗi thẻ có tên, ảnh QR Code, và thiết kế thống nhất theo mẫu HTML.
- **Gửi email tự động**: Thẻ được gởi kèm email với hướng dẫn check-in và liên lạc.
- **Ghi log toàn bộ**: Dữ liệu đăng ký được lưu vào Google Sheets để theo dõi và phân tích.
- **Hoạt động 24/7**: Workflow chạy liên tục, không cần can thiệp của con người.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để workflow chạy 24/7 ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **API Keys & Credentials**:
   - **HTMLCSStoImage API** (để chuyển đổi HTML thành ảnh):
     - Đăng ký tại: [https://htmlcsstoimg.com](https://htmlcsstoimg.com)
     - Lấy **Basic Auth Credential** từ dashboard và thêm vào n8n.
   - **Gmail OAuth2** (để gửi email thẻ hẹn hò):
     - Sử dụng một **tài khoản Gmail riêng** (không dùng tài khoản cá nhân).
     - Cấu hình OAuth2 trong n8n và cấp quyền gửi email.
   - **Google Sheets OAuth2** (để ghi log dữ liệu):
     - Tạo một **Google Sheet mới** để lưu dữ liệu đăng ký.
     - Cấu hình OAuth2 trong n8n và cấp quyền đọc/ghi.

3. **Google Sheet mẫu**:
   - Tạo một bảng tên **"Event Badge Tracker"** với các cột:
     - Name, Email, Event, Role, Attendee ID, Badge URL, Timestamp.
   - **Không dùng Sheet chung** để tránh trùng dữ liệu.

4. **Webhook URL**:
   - Sau khi cài đặt n8n, lấy **URL Webhook** từ node `Webhook` (ví dụ: `https://your-n8n.com/webhook/new-attendee`).
   - Sử dụng URL này để gửi dữ liệu đăng ký từ hệ thống của bạn (ví dụ: Form Google, CRM, hoặc website).
---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow đã được chia sẻ trên [n8n.io](https://n8n.io/workflows/10130). Các sếp có thể:
- **Tải file JSON** và import vào n8n Editor.
- **Copy JSON** từ trang chia sẻ và dán vào n8n (đường dẫn: **Workflow → Import → Paste JSON**).

:::note[LƯU Ý]
- **Không thay đổi tên node** (nếu không muốn lỗi).
- **Không xóa node nào** trừ khi hiểu rõ tác dụng của nó.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔐 Cấu hình Credentials (Bắt buộc)**
| Node | Yêu cầu cấu hình | Ghi chú |
|------|------------------|---------|
| **Webhook** | Không cần cấu hình (sử dụng URL mặc định) | Chỉ cần lưu URL để gửi dữ liệu đăng ký. |
| **Prepare QR URL** (Code Node) | Không cần thay đổi | Node này tự động tạo URL QR từ ID người tham dự. |
| **Generate QR Code** (HTTP Request) | Không cần thay đổi | Sử dụng API miễn phí của [qrserver.com](https://api.qrserver.com/). |
| **Badge Design** (HTMLCSStoImage) | **Thêm API Key** từ HTMLCSStoImage | Điền vào `htmlcsstoimgApi` trong Credentials. |
| **Send Badge Email** (Gmail) | **Chọn tài khoản Gmail** đã cấu hình OAuth2 | Đảm bảo tài khoản có quyền gửi email. |
| **Log to Sheets** (Google Sheets) | **Chọn Sheet** và trang tính | Chọn trang tính **"Event Badge Tracker"** và cột đầu tiên là `A1`. |

#### **📝 Cấu hình Node `Validate & Sanitize` (Code Node)**
Node này **kiểm tra và chuẩn hóa dữ liệu** trước khi tạo thẻ. Các sếp **không cần chỉnh sửa mã**, nhưng có thể tham khảo logic:
```javascript
// Kiểm tra email hợp lệ
if (!email.match(/^[^\s@]+@[^\s@]+\.[^\s@]+$/)) {
  throw new Error("Email không hợp lệ!");
}

// Tạo ID duy nhất (ví dụ: ATD-2025-001)
const attendeeId = `ATD-${event}-${Math.floor(Math.random() * 1000)}`;

// Chuyển tên thành chữ hoa và lấy 2 chữ cái đầu
const formattedName = name.toUpperCase();
const initials = name.split(' ').map(n => n.charAt(0)).join('');

// Chuyển email thành lowercase
const normalizedEmail = email.toLowerCase();
```
**Lưu ý**: Nếu dữ liệu đầu vào không đúng định dạng, workflow sẽ **dừng lại và gửi email báo lỗi** cho admin.

#### **🎨 Cấu hình Node `Badge Design` (HTMLCSStoImage)**
Node này **chuyển đổi HTML thành ảnh PNG**. Các sếp cần:
1. **Tạo mẫu HTML thẻ hẹn hò** (ví dụ):
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <style>
           body {
               width: 400px;
               height: 680px;
               background-color: #2c3e50;
               color: white;
               font-family: Arial, sans-serif;
               display: flex;
               flex-direction: column;
               align-items: center;
               padding: 20px;
           }
           .qr-code {
               width: 150px;
               height: 150px;
               margin: 20px 0;
           }
           .name {
               font-size: 24px;
               margin-bottom: 10px;
           }
           .event {
               font-size: 18px;
               margin-bottom: 5px;
           }
           .role {
               font-size: 14px;
               margin-bottom: 20px;
           }
       </style>
   </head>
   <body>
       <div class="qr-code">
           <img src="{{ $json.qrUrl }}" alt="QR Code">
       </div>
       <div class="name">{{ $json.name }}</div>
       <div class="event">Event: {{ $json.event }}</div>
       <div class="role">Role: {{ $json.role }}</div>
   </body>
   </html>
   ```
2. **Gửi dữ liệu vào node**:
   - Tham số `html` (HTML code trên).
   - Tham số `viewport` (định dạng ảnh: `400x680px`).
   - **Credentials**: Chọn `htmlcsstoimgApi` đã cấu hình trước.

#### **📧 Cấu hình Node `Send Badge Email` (Gmail)**
Node này **gửi email kèm thẻ PNG** cho người tham dự. Các sếp cần:
1. **Chọn tài khoản Gmail** đã cấu hình OAuth2.
2. **Cấu hình email mẫu**:
   - **Tiêu đề**: `🎟️ Thẻ Hẹn Hò Sự Kiện: {{ $json.event }}`
   - **Nội dung HTML**:
     ```html
     <p>Chào {{ $json.name }},</p>
     <p>Xin chúc mừng bạn đã được chọn tham dự sự kiện <strong>{{ $json.event }}</strong>!</p>
     <p>Dưới đây là thẻ hẹn hò của bạn:</p>
     <p><a href="{{ $json.badgeUrl }}">Tải thẻ PNG</a></p>
     <p>Hướng dẫn check-in:</p>
     <ol>
         <li>Quét QR Code trên thẻ bằng ứng dụng scan QR.</li>
         <li>Đăng ký tại quầy check-in.</li>
     </ol>
     <p>Nếu có vấn đề, liên hệ: admin@example.com</p>
     ```
3. **Kèm file ảnh**:
   - Sử dụng `{{ $json.imageUrl }}` (URL ảnh từ node `Badge Design`).

#### **📊 Cấu hình Node `Log to Sheets` (Google Sheets)**
Node này **ghi log dữ liệu đăng ký** vào Google Sheet. Các sếp cần:
1. **Chọn Sheet** và trang tính `"Event Badge Tracker"`.
2. **Cấu hình cột**:
   - `Name`, `Email`, `Event`, `Role`, `Attendee ID`, `Badge URL`, `Timestamp`.
3. **Chế độ hoạt động**: `Append` (thêm dữ liệu vào cuối bảng).

---

### **3. Kích hoạt ⚡️ Workflow**
1. **Test với dữ liệu mẫu** (sử dụng cURL):
   ```bash
   curl -X POST https://your-n8n.com/webhook/new-attendee \
   -H "Content-Type: application/json" \
   -d '{
       "name": "Nguyễn Văn A",
       "email": "a@example.com",
       "event": "TechCon 2025",
       "role": "VIP Speaker"
   }'
   ```
   - Nếu thành công, bạn sẽ nhận **email thẻ hẹn hò** và **dữ liệu được ghi vào Google Sheet**.
   - Nếu thất bại, **email báo lỗi** sẽ được gửi đến admin.

2. **Bật chế độ Active**:
   - Trong n8n Editor, chuyển **switch Active** sang `ON`.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIẾP CẬN HƠN]
1. **Tích hợp với Form Google**:
   - Sử dụng **Google Form** để thu thập dữ liệu đăng ký và gửi webhook tự động đến n8n.
   - Cài đặt **App Script** để chuyển đổi dữ liệu Form thành JSON và gửi đến Webhook.

2. **Gửi báo cáo định kỳ**:
   - Tạo một **workflow mới** để gửi email báo cáo tổng hợp (số lượng đăng ký, sự kiện, role...) từ Google Sheets.

3. **Thiết kế thẻ động**:
   - Sử dụng **variables** trong HTML để thay đổi màu sắc, logo sự kiện, hoặc nội dung tùy theo role (ví dụ: VIP, Speaker, Participant).

4. **Lưu log lỗi**:
   - Thêm một **Google Sheet mới** để ghi tất cả lỗi (ví dụ: `Event Badge Errors`).
   - Sử dụng node `Send Error Alert` để gửi email báo lỗi chi tiết.

5. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi có người mới đăng ký.
   - Ví dụ:
     ```json
     {
       "text": "🎟️ New Registration: {{ $json.name }} ({{ $json.email }}) for {{ $json.event }}"
     }
     ```
---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc thủ công, đồng thời **tăng cường trải nghiệm người tham dự** với thẻ hẹn hò chuyên nghiệp. **Chỉ cần 5 phút để cấu hình**, và bạn đã có một hệ thống tự động hóa hoàn chỉnh!

:::tip[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Cài đặt n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Cấu hình API Keys** (HTMLCSStoImage, Gmail, Google Sheets).
3. **Import workflow** và test với dữ liệu mẫu.
4. **Tích hợp với hệ thống đăng ký** của bạn (Form Google, CRM, website).
5. **Bật chế độ Active** và bắt đầu tự động hóa!

**Chúc các sếp thành công!** 🚀
---

:::note[HỖ TRỢ]
- **Nếu gặp lỗi**, kiểm tra:
  - **Credentials** có đúng không?
  - **Google Sheet** có cấu trúc đúng không?
  - **Email Gmail** có quyền gửi email không?
- **Cần hỗ trợ kỹ thuật**, liên hệ tại [n8n Community](https://community.n8n.io/) hoặc [Facebook Group](https://www.facebook.com/groups/n8n.io/).