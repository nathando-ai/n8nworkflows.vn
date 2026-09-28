---
title: "🚀 Hệ thống xác minh số WhatsApp & xác nhận tự động với Rapiwa API và Google Sheets"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp xác minh số WhatsApp, gửi xác nhận và lưu dữ liệu vào Google Sheets một cách hiệu quả"
slug: "he-thong-xac-minh-so-whatsapp-voi-rapiwa-google-sheets"
tags: [n8n, automation, no-code, whatsapp, google-sheets]
keywords: [n8n workflow, tự động hóa, xác minh số điện thoại, whatsapp, google sheets]
---

# 🚀 Hệ thống xác minh số WhatsApp & xác nhận tự động với Rapiwa API và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải xác minh số WhatsApp thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý thủ công lên tới 90%
- Tự động xác minh số WhatsApp hợp lệ với Rapiwa API
- Gửi tin nhắn xác nhận tự động cho khách hàng
- Lưu trữ dữ liệu khách hàng có cấu trúc trên Google Sheets
- Hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets với cấu trúc bảng như [mẫu này](https://docs.google.com/spreadsheets/d/1H29z_8tnsu8AvCsI7o1SjiV-5LDTwiVVQk-BNr8SMk0/edit?usp=sharing)
- Credentials Google Sheets OAuth2 đã kết nối với n8n
- Tài khoản Rapiwa API với:
  - Số WhatsApp đã kết nối và ủy quyền
  - Bearer Token hợp lệ
  - Quyền truy cập các endpoint: verify-whatsapp và send-message
- Số WhatsApp cá nhân hoặc doanh nghiệp
- Form web gửi dữ liệu POST với các trường: business_name, location, whatsapp, email, name
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [https://n8n.io/workflows/8576](https://n8n.io/workflows/8576)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**:
   - Đảm bảo đường dẫn webhook trùng khớp với form của bạn: `POST /a9b6a936-e5f2-4d4c-9cf9-182de0a970d5`
   - Nếu cần bảo mật, hãy cấu hình xác thực cho webhook

2. **Node Google Sheets**:
   - Cấu hình credentials Google Sheets OAuth2
   - Điền chính xác ID của Google Sheet và tên sheet
   - Đảm bảo cấu trúc cột phù hợp với mẫu:
     ```
     Business Name | Location | WhatsApp Number | Email | Name | Date | validity
     ```

3. **Node HTTP Request (Rapiwa API)**:
   - Cấu hình credentials HTTP Bearer Auth với token Rapiwa
   - Kiểm tra endpoint API: `https://app.rapiwa.com/api/verify-whatsapp`

4. **Node Send Message Using Rapiwa**:
   - Chỉnh sửa nội dung tin nhắn xác nhận theo thương hiệu của bạn
   - Đảm bảo số WhatsApp của bạn đã được kết nối với Rapiwa

#### 3. Kích hoạt ⚡️
1. Kiểm tra workflow bằng cách gửi dữ liệu mẫu từ form của bạn
2. Nhấn "Execute Node" để kiểm tra từng node
3. Sau khi kiểm tra thành công, nhấn "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh tin nhắn**: Chỉnh sửa nội dung tin nhắn xác nhận trong node "Send Message Using Rapiwa" để phù hợp với thương hiệu của bạn
2. **Xử lý hàng loạt**: Nếu nhận nhiều yêu cầu cùng lúc, hãy tăng số lượng batch trong node "Loop Over Items"
3. **Báo cáo định kỳ**: Kết hợp với node gửi email để tạo báo cáo hàng ngày về các số WhatsApp đã xác minh
4. **Kết nối Slack**: Thêm node gửi thông báo Slack khi có số WhatsApp mới được xác minh

### 📌 Kết luận
Hệ thống xác minh số WhatsApp này giúp các sếp tiết kiệm thời gian đáng kể trong quá trình xử lý dữ liệu khách hàng. Với khả năng tự động xác minh số WhatsApp, gửi tin nhắn xác nhận và lưu trữ dữ liệu có cấu trúc, workflow này là giải pháp hoàn hảo cho các doanh nghiệp muốn tối ưu hóa quy trình làm việc của mình. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tăng hiệu quả kinh doanh!