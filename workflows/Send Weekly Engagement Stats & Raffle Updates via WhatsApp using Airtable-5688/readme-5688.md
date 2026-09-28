---
title: "🚀 Gửi Thống Kê Tương Tác & Cập Nhật Vé Xoay Quay Hàng Tuần qua WhatsApp bằng Airtable"
description: "Tự động hóa gửi thông báo hàng tuần về điểm tương tác và vé xoay quay qua WhatsApp, giúp doanh nghiệp duy trì tương tác với khách hàng một cách cá nhân hóa và hiệu quả."
slug: "gui-thong-ke-tuong-tac-ve-xoay-quay-qua-whatsapp-bang-airtable"
tags: [n8n, automation, no-code, social-media, airtable, whatsapp]
keywords: [n8n workflow, tự động hóa, airtable, whatsapp, thống kê tương tác, vé xoay quay]
---

# 🚀 Gửi Thống Kê Tương Tác & Cập Nhật Vé Xoay Quay Hàng Tuần qua WhatsApp bằng Airtable

[Các sếp đang làm thủ công việc gửi thông báo hàng tuần về điểm tương tác và vé xoay quay cho khách hàng qua WhatsApp? Hãy để n8n giúp các sếp tự động hóa quy trình này một cách hoàn toàn không cần code!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi thông báo hàng tuần mà không cần can thiệp thủ công.
- **Cá nhân hóa**: Gửi thông tin cụ thể về điểm tương tác và vé xoay quay cho từng khách hàng.
- **Duy trì tương tác**: Giữ khách hàng luôn được cập nhật về hoạt động và cơ hội trúng thưởng.
- **Tăng cường sự hài lòng**: Khách hàng sẽ cảm thấy được quan tâm và được trải nghiệm dịch vụ tốt hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtable với bảng dữ liệu chứa thông tin khách hàng (ID WhatsApp, điểm tương tác, vé xoay quay).
- API Key của Airtable để truy cập dữ liệu.
- Tài khoản WhatsApp Business API (hoặc sử dụng dịch vụ như Whapi) để gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/5688](https://n8n.io/workflows/5688).
3. Hoặc, các sếp có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Every wednesday at 1 pm"**: Đảm bảo thời gian và ngày trong node này được đặt chính xác để workflow chạy đúng vào thứ Tư lúc 13:00.
- **Node "Search records"**: Cần cấu hình đúng thông tin credentials của Airtable và chỉ định chính xác bảng dữ liệu chứa thông tin khách hàng.
- **Node "Send WhasApp (Weekly Message)"**: Cần cấu hình đúng thông tin API của WhatsApp Business API hoặc dịch vụ gửi tin nhắn tương tự.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, các sếp nên chạy thử workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng.
2. Khi đã kiểm tra và đảm bảo workflow hoạt động tốt, các sếp có thể bật chế độ Active để workflow chạy tự động hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm node để gửi thông báo về kênh Slack hoặc Telegram khi workflow chạy thành công hoặc gặp lỗi.
- **Lưu log hoạt động**: Thêm node để lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.
- **Gửi báo cáo định kỳ**: Mở rộng workflow để gửi báo cáo tổng hợp về hoạt động tương tác hàng tuần cho quản lý.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc gửi thông báo hàng tuần về điểm tương tác và vé xoay quay qua WhatsApp, duy trì tương tác với khách hàng một cách hiệu quả và cá nhân hóa. Hãy áp dụng ngay để tiết kiệm thời gian và tăng cường sự hài lòng của khách hàng!