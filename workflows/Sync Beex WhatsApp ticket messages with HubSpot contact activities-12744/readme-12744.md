---
title: "🚀 Tự động đồng bộ tin nhắn WhatsApp từ Beex với hoạt động liên hệ HubSpot"
description: "Hướng dẫn chi tiết cách tự động đồng bộ tin nhắn WhatsApp từ Beex với hoạt động liên hệ HubSpot trong n8n, giúp quản lý khách hàng hiệu quả hơn"
slug: "tu-dong-dong-bo-tin-nhan-whatsapp-beex-hubspot"
tags: [n8n, automation, no-code, whatsapp, hubspot]
keywords: [n8n workflow, tự động hóa, whatsapp, hubspot, quản lý khách hàng]
---

# 🚀 Tự động đồng bộ tin nhắn WhatsApp từ Beex với hoạt động liên hệ HubSpot

[Khi làm thủ công, các sếp phải tốn nhiều thời gian để theo dõi và quản lý tin nhắn WhatsApp từ Beex và đồng bộ với hệ thống HubSpot. Workflow này giúp tự động hóa toàn bộ quá trình này, tiết kiệm thời gian và giảm thiểu lỗi con người.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ tin nhắn WhatsApp từ Beex với HubSpot
- Tiết kiệm thời gian quản lý khách hàng
- Giảm thiểu lỗi con người trong quá trình đồng bộ dữ liệu
- Theo dõi hoạt động liên hệ khách hàng một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Beex với quyền truy cập API
- Tài khoản HubSpot với quyền truy cập API
- API Key từ Beex
- Private App Token từ HubSpot với quyền đọc/ghi Contacts
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/12744)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Beex Trigger Node**:
   - Đảm bảo đã cấu hình đúng webhook URL trong Beex
   - Kiểm tra lại rằng chỉ xử lý sự kiện "On Management Create"

2. **Get Phone Node**:
   - Cần cấu hình mã quốc gia cho số điện thoại
   - Ví dụ: Nếu số điện thoại là 123456789, cần thêm mã quốc gia như +84123456789

3. **Search Contact Node**:
   - Đảm bảo đã cấu hình đúng HubSpot App Token
   - Kiểm tra lại rằng đang sử dụng đúng tài khoản HubSpot

4. **Get Messages Node**:
   - Cập nhật API Key từ Beex vào trường credentials
   - Đảm bảo đã bật "Typing Registry in Callback Integration" trong Beex

5. **Register Activity Node**:
   - Kiểm tra lại URL API HubSpot
   - Đảm bảo đã cấu hình đúng phương thức HTTP (POST)

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra lại kết quả đồng bộ trên HubSpot
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo Slack/Telegram khi có sự kiện mới
- Lưu log hoạt động vào Google Sheets để theo dõi lịch sử
- Tự động gửi báo cáo hàng ngày về hoạt động liên hệ khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ tin nhắn WhatsApp từ Beex với hoạt động liên hệ HubSpot một cách hiệu quả. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian và giảm thiểu lỗi con người trong quá trình quản lý khách hàng. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!