---
title: "🛡️ Bảo vệ Telegram Groups bằng CAPTCHA Toán Học + Google Sheets (Tự động hóa 100% không code)"
description: "Giải pháp tự động hóa bảo vệ nhóm Telegram khỏi spam và thành viên giả mạo bằng hệ thống CAPTCHA toán học tự động, kết hợp lưu trữ dữ liệu trên Google Sheets. Tiết kiệm thời gian quản trị và tăng tính chuyên nghiệp cho nhóm."
slug: "bao-ve-telegram-capcha-google-sheets"
tags: [n8n, automation, telegram, google-sheets, captcha, no-code, ai-multimodal]
keywords: [tự động hóa telegram, bảo vệ nhóm telegram, captcha toán học, google sheets n8n, tự động hóa không code, giải pháp chống spam telegram]
---

# 🛡️ **Bảo vệ Nhóm Telegram bằng CAPTCHA Toán Học + Google Sheets**

## **🔥 Nỗi đau của quản trị viên Telegram**
Quản lý nhóm Telegram lớn không chỉ tốn thời gian mà còn phải đối mặt với:
- **Spam và thành viên giả mạo** tự động join để quảng cáo hoặc gây rối.
- **Tốn công kiểm tra thủ công** mỗi khi có thành viên mới.
- **Không có hệ thống tự động** để xác minh tính thật của người dùng.

