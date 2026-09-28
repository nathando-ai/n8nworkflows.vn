---
title: "🚀 Tự Động Hóa Email Outreach Từ Telegram Sang Gmail & Google Sheets - Giảm 90% Thời Gian Làm Thủ Công"
description: "Workflow tự động hóa gửi email B2B từ Telegram, kết hợp Gmail và Google Sheets để quản lý danh sách liên hệ, gửi email cá nhân hóa và theo dõi kết quả - hoàn toàn không cần code."
slug: "tu-dong-hoa-email-outreach-tu-telegram"
tags: [n8n, automation, email outreach, telegram, google-sheets, gmail, no-code, b2b-marketing]
keywords: [tự động hóa email outreach, n8n workflow telegram, gửi email tự động từ telegram, quản lý email b2b, google sheets + gmail automation]
---

# 🚀 **Tự Động Hóa Email Outreach Từ Telegram Sang Gmail & Google Sheets**

### **Giải Pháp Cho Các Sếp Bán Hàng & Marketing Mệt Mỏi Với Công Việc Lặp Lại**
Bạn có bao giờ phải:
- **Nhập liệu danh sách email** vào Google Sheets một cách thủ công?
- **Gửi email cá nhân hóa** cho từng khách hàng một, nhưng lại mất nhiều giờ để viết nội dung?
- **Theo dõi phản hồi** từ khách hàng và cập nhật trạng thái trong bảng tính?
- **Lo lắng về việc quên gửi email** hoặc gửi sai thời điểm?

Workflow này **giải quyết tất cả** bằng cách tự động hóa **tất cả quá trình outreach email từ Telegram**, kết hợp với **Gmail và Google Sheets**, giúp bạn:
✅ **Gửi email cá nhân hóa** chỉ với một cú nhấp chuột từ Telegram.
✅ **Quản lý danh sách liên hệ** trong Google Sheets một cách tự động.
✅ **Theo dõi trạng thái** (đã gửi, đã phản hồi, đã hủy) mà không cần làm thủ công.
✅ **Tiết kiệm 90% thời gian** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
Workflow này giúp bạn **tự động hóa toàn bộ chu trình outreach email** từ Telegram, với những lợi ích cụ thể sau:

| **Lợi Ích**               | **Giải Pháp**                                                                 |
|---------------------------|------------------------------------------------------------------------------|
| **Tiết kiệm thời gian**   | Không cần nhập liệu vào Google Sheets, gửi email thủ công hoặc theo dõi phản hồi. |
| **Cá nhân hóa email**     | Sử dụng **Telegram Trigger** để gửi email với nội dung tùy chỉnh từ từng tin nhắn. |
| **Quản lý danh sách**    | **Google Sheets** tự động cập nhật trạng thái (đã gửi, đã phản hồi, đã hủy). |
| **Hoạt động 24/7**       | Workflow chạy tự động, không phụ thuộc vào giờ làm việc của bạn.            |
| **Theo dõi hiệu quả**     | **Gmail + Google Sheets** giúp bạn phân tích phản hồi và tối ưu chiến dịch. |

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:

#### **1. Tài Khoản & API Keys**
| **Dịch Vụ**       | **Thông Tin Cần Thiết**                                                                 |
|-------------------|----------------------------------------------------------------------------------------|
| **Gmail**         | - Tài khoản Gmail chính (được kết nối với n8n).                                      |
|                   | - **OAuth 2.0 Credentials** (cấu hình trong n8n).                                      |
| **Google Sheets**  | - **Google Workspace** (tài khoản Google Business/Enterprise).                         |
|                   | - **Sheet cụ thể** để lưu danh sách liên hệ và trạng thái (ví dụ: `Outreach Campaign`). |
| **Telegram**      | - **Bot Telegram** (để nhận tin nhắn và kích hoạt workflow).                          |
|                   | - **Chat ID** của bot (để cấu hình trong n8n).                                         |
| **n8n Self-Hosted**| - **VPS** (để chạy workflow 24/7).                                                   |

