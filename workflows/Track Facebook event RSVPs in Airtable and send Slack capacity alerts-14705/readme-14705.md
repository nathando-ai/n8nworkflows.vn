---
title: "🚀 Theo dõi RSVP sự kiện Facebook trong Airtable và cảnh báo vượt sức chứa trên Slack"
description: "Hướng dẫn tự động hóa theo dõi RSVP sự kiện Facebook trong Airtable và gửi cảnh báo vượt sức chứa lên Slack bằng n8n"
slug: "theo-doi-rsvp-su-kien-facebook-trong-airtable-va-slack"
tags: [n8n, automation, no-code, project-management, airtable, slack]
keywords: [n8n workflow, tự động hóa, quản lý dự án, airtable, slack]
---

# 🚀 Theo dõi RSVP sự kiện Facebook trong Airtable và cảnh báo vượt sức chứa trên Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa việc theo dõi RSVP sự kiện Facebook
- Cảnh báo vượt sức chứa ngay lập tức trên Slack
- Dữ liệu được lưu trữ và quản lý trong Airtable
- Tránh gửi nhiều cảnh báo trùng lặp
- Tiết kiệm thời gian và công sức thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtable với API Key
- Tài khoản Slack với API Key
- URL webhook của Facebook Event
- Biết ID sự kiện Facebook và sức chứa tối đa của sự kiện
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14705](https://n8n.io/workflows/14705)
2. Nhấn nút "Import" để tải workflow về máy
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Facebook Event RSVP Webhook** (Node Webhook):
   - Chọn HTTP Method: POST
   - Đặt Path: facebook-event-rsvp
   - Thiết lập webhook trên Facebook Developer Portal để gửi dữ liệu đến URL: `https://your-n8n-instance.com/webhook/facebook-event-rsvp`

2. **Edit Fields** (Node Set):
   - Thiết lập các trường cần thiết từ dữ liệu RSVP: event_id, user_id, rsvp_status, timestamp
   - Xóa các trường không cần thiết

3. **Upsert RSVP in Airtable** (Node Airtable):
   - Chọn credentials: airtableTokenApi
   - Chọn Base ID và Table Name chứa dữ liệu RSVP
   - Thiết lập các trường mapping: event_id, user_id, rsvp_status, timestamp
   - Đặt trường unique key là combination của event_id và user_id

4. **Fetch Attending RSVPs for Event** (Node Airtable):
   - Chọn credentials: airtableTokenApi
   - Chọn Base ID và Table Name chứa dữ liệu RSVP
   - Thiết lập filter: event_id = [event_id] AND rsvp_status = "attending"

5. **Is Event Capacity Exceeded?** (Node If):
   - Thiết lập điều kiện: {{ $node["Fetch Attending RSVPs for Event"].json.length }} > [event_capacity]

6. **Is Capacity Alert Already Sent?** (Node If):
   - Thiết lập điều kiện: {{ $node["Fetch Attending RSVPs for Event"].json[0].capacity_alert_sent }} == true

7. **Send Slack Capacity Alert** (Node Slack):
   - Chọn credentials: slackApi
   - Thiết lập Channel ID hoặc Channel Name để gửi cảnh báo
   - Tùy chỉnh nội dung cảnh báo: "Event [event_name] has reached capacity! Current attendees: [number_of_attendees]"

8. **Mark Capacity Alert as Sent** (Node Airtable):
   - Chọn credentials: airtableTokenApi
   - Chọn Base ID và Table Name chứa dữ liệu sự kiện
   - Thiết lập các trường mapping: event_id, capacity_alert_sent = true

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để kiểm tra workflow hoạt động đúng.
- Bật Active workflow để bắt đầu theo dõi RSVP sự kiện Facebook.

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập webhook trên Facebook để nhận dữ liệu RSVP ngay lập tức
- Tạo một bảng riêng trong Airtable để lưu trữ thông tin sự kiện và sức chứa
- Thêm các trường bổ sung như tên người tham dự, email, số điện thoại vào dữ liệu RSVP
- Tích hợp với các công cụ khác như Google Sheets để lưu trữ dữ liệu
- Thiết lập cảnh báo cho các trạng thái RSVP khác như "maybe" hoặc "declined"

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi RSVP sự kiện Facebook, cảnh báo vượt sức chứa ngay lập tức trên Slack và quản lý dữ liệu trong Airtable. Hãy áp dụng ngay để tiết kiệm thời gian và công sức thủ công!