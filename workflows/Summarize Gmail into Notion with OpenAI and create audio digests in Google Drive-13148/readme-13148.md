---
title: "🚀 Tự động hóa Email: Tóm tắt Gmail vào Notion với OpenAI và tạo bản ghi âm trong Google Drive"
description: "Hướng dẫn tự động hóa quy trình tóm tắt email từ Gmail vào Notion và tạo bản ghi âm trong Google Drive sử dụng n8n và OpenAI"
slug: "tu-dong-hoa-tom-tat-gmail-vao-notion-voi-openai"
tags: [n8n, automation, no-code, gmail, notion, openai, google-drive]
keywords: [n8n workflow, tự động hóa email, tóm tắt văn bản, openai, google drive]
---

# 🚀 Tự động hóa Email: Tóm tắt Gmail vào Notion với OpenAI và tạo bản ghi âm trong Google Drive

[Các sếp] có bao giờ cảm thấy bị ngập ngụa bởi lượng email hàng ngày không? Với workflow này, các sếp có thể tự động hóa quy trình tóm tắt email từ Gmail vào Notion và tạo bản ghi âm trong Google Drive, giúp tiết kiệm thời gian và tập trung vào những việc quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tóm tắt email hàng ngày từ Gmail vào Notion
- Tạo bản ghi âm từ văn bản tóm tắt và lưu vào Google Drive
- Tiết kiệm thời gian và công sức trong việc xử lý email hàng ngày
- Tạo ra một hệ thống lưu trữ kiến thức cá nhân hóa và dễ truy cập
- Hoạt động liên tục theo lịch trình hàng tuần
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ
- Tài khoản Notion với quyền tạo và chỉnh sửa trang
- Tài khoản Google Drive với quyền tải lên và chia sẻ
- API Key từ OpenAI
- API Key từ ElevenLabs (dùng cho chuyển đổi văn bản thành giọng nói)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n bằng cách:
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: [https://n8n.io/workflows/13148](https://n8n.io/workflows/13148)
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Get many messages**: Cấu hình credentials Gmail và chọn operation "getAll"
- **OpenAI Chat Model**: Cấu hình credentials OpenAI và chọn model "gpt-5.2"
- **Get a message**: Cấu hình credentials Gmail và chọn operation "get"
- **Code in JavaScript**: Không cần cấu hình, nhưng các sếp có thể chỉnh sửa logic nếu cần
- **OpenAI Chat Model1**: Cấu hình credentials OpenAI và chọn model "gpt-5.2"
- **Import body emails**: Không cần cấu hình
- **Final Summary**: Không cần cấu hình
- **Convert text to speech**: Cấu hình credentials ElevenLabs
- **Upload file**: Cấu hình credentials Google Drive
- **Share file**: Cấu hình credentials Google Drive và chọn operation "share"
- **Generate audio**: Cấu hình credentials OpenAI và chọn model "tts-1-hd"
- **Weekly trigger**: Cấu hình lịch trình hàng tuần
- **Mark as read**: Cấu hình credentials Gmail và chọn operation "removeLabels"
- **Create Google Drive URL**: Không cần cấu hình
- **Create a link to audio file in Notion**: Cấu hình credentials Notion và chọn resource "block"
- **Create a text block Notion**: Cấu hình credentials Notion và chọn resource "block"

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
- Bật Active workflow và kiểm tra kết quả sau mỗi lần chạy

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Gửi báo cáo định kỳ về số lượng email đã xử lý và thời gian thực hiện
- Tùy chỉnh prompt cho OpenAI để phù hợp với nhu cầu cụ thể của doanh nghiệp
- Thêm bước xác thực hai yếu tố cho các tài khoản quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình tóm tắt email hàng ngày, tạo ra một hệ thống lưu trữ kiến thức cá nhân hóa và dễ truy cập. Với việc tích hợp OpenAI và Google Drive, các sếp có thể dễ dàng quản lý và chia sẻ thông tin quan trọng. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!