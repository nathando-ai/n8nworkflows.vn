---
title: "📅 Tự Động Hóa Báo Cáo Lịch Hàng Ngày Trên Telegram Từ Google Calendar (N8n)"
description: "Workflow tự động gửi tóm tắt lịch hằng ngày qua Telegram từ Google Calendar, tiết kiệm thời gian và giúp bạn không bỏ lỡ bất kỳ cuộc họp hay sự kiện quan trọng nào. Hoạt động tự động 7h sáng hàng ngày, không cần can thiệp thủ công."
slug: "tieu-dong-hoa-bao-cao-lich-hang-ngay-tren-telegram"
tags: [n8n, automation, google-calendar, telegram-bot, productivity, no-code]
keywords: [n8n workflow, tự động hóa lịch google, báo cáo hàng ngày telegram, tự động hóa productivity, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Báo Cáo Lịch Hàng Ngày Trên Telegram Từ Google Calendar**

### **Giải pháp cho ai?**
Các sếp, quản lý hoặc người làm việc với lịch trình bận rộn thường gặp phải vấn đề:
- **Quên bỏ lỡ cuộc họp quan trọng** vì không kiểm tra lịch thường xuyên.
- **Phải mở nhiều ứng dụng** để xem lịch và thông báo từ nhiều nguồn.
- **Tốn thời gian** để tổng hợp thông tin và gửi báo cáo cho đồng nghiệp.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động:
✅ **Gửi tóm tắt lịch hằng ngày** qua Telegram vào 7h sáng.
✅ **Tự động phân tích và tổng hợp** tất cả sự kiện trong ngày.
✅ **Gửi thông báo cá nhân hóa** nếu không có cuộc họp nào (tránh nhầm lẫn).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **30 phút/ngày** (không phải mở Google Calendar thủ công).
- **Không bỏ lỡ bất kỳ cuộc họp nào** nhờ thông báo tự động.
- **Tính năng cá nhân hóa** với thông báo "Không có cuộc họp hôm nay" nếu lịch trống.
- **Hoạt động liên tục** ngay cả khi bạn đang ngủ hoặc bận rộn.
- **Dễ dàng mở rộng** để kết hợp với Slack, Email hoặc lưu log lịch sử.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tài khoản Google** (để kết nối với Google Calendar).
- **Google Calendar API** (đăng ký và tạo OAuth 2.0 credentials).
- **Bot Telegram** (tạo bot và lấy API Key).
- **n8n Self-hosted** (để workflow chạy 24/7 ổn định).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/6952](https://n8n.io/workflows/6952) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6952) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần cấu hình như sau:

##### **🔹 Node 1: 7am trigger (scheduleTrigger)**
- **Không cần chỉnh sửa gì** (cấu hình mặc định là 7h sáng hàng ngày).

##### **🔹 Node 2: Check google Calendar (googleCalendar)**
- **Credentials:** Chọn `"googleCalendarOAuth2Api"` (đã tạo trước khi import).
- **Operation:** Để mặc định là `"getAll"` (lấy tất cả sự kiện trong ngày).
- **Lưu ý:**
  - Đảm bảo **Google Calendar API** đã được kích hoạt trong [Google Cloud Console](https://console.cloud.google.com/).
  - **Cấp quyền** cho OAuth 2.0 credentials (quyền đọc lịch).

##### **🔹 Node 3: Count event (code)**
- **Không cần chỉnh sửa** (node này tự động đếm số lượng sự kiện).

##### **🔹 Node 4: If condition (if)**
- **Không cần chỉnh sửa** (node này phân nhánh dựa trên số lượng sự kiện).

##### **🔹 Node 5: Message code (code) & Send sum up message (telegram) [True branch]**
- **Cấu hình Telegram Bot:**
  - Đăng ký bot trên [@BotFather](https://t.me/BotFather) và lấy **API Key**.
  - Trong node `Message code`, chỉnh sửa **JavaScript** để hiển thị thông tin sự kiện (ví dụ: tên, thời gian, địa điểm).
  - **Dữ liệu mẫu trong code:**
    ```javascript
    // Dữ liệu mẫu (các sếp có thể chỉnh sửa theo ý muốn)
    const events = $input.all();
    let message = `📅 **Lịch hôm nay (${new Date().toLocaleDateString()})**\n\n`;

    events.forEach(event => {
      message += `🕒 ${event.start.dateTime || event.start.date} - ${event.end.dateTime || event.end.date}\n`;
      message += `📍 ${event.summary}\n`;
      message += `📌 ${event.description || 'Không có mô tả'}\n\n`;
    });

    return { json: { text: message } };
    ```
- **Node `Send sum up message`:**
  - Chọn **credentials** là `"telegramApi"` (đã tạo từ API Key).
  - **Message format:** Sử dụng kết quả từ node `Message code`.

##### **🔹 Node 6: Message no meeting today (telegram) [False branch]**
- **Cấu hình Telegram Bot:**
  - Sử dụng cùng **credentials** `"telegramApi"` như trên.
  - **Message mẫu:**
    ```
    🚨 **Không có cuộc họp nào hôm nay!** 🎉
    Bạn có thể nghỉ ngơi hoặc làm việc khác nhé!
    ```

---

#### **3. Kích hoạt ⚡️**
- **Test run:**
  - Chạy **manual execution** để kiểm tra workflow với dữ liệu mẫu.
  - Kiểm tra **Telegram Bot** có nhận được thông báo không.
- **Bật Active:**
  - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Slack:** Thay vì Telegram, các sếp có thể gửi báo cáo lên Slack bằng node `slack`.
- **Lưu log lịch sử:** Sử dụng node `stickyNote` hoặc `database` để lưu lịch sử báo cáo.
- **Gửi báo cáo định kỳ:** Thay vì 7h sáng, các sếp có thể điều chỉnh thời gian bằng node `scheduleTrigger`.
- **Tích hợp với Notion/Google Sheets:** Lưu thông tin lịch vào Notion hoặc Google Sheets bằng node `notion` hoặc `googleSheets`.
- **Cảnh báo trước cuộc họp:** Sử dụng node `webhook` để gửi thông báo cảnh báo 10 phút trước cuộc họp.
:::

---

### 📌 **Kết luận**
Workflow **Daily Calendar Summary Notifications via Telegram** là giải pháp **tự động hóa hoàn hảo** để các sếp không bao giờ bỏ lỡ cuộc họp, tiết kiệm thời gian và tăng hiệu suất làm việc.

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận báo cáo lịch tự động mỗi sáng!

👉 **🎁 Mã giảm giá VPS cho n8n:**
- [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã: **VPSN8N** - giảm tới 39%)
- [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ **50k/tháng**)

**Chúc các sếp tự động hóa thành công!** 🚀