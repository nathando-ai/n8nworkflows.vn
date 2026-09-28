---
title: "🚀 Tự Động Hóa Theo Dõi Đơn Hàng Shopify Qua Telegram - Không Cần Code!"
description: "Giải pháp tự động hóa theo dõi đơn hàng Shopify 24/7 qua Telegram, giúp các sếp tiết kiệm thời gian kiểm tra hàng ngày và nhận thông báo chi tiết đơn hàng mới/đã cập nhật. Hoạt động liên tục, không bỏ lỡ đơn hàng nào!"
slug: "tu-dong-hoa-theo-doi-don-hang-shopify-qua-telegram"
tags: [n8n, automation, shopify, telegram, no-code, sales, ecommerce]
keywords: [tự động hóa shopify telegram, theo dõi đơn hàng shopify, bot telegram shopify, tự động hóa bán hàng online, n8n workflow shopify]
---

# 🚀 **Tự Động Hóa Theo Dõi Đơn Hàng Shopify Qua Telegram - Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp Trong Quản Lý Đơn Hàng**
Hàng ngày, các sếp phải:
- **Lặp đi lặp lại** kiểm tra đơn hàng mới trên Shopify qua email hoặc dashboard.
- **Bỏ lỡ thông báo** khi đơn hàng được cập nhật (đã ship, hủy, hoàn tiền).
- **Phải chuyển đổi giữa nhiều tab** (Shopify → Telegram → Email) để theo dõi tình trạng.
- **Tốn thời gian** để tổng hợp báo cáo đơn hàng cho team.