**Workflow này giải quyết tất cả!** Sử dụng **CAPTCHA toán học tự động** để yêu cầu thành viên mới giải một bài toán đơn giản trước khi được chấp nhận. Dữ liệu được lưu trữ trên **Google Sheets** để theo dõi và phân tích.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100% không code** – Không cần viết một dòng code nào.
✅ **Chống spam hiệu quả** – Chỉ những thành viên thật mới được chấp nhận.
✅ **Lưu trữ dữ liệu chuyên nghiệp** – Tất cả thông tin được ghi lại trên Google Sheets.
✅ **Tiết kiệm thời gian** – Không cần kiểm tra thủ công mỗi khi có thành viên mới.
✅ **Cá nhân hóa** – Có thể tùy chỉnh CAPTCHA theo mức độ khó.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản Telegram Bot** (để tạo bot và lấy `API Token`).
- **Google Sheets** (để lưu trữ dữ liệu thành viên và câu trả lời CAPTCHA).
- **API Key của Google Sheets** (để n8n có thể đọc/ghi dữ liệu).
- **URL của nhóm Telegram** (để bot theo dõi thành viên mới).
- **Mã giảm giá VPS** (nếu tự host n8n để workflow hoạt động 24/7).
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấp vào **"Create Workflow"** → **"Import from JSON"**.
3. Dán JSON từ [link gốc](https://n8n.io/workflows/8016) hoặc tải file JSON từ đó.
4. Nhấp **"Import"** để hoàn tất.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node "Telegram Trigger" (📱)**
- **Cấu hình**:
  - Chọn **Bot Token** từ tài khoản Telegram Bot.
  - Chọn **Update Type** là **"New Member"** (để bot phát hiện thành viên mới).
  - Điền **URL của nhóm Telegram** (ví dụ: `https://t.me/tennhom`).

#### **🔹 Node "Generate CAPTCHA Question" (🎲)**
- **Lưu ý**:
  - Node này sử dụng **Code Node** để tạo câu hỏi CAPTCHA ngẫu nhiên.
  - Các sếp có thể **tùy chỉnh logic** trong Code Node để thay đổi độ khó (ví dụ: phép cộng, trừ, nhân, chia).
  - **Ví dụ mã JavaScript**:
    ```javascript
    const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    const num1 = numbers[Math.floor(Math.random() * numbers.length)];
    const num2 = numbers[Math.floor(Math.random() * numbers.length)];
    const operator = ['+', '-', '*', '/'][Math.floor(Math.random() * 4)];
    const question = `${num1} ${operator} ${num2} = ?`;
    return { question, answer: eval(`${num1} ${operator} ${num2}`) };
    ```

#### **🔹 Node "Store User Answer" (💾)**
- **Cấu hình**:
  - Chọn **Google Sheets Credential** (đã cấu hình trước).
  - Chọn **Sheet Name** (tên bảng dữ liệu).
  - Điền **Range** (ví dụ: `Sheet1!A1`).
  - **Cột cần lưu**: `user_id`, `question`, `answer`, `timestamp`.

#### **🔹 Node "Send CAPTCHA Question" (❓)**
- **Cấu hình**:
  - Chọn **Bot Token** từ tài khoản Telegram Bot.
  - Chọn **Chat ID** của nhóm Telegram.
  - **Thể loại tin nhắn**: `Text` với nội dung:
    ```
    Xin chào! Để trở thành thành viên chính thức, hãy giải câu hỏi này:
    **${question}**
    Trả lời bằng cách gửi kết quả cho bot.
    ```

#### **🔹 Node "Verify Answer" (✅)**
- **Cấu hình**:
  - Kết nối với **Google Sheets** để lấy câu trả lời của người dùng.
  - So sánh với **answer** từ node `Generate CAPTCHA Question`.
  - Nếu đúng → cho phép join, nếu sai → ban user.

#### **🔹 Node "Ban User (Failed CAPTCHA)" (🚫)**
- **Cấu hình**:
  - Sử dụng **HTTP Request** để gọi API Telegram để **ban user**.
  - **URL API**: `https://api.telegram.org/bot<BOT_TOKEN>/banChatMember`
  - **Body**:
    ```json
    {
      "chat_id": "${$node["Telegram Trigger"].json()["chat"]["id"]}",
      "user_id": "${$node["Telegram Trigger"].json()["new_chat_members"][0].id}",
      "until_date": 0
    }
    ```

#### **🔹 Node "Welcome New Member" (🎉)**
- **Cấu hình**:
  - Gửi tin nhắn chào mừng cho thành viên mới:
    ```
    Chào mừng bạn đã trở thành thành viên chính thức của nhóm!
    ```

#### **🔹 Node "Clean User Data (Success)" (🗑️)**
- **Cấu hình**:
  - Xóa dữ liệu của người dùng thành công khỏi **Google Sheets** để tránh trùng lặp.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấp **"Run Workflow"** và kiểm tra từng node.
   - Đảm bảo **CAPTCHA hoạt động** và **Google Sheets được cập nhật**.
2. **Bật Active**:
   - Sau khi test thành công, nhấp **"Active"** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC TỐT NHẤT KHI SỬ DỤNG]
🔹 **Tùy chỉnh độ khó CAPTCHA**:
   - Thay đổi logic trong **Code Node** để tăng/giảm độ khó (ví dụ: phép nhân thay vì phép cộng).

🔹 **Gửi báo cáo định kỳ**:
   - Sử dụng **Google Sheets + n8n** để tự động gửi báo cáo thống kê thành viên mới qua **Email/Telegram**.

🔹 **Kết hợp với Slack/Telegram Notifications**:
   - Thêm node **Slack/Telegram** để thông báo khi có thành viên mới hoặc bị ban.

🔹 **Lưu log hoạt động**:
   - Sử dụng **Sticky Note** hoặc **Google Sheets** để ghi lại tất cả hoạt động của bot.
:::

---

## 📌 **Kết luận**
Workflow này giúp **bảo vệ nhóm Telegram hiệu quả** bằng cách tự động hóa quá trình xác minh thành viên mới. **Không cần code**, chỉ cần cấu hình vài bước là có thể áp dụng ngay!

**Hãy thử ngay và bảo vệ nhóm của mình khỏi spam!** 🚀

---
**🔗 [Tải workflow từ nguồn gốc](https://n8n.io/workflows/8016)**
**💡 Cần hỗ trợ?** Đăng ký VPS n8n để tự host và chạy 24/7!