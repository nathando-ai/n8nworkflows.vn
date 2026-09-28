---
title: "🎮 Kiểm Tra Trực Tiếp Live Twitch Tự Động - Không Cần Code!"
description: "Tự động hóa việc kiểm tra trạng thái live của streamer Twitch bằng n8n, tiết kiệm thời gian và tránh bỏ lỡ những buổi stream quan trọng. Workflow hoạt động 24/7, kết quả chính xác 100%."
slug: kiem-tra-twitch-stream-live-tu-dong
tags: [n8n, automation, twitch, marketing, no-code]
keywords: [kiểm tra stream twitch tự động, tự động hóa twitch, n8n workflow twitch, check live twitch, tự động hóa marketing]
---

# 🎮 **Kiểm Tra Trực Tiếp Live Twitch Tự Động - Không Cần Code!**

### **Nỗi Đau Của Các Sếp**
Làm sao để **biết ngay khi một streamer Twitch bắt đầu live** mà không phải phải **quay lại và check liên tục** trên trang web? Hay khi tổ chức **event marketing** trên Twitch, bạn **không thể bỏ lỡ** những buổi stream quan trọng vì phải theo dõi thủ công? Hay đơn giản là **muốn tự động hóa việc kiểm tra trạng thái live** để **tích hợp với Slack/Telegram/Email** báo động?

**Workflow này giải quyết tất cả!** Với chỉ **4 node đơn giản**, bạn có thể **kiểm tra trạng thái live của bất kỳ streamer Twitch nào** và **tự động hóa cảnh báo** khi họ bắt đầu hoặc kết thúc stream.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
✅ **Tiết kiệm thời gian** – Không phải check thủ công trên Twitch mỗi giờ.
✅ **Chính xác 100%** – Dựa trên API GraphQL của Twitch, không sai sót.
✅ **Tích hợp dễ dàng** – Kết nối với **Slack, Telegram, Email, hoặc bất kỳ hệ thống nào** để báo động.
✅ **Hoạt động liên tục** – Chạy tự động 24/7 trên VPS, không cần can thiệp.
✅ **Miễn phí** – Sử dụng phiên bản **Self-hosted** của n8n.

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi **lên đồ**, các sếp cần chuẩn bị:
✔ **Tài khoản Twitch** (để lấy **username** của streamer cần check).
✔ **Client ID của Twitch** (mã API được cung cấp bởi Twitch cho phép gọi API).
   - **Lấy Client ID**:
     1. Đăng nhập vào [Twitch Developer Console](https://dev.twitch.tv/console/apps).
     2. Tạo một **new app** (nếu chưa có).
     3. Copy **Client ID** từ trang app của bạn.
✔ **Tài khoản n8n** (cài đặt **Self-hosted** trên VPS).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2684) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không cần nhiều cấu hình**, nhưng có **2 điểm quan trọng** cần chú ý:

##### **A. Node "Twitch GraphQL" (Gọi API Twitch)**
- **Query GraphQL** đã được **cấu hình sẵn** để lấy trạng thái live của streamer.
- **Tham số cần điền:**
  - **`clientId`**: Dán **Client ID** của bạn (lấy từ Twitch Developer Console).
  - **`username`**: Điền **username Twitch** của streamer bạn muốn check (ví dụ: `"ngocdieunhi"`).
  - **Headers**:
    - `Client-ID`: Dán **Client ID** của bạn.
    - `Authorization`: Trống (Twitch cho phép gọi API không cần token cho trường hợp này).

##### **B. Node "Is Online" (Kiểm Tra Trạng Thái)**
- Workflow **so sánh giá trị `stream`** trong kết quả API:
  - Nếu `stream` là **`null`** → Streamer **không live**.
  - Nếu `stream` có **giá trị** → Streamer **đang live**.

##### **C. Node "Manual Trigger" (Test Run)**
- **Không cần cấu hình gì** – chỉ dùng để **test workflow** trước khi kích hoạt.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **username** của streamer bạn muốn check.
2. Kiểm tra kết quả:
   - Nếu streamer **live**, workflow sẽ **trả về `stream` có giá trị**.
   - Nếu **không live**, `stream` sẽ là `null`.
3. **Bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Tích Hợp Với Slack/Telegram/Báo Động Email**
- **Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.email`** để gửi thông báo khi streamer live.
- **Ví dụ:**
  - Nếu `stream` có giá trị → Gửi tin nhắn Slack: *"🚨 [Username] đã bắt đầu live!"*
  - Nếu `stream` là `null` → Gửi tin nhắn: *"[Username] đã offline."*

#### **2. Lưu Log Kết Quả**
- **Thêm node `n8n-nodes-base.googleSheets`** để lưu lịch sử check live vào Google Sheets.
- **Cấu hình:**
  - Chọn **Sheet** và **Sheet Name** phù hợp.
  - Lưu các trường: `username`, `timestamp`, `isLive`.

#### **3. Chạy Định Kỳ (Cron Job)**
- **Sử dụng node `n8n-nodes-base.schedule`** để **check live tự động** mỗi 5-10 phút thay vì phải kích hoạt thủ công.
- **Cấu hình:**
  - Chọn **lịch trình** (ví dụ: `0 */5 * * *` để chạy mỗi 5 phút).

#### **4. Kết Hợp Với Bot Telegram**
- **Sử dụng node `n8n-nodes-base.telegram`** để **báo động qua Telegram** khi streamer live.
- **Cấu hình:**
  - Điền **Token API** và **Chat ID** của bot Telegram.
  - Gửi tin nhắn tự động khi có sự kiện live.

---

### 📌 **Kết Luận**
**Workflow này giúp các sếp:**
✔ **Tự động hóa việc check live Twitch** mà không cần code.
✔ **Tiết kiệm thời gian** và tránh bỏ lỡ những buổi stream quan trọng.
✔ **Tích hợp với nhiều hệ thống** (Slack, Email, Telegram, Google Sheets...).

**Hãy áp dụng ngay!** Nếu có **yêu cầu tùy chỉnh** (ví dụ: check nhiều streamer cùng lúc, báo động với điều kiện đặc biệt), **liên hệ với tôi** để hỗ trợ!

---
**🚀 Bắt đầu tự động hóa ngay hôm nay!** 🚀