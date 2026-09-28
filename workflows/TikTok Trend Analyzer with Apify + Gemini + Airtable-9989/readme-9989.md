---
title: "🚀 Tự động hóa Phân tích Xu hướng TikTok với Apify + Gemini + Airtable"
description: "Hướng dẫn chi tiết cách tự động thu thập, phân tích video TikTok xu hướng và lưu trữ thông tin vào Airtable bằng n8n"
slug: "tu-dong-hoa-phan-tich-xu-huong-tiktok"
tags: [n8n, automation, no-code, marketing, ai, apify, airtable, gemini]
keywords: [n8n workflow, tự động hóa, phân tích xu hướng, tiktok, apify, airtable, gemini]
---

# 🚀 Tự động hóa Phân tích Xu hướng TikTok với Apify + Gemini + Airtable

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp marketing và nhà sáng tạo luôn gặp khó khăn khi phải theo dõi hàng nghìn video TikTok mỗi ngày để tìm ra những xu hướng đang hot. Việc này tốn rất nhiều thời gian và công sức, đồng thời không đảm bảo độ chính xác và tính cá nhân hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến phân tích và lưu trữ thông tin, giúp tiết kiệm thời gian và tăng hiệu quả công việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động thu thập và phân tích dữ liệu hàng tuần mà không cần can thiệp thủ công.
- Chính xác: Sử dụng AI Gemini để phân tích chi tiết các yếu tố làm nên sự thành công của video.
- Cá nhân hóa: Lưu trữ thông tin chi tiết về từng video xu hướng trong Airtable để dễ dàng truy cập và sử dụng.
- Hoạt động liên tục: Workflow có thể chạy tự động theo lịch trình hàng tuần mà không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify với API key để truy cập dữ liệu TikTok.
- Tài khoản Airtable với cơ sở dữ liệu đã tạo sẵn để lưu trữ thông tin.
- API key của Google Gemini hoặc OpenAI để phân tích video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [TikTok Trend Analyzer with Apify + Gemini + Airtable](https://n8n.io/workflows/9989).
2. Click vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Start TikTok Trends Scraper (Apify)"**:
   - Cấu hình credentials cho Apify bằng cách thêm API key vào Credential Manager.
   - Đảm bảo URL và tham số truy vấn đúng với API của Apify.

2. **Node "Fetch TikTok Dataset (Apify)"**:
   - Cấu hình credentials cho Apify bằng cách thêm API key vào Credential Manager.
   - Đảm bảo URL và tham số truy vấn đúng với API của Apify.

3. **Node "Save Trending TikToks to Airtable"**:
   - Cấu hình credentials cho Airtable bằng cách thêm API key vào Credential Manager.
   - Cập nhật Base ID và Table ID của Airtable.
   - Đảm bảo các trường dữ liệu được ánh xạ đúng với cấu trúc của Airtable.

4. **Node "Find Airtable Record by URL"**:
   - Cấu hình credentials cho Airtable bằng cách thêm API key vào Credential Manager.
   - Cập nhật Base ID và Table ID của Airtable.
   - Đảm bảo các trường dữ liệu được ánh xạ đúng với cấu trúc của Airtable.

5. **Node "Analyze TikTok Video (Gemini 2.5)"**:
   - Cấu hình credentials cho Google Gemini bằng cách thêm API key vào Credential Manager.
   - Đảm bảo các tham số phân tích được cấu hình đúng với nhu cầu của các sếp.

6. **Node "Extract Insights (LLM)"**:
   - Đảm bảo các tham số trích xuất thông tin được cấu hình đúng với nhu cầu của các sếp.

7. **Node "Update Airtable with AI Insights"**:
   - Cấu hình credentials cho Airtable bằng cách thêm API key vào Credential Manager.
   - Cập nhật Base ID và Table ID của Airtable.
   - Đảm bảo các trường dữ liệu được ánh xạ đúng với cấu trúc của Airtable.

8. **Node "Weekly Trend Trigger"**:
   - Cấu hình lịch trình chạy workflow hàng tuần theo nhu cầu của các sếp.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi có video mới được phân tích.
- Lưu log hoạt động của workflow để theo dõi và kiểm tra lỗi.
- Gửi báo cáo định kỳ về xu hướng TikTok hàng tuần để các sếp có thể dễ dàng theo dõi và đưa ra quyết định.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình phân tích xu hướng TikTok, từ thu thập dữ liệu đến lưu trữ thông tin, giúp tiết kiệm thời gian và tăng hiệu quả công việc. Hãy áp dụng ngay để có được những thông tin chi tiết và chính xác về xu hướng TikTok hàng tuần.