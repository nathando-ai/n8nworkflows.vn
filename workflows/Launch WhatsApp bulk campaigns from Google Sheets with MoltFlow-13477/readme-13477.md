---
title: "🚀 Tự động gửi chiến dịch WhatsApp hàng loạt từ Google Sheets với MoltFlow"
description: "Hướng dẫn chi tiết cách tự động hóa chiến dịch marketing WhatsApp bằng n8n, Google Sheets và MoltFlow giúp tiết kiệm thời gian, cá nhân hóa tin nhắn hàng loạt."
slug: "tu-dong-gui-whatsapp-hang-loat-tu-google-sheets-moltflow"
tags: [n8n, automation, no-code, whatsapp, google-sheets, moltflow, marketing]
keywords: [n8n workflow, tự động hóa whatsapp, gui tin nhan whatsapp hang loat, google sheets whatsapp, moltflow n8n]
---

# 🚀 Tự động gửi chiến dịch WhatsApp hàng loạt từ Google Sheets với MoltFlow

Việc gửi tin nhắn chăm sóc khách hàng hay thông báo chương trình khuyến mãi thủ công qua WhatsApp tốn rất nhiều thời gian và dễ xảy ra sai sót. Nếu các sếp đang tìm kiếm giải pháp tiếp cận hàng trăm, hàng nghìn khách hàng một cách tự động, cá nhân hóa mà không sợ bị khóa tài khoản, thì workflow n8n này chính là mảnh ghép hoàn hảo.

Sự kết hợp giữa **Google Sheets** (quản lý danh bạ), **MoltFlow** (nền tảng API WhatsApp) và **n8n** sẽ giúp các sếp tự động hóa toàn bộ quy trình chỉ bằng 1 cú click chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Đẩy toàn bộ danh bạ từ Google Sheets lên hệ thống WhatsApp để gửi tin nhắn hàng loạt.
- **Cá nhân hóa nội dung:** Mỗi khách hàng sẽ nhận được thông điệp riêng biệt (hỗ trợ trường `message_override`).
- **Kiểm soát tiến độ thông minh:** Workflow tự động chờ (Wait node) và kiểm tra trạng thái chiến dịch, sau đó trả về bản tổng kết chi tiết.
- **An toàn, mượt mà:** Tích hợp độ trễ thông minh giữa các lần gửi giúp hạn chế tối đa việc bị spam hoặc chặn tài khoản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google Sheets chứa danh sách liên hệ (cần có các cột: `phone`, `name`, `message_override`).
- Tài khoản [MoltFlow](https://molt.waiflow.app) đã kết nối với số điện thoại WhatsApp của các sếp.
- API Key từ MoltFlow (với cấu hình quyền Outreach).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy ngon nghẻ, các sếp cần cấu hình chính xác các node sau:

- **Read Contacts from Sheet (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets thông qua OAuth2.
  - Dán đường dẫn Google Sheet của các sếp vào phần cấu hình node, chọn đúng Sheet chứa danh sách khách hàng (đảm bảo có các cột `phone`, `name`, `message_override`).
- **Format Contacts (`code`):** 
  - Mở node này và cấu hình lại giá trị `YOUR_SESSION_ID` thành Session ID thực tế trên tài khoản MoltFlow của các sếp.
- **Create Custom Group & Create Bulk Send Job (`httpRequest`):** 
  - Tạo Credentials loại **Header Auth** với tên Header là `X-API-Key`, giá trị là API Key lấy từ tài khoản MoltFlow của các sếp. Áp dụng credentials này cho các node gọi API HTTP trong workflow.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** (hoặc dùng node `Start Campaign` - `manualTrigger`) để test thử với một vài dữ liệu mẫu trên Google Sheets.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** để sẵn sàng sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook/Telegram:** Thêm một node Telegram hoặc Slack ở cuối workflow (`Campaign Summary`) để bot tự động gửi thông báo báo cáo kết quả chiến dịch ngay khi hoàn tất.
- **Lưu lịch sử gửi:** Thêm một bước cập nhật ngược lại Google Sheets (Cột trạng thái: *Đã gửi* / *Thất bại*) dựa trên kết quả trả về từ `Campaign Summary`.
- **Lên lịch tự động (Schedule Trigger):** Thay thế node `manualTrigger` bằng `Schedule Trigger` nếu các sếp muốn hệ thống tự động chạy chiến dịch vào những khung giờ vàng cố định hàng ngày/hàng tuần.

### 📌 Kết luận
Tự động hóa chiến dịch WhatsApp marketing chưa bao giờ dễ dàng đến thế. Với workflow này, các sếp có thể tiết kiệm hàng giờ đồng hồ thao tác tay mỗi tuần, tối ưu hóa tỷ lệ chuyển đổi và chăm sóc khách hàng chuyên nghiệp hơn. Chúc các sếp "lên đồ" thành công!