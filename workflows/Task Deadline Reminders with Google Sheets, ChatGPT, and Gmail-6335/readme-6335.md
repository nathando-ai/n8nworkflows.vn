---
title: "🚀 Tự động nhắc nhở deadline công việc qua Google Sheets, ChatGPT và Gmail"
description: "Hướng dẫn tự động hóa nhắc nhở deadline công việc bằng n8n, kết hợp Google Sheets, ChatGPT và Gmail để tiết kiệm thời gian và tăng hiệu quả làm việc"
slug: "tu-dong-nhac-nho-deadline-cong-viec-n8n"
tags: [n8n, automation, no-code, google-sheets, chatgpt, gmail]
keywords: [n8n workflow, tự động hóa, nhắc nhở deadline, google sheets, chatgpt, gmail]
---

# 🚀 Tự động nhắc nhở deadline công việc với Google Sheets, ChatGPT và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải nhắc nhở deadline công việc cho từng thành viên trong team một cách thủ công. Việc này tốn thời gian, dễ bỏ sót và không cá nhân hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần lập trình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động kiểm tra và nhắc nhở deadline hàng ngày
- Cá nhân hóa: Mỗi email nhắc nhở được tùy chỉnh theo nội dung công việc
- Chính xác: Không bỏ sót bất kỳ deadline nào
- Hoạt động liên tục: Chạy tự động 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được chia sẻ
- Tài khoản OpenAI với API key
- Tài khoản Gmail để gửi email nhắc nhở
- Bảng dữ liệu Google Sheets có cấu trúc như sau:
  - Cột A: Tên công việc
  - Cột B: Mô tả công việc
  - Cột C: Deadline (định dạng ngày tháng)
  - Cột D: Email người nhận
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: https://n8n.io/workflows/6335
3. Hoặc copy nội dung JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Schedule Trigger1**:
   - Cấu hình lịch chạy hàng ngày (ví dụ: 9:00 sáng mỗi ngày)
   - Thiết lập timezone phù hợp với múi giờ của bạn

2. **Get row(s) in sheet1**:
   - Chọn credentials Google Sheets OAuth2 API đã được thiết lập
   - Nhập ID của Google Sheet chứa dữ liệu công việc
   - Chỉ định tên sheet cần truy cập
   - Thiết lập truy vấn để chỉ lấy các công việc có deadline là ngày hiện tại:
     ```
     SELECT * WHERE C = TODAY()
     ```

3. **If1**:
   - Thiết lập điều kiện để kiểm tra xem có công việc nào đến deadline không
   - Ví dụ: `{{ $node["Get row(s) in sheet1"].json.length > 0 }}`

4. **Summarize1**:
   - Thiết lập mô hình ChatGPT để tóm tắt nội dung công việc
   - Ví dụ prompt:
     ```
     Tóm tắt nội dung công việc sau đây trong 3 câu ngắn gọn:
     {{ $node["Get row(s) in sheet1"].json[0].B }}
     ```

5. **Message a model1**:
   - Chọn credentials OpenAI API đã được thiết lập
   - Thiết lập mô hình ChatGPT phù hợp (ví dụ: gpt-3.5-turbo)
   - Nhập prompt để tạo nội dung email nhắc nhở:
     ```
     Tạo nội dung email nhắc nhở deadline công việc cho người nhận với các thông tin sau:
     - Tên công việc: {{ $node["Get row(s) in sheet1"].json[0].A }}
     - Mô tả tóm tắt: {{ $node["Summarize1"].json.summary }}
     - Deadline: {{ $node["Get row(s) in sheet1"].json[0].C }}
     ```

6. **Send a message1**:
   - Chọn credentials Gmail OAuth2 đã được thiết lập
   - Thiết lập địa chỉ email người gửi
   - Nhập tiêu đề email: `Nhắc nhở: Deadline công việc {{ $node["Get row(s) in sheet1"].json[0].A }}`
   - Nội dung email sử dụng từ node Message a model1: `{{ $node["Message a model1"].json.text }}`
   - Địa chỉ email người nhận lấy từ cột D của Google Sheet: `{{ $node["Get row(s) in sheet1"].json[0].D }}`

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra email nhắc nhở đã được gửi đến địa chỉ email của bạn
3. Nếu mọi thứ hoạt động tốt, nhấn nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để gửi nhắc nhở qua các kênh chat
- Thêm node lưu log các email đã gửi để theo dõi lịch sử
- Tạo báo cáo hàng tuần về tiến độ công việc sử dụng Google Sheets
- Thiết lập nhiều lịch trình khác nhau cho các nhóm công việc khác nhau

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý deadline công việc. Bằng cách tự động hóa toàn bộ quá trình từ kiểm tra đến gửi nhắc nhở, các sếp có thể tập trung vào những công việc quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của team!