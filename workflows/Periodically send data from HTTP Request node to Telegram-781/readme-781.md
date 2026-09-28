---
title: "🚀 Tự Động Gửi Dữ Liệu Từ API Sang Telegram Hàng Ngày - Không Cần Code!"
description: "Workflow tự động hóa gửi dữ liệu từ HTTP Request sang Telegram định kỳ (hàng ngày/tuần) bằng n8n, giúp các sếp tiết kiệm thời gian và cập nhật thông tin nhanh chóng. Phù hợp cho báo cáo, alert, hoặc chia sẻ dữ liệu quan trọng."
slug: "tieu-dong-gui-du-lieu-api-sang-telegram"
tags: [n8n, automation, telegram-bot, cron-job, http-api]
keywords: [n8n workflow telegram, tự động hóa telegram, gửi dữ liệu định kỳ, cron job n8n, API Telegram]
---

# 🚀 **Tự Động Gửi Dữ Liệu Từ API Sang Telegram Hàng Ngày - Không Cần Code!**

### **💡 Giải quyết vấn đề gì?**
Các sếp thường phải **thủ công** kiểm tra dữ liệu từ API (ví dụ: API nội bộ, API công cộng) và **gửi thông báo qua Telegram** để cập nhật cho team hoặc khách hàng. Đây là một công việc **lặp đi lặp lại, tốn thời gian** và dễ bị bỏ quên. **Workflow này tự động hóa toàn bộ quá trình** bằng cách:
✅ **Lấy dữ liệu từ API** (HTTP Request) **mỗi ngày/tuần** (bằng Cron Job).
✅ **Gửi kết quả dưới dạng ảnh** (hoặc text) **vào Telegram** một cách tự động.
✅ **Không cần viết code**, chỉ cần cấu hình đơn giản trên n8n.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải **thủ công** lấy dữ liệu và gửi Telegram hàng ngày.
- **Chính xác & không bỏ lỡ**: Cron Job đảm bảo **gửi dữ liệu đúng thời gian** (mặc dù máy tính tắt, workflow vẫn hoạt động).
- **Cá nhân hóa thông báo**: Chỉ cần **cấu hình API URL** và **thiết lập Telegram Bot**, workflow sẽ tự động xử lý.
- **Dễ dàng mở rộng**: Có thể **thêm nhiều API khác** hoặc **chuyển đổi dữ liệu** trước khi gửi.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram** và **Token API** của Bot Telegram:
   - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy **Token API** (dạng `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`).
✔ **URL API** mà workflow sẽ gọi (ví dụ: `https://api.example.com/data`).
✔ **VPS n8n** (nếu tự host) hoặc tài khoản **n8n Cloud** (miễn phí cho workflow đơn giản).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/781](https://n8n.io/workflows/781) và **import** vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/781) và **paste** vào **Create Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **3 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: HTTP Request (Lấy dữ liệu từ API)**
- **Method**: Chọn `GET` (hoặc `POST` nếu API yêu cầu).
- **URL**: Điền **URL API** của các sếp (ví dụ: `https://api.example.com/data`).
- **Headers (nếu cần)**: Nếu API yêu cầu **Headers** (ví dụ: `Authorization: Bearer token`), thêm vào **Request Headers**.
- **Test Run**: Nhấn **Execute Node** để kiểm tra dữ liệu trả về.

##### **🔹 Node 2: Cron (Thiết lập lịch chạy)**
- **Schedule**: Chọn **lịch chạy** (ví dụ: `0 0 * * *` = **lúc 00:00 hàng ngày**).
   - Cú pháp Cron: [Tìm hiểu chi tiết](https://crontab.guru/).
- **Timezone**: Chọn **múi giờ** phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Test Run**: Nhấn **Execute Node** để kiểm tra lịch chạy.

##### **🔹 Node 3: Telegram (Gửi dữ liệu)**
- **Credentials**: Chọn **telegramApi** (cần **cấu hình trước** trong n8n).
   - **Cách cấu hình Telegram API**:
     1. Vào **Credentials** → **Add Credential** → **Telegram**.
     2. Điền **Token API** từ BotFather và **Chat ID** (lấy bằng cách gửi `/start` cho bot và copy ID từ Telegram).
- **Operation**: Chọn **`sendPhoto`** (gửi dưới dạng ảnh) hoặc **`sendMessage`** (gửi text).
   - **Nếu gửi ảnh**:
     - Sử dụng **`{{ $json }}`** để chuyển đổi dữ liệu JSON thành ảnh (có thể sử dụng **n8n-nodes-base.helpers** để format).
     - Ví dụ: Sử dụng **`{{ $node["HTTP Request"].json | toString }}`** và chuyển đổi thành ảnh bằng **n8n-nodes-base.helpers**.
   - **Nếu gửi text**:
     - Sử dụng **`{{ $node["HTTP Request"].json }}`** để hiển thị dữ liệu JSON.
- **Test Run**: Nhấn **Execute Node** để kiểm tra thông báo Telegram.

#### **3. Kích hoạt ⚡️**
- **Bật Active**: Sau khi cấu hình xong, **bật workflow** và **chờ Cron chạy**.
- **Kiểm tra**: Mở Telegram và kiểm tra bot đã nhận được thông báo chưa.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Chuyển đổi dữ liệu trước khi gửi**:
   - Sử dụng **`n8n-nodes-base.helpers`** để **format dữ liệu** (ví dụ: chuyển JSON thành bảng hoặc biểu đồ) trước khi gửi Telegram.
   - Ví dụ: Sử dụng **`{{ $node["HTTP Request"].json | toPrettyJson }}`** để hiển thị dữ liệu đẹp mắt.

2. **Gửi nhiều bot/nhóm Telegram**:
   - Sử dụng **`n8n-nodes-base.telegram`** với **một bot** và **nhiều Chat ID** (tách nhau bằng dấu phẩy).
   - Ví dụ: `chatId1,chatId2,chatId3`.

3. **Lưu log dữ liệu**:
   - Thêm **`n8n-nodes-base.googleSheets`** hoặc **`n8n-nodes-base.slack`** để **lưu lịch sử** của dữ liệu đã gửi.

4. **Kết hợp với Slack**:
   - Thêm **`n8n-nodes-base.slack`** để **gửi thông báo đồng thời** đến Slack và Telegram.

5. **Sử dụng biến môi trường**:
   - Để **an toàn**, các sếp có thể **lưu Token API** trong **biến môi trường** thay vì trong Credentials.

---
### 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa việc lấy dữ liệu từ API và gửi thông báo Telegram hàng ngày/tuần**, **không cần viết code**. **Chỉ cần cấu hình 3 node** và **bật Cron**, workflow sẽ hoạt động **một cách tự động và không ngừng**.

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và tránh bỏ quên công việc quan trọng!**
Nếu có vấn đề, các sếp có thể **comment dưới bài** hoặc liên hệ qua **Telegram** để được hỗ trợ.

---
**🔹 Xem thêm:**
- [Cách tạo Bot Telegram](https://core.telegram.org/bots/api)
- [Cú pháp Cron](https://crontab.guru/)
- [Tự host n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)