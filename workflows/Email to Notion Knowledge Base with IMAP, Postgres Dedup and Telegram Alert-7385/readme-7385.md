---
title: "🚀 Tự động lưu Email vào Notion Knowledge Base với IMAP, Postgres Dedup & Telegram"
description: "Xây dựng hệ thống tự động hóa chuyển đổi email quan trọng thành trang Notion Knowledge Base, chống trùng lặp qua PostgreSQL và nhận thông báo Telegram tức thì."
slug: "tu-dong-luu-email-vao-notion-knowledge-base-imap-postgres-telegram"
tags: [n8n, automation, notion, postgresql, telegram, imap, email-automation]
keywords: [n8n workflow, email to notion, imap trigger, postgresql dedup, telegram alert, knowledge base tự động]
---

# 🚀 Tự động hóa đồng bộ Email thành Notion Knowledge Base siêu tốc

Các sếp có bao giờ cảm thấy ngợp trước hàng tá email quan trọng, newsletter hữu ích hay tài liệu từ khách hàng gửi đến mỗi ngày? Việc copy-paste thủ công từng email vào Notion để làm kho tri thức (Knowledge Base) vừa tốn thời gian, vừa dễ bỏ sót, lại cực kỳ nhàm chán.

Đừng lo, workflow n8n này sinh ra là để giải quyết triệt để vấn đề đó cho các sếp! Hệ thống sẽ tự động quét email đến qua **IMAP**, chuẩn hóa nội dung, kiểm tra trùng lặp thông minh bằng **PostgreSQL**, lưu trữ gọn gàng vào **Notion Database** và bắn thông báo báo cáo trực tiếp qua **Telegram** mà không cần đụng đến một dòng code thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Biến hòm thư đến thành kho kiến thức Notion sống động mà không cần thao tác tay.
- **Chống trùng lặp thông minh (Dedup)**: Nhờ PostgreSQL kiểm tra `message_id`, hệ thống đảm bảo không bao giờ lưu một email hai lần dù trigger chạy nhiều lần.
- **Cá nhân hóa dữ liệu**: Tự động trích xuất tiêu đề, tóm tắt (snippet), ngày tháng, đường dẫn nguồn và định dạng lại nội dung rõ ràng.
- **Theo dõi thời gian thực**: Nhận thông báo qua Telegram ngay khi email mới được xử lý và lưu thành công vào Notion.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance**: Đã cài đặt sẵn (Khuyến nghị bản Self-hosted trên VPS).
- **Tài khoản Email (IMAP)**: Thông tin kết nối IMAP (Ví dụ: Gmail bật App Password, Host: `imap.gmail.com`, Port: `993`, SSL/TLS).
- **PostgreSQL Database**: Một cơ sở dữ liệu Postgres để lưu index chống trùng lặp.
- **Notion Integration**: Đã tạo Database chứa Knowledge Base và cấp quyền (Share) cho Integration Token của n8n.
- **Telegram Bot**: Token của Bot và Chat ID để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node chính sau:

- **Email Trigger (IMAP)**: 
  - Cấu hình credentials kết nối đến hòm thư của các sếp.
  - Tại phần *Options* -> Thêm `customEmailConfig` với giá trị `["UNSEEN"]` để chỉ quét các email chưa đọc.
- **Node Code (Normalize)**: 
  - Chức năng chuẩn hóa HTML sang plain text, tạo slug thân thiện cho URL, trích xuất `messageId`, `sentAt`, `fromAddress` và `sourceUrl`.
- **Execute a SQL query (Postgres)**: 
  - Chạy câu lệnh tạo bảng lần đầu tiên (nếu chưa có):
  ```sql
  CREATE TABLE IF NOT EXISTS email_kb_index (
    message_id     TEXT PRIMARY KEY,
    slug           TEXT,
    created_at     TIMESTAMPTZ NOT NULL DEFAULT now(),
    notion_page_id TEXT
  );
  ```
  - Sử dụng câu truy vấn kiểm tra trùng lặp (`SELECT EXISTS...`) với tham số `$1 = ={{ $json.messageId }}`.
- **If Node**: 
  - Thiết lập điều kiện: Chỉ cho phép đi tiếp (`True`) nếu kết quả kiểm tra `exists` bằng `false`.
- **Create a database page (Notion)**: 
  - Dán 32 ký tự ID của Notion Database vào ô cấu hình và đảm bảo database đã được share với Integration.
  - Map các properties tương ứng: Title, Summary, Tags, Source, From, Date, Slug, Notes (`{{ $json.bodyText }}`).
- **Send a text message (Telegram)**: 
  - Điền Chat ID (`={{ $env.TELEGRAM_CHAT_ID }}`) và mẫu tin nhắn Markdown để nhận thông báo thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Node** từng phần để test thử với dữ liệu email mẫu.
- Sau khi kiểm tra mọi thứ chạy xanh mướt, bật công tắc **Active** để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI phân loại**: Các sếp có thể chèn thêm một node OpenAI hoặc Anthropic Claude trước bước ghi vào Notion để tự động tóm tắt hoặc gắn nhãn (Tags) thông minh dựa trên nội dung email.
- **Lưu log lỗi ra Slack/Telegram**: Thêm nhánh `False` ở node IF hoặc xử lý lỗi (Error Trigger) để cảnh báo khi email lỗi định dạng hoặc không lưu được vào Notion.
- **Mở rộng nguồn quét**: Thay vì chỉ dùng IMAP cho 1 tài khoản, các sếp có thể nhân bản cụm node để quét nhiều hòm thư công ty cùng lúc vào chung một kho Notion.

### 📌 Kết luận
Workflow **Email to Notion Knowledge Base** là trợ thủ đắc lực giúp tối ưu hóa quy trình quản lý thông tin cá nhân và doanh nghiệp. Hãy thiết lập ngay hôm nay để biến hòm thư bộn bề thành một cơ sở tri thức số khoa học và tự động hoàn toàn!