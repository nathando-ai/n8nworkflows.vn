---
title: "🚀 Tự động hóa thu thập thông tin khách hàng vào Google Sheets - SmartLead Sheet Sync"
description: "Hướng dẫn tự động hóa thu thập thông tin khách hàng từ form liên hệ vào Google Sheets bằng n8n, tiết kiệm thời gian và tránh lỗi thủ công"
slug: "tu-dong-hoa-thu-thap-thong-tin-khach-hang-vao-google-sheets"
tags: [n8n, automation, no-code, google-sheets, marketing]
keywords: [n8n workflow, tự động hóa, google sheets, form liên hệ, marketing automation]
---

# 🚀 Tự động hóa thu thập thông tin khách hàng vào Google Sheets - SmartLead Sheet Sync

[Các sếp đang gặp khó khăn khi phải thu thập thông tin khách hàng từ nhiều nguồn khác nhau và nhập thủ công vào Google Sheets. Việc này tốn thời gian, dễ xảy ra lỗi và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa quy trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần nhập thủ công dữ liệu từ form liên hệ
- Giảm thiểu lỗi: Dữ liệu được xử lý và lưu tự động, chính xác
- Trung tâm hóa dữ liệu: Tất cả thông tin khách hàng được lưu trữ tập trung trong Google Sheets
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt
- Form liên hệ hoặc bất kỳ nguồn dữ liệu nào có thể gửi webhook
- Tài khoản n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/4148
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Form Submission Hook** (Webhook node):
   - Chọn "HTTP Request" làm trigger
   - Đặt phương thức là "POST"
   - Đặt path là "/webhook" (hoặc bất kỳ path nào các sếp muốn)
   - Lưu ý: Các sếp cần cấu hình form liên hệ của mình để gửi dữ liệu đến webhook này

2. **Parse + Clean Lead Data** (Code node):
   - Node này xử lý dữ liệu thô từ form liên hệ
   - Các sếp có thể chỉnh sửa code để phù hợp với cấu trúc dữ liệu của form
   - Đảm bảo output của node này có các trường: name, email, phone, message (hoặc các trường phù hợp với form của các sếp)

3. **Save To Google Sheets** (Google Sheets node):
   - Chọn "Append a row" làm operation
   - Chọn Google Sheets credentials đã được cấu hình
   - Nhập Spreadsheet ID của Google Sheets cần lưu dữ liệu
   - Nhập tên Sheet (tab) cần lưu dữ liệu
   - Đảm bảo các trường trong Google Sheets phù hợp với output của node trước đó

#### 3. Kích hoạt ⚡️
1. Kiểm tra workflow bằng cách gửi dữ liệu mẫu từ form liên hệ
2. Kiểm tra Google Sheets để xác nhận dữ liệu đã được lưu đúng
3. Bật Active workflow để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có lead mới
- Thêm node để gửi email tự động cho lead mới
- Tự động phân loại lead theo các tiêu chí nhất định
- Kết nối với CRM để tự động tạo lead trong hệ thống CRM

### 📌 Kết luận
Workflow SmartLead Sheet Sync giúp các sếp tự động hóa hoàn toàn quy trình thu thập thông tin khách hàng, tiết kiệm thời gian và giảm thiểu lỗi. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ marketing!