---
title: "🌤️ **Hệ Thống Cảnh Báo Thời Tiết BMKG Tự Động + Thông Báo Telegram (N8N)**"
description: "Tự động lấy dữ liệu thời tiết từ BMKG và gửi cảnh báo định kỳ qua Telegram, giúp các sếp theo dõi thời tiết chính xác 24/7 mà không cần code. Giúp tiết kiệm thời gian, tránh mất mát do thời tiết bất ngờ."
slug: "huyet-thoi-tiet-bmkg-telegram-n8n"
tags: [n8n, automation, no-code, thời tiết, BMKG, Telegram, tự động hóa doanh nghiệp]
keywords: [n8n workflow thời tiết, tự động hóa cảnh báo thời tiết, BMKG API Telegram, tự động hóa doanh nghiệp, cảnh báo thời tiết tự động]
---

# 🚀 **Hệ Thống Cảnh Báo Thời Tiết BMKG Tự Động + Thông Báo Telegram (N8N)**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Hàng ngày, các sếp phải theo dõi thời tiết để điều chỉnh kế hoạch sản xuất, vận chuyển hàng hóa, hoặc tổ chức sự kiện ngoài trời. Tuy nhiên, việc **check thủ công** trên trang web BMKG hoặc ứng dụng thời tiết không chỉ tốn thời gian mà còn dễ bị bỏ qua hoặc sai sót. **Giải pháp này tự động lấy dữ liệu thời tiết từ BMKG và gửi cảnh báo qua Telegram**, giúp các sếp **nhận thông tin chính xác, kịp thời và không cần can thiệp thủ công**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần check thủ công hàng ngày.
- **Chính xác 100%**: Dữ liệu thời tiết từ **BMKG (Cục Khí tượng Thủy văn Quốc gia)**.
- **Cảnh báo kịp thời**: Nhận thông báo qua Telegram ngay khi có thay đổi thời tiết.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình (mỗi 6 giờ).
- **Dễ dàng mở rộng**: Thêm nhiều vùng miền hoặc thay đổi thời gian cảnh báo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Lấy **Chat ID** của tài khoản Telegram cá nhân (hướng dẫn dưới đây).
2. **API Key BMKG (nếu cần)**: Mặc định workflow lấy dữ liệu **miễn phí** từ BMKG, nhưng các sếp có thể tùy chỉnh thêm.
3. **Thông tin vùng miền BMKG** (tùy chọn):
   - Mỗi vùng miền có **mã adm4** (ví dụ: `31.71.03.1001` cho Hà Nội).
   - Danh sách mã vùng: [BMKG API Documentation](https://api.bmkg.go.id).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9675](https://n8n.io/workflows/9675).
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
- **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** (Ctrl+Shift+I).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Telegram Bot**
1. **Tạo Bot Telegram**:
   - Mở Telegram, tìm `@BotFather` và gửi `/newbot`.
   - Theo hướng dẫn đặt tên và username (ví dụ: `@WeatherBot`).
   - **Lưu API Token** (dạng `123456789:ABCdef...`).

2. **Lấy Chat ID**:
   - Gửi tin nhắn nào đó cho bot mới tạo.
   - Mở trình duyệt và truy cập:
     ```
     https://api.telegram.org/bot<API_TOKEN>/getUpdates
     ```
     (Thay `<API_TOKEN>` bằng token của bạn).
   - Trong JSON response, tìm `chat.id` (ví dụ: `123456789`).

3. **Cấu Hình Credentials Telegram**:
   - Trong n8n, đi đến **Credentials** → **Add** → **Telegram**.
   - Nhập **API Token** và tên credential (ví dụ: `telegramApi`).
   - **Áp dụng** cho cả hai node:
     - `Send Weather Report`
     - `Send Error Alert`

4. **Điền Chat ID**:
   - Trong hai node trên, thay thế `{{TELEGRAM_CHAT_ID}}` bằng **Chat ID** của bạn.

##### **B. Cấu Hình Vùng Miền BMKG (Tùy Chọn)**
- Mở node **Get BMKG Weather Data**.
- Thêm **Query Parameter** `adm4` với mã vùng của bạn (ví dụ: `31.71.03.1001` cho Hà Nội).
- Nếu không điền, workflow sẽ lấy dữ liệu mặc định (thường là toàn quốc).

##### **C. Cấu Hình Lịch Trình (Schedule Trigger)**
- Mặc định, workflow chạy **mỗi 6 giờ** (4 lần/ngày).
- Để thay đổi:
  - Nhấn **Edit** trên node **Schedule Trigger**.
  - Chọn **Cron Expression** hoặc thời gian cụ thể (ví dụ: `0 0 */6 * * *` để chạy lúc 00:00, 06:00, 12:00, 18:00).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra Telegram xem có nhận được thông báo không.
2. **Bật Active**:
   - Nhấn **Active** trên thanh công cụ để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Nhiều Vùng Miền**:
   - Sử dụng node **Code** để xử lý nhiều mã `adm4` cùng một lúc.
   - Ví dụ: Lấy dữ liệu cho Hà Nội, TP.HCM, Đà Nẵng trong một workflow.

2. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **Google Sheets** hoặc **Email** để lưu lịch sử thời tiết.
   - Sử dụng node **HTTP Request** để gửi dữ liệu đến API của mình.

3. **Cảnh Báo Trên Slack**:
   - Thay thế Telegram bằng **Slack Webhook** để cảnh báo trong nhóm làm việc.

4. **Lưu Log Lỗi**:
   - Node **Error Handler** đã được cấu hình để gửi lỗi qua Telegram.
   - Các sếp có thể mở rộng để lưu log vào **Google Drive** hoặc **Database**.

5. **Tùy Chỉnh Nội Dung Thông Báo**:
   - Sửa node **Format Telegram Message** để thay đổi định dạng tin nhắn (ví dụ: thêm biểu tượng thời tiết).

---

### 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa việc theo dõi thời tiết**, tiết kiệm thời gian và tránh mất mát do thời tiết bất ngờ. **Chỉ cần cài đặt một lần**, hệ thống sẽ hoạt động **24/7** mà không cần can thiệp thủ công.

**🚀 Hãy áp dụng ngay và làm việc thông minh hơn!**
Nếu có vấn đề, các sếp có thể tham khảo:
- [BMKG API Documentation](https://api.bmkg.go.id)
- [n8n Documentation](https://docs.n8n.io)
- [Hướng Dẫn Tạo Bot Telegram](https://core.telegram.org/bots)

---
**💡 Mẹo cuối**: Để workflow chạy ổn định, các sếp nên **self-host n8n trên VPS** (không phụ thuộc vào phiên bản miễn phí). [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**!