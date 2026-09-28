---
title: "🤖 Tạo Hệ Thống Menu Telegram Tự Động Hóa Với Navegation Multi-Level (Không Cần Code)"
description: "Workflow này giúp các sếp xây dựng một bot Telegram thông minh với menu đa cấp, hỗ trợ tương tác người dùng tự động hóa 100% qua n8n. Giải phóng thời gian, tăng trải nghiệm người dùng và mở rộng tính năng dễ dàng."
slug: "tao-he-thong-menu-telegram-tu-dong-hoa"
tags: [n8n, automation, telegram-bot, no-code, content-creation]
keywords: [n8n workflow telegram, tự động hóa bot telegram, menu đa cấp telegram, n8n self-hosted, tự động hóa không cần code]
---

# 🚀 **Tạo Bot Telegram Tự Động Hóa Với Menu Đa Cấp (Multi-Level Navigation)**

## **Giới Thiệu: Giải Pháp Tự Động Hóa Cho Bot Telegram**
Các sếp đang gặp khó khăn khi phải quản lý bot Telegram thủ công? Cần một cách để tạo menu đa cấp, hỗ trợ người dùng tương tác một cách tự động hóa mà không cần viết một dòng code? **Workflow này là giải pháp hoàn hảo!**

Với **n8n**, các sếp có thể xây dựng một hệ thống menu Telegram **đa cấp, động态 và cá nhân hóa**, giúp người dùng dễ dàng điều hướng và tương tác với bot thông qua các nút bấm, phản hồi callback, và logic xử lý tự động. Đây là cách để **tăng trải nghiệm người dùng, tiết kiệm thời gian và mở rộng tính năng một cách linh hoạt**.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Menu đa cấp tự động hóa**: Tạo menu với nhiều cấp độ (ví dụ: Contact → Email/Chat/Phone) mà không cần code.
- **Tương tác người dùng thông minh**: Hỗ trợ phản hồi callback (callback_data) để xử lý các hành động phức tạp như thay đổi ngôn ngữ, cài đặt, hoặc phản hồi đánh giá.
- **Tích hợp logic nghiệp vụ**: Xử lý các yêu cầu đặc biệt như kiểm tra trạng thái đăng ký, thống kê, hoặc phản hồi người dùng một cách tự động.
- **Hoạt động 24/7**: Workflow chạy liên tục trên VPS, không cần can thiệp thủ công.
- **Dễ dàng mở rộng**: Thêm menu mới, tính năng mới chỉ cần chỉnh sửa cấu hình trong node **Load Menu Config**.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Tạo bot Telegram thông qua [@BotFather](https://t.me/BotFather) bằng lệnh `/newbot`.
   - Lưu **bot token** (sẽ dùng để cấu hình trong workflow).
2. **VPS hoặc máy chủ n8n**:
   - Workflow này hoạt động tốt nhất khi **self-hosted** trên VPS để đảm bảo tính liên tục.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
3. **N8n Editor**:
   - Cài đặt và khởi động n8n trên VPS (hướng dẫn [tại đây](https://docs.n8n.io/hosting/installation/)).
4. **Credentials Telegram**:
   - Trong n8n Editor, thêm **credentials** mới với tên `telegramApi` và điền **bot token** vừa lấy từ BotFather.
---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** của workflow từ [link gốc](https://n8n.io/workflows/8844) hoặc copy/paste JSON từ trang đó.
- Trong n8n Editor, nhấn **Import Workflow** và chọn file JSON đã tải.
- **Lưu ý**: Workflow này có **20 node**, bao gồm các node chính như:
  - `telegramTrigger`: Nhận tin nhắn từ Telegram.
  - `function`: Xử lý logic (ví dụ: `Load Menu Config`, `Extract Command`, `Build Response`).
  - `merge`: Gộp dữ liệu từ các node.
  - `switch`: Router để phân loại hành động người dùng.
  - `httpRequest`: Gửi phản hồi về Telegram.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Bot Token**
1. Tìm node **`Set Bot Token4`** (màu tím).
2. Thay thế `YOUR_BOT_TOKEN_HERE` bằng **bot token** của bạn (đã lấy từ BotFather).
   ```javascript
   $json.botToken = "YOUR_BOT_TOKEN_HERE";
   ```
3. **Lưu workflow** sau khi thay đổi.

##### **B. Cấu hình Webhook**
1. Sau khi import xong, nhấn **Production** trên thanh công cụ.
2. Copy **URL Webhook** hiển thị (dạng: `https://your-vps-ip:5678/webhook/telegramTrigger4`).
3. Trong Telegram, gửi lệnh `/setwebhook` cho bot của bạn với URL này:
   ```
   /setwebhook https://your-vps-ip:5678/webhook/telegramTrigger4
   ```
   - **Lưu ý**: Nếu VPS có IP động, sử dụng dịch vụ như **ngrok** để tạo URL ổn định.

##### **C. Cấu hình Menu và Hành Động**
Workflow này sử dụng **cấu trúc menu JSON** trong node `Load Menu Config`. Các sếp có thể tùy chỉnh menu theo **2 cách**:
- **Thêm menu mới** (ví dụ: Contact, Settings, Subscription).
- **Thêm hành động** (ví dụ: đánh giá, thay đổi ngôn ngữ, thống kê).

**Ví dụ 1: Thêm Menu Contact**
1. Mở node **`Load Menu Config2`**.
2. Thêm cấu trúc menu dưới dạng JSON:
   ```javascript
   contact: {
     text: '📞 <b>Liên Hệ Chúng Tôi</b>\n\nCần hỗ trợ gì?',
     keyboard: [
       [{ text: '📧 Email', callback_data: 'email' }],
       [{ text: '💬 Chat', callback_data: 'chat' }],
       [{ text: '📱 Gọi Điện Thoại', callback_data: 'phone' }],
       [{ text: '🔙 Trở Lại', callback_data: 'main' }]
     ]
   },
   email: {
     text: '📧 Email: support@example.com',
     keyboard: [[{ text: '🔙 Trở Lại', callback_data: 'contact' }]]
   }
   ```
3. **Thêm nút "Contact" vào menu chính**:
   ```javascript
   { text: '📞 Liên Hệ', callback_data: 'contact' }
   ```

**Ví dụ 2: Thêm Hành Động Kiểm Tra Đăng Ký**
1. Thêm `check_subscription` vào danh sách `actionCommands` trong node `Process Command2`:
   ```javascript
   const actionCommands = ['check_subscription', 'rate_1', 'rate_2'];
   ```
2. Cập nhật **Action Router** để xử lý `check_subscription`:
   ```javascript
   $json.command === 'check_subscription' ? 6 :
   ```
3. Trong node **`Default Handler2`**, thêm logic kiểm tra trạng thái:
   ```javascript
   if (input.command === 'check_subscription') {
     input.customData = {
       status: 'Người dùng Premium',
       expires: '30 ngày'
     };
   }
   ```
4. Thêm menu hiển thị trạng thái:
   ```javascript
   subscription: {
     text: 'Trạng Thái: {status}\nHết hạn: {expires}',
     keyboard: [[{ text: '🔙', callback_data: 'main' }]]
   }
   ```

##### **D. Kích hoạt Workflow**
1. Nhấn **Active** trên thanh công cụ để bật workflow.
2. **Test run**:
   - Gửi tin nhắn `/start` hoặc `/help` cho bot.
   - Kiểm tra các nút bấm trong menu (ví dụ: Contact, Settings).
   - Đảm bảo phản hồi callback (`callback_data`) hoạt động đúng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::note[Mở rộng tính năng]
1. **Tích hợp Slack/Telegram Logs**:
   - Sử dụng node `slackWebhook` để gửi log hoạt động của bot vào Slack.
   - Cấu hình trong node `Build Response` để gửi thông báo khi người dùng thực hiện hành động.
2. **Lưu lịch sử tương tác**:
   - Sử dụng node `database` (n8n-nodes-base.database) để lưu dữ liệu tương tác của người dùng.
   - Ví dụ: Lưu lịch sử đánh giá, thay đổi cài đặt.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `set` + `schedule` để gửi báo cáo thống kê (ví dụ: số lượng người dùng, hành động phổ biến) qua email hoặc Telegram.
4. **Hỗ trợ nhiều ngôn ngữ**:
   - Tạo menu riêng cho từng ngôn ngữ (Việt Nam, Anh, Nhật) và sử dụng node `Language Handler2` để chuyển đổi ngôn ngữ tự động.
5. **Tích hợp API bên thứ ba**:
   - Ví dụ: Kết nối với API CRM (HubSpot, Zoho) để lấy thông tin khách hàng khi người dùng nhấp vào nút "Contact".
---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp xây dựng một bot Telegram **tự động hóa, đa cấp và thông minh** mà không cần viết code. Với **n8n**, các sếp có thể:
- **Tạo menu đa cấp** một cách dễ dàng.
- **Xử lý logic nghiệp vụ** thông qua các handler riêng biệt.
- **Mở rộng tính năng** chỉ bằng cách chỉnh sửa cấu hình JSON.
- **Hoạt động liên tục** trên VPS 24/7.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình bot token.
3. **Tùy chỉnh menu** theo nhu cầu của doanh nghiệp.
4. **Test và phát triển** thêm tính năng mới!

**Chúc các sếp thành công với bot Telegram tự động hóa của mình!** 🚀