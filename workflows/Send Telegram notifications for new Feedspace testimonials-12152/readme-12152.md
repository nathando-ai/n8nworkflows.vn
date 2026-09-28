---
title: "🚀 [Tự động hóa] Gửi thông báo Telegram cho đánh giá mới từ Feedspace"
description: "Hướng dẫn tự động hóa gửi thông báo Telegram ngay khi có đánh giá mới từ Feedspace, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "tu-dong-hoa-thong-bao-telegram-feedspace"
tags: [n8n, automation, no-code, social media, telegram]
keywords: [n8n workflow, tự động hóa, feedspace, telegram, đánh giá khách hàng]
---

# 🚀 [Tự động hóa] Gửi thông báo Telegram cho đánh giá mới từ Feedspace

[Các sếp đang sử dụng Feedspace để thu thập đánh giá khách hàng nhưng vẫn phải theo dõi thủ công trên trang quản trị? Workflow này sẽ giúp các sếp tự động nhận thông báo ngay khi có đánh giá mới trên Telegram, tiết kiệm thời gian và nâng cao hiệu quả quản lý.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận thông báo ngay lập tức khi có đánh giá mới (không cần truy cập trang quản trị Feedspace)
- Tiết kiệm thời gian theo dõi thủ công
- Nâng cao hiệu quả quản lý đánh giá khách hàng
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Feedspace đã kích hoạt
- Tài khoản Telegram cá nhân
- API token của Telegram bot
- Chat ID của kênh/nhóm Telegram nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12152)
2. Click nút "Download" để tải file JSON
3. Trong n8n Editor, click "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive Feedspace Webhook"**:
   - Đảm bảo đường dẫn webhook là duy nhất và không bị trùng lặp
   - Giữ nguyên phương thức HTTP là POST

2. **Node "Send Telegram Notification"**:
   - Thêm credentials cho Telegram API
   - Điền API token của Telegram bot
   - Tạo biến môi trường `TELEGRAM_CHAT_ID` với giá trị là Chat ID của kênh/nhóm nhận thông báo

3. **Node "Has Error?"**:
   - Giữ nguyên cấu hình kiểm tra lỗi
   - Đảm bảo kết nối đúng với các node "Success Response" và "Error Response"

4. **Node "Format Error Details"**:
   - Giữ nguyên mã xử lý lỗi
   - Đảm bảo định dạng thông báo lỗi phù hợp với yêu cầu

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click nút "Activate" để kích hoạt workflow
2. Copy URL webhook từ node "Receive Feedspace Webhook"
3. Truy cập trang quản trị Feedspace → Automations → Webhook
4. Dán URL webhook vào trường tương ứng và lưu cấu hình
5. Test workflow bằng cách tạo một đánh giá mới trên Feedspace

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Slack" để nhận thông báo đồng thời trên Slack
- Cấu hình gửi báo cáo hàng ngày về số lượng đánh giá mới
- Tích hợp với Google Sheets để lưu trữ và phân tích dữ liệu đánh giá
- Thiết lập thông báo theo mức độ đánh giá (tích cực/tiêu cực)

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình theo dõi đánh giá từ Feedspace, tiết kiệm thời gian và nâng cao hiệu quả quản lý. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!