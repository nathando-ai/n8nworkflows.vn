---
title: "🚀 Tự động hóa cảnh báo gia hạn hợp đồng qua Slack từ Google Sheets"
description: "Hướng dẫn tự động hóa cảnh báo gia hạn hợp đồng theo 3 mức độ ưu tiên (🔴 Khẩn cấp, 🟡 Cần hành động, 🟢 Thông báo) từ Google Sheets sang Slack mỗi ngày lúc 9am."
slug: "tu-dong-hoa-canh-bao-gia-han-hop-dong-qua-slack-tu-google-sheets"
tags: [n8n, automation, no-code, google-sheets, slack]
keywords: [n8n workflow, tự động hóa hợp đồng, cảnh báo hợp đồng, google sheets, slack]
---

# 🚀 Tự động hóa cảnh báo gia hạn hợp đồng qua Slack từ Google Sheets

[Các sếp đang làm việc thủ công với hàng chục hợp đồng hàng tháng, theo dõi ngày hết hạn và gửi cảnh báo thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này trong vòng 15 phút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng chục hợp đồng mỗi ngày.
- **Cảnh báo chính xác**: Nhận thông báo đúng lúc, tránh bỏ sót hợp đồng quan trọng.
- **Tự động phân loại**: Hợp đồng được phân loại tự động theo mức độ ưu tiên (🔴, 🟡, 🟢).
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày lúc 9am mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã chuẩn bị (theo hướng dẫn phần 1).
- Tài khoản Slack với quyền gửi tin nhắn vào kênh hoặc DM.
- Google Sheets API credentials (OAuth).
- Slack API credentials (OAuth).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15231).
2. Click vào nút "Import" và chọn "Import from URL".
3. Dán link workflow vào ô nhập liệu và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets**:
   - Thêm 2 cột `Last Alert Tier` và `Last Alert Date` vào tất cả 5 tab (SaaS, Leases, Services, Insurance, Other).
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet trong tất cả 5 node "Read".
   - Kết nối Google Sheets credentials (OAuth).

2. **Slack**:
   - Thay thế `YOUR_SLACK_CHANNEL_ID` bằng ID kênh Slack trong tất cả 3 node "Slack".
   - Kết nối Slack credentials (OAuth).

3. **Trigger**:
   - Thay đổi giờ chạy trong node "Trigger: Daily at 9am" nếu cần.

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu:
   - Tạm thời đặt ngày hết hạn của một hợp đồng thành ~10 ngày sau ngày hiện tại.
   - Xóa giá trị trong cột `Last Alert Tier` của hợp đồng này.
   - Click "Execute Workflow" và kiểm tra xem có nhận được cảnh báo 🟡 trên Slack không.
2. Sau khi test thành công, khôi phục lại dữ liệu và kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thêm node Telegram để nhận cảnh báo ngoài Slack.
- **Lưu log**: Thêm node Google Sheets để lưu lại lịch sử cảnh báo.
- **Gửi báo cáo định kỳ**: Thêm node Email để gửi báo cáo tổng hợp hàng tuần.
- **Tự động cập nhật**: Thêm node Google Sheets Update để tự động ghi nhận cảnh báo đã gửi.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi và cảnh báo gia hạn hợp đồng, tiết kiệm thời gian và giảm thiểu rủi ro bỏ sót hợp đồng quan trọng. Hãy áp dụng ngay để nâng cao hiệu quả quản lý hợp đồng của doanh nghiệp!