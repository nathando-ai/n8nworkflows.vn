---
title: "🚀 Tự động hóa: Chuyển đổi trang web thành cơ sở dữ liệu Google Sheets với MrScraper và Gmail"
description: "Hướng dẫn tự động hóa quy trình trích xuất dữ liệu từ trang web và lưu vào Google Sheets thông qua MrScraper và Gmail, tiết kiệm thời gian và công sức cho các sếp."
slug: "tu-dong-hoa-chuyen-doi-trang-web-thanh-google-sheets"
tags: [n8n, automation, no-code, google-sheets, web-scraping]
keywords: [n8n workflow, tự động hóa, trích xuất dữ liệu, google sheets, mrscraper]
---

# 🚀 Tự động hóa: Chuyển đổi trang web thành cơ sở dữ liệu Google Sheets với MrScraper và Gmail

[Các sếp] có bao giờ phải tự tay copy dữ liệu từ trang web vào Google Sheets không? Việc này tốn thời gian, dễ sai sót và không thể thực hiện liên tục. Với workflow này, các sếp có thể tự động hóa quy trình này hoàn toàn, chỉ cần một lần cài đặt và workflow sẽ chạy tự động mỗi khi có dữ liệu mới.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tự tay copy dữ liệu từ trang web vào Google Sheets.
- **Chính xác**: Dữ liệu được trích xuất tự động, giảm thiểu sai sót do con người.
- **Tự động hóa**: Workflow chạy tự động mỗi khi có dữ liệu mới, không cần can thiệp.
- **Lưu trữ dữ liệu**: Dữ liệu được lưu trữ trong Google Sheets, dễ dàng truy cập và quản lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Tài khoản Gmail để gửi email thông báo khi workflow hoàn thành.
- API key của MrScraper để trích xuất dữ liệu từ trang web.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/13798](https://n8n.io/workflows/13798).
3. Nhấn "Import" để tải workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node MrScraper**: Cần cấu hình API key của MrScraper và URL của trang web cần trích xuất dữ liệu.
- **Node Google Sheets**: Cần cấu hình ID của Google Sheet và tên của sheet cần lưu dữ liệu.
- **Node Gmail**: Cần cấu hình tài khoản Gmail để gửi email thông báo khi workflow hoàn thành.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để chạy workflow với dữ liệu mẫu.
2. Kiểm tra kết quả trên Google Sheets và email thông báo.
3. Nếu mọi thứ hoạt động tốt, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành.
- **Lưu log**: Thêm node để lưu log của workflow để theo dõi quá trình chạy.
- **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo định kỳ về dữ liệu đã trích xuất.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình trích xuất dữ liệu từ trang web và lưu vào Google Sheets, tiết kiệm thời gian và công sức. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!