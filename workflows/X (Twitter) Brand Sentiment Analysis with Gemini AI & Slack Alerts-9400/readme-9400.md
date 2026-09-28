---
title: "🚀 Phân tích cảm xúc thương hiệu X (Twitter) với AI Gemini và cảnh báo Slack"
description: "Tự động thu thập, phân tích cảm xúc và theo dõi phản hồi thương hiệu trên X (Twitter) bằng công nghệ AI tiên tiến, gửi cảnh báo tức thời qua Slack"
slug: "phan-tich-cam-xuc-thuong-hieu-x-voi-ai-gemini-va-slack"
tags: [n8n, automation, no-code, twitter, google-sheets, ai, slack]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, X (Twitter), AI Gemini, Slack]
---

# 🚀 Phân tích cảm xúc thương hiệu X (Twitter) với AI Gemini và cảnh báo Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải theo dõi và phản hồi hàng nghìn tweet về thương hiệu mỗi ngày. Quá trình này tốn thời gian, dễ bỏ sót và không thể tự động hóa hoàn toàn. Workflow này sẽ giúp các sếp tự động thu thập, phân tích cảm xúc và theo dõi phản hồi thương hiệu trên X (Twitter) bằng công nghệ AI tiên tiến, gửi cảnh báo tức thời qua Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động thu thập hàng nghìn tweet về thương hiệu mỗi ngày
- Phân tích cảm xúc và chủ đề chính của từng tweet bằng AI tiên tiến
- Nhận cảnh báo tức thời về các phản hồi tiêu cực hoặc quan trọng
- Lưu trữ và theo dõi tất cả phản hồi thương hiệu trong Google Sheets
- Tự động tổng hợp báo cáo hàng ngày và gửi qua Slack
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản X (Twitter) Developer với quyền truy cập API
- Tài khoản Google Cloud với API Google Sheets và Google Gemini
- Tài khoản Slack với quyền tạo channel và gửi tin nhắn
- Google Sheets với 2 bảng: "Raw Tweets" và "AI Analysis"
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/9400)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node Schedule Trigger (Lịch chạy workflow):**
- Chỉnh sửa thời gian chạy theo nhu cầu (mặc định là hàng ngày)

**Node Tweet Scraper (Thu thập tweet):**
- Chọn credentials "httpHeaderAuth" đã cấu hình với API key của X (Twitter)
- Thay đổi tham số "q" trong URL để tìm kiếm thương hiệu của các sếp

**Node Google Gemini Chat Model (Phân tích AI):**
- Chọn credentials "googlePalmApi" đã cấu hình với API key của Google Cloud
- Có thể điều chỉnh prompt trong node để phù hợp với nhu cầu phân tích

**Node Append row in sheet (Lưu tweet thô):**
- Chọn credentials "googleSheetsOAuth2Api" đã cấu hình
- Đảm bảo bảng "Raw Tweets" đã được tạo trong Google Sheets

**Node Append row in sheet1 (Lưu kết quả phân tích):**
- Chọn credentials "googleSheetsOAuth2Api" đã cấu hình
- Đảm bảo bảng "AI Analysis" đã được tạo trong Google Sheets

**Node Send a message (Gửi báo cáo tổng hợp):**
- Chọn credentials "slackOAuth2Api" đã cấu hình
- Thay đổi channel ID để gửi báo cáo đến kênh phù hợp

**Node Send a message1 (Gửi cảnh báo khẩn cấp):**
- Chọn credentials "slackOAuth2Api" đã cấu hình
- Thay đổi channel ID để gửi cảnh báo đến kênh phù hợp

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Activate" để kích hoạt workflow
2. Chạy test với 1-2 tweet mẫu để đảm bảo workflow hoạt động đúng
3. Sau khi kiểm tra thành công, workflow sẽ tự động chạy theo lịch đã cài đặt

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi báo cáo qua email hàng ngày
- Kết hợp với workflow khác để tự động phản hồi các tweet tích cực
- Thêm node để lưu trữ dữ liệu phân tích vào cơ sở dữ liệu khác
- Tùy chỉnh prompt của AI để phù hợp với ngành nghề và thương hiệu cụ thể
- Thêm node để theo dõi và cảnh báo về các từ khóa quan trọng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi và phản hồi thương hiệu trên X (Twitter) bằng công nghệ AI tiên tiến. Với khả năng tự động thu thập, phân tích và cảnh báo, các sếp có thể tiết kiệm thời gian và tập trung vào các chiến lược quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất quản lý thương hiệu của các sếp!