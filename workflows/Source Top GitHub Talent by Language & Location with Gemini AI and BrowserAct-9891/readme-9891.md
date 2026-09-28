---
title: "🚀 Tự động tìm kiếm và xếp hạng tài năng lập trình từ GitHub bằng AI và BrowserAct"
description: "Hướng dẫn chi tiết cách tự động tìm kiếm và xếp hạng tài năng lập trình trên GitHub theo ngôn ngữ và vị trí bằng công cụ AI Gemini và BrowserAct trong n8n"
slug: "tu-dong-tim-kiem-tai-nang-lap-trinh-github-ai-browseract"
tags: [n8n, automation, no-code, github, ai]
keywords: [n8n workflow, tự động hóa, tìm kiếm tài năng, github, ai]
---

# 🚀 Tự động tìm kiếm và xếp hạng tài năng lập trình từ GitHub bằng AI và BrowserAct

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tìm kiếm và xếp hạng tài năng lập trình trên GitHub theo ngôn ngữ và vị trí
- Tiết kiệm thời gian và công sức cho việc tìm kiếm và đánh giá tài năng
- Tăng hiệu quả tuyển dụng bằng cách tập trung vào những ứng viên tiềm năng nhất
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BrowserAct API để thực hiện web scraping
- Tài khoản Google Gemini để sử dụng AI Agent
- Tài khoản Google Sheets để lưu trữ dữ liệu
- Tài khoản Slack để nhận thông báo
- Cài đặt n8n-nodes-browseract-workflows community node
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Schedule Trigger**: Cấu hình thời gian chạy workflow (mặc định là hàng giờ)
- **Run a workflow task**: Cấu hình credentials BrowserAct API và tham số tìm kiếm (ngôn ngữ, vị trí, số trang, số repository công khai)
- **Get details of a workflow task**: Cấu hình credentials BrowserAct API và tham số operation là "getTask"
- **Code in JavaScript**: Chỉnh sửa mã JavaScript để xử lý dữ liệu thô từ BrowserAct
- **AI Agent**: Cấu hình credentials Google Gemini và tham số cho AI Agent
- **Structured Output Parser**: Cấu hình tham số cho Structured Output Parser
- **Append or update row in sheet**: Cấu hình credentials Google Sheets và tham số cho Google Sheets
- **Gemini Chat**: Cấu hình credentials Google Gemini và tham số cho Gemini Chat
- **Send a message**: Cấu hình credentials Slack và tham số cho Slack

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có lỗi xảy ra trong quá trình scraping
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Gửi báo cáo định kỳ về danh sách tài năng mới được tìm thấy
- Tích hợp với các công cụ tuyển dụng khác để tự động gửi hồ sơ ứng viên

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động tìm kiếm và xếp hạng tài năng lập trình trên GitHub. Bằng cách kết hợp công nghệ AI Gemini và công cụ web scraping BrowserAct, các sếp có thể tiết kiệm thời gian và công sức trong quá trình tuyển dụng, đồng thời tập trung vào những ứng viên tiềm năng nhất.