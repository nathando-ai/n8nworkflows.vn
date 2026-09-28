---
title: "🚀 Tự động hóa YouTube: Tóm tắt video, duyệt Slack và đăng lên Reddit với n8n"
description: "Workflow n8n tự động hóa toàn bộ quy trình từ theo dõi video mới đến đăng bài lên Reddit thông qua tóm tắt AI và duyệt nội dung trên Slack"
slug: "tu-dong-hoa-youtube-tom-tat-video-slack-reddit"
tags: [n8n, automation, no-code, youtube, reddit, slack, ai, marketing]
keywords: [n8n workflow, tự động hóa youtube, tóm tắt video, duyệt nội dung slack, đăng bài reddit, ai marketing]
---

# 🚀 Tự động hóa YouTube: Tóm tắt video, duyệt Slack và đăng lên Reddit với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý hàng trăm video YouTube hàng ngày
- Tăng độ chính xác và nhất quán trong nội dung đăng bài
- Tích hợp kiểm duyệt nội dung qua Slack trước khi đăng
- Lưu trữ lịch sử tóm tắt video trong Google Sheets
- Tự động đăng bài lên Reddit sau khi duyệt nội dung
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản YouTube (để lấy RSS feed)
- Tài khoản Google (để tạo Google Sheet lưu trữ)
- Tài khoản Slack (để duyệt nội dung)
- Tài khoản Reddit (để đăng bài)
- API Key OpenAI (để sử dụng GPT tóm tắt)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4581)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "YouTube RSS Trigger"**:
   - Cấu hình URL RSS feed của kênh YouTube cần theo dõi
   - Ví dụ: `https://www.youtube.com/feeds/videos.xml?channel_id=UC...`

2. **Node "Fetch Video Details"**:
   - Cần thêm YouTube API Key trong credentials
   - Đảm bảo API Key có quyền truy cập YouTube Data API

3. **Node "OpenAI GPT Summary Model"**:
   - Chọn model GPT phù hợp (gpt-4o-mini, gpt-4o...)
   - Cấu hình API Key OpenAI trong credentials

4. **Node "Store results to Google Sheet"**:
   - Tạo Google Sheet mới và chia sẻ với service account
   - Cấu hình Spreadsheet ID và tên Sheet trong node

5. **Node "Send Summary for Approval"**:
   - Tạo channel Slack mới để duyệt nội dung
   - Cấu hình channel ID trong node

6. **Node "Publish To Reddit"**:
   - Tạo subreddit mới hoặc sử dụng subreddit hiện có
   - Cấu hình Reddit API credentials

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node gửi email thông báo khi có video mới
2. Tích hợp với Discord thay vì Reddit
3. Thêm phân tích cảm xúc cho nội dung tóm tắt
4. Tự động dịch nội dung sang nhiều ngôn ngữ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình từ theo dõi video YouTube đến đăng bài lên Reddit, với kiểm duyệt nội dung qua Slack và tóm tắt AI. Hãy thử ngay để tiết kiệm thời gian và nâng cao hiệu quả marketing!