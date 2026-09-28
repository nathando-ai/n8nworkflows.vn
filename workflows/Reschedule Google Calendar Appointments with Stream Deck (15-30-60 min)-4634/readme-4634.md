---
title: "🔄 **Tự Động Hoàn Tất Cuộc Hẹn Google Calendar Với Stream Deck (15-30-60 Phút) – Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn tất cuộc hẹn Google Calendar chỉ bằng một nút nhấn trên Stream Deck, tiết kiệm thời gian và giảm thiểu lỗi quên. Hoạt động 24/7, phù hợp cho doanh nghiệp và cá nhân bận rộn."
slug: "tieu-dong-hoan-tat-cuoc-hen-google-calendar-stream-deck"
tags: [n8n, automation, google-calendar, stream-deck, no-code, productivity]
keywords: [tự động hóa google calendar, stream deck n8n, hoàn tất cuộc hẹn tự động, tiết kiệm thời gian, workflow n8n google calendar]
---

# 🚀 **Hoàn Tất Cuộc Hẹn Google Calendar Với Stream Deck – Không Cần Code!**

### **💥 Nỗi Đau Thực Tế Của Các Sếp**
Bạn có bao giờ **quên hoàn tất cuộc hẹn** trong Google Calendar, dẫn đến mất thời gian gọi lại hoặc làm mất uy tín với khách hàng? Hay phải **nhấn chuột nhiều lần** để hoàn tất hàng loạt cuộc hẹn, khiến công việc trở nên chậm chạp?

Với **workflow này**, các sếp có thể:
✅ **Hoàn tất cuộc hẹn chỉ bằng một nút nhấn** trên Stream Deck.
✅ **Tự động đẩy lại cuộc hẹn** sau 15, 30 hoặc 60 phút nếu chưa hoàn tất.
✅ **Tiết kiệm thời gian** lên đến **30 phút/ngày** cho các cuộc họp thường xuyên.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải nhấn chuột nhiều lần để hoàn tất cuộc hẹn.
- **Tăng hiệu quả**: Hoàn tất cuộc hẹn chỉ bằng **một nút nhấn** trên Stream Deck.
- **Không quên cuộc hẹn**: Hệ thống tự động đẩy lại cuộc hẹn nếu chưa hoàn tất.
- **Hoạt động liên tục**: Workflow chạy tự động, không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để kết nối với Google Calendar).
✔ **API Key của Google Calendar** (cần cấp quyền cho ứng dụng n8n).
✔ **Stream Deck** (để tạo nút nhấn kích hoạt workflow).
✔ **n8n Self-hosted** (để chạy workflow 24/7).

---
:::info[CHUẨN BỊ]
**Cách lấy API Key Google Calendar:**
1. Truy cập [Google Cloud Console](https://console.cloud.google.com/).
2. Tạo một **projet mới**.
3. Bật **Google Calendar API**.
4. Tạo **OAuth 2.0 Client ID** và sao chép **Client ID** và **Client Secret**.
5. Trong n8n, thêm **credentials mới** cho Google Calendar và nhập thông tin OAuth.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor.

**Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/4634).
**Bước 2:** Trong n8n Editor, nhấn **Import** và chọn file JSON.
**Bước 3:** Workflow sẽ xuất hiện với **11 node** như sau:

| STT | Tên Node | Loại Node | Mô Tả |
|-----|----------|-----------|--------|
| 1 | Get the Events for the Rest of the Day | Google Calendar | Lấy danh sách cuộc hẹn còn lại trong ngày. |
| 2 | Respond with 200 | Respond to Webhook | Trả lời thành công khi nhận được yêu cầu. |
| 3 | Hit this URL from Streamdeck http request button | Webhook | Nút nhấn trên Stream Deck để kích hoạt workflow. |
| 4 | Push All Meetings 15 Minutes Later | Google Calendar | Đẩy lại cuộc hẹn sau 15 phút. |
| 5 | Push All Meetings 30 Minutes Later | Google Calendar | Đẩy lại cuộc hẹn sau 30 phút. |
| 6 | Push All Meetings 60 Minutes Later | Google Calendar | Đẩy lại cuộc hẹn sau 60 phút. |
| 7 | Get the Events for the Rest of the Day 15 | Google Calendar | Lấy lại danh sách cuộc hẹn sau 15 phút. |
| 8 | Hit this URL from Streamdeck http request button 15 | Webhook | Nút nhấn Stream Deck cho thời gian 15 phút. |
| 9 | Get the Events for the Rest of the Day 60 | Google Calendar | Lấy lại danh sách cuộc hẹn sau 60 phút. |
| 10 | Hit this URL from Streamdeck http request button 60 | Webhook | Nút nhấn Stream Deck cho thời gian 60 phút. |
| 11 | Respond with 500 | Respond to Webhook | Trả lời lỗi nếu có vấn đề. |

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Các node quan trọng cần cấu hình:

##### **🔹 Node Webhook (Nút nhấn Stream Deck)**
- **Cấu hình URL Webhook** trong Stream Deck:
  - Mở **Stream Deck** → Tạo một **Action mới** → Chọn **HTTP Request**.
  - Nhập **URL Webhook** từ node `Hit this URL from Streamdeck http request button` (của workflow).
  - Chọn **POST** và gửi yêu cầu.

##### **🔹 Node Google Calendar**
- **Thiết lập credentials**:
  - Trong n8n, chọn **Google Calendar** → **Add Credentials** → Nhập **Client ID** và **Client Secret** từ Google Cloud Console.
  - Chọn **OAuth 2.0** và cấp quyền cho ứng dụng.
- **Cấu hình node `Get the Events for the Rest of the Day`**:
  - Chọn **Calendar ID** (thường là email của tài khoản Google).
  - Chọn **Time Zone** (ví dụ: `Asia/Ho Chi Minh`).
  - Chọn **Start Time** (ví dụ: `2024-01-01T00:00:00Z`).
  - Chọn **End Time** (ví dụ: `2024-12-31T23:59:59Z`).

##### **🔹 Node `Push All Meetings X Minutes Later`**
- **Cấu hình thời gian đẩy lại**:
  - Trong mỗi node `Push All Meetings 15/30/60 Minutes Later`, chọn **Event ID** từ danh sách cuộc hẹn.
  - Chọn **New Start Time** (ví dụ: `+15 minutes`, `+30 minutes`, `+60 minutes`).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** để kiểm tra.
  - Kiểm tra **Google Calendar** xem cuộc hẹn có được đẩy lại không.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi cuộc hẹn được hoàn tất.
2. **Lưu Log**:
   - Sử dụng node **Set** hoặc **Sticky Note** để lưu lịch sử cuộc hẹn đã hoàn tất.
3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một workflow khác để gửi **báo cáo tổng hợp** về cuộc hẹn đã hoàn tất hàng tuần.

---
### 📌 **Kết Luận**
Với **workflow này**, các sếp không chỉ **tiết kiệm thời gian** mà còn **tránh được lỗi quên cuộc hẹn**. Hãy **import ngay** và **cài đặt Stream Deck** để bắt đầu tự động hóa cuộc hẹn của mình!

**🚀 Bắt đầu tự động hóa ngay hôm nay!** 🚀