#### **2. File Google Sheets Mẫu**
Workflow cần một **bảng tính Google Sheets** có cấu trúc như sau (các sếp có thể sao chép mẫu từ [đây](https://docs.google.com/spreadsheets/d/1XYZ...)):

| **Cột**          | **Mô Tả**                                                                 |
|------------------|---------------------------------------------------------------------------|
| `Email`          | Email của khách hàng (cần phải là định dạng chuẩn).                      |
| `Name`           | Tên khách hàng (để cá nhân hóa email).                                  |
| `Company`        | Tên công ty của khách hàng.                                              |
| `Status`         | Trạng thái (chưa gửi, đã gửi, đã phản hồi, đã hủy).                     |
| `Last Contact`   | Ngày giờ cuối cùng liên lạc.                                             |
| `Notes`          | Ghi chú thêm (nếu có).                                                    |

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này **không có file JSON** (do tác giả không cung cấp), nhưng các sếp có thể **tạo mới từ đầu** bằng cách sử dụng các node sau:

##### **Bước 1: Tạo Workflow Mới**
1. Mở **n8n Editor** và tạo một workflow mới.
2. **Tên workflow**: `Telegram Email Outreach Automation`.

##### **Bước 2: Thiết Lập Các Node Cần Thiết**
Workflow này sử dụng **các node chính** sau (sắp xếp theo thứ tự hoạt động):

| **Node**                     | **Vai Trò**                                                                 | **Cấu Hình Cần Thiết**                                                                 |
|------------------------------|----------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| **Telegram Trigger**         | Nhận tin nhắn từ Telegram để kích hoạt workflow.                         | - **Bot Token**: Token của bot Telegram.                                                |
|                              |                                                                            | - **Chat ID**: Chat ID của bot (để nhận tin nhắn).                                   |
| **Set (n8n-nodes-base.set)** | Lưu tin nhắn Telegram vào biến để sử dụng sau.                          | - **Key**: `telegramMessage` (hoặc tên tùy chỉnh).                                     |
| **Code (n8n-nodes-base.code)**| Xử lý logic cá nhân hóa email từ tin nhắn Telegram.                     | - **JavaScript**: Xác định nội dung email từ tin nhắn (ví dụ: `{{ $node["telegramMessage"].json["text"] }}`). |
| **Google Sheets Trigger**    | Đọc dữ liệu từ Google Sheets (danh sách email).                            | - **Sheet Name**: Tên sheet (ví dụ: `Outreach Campaign`).                              |
| **Split in Batches**         | Chia danh sách email thành batch để gửi theo thời gian.                  | - **Batch Size**: Số email gửi cùng một lúc (ví dụ: 5).                               |
| **Gmail (Send Email)**       | Gửi email cá nhân hóa đến từng khách hàng.                                | - **From**: Email của bạn.                                                              |
|                              |                                                                            | - **To**: `{{ $node["googleSheets"].json[].Email }}`.                                |
|                              |                                                                            | - **Subject**: `{{ $node["telegramMessage"].json["subject"] }}`.                     |
|                              |                                                                            | - **Body**: Nội dung email từ tin nhắn Telegram (cá nhân hóa).                         |
| **Set (Update Status)**      | Cập nhật trạng thái trong Google Sheets sau khi gửi email.                 | - **Key**: `Status` (giá trị: `Đã gửi`).                                               |
| **Google Sheets (Update)**   | Cập nhật trạng thái trong sheet.                                           | - **Range**: `A2:E` (các cột cần cập nhật).                                           |
| **Wait (n8n-nodes-base.wait)**| Chờ một khoảng thời gian trước khi gửi batch tiếp theo.                     | - **Time**: 5 phút (để tránh bị đánh dấu là spam).                                     |
| **Switch (Conditional Logic)**| Kiểm tra phản hồi từ Gmail (nếu có).                                      | - **Condition**: Nếu email đã được gửi thành công, cập nhật trạng thái.              |
| **Telegram (Send Response)** | Gửi phản hồi tự động về Telegram khi workflow hoàn thành.                 | - **Text**: `Email đã được gửi thành công cho {{ $node["googleSheets"].json[].Name }}!` |

##### **Bước 3: Kết Nối Các Node**
- **Telegram Trigger** → **Set** → **Code** → **Google Sheets Trigger** → **Split in Batches** → **Gmail (Send Email)** → **Set (Update Status)** → **Google Sheets (Update)** → **Wait** → **Switch** → **Telegram (Send Response)**.

---
#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **a. Cấu Hình Telegram Trigger**
- **Bot Token**: Lấy từ [@BotFather](https://t.me/BotFather) trên Telegram.
- **Chat ID**: Lấy bằng cách gửi tin nhắn cho bot và kiểm tra URL Telegram (ví dụ: `https://t.me/yourbot?start=123` → `123` là Chat ID).
- **Filter**: Chỉ kích hoạt khi nhận tin nhắn có định dạng:
  ```json
  {
    "text": "/send_email {email} {subject} {message}"
  }
  ```
  (Ví dụ: `/send_email john@example.com "Hello John" "Xin chào John, tôi là [Tên],..."`)

##### **b. Cấu Hình Gmail**
- **OAuth 2.0 Credentials**:
  1. Tạo **OAuth Client ID** trong [Google Cloud Console](https://console.cloud.google.com/).
  2. Cấu hình trong n8n với **Client ID** và **Client Secret**.
- **Email From**: Đảm bảo email này **không bị đánh dấu là spam**.

##### **c. Cấu Hình Google Sheets**
- **Sheet Name**: Đặt tên sheet là `Outreach Campaign` (hoặc tên tùy chỉnh).
- **Range**: Đảm bảo cột `Email`, `Name`, `Status` và `Company` được định nghĩa rõ ràng.

##### **d. Logic Cá Nhân Hóa Email**
Trong **node Code**, sử dụng JavaScript để xử lý tin nhắn Telegram:
```javascript
// Ví dụ: Lấy email, subject và message từ tin nhắn Telegram
const telegramData = $input.all();
const email = telegramData[0].json.text.split(" ")[1]; // Lấy email từ tin nhắn
const subject = telegramData[0].json.text.split(" ")[2]; // Lấy subject
const message = telegramData[0].json.text.slice(30); // Lấy message (cá nhân hóa)

// Trả về dữ liệu để sử dụng trong Gmail
return {
  email: email,
  subject: subject,
  body: message
};
```

##### **e. Batch Size & Delay**
- **Split in Batches**: Đặt `Batch Size = 5` (để tránh bị Gmail đánh dấu là spam).
- **Wait Node**: Đặt `Time = 5 minutes` giữa các batch.

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn Telegram: `/send_email test@example.com "Test" "Xin chào, đây là email test."`
   - Kiểm tra:
     - Email có được gửi không?
     - Trạng thái trong Google Sheets có được cập nhật không?
     - Bot Telegram có trả lời không?

2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và **đặt chế độ Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Tự Động Cập Nhật Danh Sách Email**
- Sử dụng **Google Sheets Trigger** để **cập nhật danh sách liên hệ** từ một file CSV hoặc Excel tự động.
- Ví dụ: Kết nối với **Google Drive** để tải file mới vào sheet.

#### **2. Gửi Email Theo Thời Gian**
- Sử dụng **node Schedule** (n8n-nodes-base.schedule) để **gửi email vào giờ nhất định** (ví dụ: 9h sáng).
- Cấu hình trong **node Set** để lưu thời gian gửi.

#### **3. Theo Dõi Phản Hồi Từ Gmail**
- Sử dụng **node Gmail (Watch)** để **nhận email phản hồi** và cập nhật trạng thái trong Google Sheets.
- Ví dụ: Nếu nhận email từ `john@example.com`, cập nhật `Status = "Đã phản hồi"`.

#### **4. Gửi Báo Cáo Định Kỳ**
- Sử dụng **node Telegram (Send Response)** để **gửi báo cáo hàng tuần** về số email đã gửi và phản hồi.
- Ví dụ:
  ```
  "Báo cáo Outreach - Tuần 12:
  - Email gửi: 50
  - Đã phản hồi: 12
  - Tỷ lệ mở: 30%"
  ```

#### **5. Kết Hợp Với Slack/Telegram**
- Thay vì chỉ gửi phản hồi qua Telegram, **kết nối với Slack** để thông báo khi workflow hoàn thành.
- Sử dụng **node Slack** để gửi thông báo vào channel cụ thể.

---
### 📌 **Kết Luận**
Workflow này **giải phóng bạn khỏi công việc lặp lại** trong outreach email, giúp bạn:
✔ **Tiết kiệm thời gian** (không cần nhập liệu, gửi email thủ công).
✔ **Tăng hiệu quả** (email cá nhân hóa, theo dõi tự động).
✔ **Hoạt động 24/7** (không phụ thuộc vào giờ làm việc).

**Hành động ngay hôm nay!**
1. **Self-host n8n** trên VPS (để workflow chạy liên tục).
2. **Tạo workflow** theo hướng dẫn trên.
3. **Test và bật chạy** để tự động hóa outreach email của bạn!

---
**💡 Mẹo cuối:** Nếu các sếp muốn **cá nhân hóa email thêm sâu**, có thể kết hợp với **AI (n8n-nodes-ai)** để tự động viết nội dung email từ tin nhắn Telegram.

---
**📌 Chia sẻ & Hỏi Đáp:**
- Có vấn đề khi cấu hình? **Hỏi trong cộng đồng n8n** [đây](https://community.n8n.io/).
- Muốn workflow **mở rộng thêm tính năng**? **Liên hệ tác giả Milo Bravo** qua [LinkedIn](https://www.linkedin.com/in/milobravo/).