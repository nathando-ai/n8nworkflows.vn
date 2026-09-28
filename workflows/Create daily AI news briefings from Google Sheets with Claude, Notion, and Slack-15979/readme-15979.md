---
title: "🚀 Tự động tạo bản tóm tắt tin tức AI hàng ngày từ Google Sheets với Claude, Notion và Slack"
description: "Giải pháp tự động 100% không cần code: lấy danh sách URL, lấy nội dung, tóm tắt bằng Claude, lưu vào Notion, gửi digest Slack và ghi log vào Google Sheets."
slug: "tua-dong-tao-bat-tom-tat-tin-tuc-ai-hang-ngay"
tags: [n8n, automation, no-code, AI, Notion, Slack, GoogleSheets]
keywords: [n8n workflow, tự động hóa, AI summarization, Notion integration, Slack notification]
---

# 🚀 Tự động tạo bản tóm tắt tin tức AI hàng ngày từ Google Sheets với Claude, Notion và Slack

Bạn đang phải lướt qua hàng trăm bài viết mỗi ngày để tìm ra những điểm quan trọng? Bạn muốn chuyển công việc này thành một quy trình tự động, chính xác và không mất thời gian? Workflow này sẽ giúp bạn:

- **Thu thập** danh sách URL từ Google Sheets.
- **Lấy nội dung** từng bài viết.
- **Tóm tắt** bằng Claude (Anthropic) thành một briefing có cấu trúc: tiêu đề, tóm tắt, lý do quan trọng, điểm liên quan.
- **Lưu** mỗi briefing vào Notion như một trang mới.
- **Gửi** một digest tổng hợp qua Slack.
- **Ghi log** toàn bộ kết quả vào một sheet log để theo dõi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ lướt bài viết xuống vài phút tạo briefing.
- **Độ chính xác cao**: Claude luôn giữ định dạng và nội dung chính xác.
- **Tự động liên tục**: Chạy hàng ngày mà không cần can thiệp.
- **Ghi log minh bạch**: Mọi briefing được lưu lại trong Google Sheets, dễ dàng tra cứu.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: 2 sheet – một chứa danh sách URL (`url` column) và một sheet log (`log`).
- **Anthropic API key**: Đăng ký tại [Anthropic](https://anthropic.com) và tạo credential “Anthropic Account” trong n8n.
- **Notion integration**: Token và ID database (`YOUR_NOTION_DATABASE_ID`) trong node “Save to Notion”.
- **Slack credentials**: Token bot và ID channel (`YOUR_SLACK_CHANNEL`) trong node “Send Slack Digest”.
- **Google Sheets credentials**: Đăng ký “Google Sheets” trong n8n và cấp quyền đọc/ghi.
- **Schedule Trigger**: Đặt thời gian chạy hàng ngày (ví dụ 08:00 UTC).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc hoặc copy toàn bộ JSON của workflow.
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON → **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Mô tả | Tham số cần chỉnh |
|------|----------|-------|-------------------|
| 1 | **Schedule Trigger** | Đặt thời gian chạy hàng ngày. | `cron` expression |
| 2 | **Configure Settings** | Định nghĩa tất cả API key, ID, prompt. | `anthropicApiKey`, `notionToken`, `notionDatabaseId`, `slackChannel`, `googleSheetId`, `logSheetId`, `claudePrompt` |
| 3 | **Read URL List from Sheets** | Đọc danh sách URL. | `sheetId`, `range` |
| 4 | **Limit to Max Articles** | Giới hạn số bài viết tối đa. | `limit` |
| 5 | **Fetch Article Content** | Lấy nội dung bài viết. | `url` |
| 6 | **Prepare Article Text** | Chuẩn bị văn bản cho Claude. | `articleText` |
| 7 | **Claude AI Chain** | Gọi Claude để tóm tắt. | `model`, `prompt` |
| 8 | **Claude Model** | Chọn mô hình. | `model = claude-sonnet-4-6` |
| 9 | **Parse Claude Briefing** | Phân tích JSON trả về. | `response` |
|10 | **Save to Notion** | Tạo trang mới trong database. | `notionToken`, `databaseId`, `briefingData` |
|11 | **Log to Google Sheets** | Ghi log vào sheet. | `sheetId`, `range`, `values` |
|12 | **Aggregate Briefings** | Tập hợp tất cả briefing. | `values` |
|13 | **Build Slack Digest** | Xây dựng nội dung Slack. | `briefings` |
|14 | **Send Slack Digest** | Gửi tin nhắn Slack. | `slackChannel`, `message` |

> **Lưu ý**: Đảm bảo node “Configure Settings” được chỉnh đúng trước khi chạy thử.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow bằng nút “Execute Workflow” với dữ liệu mẫu.
2. Kiểm tra log trong Google Sheets và Notion để xác nhận.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node “Telegram” để nhận digest qua bot.
- **Lưu log chi tiết**: Thêm node “Code” để ghi log lỗi vào Google Sheets.
- **Định kỳ gửi báo cáo**: Sử dụng node “Schedule Trigger” thứ 2 để gửi báo cáo tuần.
- **Tùy chỉnh prompt**: Thay đổi `claudePrompt` trong “Configure Settings” để nhấn mạnh các khía cạnh khác nhau (ví dụ: “Chỉ tóm tắt 3 điểm chính”).

## 📌 Kết luận
Workflow này đã được thiết kế để bạn **đưa công việc tóm tắt tin tức** từ thủ công sang tự động, giảm tải công việc hàng ngày và tăng tính chính xác. Hãy thử ngay, điều chỉnh theo nhu cầu và chia sẻ kết quả! 🚀