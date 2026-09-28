---
title: "🚀 Tự động hóa Daily AI News Digest lên LinkedIn với n8n, OpenAI và RSS"
description: "Giải pháp tự động thu thập, tóm tắt và đăng bài AI News hàng ngày lên LinkedIn, giảm công sức 100% và tăng tương tác."
slug: "tang-dong-automation-daily-ai-news-digest-len-linkedin"
tags: [n8n, automation, no-code, AI, RSS, LinkedIn, OpenAI]
keywords: [n8n workflow, tự động hóa, AI news digest, LinkedIn post, OpenAI, RSS feed]
---

# 🚀 Tự động hóa Daily AI News Digest lên LinkedIn với n8n, OpenAI và RSS

Bạn đang phải dành hàng giờ mỗi ngày để tìm kiếm, đọc và viết lại những tin tức AI mới nhất? Workflow này sẽ giúp các sếp tiết kiệm thời gian, giảm sai sót và tăng cường sự hiện diện trên LinkedIn mà không cần viết code. Hãy cùng khám phá cách triển khai chi tiết dưới đây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và tóm tắt nội dung, giảm công việc thủ công lên 90%.
- **Chính xác và nhất quán**: Đảm bảo mỗi bài đăng luôn có cấu trúc chuẩn, tránh lỗi ngữ pháp và định dạng.
- **Tăng tương tác**: Đăng bài liên tục, thu hút người theo dõi và mở rộng mạng lưới chuyên nghiệp.
- **Hoạt động liên tục**: Chạy 24/7, không bị gián đoạn dù sếp đang bận công việc khác.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản OpenAI**: API Key (được lưu trong credential `openAiApi`).
- **Tài khoản Gmail**: OAuth2 (được lưu trong credential `gmailOAuth2`).
- **Địa chỉ email nhận báo cáo**: Được cấu hình trong node `Send for Review1` và `No Articles Notification1`.
- **Địa chỉ RSS Feed**: 3 nguồn (VentureBeat AI, TechCrunch AI, OpenAI Blog) – được nhập trong các node `rssFeedRead`.
- **VPS hoặc môi trường n8n**: Đảm bảo đã cài đặt n8n và có quyền truy cập internet.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/5068>.
2. Trong n8n Editor, chọn **Import** → **Upload JSON** → chọn file đã tải.
3. Hoặc copy toàn bộ JSON và dán vào **Import from Clipboard**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Daily AI News Check1** | ScheduleTrigger | `Interval: 24h` (hoặc tùy chỉnh) |
| **VentureBeat AI RSS1**, **TechCrunch AI RSS1**, **OpenAI Blog RSS1** | rssFeedRead | `URL: https://.../rss` (địa chỉ RSS) |
| **Filter Recent AI Articles1** | Code | `inputData` → `items` → lọc theo `publishedDate` > `lastRun` |
| **Merge All Sources1** | Merge | Kết hợp 3 mảng RSS thành 1 mảng duy nhất |
| **AI News Summarizer1** | OpenAI | `Prompt: "Summarize the following AI articles into a concise paragraph."` |
| **Prepare Articles for Summary1** | Code | Chuẩn bị dữ liệu đầu vào cho OpenAI (định dạng JSON) |
| **Generate LinkedIn Post1** | OpenAI | `Prompt: "Create a LinkedIn post based on the summary above, including a catchy headline and relevant hashtags."` |
| **Send for Review1** | Gmail | `To: <địa chỉ email>`, `Subject: AI News Digest`, `Body: <generated post>` |
| **Check Articles Exist1** | If | Kiểm tra `items.length > 0` |
| **No Articles Notification1** | Gmail | `To: <địa chỉ email>`, `Subject: No new AI articles`, `Body: No articles found in the last run.` |

> **Lưu ý**: Mỗi node `OpenAI` cần credential `openAiApi`. Mỗi node `Gmail` cần credential `gmailOAuth2`. Đảm bảo credential đã được tạo trong phần **Credentials** của n8n.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công với dữ liệu mẫu (bấm **Execute Workflow**).
2. Kiểm tra log, đảm bảo không có lỗi.
3. Bật **Active** (đánh dấu nút xanh) để workflow tự động chạy theo lịch.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram Notification**: Thêm node `Slack` hoặc `Telegram` để nhận thông báo khi bài đăng đã được gửi.
- **Lưu trữ lịch sử**: Dùng node `Google Sheets` hoặc `MySQL` để ghi lại tiêu đề, link, và thời gian đăng.
- **Đăng bài lên LinkedIn API**: Thay vì gửi qua Gmail, dùng node `LinkedIn` (hoặc HTTP Request) để đăng trực tiếp.
- **Tùy chỉnh tóm tắt**: Thay đổi prompt của `AI News Summarizer1` để lấy 3 điểm nổi bật thay vì đoạn văn ngắn.

## 📌 Kết luận
Workflow này giúp các sếp chuyển từ công việc thủ công sang tự động hóa hoàn toàn, tiết kiệm thời gian và tăng hiệu quả truyền thông. Hãy thử triển khai ngay hôm nay, và nếu cần hỗ trợ tùy chỉnh, đừng ngần ngại liên hệ với iTechNotion – nơi biến ý tưởng thành quy trình tự động thực thụ!