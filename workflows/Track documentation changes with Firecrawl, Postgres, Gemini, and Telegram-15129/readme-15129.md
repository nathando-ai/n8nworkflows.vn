---
title: "🚀 Theo dõi thay đổi tài liệu với Firecrawl, Postgres, Gemini và Telegram"
description: "Tự động hóa theo dõi thay đổi tài liệu với Firecrawl, Postgres, Gemini và Telegram - Giải pháp hoàn hảo cho các sếp quản lý tài liệu Zalo Bot Platform"
slug: "theo-doi-thay-doi-tai-lieu-voi-firecrawl-postgres-gemini-telegram"
tags: [n8n, automation, no-code, firecrawl, postgres, gemini, telegram]
keywords: [n8n workflow, tự động hóa, theo dõi tài liệu, firecrawl, postgres, gemini, telegram]
---

# 🚀 Theo dõi thay đổi tài liệu với Firecrawl, Postgres, Gemini và Telegram

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công các thay đổi trong tài liệu của Zalo Bot Platform (hoặc bất kỳ tài liệu nào khác). Việc này tốn thời gian, dễ bỏ sót và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình theo dõi, phát hiện thay đổi và nhận báo cáo bằng tiếng Việt thông qua Telegram.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công mỗi ngày.
- **Chính xác**: Phát hiện mọi thay đổi trong tài liệu.
- **Cá nhân hóa**: Nhận báo cáo bằng tiếng Việt, dễ hiểu.
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Firecrawl API (Cloud hoặc self-hosted).
- Tài khoản Google Gemini (từ [Google AI Studio](https://aistudio.google.com)).
- Tài khoản Telegram Bot (token từ @BotFather).
- Cơ sở dữ liệu Postgres (có thể sử dụng dịch vụ như [Neon](https://neon.tech/)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15129](https://n8n.io/workflows/15129).
2. Nhấn nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Firecrawl Map Docs**:
   - Chọn credentials "firecrawlApi".
   - Thay đổi URL trong tham số "url" thành URL tài liệu cần theo dõi (ví dụ: `https://bot.zapps.me/docs`).

2. **Split & Filter Links**:
   - Chỉnh sửa code để lọc đúng các đường dẫn tài liệu (ví dụ: chỉ giữ các đường dẫn bắt đầu bằng `/docs`).

3. **Postgres Upsert & Diff**:
   - Chọn credentials "postgres".
   - Chạy câu lệnh SQL tạo bảng `docs_snapshots` như trong phần Database schema.

4. **Send Telegram Alert**:
   - Chọn credentials "telegramApi".
   - Thay đổi tham số "chatId" thành ID của Telegram chat cần nhận thông báo.

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test Workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Theo dõi nhiều tài liệu**: Sao chép nhánh Map + Scrape và thay đổi URL cho từng tài liệu.
- **Thay đổi tần suất**: Chỉnh sửa Schedule Trigger để chạy theo giờ hoặc hàng tuần.
- **Sử dụng LLM khác**: Thay thế Google Gemini bằng OpenAI, Claude hoặc LLM cục bộ.
- **Gửi thông báo đến Slack/Discord**: Thay thế node Telegram bằng node Slack/Discord tương ứng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi thay đổi tài liệu, tiết kiệm thời gian và đảm bảo không bỏ sót bất kỳ thay đổi quan trọng nào. Hãy áp dụng ngay để tối ưu hóa quá trình quản lý tài liệu của các sếp!