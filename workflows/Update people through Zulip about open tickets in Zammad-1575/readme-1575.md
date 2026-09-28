---
title: "🚀 Tự động thông báo vé hỗ trợ mở trong Zammad lên Zulip hàng ngày"
description: "Hướng dẫn tự động hóa thông báo các vé hỗ trợ chưa giải quyết trong Zammad lên Zulip hàng ngày, tiết kiệm thời gian và nâng cao hiệu quả làm việc cho đội ngũ IT Ops."
slug: "tu-dong-thong-bao-ve-ho-tro-moi-trong-zammad-len-zulip"
tags: [n8n, automation, no-code, zammad, zulip, it-ops, support]
keywords: [n8n workflow, tự động hóa, zammad, zulip, thông báo vé hỗ trợ, it ops]
---

# 🚀 Tự động thông báo vé hỗ trợ mở trong Zammad lên Zulip hàng ngày

[Các sếp IT Ops] đang gặp khó khăn khi phải theo dõi và thông báo các vé hỗ trợ chưa giải quyết hàng ngày. Việc này tốn thời gian và dễ bị bỏ sót. Workflow này sẽ giúp các sếp tự động hóa quy trình này hoàn toàn, đảm bảo không bỏ sót bất kỳ vé nào và nâng cao hiệu quả làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải theo dõi thủ công các vé hỗ trợ hàng ngày.
- **Chính xác**: Đảm bảo không bỏ sót bất kỳ vé nào.
- **Cá nhân hóa**: Có thể tùy chỉnh nội dung thông báo theo nhu cầu của đội ngũ.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zammad với quyền truy cập API.
- Tài khoản Zulip với quyền gửi tin nhắn.
- API Key của Zammad và Zulip.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io](https://n8n.io/workflows/1575) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.
3. Hoặc copy nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "List Tickets"**:
   - Chọn credentials **zammadTokenAuthApi**.
   - Đảm bảo tài khoản Zammad có quyền truy cập API và có thể lấy danh sách vé.

2. **Node "Notify for Standup"**:
   - Chọn credentials **zulipApi**.
   - Cấu hình các tham số:
     - **Stream**: Tên stream Zulip cần gửi thông báo.
     - **Topic**: Chủ đề của tin nhắn (ví dụ: "Vé hỗ trợ chưa giải quyết").
     - **Content**: Nội dung thông báo (có thể bao gồm các thông tin từ vé hỗ trợ).

3. **Node "Standup Cron"**:
   - Cấu hình lịch chạy workflow (ví dụ: hàng ngày lúc 9:00 AM).

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút **Execute Node** để test workflow với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút **Activate Workflow** để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Có thể thêm node để gửi thông báo lên Slack hoặc Telegram cùng lúc.
- **Lưu log**: Thêm node để lưu log các vé đã thông báo để theo dõi lịch sử.
- **Gửi báo cáo định kỳ**: Có thể mở rộng workflow để gửi báo cáo tổng hợp hàng tuần hoặc hàng tháng.

### 📌 Kết luận
Workflow này giúp các sếp IT Ops tự động hóa việc thông báo các vé hỗ trợ chưa giải quyết hàng ngày, tiết kiệm thời gian và nâng cao hiệu quả làm việc. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của đội ngũ!