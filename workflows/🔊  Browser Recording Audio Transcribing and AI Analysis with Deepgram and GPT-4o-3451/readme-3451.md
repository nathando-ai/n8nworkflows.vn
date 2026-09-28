---
title: "🔊 Tự động hóa ghi âm, chuyển văn bản và phân tích AI với Deepgram và GPT-4o"
description: "Hướng dẫn tự động hóa quy trình ghi âm, chuyển văn bản và phân tích nội dung bằng Deepgram và GPT-4o trong n8n. Tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-ghi-am-chuyen-van-ban-phan-tich-ai-deepgram-gpt4o"
tags: [n8n, automation, no-code, AI, Deepgram, GPT-4o]
keywords: [n8n workflow, tự động hóa, ghi âm, chuyển văn bản, phân tích nội dung, Deepgram, GPT-4o]
---

# 🔊 Tự động hóa ghi âm, chuyển văn bản và phân tích AI với Deepgram và GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa quy trình ghi âm, chuyển văn bản và phân tích nội dung.
- Tiết kiệm thời gian và công sức cho các tác vụ thủ công.
- Nâng cao hiệu suất làm việc với các công cụ AI tiên tiến.
- Tạo ra các bản ghi và phân tích có thể tái sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive để lưu trữ và quản lý các tệp âm thanh và văn bản.
- API Key từ Deepgram để chuyển đổi âm thanh thành văn bản.
- API Key từ OpenAI để sử dụng mô hình GPT-4o.
- Tài khoản Gmail để gửi các báo cáo và thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Google Drive Trigger**: Cấu hình để theo dõi các tệp âm thanh mới được tải lên Google Drive.
- **DeepGram**: Cấu hình API Key và các tham số để chuyển đổi âm thanh thành văn bản.
- **AI Agent**: Cấu hình các công cụ và mô hình AI để phân tích nội dung.
- **Structured Output Parser**: Cấu hình để định dạng đầu ra của phân tích.
- **OpenAI Chat Model**: Cấu hình API Key và các tham số cho mô hình GPT-4o.
- **Google Docs**: Cấu hình để tạo và quản lý các tài liệu Google Docs.
- **Gmail**: Cấu hình để gửi các báo cáo và thông báo qua email.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi quy trình hoàn thành.
- Lưu log các hoạt động để theo dõi và kiểm tra lại sau này.
- Gửi báo cáo định kỳ về các phân tích và kết quả.

### 📌 Kết luận
Workflow này giúp tự động hóa quy trình ghi âm, chuyển văn bản và phân tích nội dung một cách hiệu quả. Các sếp có thể áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc.