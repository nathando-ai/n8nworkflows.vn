---
title: "🚀 Theo dõi nhắc đến thương hiệu với phân tích cảm xúc bằng Bright Data & OpenAI"
description: "Tự động hóa theo dõi nhắc đến thương hiệu trên Medium với phân tích cảm xúc sử dụng công nghệ AI và Bright Data, tiết kiệm thời gian và tăng hiệu quả nghiên cứu thị trường."
slug: "theo-doi-nhac-den-thuong-hieu-phan-tich-cam-xuc"
tags: [n8n, automation, no-code, Bright Data, OpenAI, Google Sheets, AI Summarization]
keywords: [n8n workflow, tự động hóa, Bright Data, OpenAI, phân tích cảm xúc, nghiên cứu thị trường]
---

# 🚀 Theo dõi nhắc đến thương hiệu với phân tích cảm xúc bằng Bright Data & OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình theo dõi nhắc đến thương hiệu trên Medium
- Tăng hiệu quả: Lọc nội dung liên quan đến OpenAI một cách thông minh
- Trung tâm hóa dữ liệu: Lưu trữ kết quả vào Google Sheets dễ dàng truy cập
- Tăng cường phân tích: Phân tích cảm xúc từ nội dung nhắc đến thương hiệu
- Hỗ trợ nghiên cứu thị trường: Theo dõi xu hướng và xu hướng trong ngành công nghệ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets (để lưu trữ kết quả)
- API Key từ OpenAI (để sử dụng các tính năng AI)
- Tài khoản Bright Data (để sử dụng công cụ scraping)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **🚀 Start Workflow (Manual Trigger)**: Node này cho phép bạn khởi động workflow thủ công. Bạn chỉ cần nhấn nút "Execute workflow" để bắt đầu quá trình.

- **📝 Define Medium Blog URL**: Node này cho phép bạn nhập URL của bài viết Medium mà bạn muốn phân tích. Bạn chỉ cần dán URL của bài viết vào trường nhập liệu.

- **🤖 Agent: Scrape Medium Blog (OpenAI Mentions)**: Đây là node chính của workflow, nó sử dụng AI Agent để lấy và lọc nội dung từ bài viết Medium. Bạn không cần phải cấu hình gì thêm cho node này, nó sẽ tự động hoạt động khi workflow được khởi động.

- **🧠 Chat Reasoning Engine**: Node này sử dụng mô hình OpenAI để xử lý mục tiêu của bạn (ví dụ: "Tìm nhắc đến OpenAI"). Bạn cần cấu hình credentials cho OpenAI và chọn mô hình "gpt-4.1-mini".

- **🌐 Bright Data Tool**: Node này sử dụng công cụ scraping của Bright Data để truy cập và lấy nội dung từ bài viết Medium. Bạn cần cấu hình credentials cho Bright Data và chọn công cụ "scrape_as_markdown".

- **📥 Save Results to Google Sheets**: Node này lưu trữ kết quả đã được lọc và định dạng vào Google Sheets của bạn. Bạn cần cấu hình credentials cho Google Sheets và chọn thao tác "append".

- **Auto-fixing Output Parser**: Node này tự động sửa lỗi đầu ra để đảm bảo dữ liệu được định dạng đúng.

- **OpenAI Chat Model**: Node này sử dụng mô hình OpenAI để xử lý mục tiêu của bạn. Bạn cần cấu hình credentials cho OpenAI và chọn mô hình "gpt-4.1-mini".

- **Structured Output Parser**: Node này định dạng đầu ra thành dữ liệu có cấu trúc dễ đọc.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có nhắc đến thương hiệu mới.
- Lưu log các lần chạy workflow để theo dõi lịch sử.
- Gửi báo cáo định kỳ về xu hướng nhắc đến thương hiệu qua email.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tăng hiệu quả trong việc theo dõi nhắc đến thương hiệu trên Medium. Bằng cách sử dụng công nghệ AI và Bright Data, workflow tự động hóa quá trình lọc và phân tích nội dung, giúp các sếp tập trung vào những thông tin quan trọng nhất. Hãy áp dụng ngay để nâng cao hiệu quả nghiên cứu thị trường của bạn!