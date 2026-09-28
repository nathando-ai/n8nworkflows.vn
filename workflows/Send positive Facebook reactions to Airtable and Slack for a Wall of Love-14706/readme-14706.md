---
title: "🚀 Tự động hóa phản ứng Facebook tích cực: Lưu vào Airtable & Thông báo Slack"
description: "Workflow n8n giúp tự động thu thập phản ứng tích cực từ Facebook, lưu vào Airtable và thông báo trên Slack tạo nên 'Bức tường yêu thương' tăng cường tinh thần đồng đội."
slug: "tu-dong-hoa-phan-ung-facebook-tich-cuc-airtable-slack"
tags: [n8n, automation, no-code, social media, team morale]
keywords: [n8n workflow, tự động hóa, facebook reactions, airtable, slack]
---

# 🚀 Tự động hóa phản ứng Facebook tích cực: Lưu vào Airtable & Thông báo Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 20+ giờ mỗi tháng với tự động hóa thu thập phản ứng Facebook
- Tạo ra "Bức tường yêu thương" Slack tăng cường tinh thần đồng đội
- Lưu trữ dữ liệu phản ứng trong Airtable để phân tích sau này
- Hoạt động liên tục 24/7 với lịch trình tự động
- Tăng cường tương tác khách hàng thông qua phản hồi tích cực
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook Page cần theo dõi
- API Key Facebook Developer (hoặc mock data cho testing)
- Tài khoản Airtable với bảng đã tạo sẵn
- Tài khoản Slack với channel "Wall of Love" đã tạo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [Workflow gốc trên n8n.io](https://n8n.io/workflows/14706)
2. Click "Copy Workflow" để sao chép JSON
3. Trong n8n Editor, chọn "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Node quan trọng nhất: Fetch Facebook Page Posts**
- Cần cấu hình credentials Facebook API
- Tham số bắt buộc: `pageId` (ID của Facebook Page cần theo dõi)
- Tham số tùy chọn: `fields` (các trường dữ liệu cần lấy từ API)

**Node quan trọng thứ hai: Save Reaction to Airtable**
- Cấu hình credentials Airtable
- Tham số bắt buộc:
  - `baseId`: ID của Airtable base
  - `tableName`: Tên bảng lưu dữ liệu
  - `fields`: Mapping các trường dữ liệu (userId, postId, reactionType, timestamp...)

**Node quan trọng thứ ba: Post to Slack – Wall of Love**
- Cấu hình credentials Slack
- Tham số bắt buộc:
  - `channel`: Tên channel Slack (ví dụ: #wall-of-love)
  - `text`: Nội dung thông báo (có thể sử dụng các biến từ dữ liệu phản ứng)

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết nối
2. Kích hoạt workflow bằng cách bật nút "Active" ở góc trên bên phải
3. Đặt lịch chạy workflow theo nhu cầu (ví dụ: mỗi giờ một lần)

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Email" để gửi báo cáo hàng tuần về các phản ứng tích cực
- Kết hợp với workflow khác để tự động trả lời các phản ứng tích cực
- Thêm bộ lọc để chỉ theo dõi các phản ứng từ khách hàng VIP
- Tạo dashboard trong Airtable để theo dõi xu hướng phản ứng
- Kết nối với Google Sheets để lưu trữ dữ liệu dự phòng

### 📌 Kết luận
Workflow này là công cụ hoàn hảo cho các sếp muốn tăng cường tinh thần đồng đội thông qua phản hồi tích cực từ khách hàng. Với việc tự động hóa toàn bộ quá trình từ thu thập dữ liệu đến thông báo, các sếp có thể tập trung vào công việc cốt lõi trong khi hệ thống tự động tạo ra "Bức tường yêu thương" 24/7 trên Slack. Hãy triển khai ngay để thấy sự khác biệt trong tinh thần làm việc của đội ngũ!