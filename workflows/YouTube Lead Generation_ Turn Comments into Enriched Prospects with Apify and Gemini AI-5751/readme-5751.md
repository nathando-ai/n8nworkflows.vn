---
title: "🚀 Tự động hóa Lead Generation từ YouTube: Chuyển đổi bình luận thành tiềm năng chất lượng cao với Apify và Gemini AI"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình thu thập bình luận YouTube, phân tích thông tin tiềm năng và lưu trữ dữ liệu vào Google Sheets để phát triển kinh doanh hiệu quả."
slug: "tu-dong-hoa-lead-generation-tu-youtube"
tags: [n8n, automation, no-code, lead generation, ai, google sheets]
keywords: [n8n workflow, tự động hóa, lead generation, youtube, ai, google sheets]
---

# 🚀 Tự động hóa Lead Generation từ YouTube: Chuyển đổi bình luận thành tiềm năng chất lượng cao với Apify và Gemini AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc thu thập và phân tích bình luận YouTube
- Tự động hóa quy trình tìm kiếm thông tin tiềm năng từ bình luận
- Tích hợp AI để phân tích và tổng hợp thông tin một cách hiệu quả
- Lưu trữ dữ liệu tiềm năng trong Google Sheets để quản lý dễ dàng
- Tự động hóa quy trình theo dõi và cập nhật thông tin mới
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- API Key từ OpenRouter (để sử dụng mô hình Gemini AI)
- API Token từ Apify (để sử dụng các Actor như YouTube Comments Scraper)
- API Key từ Serper (để thực hiện tìm kiếm Google)
- Tài khoản Google Cloud Platform đã cấu hình OAuth2 cho Google Sheets
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào trang workflow gốc tại [n8n.io](https://n8n.io/workflows/5751)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong giao diện n8n của bạn, click vào "Import from Clipboard" và dán JSON đã sao chép
4. Hoặc các sếp cũng có thể tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**Section 1: YouTube Comment Extraction**
- **When clicking ‘Execute workflow’**: Node này sẽ kích hoạt workflow khi được thực thi thủ công
- **HTTP apify get comments from video**: Cần cấu hình API Token của Apify
- **mark video url as scrapped**: Cần cấu hình Google Sheets OAuth2 API và chỉ định đúng Sheet ID và tên sheet
- **Get rvideo urls**: Cần cấu hình Google Sheets OAuth2 API và chỉ định đúng Sheet ID và tên sheet
- **Save scrapped comments**: Cần cấu hình Google Sheets OAuth2 API và chỉ định đúng Sheet ID và tên sheet

**Section 2: Lead Research & Enrichment (AI Agent)**
- **When chat message received**: Node này sẽ kích hoạt workflow khi nhận tin nhắn chat
- **OpenRouter Chat Model**: Cần cấu hình API Key từ OpenRouter và chọn mô hình `google/gemini-2.5-flash-preview-05-20`
- **get comments**: Cần cấu hình Google Sheets OAuth2 API và chỉ định đúng Sheet ID và tên sheet
- **search google**: Cần cấu hình API Key từ Serper
- **get url mardown**: Cần cấu hình API Token của Apify
- **create a row for new search user**: Cần cấu hình Google Sheets OAuth2 API và chỉ định đúng Sheet ID và tên sheet
- **update result for user**: Cần cấu hình Google Sheets OAuth2 API và chỉ định đúng Sheet ID và tên sheet
- **instagram full profile scraper**: Cần cấu hình API Token của Apify
- **mark comment as processed**: Cần cấu hình Google Sheets OAuth2 API và chỉ định đúng Sheet ID và tên sheet

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
- Bật Active workflow để chạy tự động theo lịch trình đã cấu hình

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với Slack/Telegram để nhận thông báo khi có tiềm năng mới
- Thêm node để gửi email tự động cho các tiềm năng quan trọng
- Tích hợp với CRM để quản lý tiềm năng một cách hiệu quả
- Thiết lập báo cáo định kỳ để theo dõi hiệu suất của workflow

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa quy trình thu thập và phân tích bình luận YouTube, giúp các doanh nghiệp tiết kiệm thời gian và nguồn lực đáng kể trong việc phát triển kinh doanh. Bằng cách tích hợp AI và các công cụ web scraping, workflow này không chỉ thu thập bình luận mà còn phân tích và tổng hợp thông tin tiềm năng một cách hiệu quả, lưu trữ dữ liệu vào Google Sheets để quản lý dễ dàng. Các sếp có thể tùy chỉnh và mở rộng workflow này để phù hợp với nhu cầu cụ thể của mình, tạo ra một hệ thống tự động hóa lead generation mạnh mẽ và hiệu quả.