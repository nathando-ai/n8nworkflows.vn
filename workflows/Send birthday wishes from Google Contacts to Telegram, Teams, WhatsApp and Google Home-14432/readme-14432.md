---
title: "🎂 **Tự Động Hóa Chúc Mừng Sinh Nhật Từ Google Contacts Đến Telegram, Teams, WhatsApp & Google Home - Không Cần Code!**"
description: "Workflow này tự động tra cứu danh sách sinh nhật từ Google Contacts và gửi lời chúc cá nhân hóa qua Telegram, Microsoft Teams, Google Home và WhatsApp hàng ngày vào 10h sáng. Giúp các sếp tiết kiệm thời gian, tăng trải nghiệm cá nhân hóa cho khách hàng/nhân viên, và tự động hóa hoàn toàn quy trình chúc mừng sinh nhật."
slug: "tieu-dong-hoa-chuc-mung-sinh-nhat-tu-google-contacts"
tags: [n8n, automation, no-code, google-contacts, telegram-bot, whatsapp-automation, microsoft-teams, google-home]
keywords: [tự động hóa sinh nhật, n8n workflow sinh nhật, gửi lời chúc sinh nhật tự động, telegram teams whatsapp google home, google contacts api]
---

# 🎂 **Tự Động Hóa Chúc Mừng Sinh Nhật Từ Google Contacts Đến Telegram, Teams, WhatsApp & Google Home**

## 🚨 **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Tra cứu thủ công** danh sách sinh nhật từ Google Contacts.
- **Ghi nhớ** gửi lời chúc cho từng nhân viên/khách hàng.
- **Phân biệt** ngày tháng sinh nhật giữa các quốc gia (ví dụ: định dạng ngày/tháng/năm).
- **Gửi lời chúc** qua nhiều kênh khác nhau (Telegram, Teams, WhatsApp, Google Home) mà không thể tự động hóa.

