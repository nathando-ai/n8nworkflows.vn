---
title: "🚀 Tự động hóa thông báo sự kiện từ TwentyCRM qua Email/Slack với ghi log chi tiết"
description: "Hướng dẫn tự động gửi thông báo sự kiện từ TwentyCRM qua email hoặc Slack dựa trên loại sự kiện, đồng thời ghi log vào Google Sheets - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-hoa-thong-bao-su-kien-twentycrm-email-slack-ghi-log"
tags: [n8n, automation, no-code, crm, google-sheets]
keywords: [n8n workflow, tự động hóa crm, twentycrm, email automation, slack notification]
---

# 🚀 Tự động hóa thông báo sự kiện từ TwentyCRM qua Email/Slack với ghi log chi tiết

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công các sự kiện quan trọng từ TwentyCRM và gửi thông báo đến các kênh khác nhau (Email/Slack) dựa trên loại sự kiện. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, không cần viết code hay hiểu sâu về lập trình.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi thông báo đến đúng kênh (Email/Slack) dựa trên loại sự kiện từ TwentyCRM
- Ghi log chi tiết tất cả các sự kiện vào Google Sheets
- Tiết kiệm thời gian đáng kể cho việc theo dõi thủ công
- Đảm bảo thông tin được gửi đến đúng người đúng lúc
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản TwentyCRM với quyền truy cập API
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản Gmail để gửi email thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/2509)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "on new twentycrm event" (Webhook)**:
   - Cần cấu hình URL webhook trong TwentyCRM:
     - Truy cập cài đặt webhook trong TwentyCRM
     - Thêm mới webhook với URL: `https://your-n8n-instance.com/webhook/8118bda9-0e4f-44cd-bf64-31020b6d5ab5`
     - Phương thức: POST
   - Đảm bảo chọn đúng loại sự kiện cần theo dõi

2. **Node "filter required data #eventType mandatory" (Set)**:
   - Chỉnh sửa điều kiện lọc dữ liệu theo nhu cầu của các sếp
   - Đảm bảo giữ lại trường `eventType` vì nó là điều kiện quan trọng cho logic sau

3. **Node "events log" (Google Sheets)**:
   - Cấu hình Google Sheets credentials
   - Chọn spreadsheet và worksheet để lưu log
   - Đảm bảo có quyền ghi dữ liệu vào sheet này

4. **Node "email channel for delete eventType" (Gmail)**:
   - Cấu hình Gmail credentials
   - Điền địa chỉ email nhận thông báo
   - Tùy chỉnh nội dung email theo nhu cầu

5. **Node "message channel for all other eventTypes" (Slack)**:
   - Cấu hình Slack credentials
   - Chọn kênh hoặc người nhận thông báo
   - Tùy chỉnh nội dung tin nhắn theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Test workflow bằng cách tạo một sự kiện trong TwentyCRM và kiểm tra:
   - Log được ghi vào Google Sheets
   - Thông báo được gửi đến đúng kênh (Email/Slack)

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung thông báo**: Chỉnh sửa template email và tin nhắn Slack để phù hợp với nhu cầu cụ thể của các sếp
2. **Thêm kênh thông báo**: Có thể thêm các kênh khác như Telegram bằng cách thêm node tương ứng
3. **Lọc sự kiện nâng cao**: Sử dụng node "Set" để thêm các điều kiện lọc phức tạp hơn
4. **Báo cáo định kỳ**: Tạo một workflow phụ để tổng hợp và gửi báo cáo từ Google Sheets định kỳ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình theo dõi và thông báo sự kiện từ TwentyCRM, tiết kiệm thời gian đáng kể và đảm bảo thông tin được gửi đến đúng người đúng lúc. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!