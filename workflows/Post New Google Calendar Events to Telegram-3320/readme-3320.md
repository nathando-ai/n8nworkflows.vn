---
title: "📅 Tự Động Hóa Sự Kiện Google Calendar Sang Telegram - Không Cần Code!"
description: "Workflow này tự động chuyển tất cả sự kiện mới từ Google Calendar sang Telegram với chi tiết đầy đủ (tên, mô tả, người tạo, thời gian, địa điểm). Giúp các sếp không bỏ lỡ bất kỳ sự kiện nào và cập nhật tức thời qua Telegram."
slug: "tu-dong-hoa-su-kien-google-calendar-sang-telegram"
tags: [n8n, automation, google-calendar, telegram-bot, no-code, calendar-notification]
keywords: [tự động hóa sự kiện google calendar, telegram bot nhận sự kiện mới, n8n workflow google calendar, cảnh báo sự kiện google calendar, tự động hóa công việc hàng ngày]
---

# 🚀 **Tự Động Hóa Sự Kiện Google Calendar Sang Telegram - Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp**
Các sếp có thể đã từng gặp phải tình huống này:
- **Bỏ lỡ sự kiện quan trọng** vì không cập nhật kịp thời từ Google Calendar.
- **Phải mở nhiều tab** để kiểm tra sự kiện mới từ Google Calendar và chuyển sang Telegram.
- **Thiếu tính cá nhân hóa** trong thông báo sự kiện, khiến việc quản lý lịch trở nên rườm rà.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động chuyển tất cả sự kiện mới từ Google Calendar sang Telegram **với chi tiết đầy đủ**, giúp các sếp **không bao giờ bỏ lỡ một sự kiện nào** và **cập nhật tức thời** qua Telegram.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải mở Google Calendar và chuyển sang Telegram thủ công.
- **Cập nhật tức thời**: Nhận thông báo ngay khi có sự kiện mới được thêm vào Google Calendar.
- **Chi tiết đầy đủ**: Nhận tất cả thông tin quan trọng (tên sự kiện, mô tả, người tạo, thời gian bắt đầu/kết thúc, địa điểm).
- **Tính cá nhân hóa cao**: Thông báo được gửi trực tiếp đến Telegram, giúp các sếp quản lý lịch một cách hiệu quả hơn.
- **Hoạt động liên tục 24/7**: Workflow chạy tự động, không phụ thuộc vào thời gian làm việc của cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar**:
   - **API Key OAuth 2.0**: Cần tạo và cấu hình trong [Google Cloud Console](https://console.cloud.google.com/).
   - **Thông tin OAuth**: Sau khi tạo, lưu lại `Client ID` và `Client Secret` để cấu hình trong n8n.
2. **Bot Telegram**:
   - **Bot Token**: Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy `API Token`.
   - **Chat ID**: Lấy `Chat ID` của nhóm hoặc tài khoản Telegram muốn nhận thông báo (có thể dùng [tool này](https://api.telegram.org/bot<BOT_TOKEN>/getUpdates) để tìm).
3. **Dịch vụ n8n**:
   - **Self-hosted n8n** (khuyến nghị) hoặc sử dụng n8n Cloud (miễn phí cho các dự án nhỏ).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON**: Tải workflow từ [đây](https://n8n.io/workflows/3320) (hoặc copy JSON từ trang này).
- **Import vào n8n**:
  - Mở **n8n Editor** → Nhấn `Import` → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
  - Nhấn `Import` để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này chỉ có **2 node chính**, nhưng các sếp cần cấu hình **cẩn thận** để hoạt động hiệu quả:

##### **Node 1: Google Calendar Trigger (`n8n-nodes-base.googleCalendarTrigger`)**
- **Credentials**:
  - Chọn `googleCalendarOAuth2Api` (đã cấu hình trước khi import).
  - Nếu chưa cấu hình, nhấn `Add` → Chọn `Google Calendar OAuth 2.0` → Điền `Client ID` và `Client Secret` từ Google Cloud Console.
- **Tham Số Cấu Hình**:
  - **Calendar ID**: Chọn **Calendar** muốn theo dõi sự kiện (ví dụ: `primary` hoặc ID cụ thể của Calendar).
  - **Event Type**: Chọn `Event` (để theo dõi tất cả sự kiện mới).
  - **Sync Mode**: Chọn `Polling` (để n8n kiểm tra sự kiện mới định kỳ).

##### **Node 2: Telegram (`n8n-nodes-base.telegram`)**
- **Credentials**:
  - Chọn `telegram` (đã cấu hình trước khi import).
  - Nếu chưa cấu hình, nhấn `Add` → Chọn `Telegram` → Điền `Bot Token` từ `@BotFather`.
- **Tham Số Cấu Hình**:
  - **Chat ID**: Điền `Chat ID` của nhóm hoặc tài khoản Telegram muốn nhận thông báo.
  - **Message**: Sử dụng **Dynamic Content** để hiển thị thông tin sự kiện:
    ```
    **Tên Sự Kiện**: $json["event"]["summary"]
    **Mô Tả**: $json["event"]["description"]
    **Người Tạo**: $json["event"]["creator"]["email"]
    **Thời Gian Bắt Đầu**: $json["event"]["start"]["dateTime"]
    **Thời Gian Kết Thúc**: $json["event"]["end"]["dateTime"]
    **Địa Điểm**: $json["event"]["location"]
    ```
  - **Parse Mode**: Chọn `Markdown` để định dạng thông báo đẹp mắt.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Thêm một sự kiện mới vào Google Calendar → Kiểm tra Telegram có nhận thông báo không.
  - Nếu không hoạt động, kiểm tra lại **credentials** và **Dynamic Content**.
- **Bật Active Workflow**:
  - Sau khi test thành công, nhấn `Active` để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo định kỳ**:
   - Sử dụng **n8n-nodes-base.set** để lọc sự kiện mới trong ngày và gửi báo cáo tổng hợp vào buổi sáng.
2. **Kết hợp với Slack**:
   - Thêm node `n8n-nodes-base.slack` để gửi thông báo sự kiện sang Slack cùng lúc.
3. **Lưu log sự kiện**:
   - Sử dụng **n8n-nodes-base.stickyNote** (đã có trong workflow) để lưu lịch sử sự kiện đã chuyển.
4. **Tự động tạo sự kiện từ Telegram**:
   - Ngược lại, các sếp có thể thêm node `n8n-nodes-base.telegram` để nhận sự kiện từ Telegram và tự động tạo vào Google Calendar.
5. **Cảnh báo trước khi sự kiện bắt đầu**:
   - Sử dụng **n8n-nodes-base.dateTime** để so sánh thời gian và gửi thông báo nhắc nhở trước 1 giờ.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách tự động hóa việc cập nhật sự kiện từ Google Calendar sang Telegram. **Không cần code**, không cần mở nhiều tab, và **không bao giờ bỏ lỡ một sự kiện nào**!

👉 **Hãy import ngay và bắt đầu sử dụng!**
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với **WeblineIndia** (tác giả của workflow) qua [đây](https://www.weblineindia.com/).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::