---
title: "🚀 Tự Động Hoàn Chỉnh Nhắc Nhở Ngày Hết Hạn Hóa Đơn Stripe Sang Google Calendar"
description: "Workflow tự động hóa hoàn toàn không cần code để theo dõi hóa đơn Stripe và tạo nhắc nhở trên Google Calendar cho các hóa đơn đến hạn trong 7 ngày tới. Giúp các sếp tiết kiệm thời gian quản lý và không bỏ lỡ bất kỳ khoản thanh toán nào."
slug: "tieu-dong-nhac-nho-hoa-don-stripe-sang-google-calendar"
tags: [n8n, automation, no-code, stripe, google-calendar, self-hosted]
keywords: [tự động hóa hóa đơn Stripe, nhắc nhở ngày hết hạn, google calendar automation, workflow n8n, quản lý tài chính tự động]
---

# 🚀 Tự Động Hoàn Chỉnh Nhắc Nhở Ngày Hết Hạn Hóa Đơn Stripe Sang Google Calendar

### 🔍 Nỗi Đau Của Các Sếp Khi Quản Lý Hóa Đơn Thủ Công
Các sếp thường phải mất thời gian quét hàng ngày qua các hóa đơn Stripe để nhớ ngày hết hạn, lo lắng về việc bỏ lỡ thanh toán, hoặc phải nhắc nhở khách hàng một cách thủ công. Điều này không chỉ tốn thời gian mà còn dễ gây ra lỗi do con người, ảnh hưởng đến dòng tiền và mối quan hệ với khách hàng.

Workflow này **tự động hóa hoàn toàn** quá trình này bằng cách:
- **Lấy dữ liệu hóa đơn** từ Stripe mỗi ngày.
- **Lọc hóa đơn đến hạn trong 7 ngày tới**.
- **Tạo nhắc nhở trên Google Calendar** chỉ cho các hóa đơn mới, tránh trùng lặp.
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công hóa đơn hàng ngày.
- **Tránh bỏ lỡ thanh toán**: Nhắc nhở tự động cho hóa đơn đến hạn.
- **Tránh trùng lặp**: Chỉ tạo nhắc nhở cho hóa đơn mới.
- **Hoạt động liên tục**: Dữ liệu cập nhật mỗi ngày vào 8h sáng.
- **Dễ dàng theo dõi**: Tất cả thông tin hóa đơn được gắn vào Google Calendar.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tài khoản Stripe** với **Stripe Secret Key** (để lấy dữ liệu hóa đơn).
- **Tài khoản Google** với **OAuth2 API Key** cho Google Calendar (để tạo nhắc nhở).
- **Google Calendar** cụ thể để lưu nhắc nhở (không phải Calendar mặc định).
- **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import Workflow** và chọn file JSON hoặc dán JSON từ [đây](https://n8n.io/workflows/8948).
3. Chọn **Create New Workflow** và nhấn **Import**.

#### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng sau:

##### **1. Schedule Trigger (Điều Khiển Lịch Trình)**
- **Cấu hình cron**: `0 8 * * *` (chạy hàng ngày lúc 8h sáng).
- **Lưu ý**:
  - Đảm bảo **timezone** trong n8n phù hợp với khu vực của bạn.
  - Test với cron ngắn (ví dụ: `0 */15 * * *` để chạy mỗi 15 phút trong quá trình thử nghiệm).

##### **2. Get Stripe Invoices (Lấy Hóa Đơn Stripe)**
- **Credentials**: Chọn **stripeApi** (đã cấu hình trước).
- **Query Parameters**:
  - `status=draft` (chỉ lấy hóa đơn chưa thanh toán).
  - `limit=100` (lấy tối đa 100 hóa đơn/lần).
- **Lưu ý**:
  - Đảm bảo **Stripe Secret Key** được nhập đúng trong **Credentials** của n8n.

##### **3. Filter Due Invoices (Lọc Hóa Đơn Đến Hạn)**
- **Logic lọc**:
  - Chỉ giữ hóa đơn có **due_date** và **due_date trong 7 ngày tới**.
  - Sử dụng biểu thức JavaScript để so sánh ngày.
- **Lưu ý**:
  - Nếu Stripe trả về dữ liệu không đúng định dạng, cần kiểm tra lại API response.

##### **4. Google Calendar Get Events (Lấy Sự Kiện Google Calendar)**
- **Credentials**: Chọn **googleCalendarOAuth2Api** (đã cấu hình trước).
- **Calendar ID**: Nhập **email của Google Calendar** bạn muốn sử dụng (ví dụ: `abc123@gmail.com`).
- **Time Range**: Cài đặt từ **hôm nay đến 30 ngày sau**.
- **Lưu ý**:
  - Đảm bảo **OAuth2 API Key** được cấp quyền truy cập vào Calendar.
  - Thay đổi **calendarId** thành email Calendar của bạn.

##### **5. Check Invoice Exists (Kiểm Tra Hóa Đơn Tồn Tại)**
- **Logic**:
  - So sánh **invoice_id** trong hóa đơn với danh sách **invoice_id** đã tồn tại trong Calendar.
  - Nếu **invoice_id** không tồn tại, thì tạo nhắc nhở mới.

##### **6. Google Calendar Create Event (Tạo Sự Kiện Mới)**
- **Event Details**:
  - **Title**: "Pending Invoice: [Invoice ID]" (ví dụ: "Pending Invoice: inv_12345").
  - **Start Time**: Ngày hết hạn của hóa đơn.
  - **Duration**: 1 giờ (có thể điều chỉnh).
  - **Description**: Thêm chi tiết như **invoice_id**, **amount**, và **link Stripe** (nếu cần).
- **Lưu ý**:
  - Thay đổi **title** và **description** theo yêu cầu cá nhân hóa.

#### 3. Kích Hoạt ⚡️
1. **Test Run**:
   - Chạy **Manual Test** với một hóa đơn mẫu để kiểm tra logic.
   - Kiểm tra **Google Calendar** xem nhắc nhở có được tạo không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Workflow Status** từ **Inactive** sang **Active**.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Thêm Slack/Telegram Notifications**: Gửi thông báo khi hóa đơn đến hạn qua Slack/Telegram.
- **Lưu Log Dữ Liệu**: Sử dụng **n8n-nodes-base.stickyNote** để ghi lại lịch sử hóa đơn đã xử lý.
- **Báo Cáo Định Kỳ**: Tạo báo cáo hàng tuần về số hóa đơn đến hạn và đã thanh toán.
- **Cá Nhân Hóa Nhắc Nhở**: Thêm thông tin khách hàng vào tiêu đề sự kiện (ví dụ: "Invoice for John Doe").
- **Kết Hợp với Email**: Gửi email tự động cho khách hàng khi hóa đơn đến hạn.
:::

---

### 📌 Kết Luận
Workflow này **giải phóng thời gian** của các sếp khỏi việc quản lý hóa đơn thủ công, đồng thời **giảm thiểu rủi ro bỏ lỡ thanh toán**. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào những việc quan trọng hơn như phát triển kinh doanh và xây dựng mối quan hệ với khách hàng.

**Hãy áp dụng ngay workflow này và trải nghiệm sự tự động hóa hoàn toàn cho quản lý hóa đơn của bạn!** 🚀

---