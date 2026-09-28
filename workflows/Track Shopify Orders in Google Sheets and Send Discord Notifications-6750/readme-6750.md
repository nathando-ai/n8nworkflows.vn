---
title: "🚀 Theo dõi đơn hàng Shopify trong Google Sheets và gửi thông báo Discord"
description: "Giải pháp tự động ghi nhận đơn hàng Shopify vào Google Sheets và gửi thông báo ngay tới Discord, giúp doanh nghiệp theo dõi đơn hàng nhanh chóng và không bỏ lỡ bất kỳ giao dịch nào."
slug: "theo-doi-don-hang-shopify-gsheet-discord"
tags: [n8n, automation, no-code, shopify, google-sheets, discord]
keywords: [n8n workflow, tự động hóa, Shopify, Google Sheets, Discord, theo dõi đơn hàng]
---

# 🚀 Theo dõi đơn hàng Shopify trong Google Sheets và gửi thông báo Discord

Bạn đang phải mất hàng giờ để nhập dữ liệu đơn hàng Shopify vào Google Sheets, đồng thời phải tự tay gửi thông báo tới Discord hoặc Slack? Đừng lo, workflow này sẽ giúp bạn tự động hoá toàn bộ quy trình, giảm thiểu sai sót và tiết kiệm thời gian đáng kể.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập dữ liệu thủ công, mọi đơn hàng mới ngay lập tức được ghi vào Google Sheets.
- **Độ chính xác cao**: Hệ thống tự động tránh sai sót khi nhập liệu.
- **Thông báo tức thì**: Mỗi đơn hàng mới sẽ được gửi tin nhắn ngay tới kênh Discord, giúp đội ngũ bán hàng luôn cập nhật.
- **Dễ dàng phân tích**: Dữ liệu trong Google Sheets có thể được dùng cho báo cáo, phân tích xu hướng bán hàng.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Shopify**: Tạo và lưu trữ `shopifyAccessTokenApi` (API access token).
- **Google Sheets**: Cài đặt `googleSheetsOAuth2Api` và có một bảng tính với các cột phù hợp (ví dụ: Order ID, Customer, Total, Status, Created At).
- **Discord**: Tạo webhook và lưu trữ `discordWebhookApi`.
- **n8n**: Đã cài đặt và chạy phiên bản 0.200+ (để hỗ trợ node `shopifyTrigger` và `discord`).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON workflow từ <https://n8n.io/workflows/6750> hoặc sao chép nội dung JSON.
2. Mở n8n Editor → `Workflows` → `Import` → `Upload file` hoặc `Paste JSON`.
3. Nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Mô tả | Cấu hình cần chỉnh |
|------|----------|-------|---------------------|
| 1 | Shopify Trigger | Gọi webhook khi có đơn hàng mới | Chọn `shopifyAccessTokenApi` đã tạo |
| 2 | Append row in sheet | Ghi dữ liệu vào Google Sheets | Chọn `googleSheetsOAuth2Api`, nhập `Spreadsheet ID`, `Sheet Name`, và cấu hình `Append` |
| 3 | Code | Xử lý dữ liệu (định dạng JSON, lấy fields) | Kiểm tra script, đảm bảo `item.json` chứa các trường cần thiết (order_id, customer, total, status, created_at) |
| 4 | Discord | Gửi tin nhắn tới kênh Discord | Chọn `discordWebhookApi`, cấu hình message template (có thể dùng `{{ $json["order_id"] }}`) |
| 5 | Code1 | Xử lý dữ liệu cho Discord (nếu cần) | Kiểm tra script, đảm bảo message payload đúng định dạng |

> **Lưu ý**: Nếu bạn muốn thay đổi cột trong Google Sheets, hãy cập nhật script trong node `Code` để phản ánh cấu trúc mới.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (sử dụng `Execute Node` trên node `Shopify Trigger`).
2. Kiểm tra Google Sheets và Discord để xác nhận dữ liệu đã được ghi và thông báo đã gửi.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: Thêm node `Slack` sau `Discord` để gửi thông báo đồng thời.
- **Lưu log**: Thêm node `Google Sheets` hoặc `Database` để ghi lại lịch sử thông báo.
- **Báo cáo định kỳ**: Sử dụng node `Cron` để gửi báo cáo hàng ngày/tuần tới Discord hoặc email.
- **Tùy chỉnh thông báo**: Sử dụng `Code` để tạo message embed phong phú, bao gồm hình ảnh sản phẩm, link tới đơn hàng.

## 📌 Kết luận
Workflow này giúp các sếp giảm bớt công việc thủ công, tăng tính chính xác và phản hồi nhanh chóng. Hãy thử ngay, cài đặt và điều chỉnh cho phù hợp với quy trình bán hàng của mình. Nếu gặp khó khăn, hãy tham khảo tài liệu n8n hoặc liên hệ với cộng đồng để được hỗ trợ. Chúc các sếp thành công!