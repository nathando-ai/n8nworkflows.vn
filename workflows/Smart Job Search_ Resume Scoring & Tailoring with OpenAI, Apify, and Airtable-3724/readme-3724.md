---
title: "🚀 Tự động hóa tìm việc thông minh: Đánh giá CV và tối ưu hồ sơ với OpenAI, Apify và Airtable"
description: "Workflow n8n này giúp tự động tìm kiếm việc làm phù hợp, đánh giá CV và tối ưu hóa hồ sơ của bạn với OpenAI, Apify và Airtable. Tiết kiệm thời gian và tăng cơ hội thành công trong tuyển dụng."
slug: "tu-dong-hoa-tim-viec-thong-minh-voi-openai-apify-airtable"
tags: [n8n, automation, no-code, AI, HR]
keywords: [n8n workflow, tự động hóa tìm việc, đánh giá CV, tối ưu hồ sơ, Apify, OpenAI, Airtable]
---

# 🚀 Tự động hóa tìm việc thông minh: Đánh giá CV và tối ưu hóa hồ sơ với OpenAI, Apify và Airtable

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng việc tìm kiếm việc làm phù hợp và tối ưu hóa hồ sơ là một quá trình tốn thời gian và công sức? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình tìm kiếm việc làm, đánh giá CV và tối ưu hóa hồ sơ của mình với OpenAI, Apify và Airtable. Workflow này sẽ giúp các sếp tiết kiệm thời gian và tăng cơ hội thành công trong tuyển dụng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức trong việc tìm kiếm việc làm phù hợp.
- Đánh giá CV và tối ưu hóa hồ sơ của mình với OpenAI.
- Tăng cơ hội thành công trong tuyển dụng.
- Tự động lưu trữ và quản lý thông tin việc làm với Airtable.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets.
- Tài khoản Airtable để lưu trữ thông tin việc làm.
- API key của OpenAI để sử dụng các tính năng AI.
- Tài khoản Apify để truy cập và sử dụng các công cụ web scraping.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **OpenAI Chat Model**: Cấu hình API key của OpenAI để sử dụng các tính năng AI.
- **Split Job Preferences**: Cấu hình số lượng việc làm cần tìm kiếm mỗi lần chạy.
- **Job Extract with revamped scoring**: Cấu hình mã JavaScript để trích xuất và đánh giá thông tin việc làm.
- **🕒 Trigger: Daily Job Fetch**: Cấu hình lịch chạy workflow hàng ngày.
- **📄 Fetch Job Preferences (Google Sheets)**: Cấu hình ID của Google Sheets chứa thông tin sở thích việc làm.
- **🔄 Loop: Search Jobs per Preference**: Cấu hình số lượng việc làm cần tìm kiếm mỗi lần chạy.
- **🔍 Apify: Scrape Jobs**: Cấu hình URL của trang web cần web scraping và cấu hình các tham số cần thiết.
- **🧹 Clean & Extract Job Data**: Cấu hình mã JavaScript để làm sạch và trích xuất thông tin việc làm.
- **Filter: Recent Jobs (<48h)**: Cấu hình điều kiện lọc việc làm mới nhất.
- **🗂️ Archive: Old Jobs (Airtable)**: Cấu hình ID của Airtable để lưu trữ thông tin việc làm cũ.
- **🔄 Loop: Score New Jobs**: Cấu hình số lượng việc làm cần đánh giá mỗi lần chạy.
- **🤖 AI: Score CV vs Job**: Cấu hình prompt và các tham số cần thiết để đánh giá CV và việc làm.
- **📄 Parse AI Score Output**: Cấu hình mã JavaScript để phân tích và xử lý kết quả đánh giá từ AI.
- **🔄 Loop: Generate CV Suggestions**: Cấu hình số lượng gợi ý CV cần tạo mỗi lần chạy.
- **✍️ AI: Revamp CV Based on Job**: Cấu hình prompt và các tham số cần thiết để tạo gợi ý CV.
- **🗂️ Save: Final Job Data (Airtable)**: Cấu hình ID của Airtable để lưu trữ thông tin việc làm cuối cùng.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi có việc làm mới phù hợp.
- Lưu log và gửi báo cáo định kỳ về tiến độ tìm kiếm việc làm.
- Tối ưu hóa prompt và các tham số của AI để tăng độ chính xác trong đánh giá CV và việc làm.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình tìm kiếm việc làm, đánh giá CV và tối ưu hóa hồ sơ của mình với OpenAI, Apify và Airtable. Các sếp có thể tiết kiệm thời gian và công sức, đồng thời tăng cơ hội thành công trong tuyển dụng. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của mình!