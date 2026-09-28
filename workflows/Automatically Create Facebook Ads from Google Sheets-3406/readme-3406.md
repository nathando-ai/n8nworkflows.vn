---
title: "🚀 Tự động tạo Facebook Ads từ Google Sheets – Giải pháp marketing không code"
description: "Giải quyết thủ công tạo quảng cáo Facebook bằng cách tự động lấy dữ liệu và hình ảnh từ Google Sheets, tạo chiến dịch, set và quảng cáo ngay lập tức."
slug: "tua-dong-tao-facebook-ads-tu-google-sheets"
tags: [n8n, automation, no-code, marketing, facebook-ads, google-sheets]
keywords: [n8n workflow, tự động hóa, Facebook Ads, Google Sheets, marketing automation]
---

# 🚀 Tự động tạo Facebook Ads từ Google Sheets – Giải pháp marketing không code

Bạn đang phải mất hàng giờ mỗi ngày để tạo quảng cáo Facebook từ dữ liệu trong Google Sheets? Mỗi lần chỉnh sửa lại phải lặp lại nhiều bước thủ công, dễ gây sai sót và mất thời gian.  
Workflow **Automatically Create Facebook Ads from Google Sheets** sẽ giúp bạn:

- Tự động lấy dữ liệu và hình ảnh từ Google Sheets.
- Tải lên Facebook, tạo Creative, Ad Set và Ad chỉ trong vài phút.
- Cập nhật lại Sheet với ID quảng cáo để theo dõi dễ dàng.
- Hoàn toàn không cần viết code, chỉ cần cấu hình một vài credential.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống chỉ còn vài phút.  
- **Độ chính xác cao**: Không còn sai sót khi nhập dữ liệu.  
- **Tự động cập nhật**: Sheet luôn được ghi lại ID quảng cáo, dễ dàng theo dõi hiệu suất.  
- **Hoạt động liên tục**: Khi có dòng dữ liệu mới, workflow tự động chạy ngay.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / Credential | Mô tả | Cách lấy |
|-----------------------|-------|----------|
| **Google Sheets API** | Để đọc dữ liệu và ghi lại ID quảng cáo. | Tạo project trên Google Cloud, bật Sheets API, tạo OAuth 2.0 client, download JSON. |
| **Facebook Graph API** | Để upload hình ảnh, tạo Creative, Ad Set và Ad. | Tạo App trên Facebook Developers, lấy Access Token (độ dài 60 ngày), xác định Ad Account ID. |
| **Google Sheets Trigger** | Định nghĩa sheet ID và range. | Dùng ID sheet (đường dẫn `https://docs.google.com/spreadsheets/d/<sheet-id>/edit`). |
| **Facebook Ad Account ID** | ID tài khoản quảng cáo. | Tìm trong Business Manager. |
| **Image URL** | Đường dẫn tới hình ảnh trong Google Sheet. | Cột trong sheet chứa URL. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/3406) hoặc copy nội dung JSON.  
2. Mở n8n Editor → **Workflows** → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | **Google Sheets Trigger** | *Spreadsheet ID*, *Range* (ví dụ `Sheet1!A2:E`) | Đảm bảo trigger được bật. |
| 2 | **Specify variables** | *Set* các trường: `ad_name`, `ad_set_name`, `image_url`, `budget`, `start_date`, `end_date`, v.v. | Dùng dữ liệu từ trigger. |
| 3 | **Get image** | *URL* lấy từ `image_url` | Đảm bảo URL hợp lệ và có thể truy cập. |
| 4 | **Upload Ad image** | *Access Token*, *Ad Account ID* | Chọn credential Facebook đã tạo. |
| 5 | **Facebook Ad Creative** | *Ad Account ID*, *Image ID* (được trả về từ node 4), *Title*, *Body*, *Link* | Dùng biến từ node 2. |
| 6 | **Create an Ad Set** | *Ad Account ID*, *Campaign ID*, *Ad Set Name*, *Budget*, *Schedule* | Campaign ID cần được nhập thủ công hoặc lấy từ node trước. |
| 7 | **Create an Ad** | *Ad Account ID*, *Ad Set ID*, *Creative ID*, *Ad Name* | Liên kết với node 5 và 6. |
| 8 | **Update Google Sheets** | *Spreadsheet ID*, *Range* (để ghi lại Ad ID), *Values* (Ad ID) | Ghi lại ID quảng cáo vào cột thích hợp. |

> **Lưu ý**: Mỗi node Facebook Graph API cần **credential** riêng. Trong n8n, vào **Credentials** → **Add New** → **Facebook Graph API** → nhập **Access Token** và **Ad Account ID**. Sau đó chọn credential trong từng node.

### 3. Kích hoạt ⚡️

1. **Test run**: Chọn một dòng mẫu trong Google Sheet, nhấn **Execute Workflow**. Kiểm tra log từng node, đảm bảo không có lỗi.  
2. **Bật Active**: Khi mọi thứ ổn, chuyển workflow sang trạng thái **Active**.  
3. **Kiểm tra Sheet**: Sau khi chạy, cột mới (ví dụ `Ad ID`) sẽ được ghi lại.  

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram Notification**: Thêm node **Slack** hoặc **Telegram** sau node 7 để gửi thông báo khi quảng cáo được tạo thành công.  
- **Lưu Log**: Sử dụng node **Google Sheets** hoặc **MySQL** để ghi lại log chi tiết (status, lỗi).  
- **Định kỳ cập nhật**: Thêm node **Cron** để chạy kiểm tra trạng thái quảng cáo và cập nhật Sheet.  
- **Tối ưu ngân sách**: Thêm node **Set** để tính toán ngân sách dựa trên giá trị doanh thu dự kiến.  

## 📌 Kết luận

Workflow **Automatically Create Facebook Ads from Google Sheets** là công cụ mạnh mẽ giúp các sếp marketing tiết kiệm thời gian, giảm sai sót và tăng hiệu quả chiến dịch. Hãy thử ngay, cấu hình nhanh chóng và trải nghiệm tự động hóa không code!