**Giải pháp?** Một **bot Telegram tự động** kết nối với Shopify, gửi thông báo chi tiết đơn hàng mới/đã thay đổi **tự động**, **24/7**, **không cần code**!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản miễn phí (có giới hạn).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho nhiều workflow)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần kiểm tra đơn hàng thủ công hàng ngày.
✅ **Thông báo tức thời** – Nhận tin nhắn Telegram khi có đơn hàng mới/đã cập nhật.
✅ **Chi tiết đơn hàng** – Xem thông tin sản phẩm, khách hàng, trạng thái giao hàng trong Telegram.
✅ **Hoạt động 24/7** – Bot không ngủ, không bỏ lỡ đơn hàng nào.
✅ **Tích hợp dễ dàng** – Chỉ cần cài đặt 1 lần, sau đó **quên đi** – bot làm việc tự động.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Shopify** (có **Shopify Access Token** để truy cập API).
   - **Cách lấy Access Token**:
     - Đăng nhập vào [Shopify Admin](https://your-store.myshopify.com/admin).
     - Tạo **Private App** tại **Apps → Develop apps**.
     - Chọn **Admin API** → **Read and Write** (để lấy danh sách đơn hàng).
     - Copy **API Key** và **API Secret** → Tạo **Access Token** tại [Shopify API Credentials](https://your-store.myshopify.com/admin/apps/private_app/credentials).
2. **Bot Telegram** (có **Telegram Bot Token** và **Chat ID**).
   - **Cách lấy Telegram Bot Token**:
     - Trên Telegram, tìm **@BotFather** → Gửi `/newbot` → Theo hướng dẫn tạo bot.
     - Copy **API Token** của bot.
   - **Cách lấy Chat ID**:
     - Gửi tin nhắn cho bot → Trên [@userinfobot](https://t.me/userinfobot) → Nhập tin nhắn của bot → Copy **Chat ID**.
3. **n8n Self-Hosted** (để workflow hoạt động liên tục).
   - **Không dùng phiên bản miễn phí** (có giới hạn node và không ổn định).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4714](https://n8n.io/workflows/4714).
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON → Nhấn **Import**.
  - **Hoặc** copy toàn bộ JSON → Paste vào **Create Workflow** → Nhấn **Create**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **11 node**, nhưng chỉ **3 node quan trọng** cần cấu hình kỹ:

##### **🔹 Node 1: Telegram Trigger (Bắt đầu workflow)**
- **Chức năng**: Nhận lệnh từ Telegram để lấy đơn hàng mới.
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi` (đã tạo trước khi import).
  - **Command**: Đặt là `/orders` (lệnh để lấy danh sách đơn hàng mới).
  - **Chat ID**: Điền **Chat ID** của bot (đã lấy từ bước trên).

##### **🔹 Node 2: Shopify - get Orders (Lấy danh sách đơn hàng mới)**
- **Chức năng**: Truy vấn API Shopify để lấy tất cả đơn hàng mới.
- **Cấu hình**:
  - **Credentials**: Chọn `shopifyAccessTokenApi` (đã tạo từ Access Token).
  - **Operation**: Đặt là `getAll` (lấy tất cả đơn hàng).
  - **Filter (nếu cần)**: Có thể thêm điều kiện như `status: 'pending'` để chỉ lấy đơn hàng mới.

##### **🔹 Node 3: Telegram - Send Order Details (Gửi thông báo chi tiết)**
- **Chức năng**: Gửi tin nhắn Telegram với thông tin đơn hàng.
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi`.
  - **Operation**: Đặt là `editMessageText` (để cập nhật tin nhắn nếu có thay đổi).
  - **Message Format**: Sử dụng **template** từ node **Code** (xem chi tiết dưới đây).

---
#### **3. Các Node Khác (Cần Chỉnh Sửa Giống Nhau)**
| **Node** | **Chức năng** | **Lưu ý** |
|----------|--------------|-----------|
| **Orders (Code)** | Lọc đơn hàng mới | Sử dụng **JavaScript** để so sánh với danh sách cũ (nếu có). |
| **No Order (Code)** | Trả lời nếu không có đơn hàng mới | Gửi tin nhắn "Không có đơn hàng mới" nếu không tìm thấy. |
| **get Order (Shopify)** | Lấy chi tiết đơn hàng cụ thể | Sử dụng **Order ID** từ node trước. |
| **Clean Up Order (Code)** | Làm sạch dữ liệu | Xóa trường không cần thiết trước khi gửi Telegram. |
| **Check If There's Any Order (If)** | Kiểm tra có đơn hàng mới không | Nếu có → gửi thông báo, không có → trả lời "Không có đơn hàng". |
| **Get All Orders/Get An Order Detail (Switch)** | Chuyển hướng logic | Chọn giữa lấy danh sách hoặc chi tiết đơn hàng. |
| **Get Order ID (Code)** | Trích xuất ID đơn hàng | Sử dụng **JavaScript** để lấy ID từ JSON Shopify. |
| **Send Orders to Telegram (HTTP Request)** | Gửi tin nhắn trước (nếu cần) | Có thể dùng để gửi tin nhắn preview. |

---
#### **4. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi lệnh `/orders` đến bot Telegram.
  - Kiểm tra nếu bot trả lời với danh sách đơn hàng mới.
- **Bật Active**:
  - Nhấn **Active** trên workflow → Workflow sẽ chạy tự động khi nhận lệnh.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi báo cáo hàng ngày**
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày (ví dụ: 8h sáng) và gửi **tóm tắt đơn hàng mới** qua Telegram.
   - **Cách làm**:
     - Thêm **Cron Trigger** vào đầu workflow.
     - Đặt lịch là `0 8 * * *` (8h sáng hàng ngày).
     - Sửa node **Telegram Trigger** thành **HTTP Request** để gửi tin nhắn tự động.

2. **Kết nối với Slack/Email**
   - Thêm **Slack Node** hoặc **Email Node** để thông báo đồng thời với Telegram.
   - **Cách làm**:
     - Sau node **Send Order Details**, thêm **Slack Node** (nếu muốn thông báo trên Slack).
     - Cấu hình **Webhook URL** từ Slack App.

3. **Lưu log đơn hàng vào Google Sheets**
   - Thêm **Google Sheets Node** để ghi lại tất cả đơn hàng vào bảng Excel.
   - **Cách làm**:
     - Sau node **Send Order Details**, thêm **Google Sheets Node**.
     - Chọn **Sheet Name** và cấu hình **Append Row** để thêm dữ liệu mới.

4. **Cập nhật trạng thái đơn hàng**
   - Sử dụng **Webhook Shopify** để nhận thông báo khi đơn hàng được cập nhật (ship, hủy, hoàn tiền).
   - **Cách làm**:
     - Tạo **Webhook** trong Shopify → Chỉ định URL của n8n.
     - Thêm **HTTP Request Node** để xử lý sự kiện cập nhật.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc kiểm tra đơn hàng thủ công, đồng thời **tăng cường hiệu quả** trong quản lý bán hàng. **Chỉ cần cài đặt 1 lần**, bot sẽ **làm việc tự động** mọi lúc, mọi nơi!

**🚀 Hãy áp dụng ngay và trải nghiệm sự tiện lợi của tự động hóa!**
- **Nếu có vấn đề**, hãy để lại comment dưới bài viết hoặc chat với **Roninimous** (tác giả workflow).
- **Bạn muốn thêm tính năng gì?** Hãy chia sẻ ý tưởng, chúng ta sẽ tối ưu workflow cho phù hợp!

---
**🔥 Cảm ơn các sếp đã đọc đến cuối!** 🔥
**#TựĐộngHóaShopify #BotTelegram #N8N #EcommerceAutomation**