**Kết quả?** Thời gian bị lãng phí, trải nghiệm cá nhân hóa không đồng đều, và dễ quên ngày sinh nhật quan trọng.

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
✅ **Tiết kiệm thời gian** lên tới **5-10 giờ/ngày** (không cần tra cứu thủ công).
✅ **Gửi lời chúc cá nhân hóa** với định dạng ngày tháng chính xác (ví dụ: **ngày/tháng** hoặc **tháng/ngày**).
✅ **Hoạt động tự động** hàng ngày vào **10h sáng** (hoặc thời gian tùy chỉnh).
✅ **Kết nối nhiều kênh** (Telegram, Teams, WhatsApp, Google Home) từ **một workflow duy nhất**.
✅ **Tránh quên ngày sinh nhật** nhờ hệ thống tự động tra cứu và gửi lời chúc.

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                          | **Lưu Ý**                                  |
|---------------------------|--------------------------------------------------|--------------------------------------------|
| **Google Contacts**       | - Tài khoản Gmail liên kết với Google Contacts  | Cần cấp quyền **Google Contacts API**     |
| **Telegram Bot**          | - Token Telegram Bot (tạo từ [@BotFather](https://t.me/BotFather)) | Bot phải là admin trong nhóm Telegram |
| **Microsoft Teams**       | - OAuth2 API Key (tạo từ [Azure Portal](https://portal.azure.com/)) | Cần cấp quyền **Teams API**              |
| **Rapiwa (WhatsApp)**     | - API Key từ [Rapiwa](https://rapiwa.com/)       | Cần số điện thoại WhatsApp của người dùng |
| **Google Home Assistant** | - Token từ [Google Home API](https://developers.google.com/assistant/sdk/guides/service/overview) | Cần thiết lập **Google Home Speaker** |

### **2. Thiết Bị & Cấu Hình**
- **Google Home Speaker** (để phát âm lời chúc sinh nhật).
- **Số điện thoại WhatsApp** của người dùng (đã đăng ký trên Rapiwa).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/14432](https://n8n.io/workflows/14432) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên máy chủ self-hosted của bạn.
3. Nhấn **Import** và chọn file JSON vừa tải.
4. **Xác nhận** và workflow sẽ được import hoàn toàn.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → **Create New Workflow** → **Import from JSON**.
3. **Dán JSON** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **17 nodes** và cần cấu hình chi tiết như sau:

#### **🔹 Node "Google Contacts (Get All Contact)"**
- **Credentials**: Chọn `googleContactsOAuth2Api` (đã cấu hình trước khi import).
- **Operation**: Đảm bảo chọn **`getAll`** để lấy tất cả liên lạc.
- **Fields to Retrieve**:
  - `birthdays` (ngày sinh)
  - `names` (tên)
  - `phoneNumbers` (số điện thoại)

#### **🔹 Node "If (Check Is there a birthday?)"**
- **Logic**: Node này kiểm tra xem ngày sinh của liên lạc có trùng với ngày hôm nay không.
- **Lưu ý**: Nếu không có sinh nhật nào, workflow sẽ chuyển sang **Node "No Birthday"** và gửi thông báo Telegram.

#### **🔹 Node "Code (Match Birthday 'Date and Month')"**
- **Mã JavaScript** (nếu cần chỉnh sửa):
  ```javascript
  // So sánh ngày tháng sinh với ngày hôm nay
  const today = new Date();
  const contactBirthday = $input.all()[0].birthdays[0].date;

  if (contactBirthday) {
    const [month, day] = contactBirthday.split('/');
    const isBirthday = (month === today.getMonth() + 1 && day === today.getDate());
    return { isBirthday };
  } else {
    return { isBirthday: false };
  }
  ```
- **Lưu ý**: Node này **bắt buộc** phải trả về `isBirthday: true/false`.

#### **🔹 Node "Rapiwa (Verify WhatsApp Number)"**
- **Credentials**: Chọn `rapiwaApi`.
- **Operation**: Chọn **`verifyWhatsAppNumber`**.
- **Input**: Điền **số điện thoại** từ Google Contacts (đã được **lọc và sạch** bởi Node "Code (Get & Clean Phone Number)").
- **Lưu ý**:
  - Nếu số điện thoại **không hợp lệ**, workflow sẽ **bỏ qua** và không gửi tin nhắn WhatsApp.
  - Cần **đăng ký số điện thoại** trên Rapiwa trước.

#### **🔹 Node "Sent Telegram Message"**
- **Credentials**: Chọn `telegramApi`.
- **Message Template** (gợi ý):
  ```
  🎉 **Happy Birthday, [Name]!** 🎂
  Chúc [Name] sinh nhật vui vẻ và đầy niềm vui!
  Ngày sinh: [Birthday Date]
  ```
- **Lưu ý**:
  - Thay thế `[Name]` và `[Birthday Date]` bằng dữ liệu từ Google Contacts.
  - Cần **định dạng ngày tháng** theo tiếng Việt (ví dụ: `15/12/2024` → `15 tháng 12`).

#### **🔹 Node "Create chat message (Microsoft Teams)"**
- **Credentials**: Chọn `microsoftTeamsOAuth2Api`.
- **Message Template**:
  ```
  **🎂 Chúc mừng sinh nhật [Name]! 🎉**
  Ngày sinh: [Birthday Date]
  ```
- **Lưu ý**:
  - Chọn **channel hoặc nhóm Teams** muốn gửi tin nhắn.
  - Cần **cấp quyền** cho Teams API.

#### **🔹 Node "Send to Google Home Speaker"**
- **Credentials**: Chọn `homeAssistant`.
- **Service**: Chọn **`tts`** (Text-to-Speech).
- **Message Template**:
  ```
  "Chúc [Name] sinh nhật vui vẻ! Hôm nay là sinh nhật của [Name], ngày [Birthday Date]."
  ```
- **Lưu ý**:
  - Cần **cài đặt Google Home Assistant** và **kết nối với Google Home**.
  - Đảm bảo **ngôn ngữ** được đặt là **Tiếng Việt**.

#### **🔹 Node "Start Everyday at 10AM"**
- **Schedule**: Đặt lại thời gian **10h sáng** (hoặc thời gian mong muốn).
- **Lưu ý**:
  - Nếu muốn chạy vào **giờ khác**, chỉnh sửa tại **`cron`** trong Node này.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra các node quan trọng:
     - `Google Contacts` (lấy được sinh nhật không?).
     - `If (Check Is there a birthday?)` (có sinh nhật hôm nay không?).
     - `Telegram/Teams/WhatsApp/Google Home` (tin nhắn được gửi không?).
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tùy Chỉnh Lời Chúc Sinh Nhật**
- **Thay đổi template** trong các node `telegram`, `teams`, và `homeAssistant` để phù hợp với văn hóa doanh nghiệp.
- **Thêm hình ảnh/emoji** vào tin nhắn (ví dụ: 🎂🎈🎁).

### **2. Gửi Lời Chúc Trước Ngày Sinh Nhật**
- Sử dụng Node **"Add 1 Day With Current Date"** để gửi lời chúc **ngày hôm trước** (ví dụ: sinh nhật ngày 15/12 → gửi ngày 14/12).

### **3. Lưu Log & Báo Cáo**
- **Thêm Node `stickyNote`** để ghi lại lịch sử sinh nhật đã gửi.
- **Kết nối với Google Sheets** để lưu dữ liệu sinh nhật và lịch sử chúc mừng.

### **4. Kết Nối Với Slack/Email**
- **Thêm Node `slack`** để gửi thông báo sinh nhật đến kênh Slack.
- **Thêm Node `email`** để gửi lời chúc qua email (nếu cần).

### **5. Hỗ Trợ Đa Ngôn Ngữ**
- **Chỉnh sửa Node `homeAssistant`** để hỗ trợ **Tiếng Anh, Tiếng Nhật, Tiếng Hàn** bằng cách thay đổi ngôn ngữ trong API.

---

## 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề tự động hóa chúc mừng sinh nhật cho các sếp, giúp:
✔ **Tiết kiệm thời gian** (không cần tra cứu thủ công).
✔ **Tăng trải nghiệm cá nhân hóa** (lời chúc được gửi qua nhiều kênh).
✔ **Hoạt động 24/7** (không cần can thiệp của con người).

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test và bật Active** để bắt đầu tự động hóa sinh nhật.
3. **Tùy chỉnh** lời chúc và kênh thông báo theo nhu cầu.

**🚀 Chúc các sếp thành công với việc tự động hóa sinh nhật hiệu quả!** 🎂🎉