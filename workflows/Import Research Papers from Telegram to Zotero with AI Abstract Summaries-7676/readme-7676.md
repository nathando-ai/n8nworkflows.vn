---
title: "🚀 Tự động hóa Import Research Papers từ Telegram vào Zotero kèm Tóm tắt AI"
description: "Hướng dẫn cài đặt workflow n8n tự động lưu tài liệu nghiên cứu từ DOI link trên Telegram vào Zotero, lấy metadata đa nguồn và tóm tắt abstract bằng AI."
slug: "import-research-papers-telegram-zotero-ai"
tags: [n8n, automation, zotero, telegram, ai-summarization, openrouter]
keywords: [n8n workflow, telegram to zotero, tu dong hoa zotero, ai tom tat tai lieu, crossref unpaywall n8n]
---

# 🚀 Tự động hóa Import Research Papers từ Telegram vào Zotero kèm Tóm tắt AI

Các sếp làm nghiên cứu khoa học hoặc tổng hợp tài liệu chắc chắn hiểu cảm giác mệt mỏi khi cứ phải copy link DOI, tìm tải PDF thủ công, rồi lại lọ mọ điền metadata vào Zotero, sau đó đọc lướt abstract để ghi chú. Quá nhiều thao tác lặp đi lặp lại khiến năng suất giảm sút!

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để vấn đề trên. Chỉ với một tin nhắn gửi link DOI qua Telegram bot, hệ thống sẽ tự động quét, lấy metadata từ các nguồn uy tín (Crossref, DataCite, Unpaywall), đính kèm file PDF, đẩy thẳng vào thư viện Zotero, đồng thời dùng AI để tóm tắt ngắn gọn nội dung abstract rồi gửi trả lại kết quả ngay trên Telegram cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Bỏ hoàn toàn các bước nhập liệu thủ công vào Zotero.
- **Độ chính xác cao**: Kết hợp dữ liệu chuẩn xác từ nhiều nguồn lớn như Crossref, DataCite, Unpaywall.
- **AI Tóm tắt tức thì**: Nhận ngay bản tóm tắt ngắn gọn bằng AI của bài báo ngay trong khung chat Telegram.
- **Quản lý thông minh**: Tự động tìm và gieo link PDF toàn văn (full-text) vào Zotero một cách mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Telegram Bot**: Tạo bot qua `@BotFather` để lấy Token và kết nối với `Telegram Trigger`, `Send a text message`.
- **Zotero Account & API Key**: Lấy API Key từ tài khoản Zotero để tạo/cập nhật tài liệu.
- **OpenRouter API Key**: Sử dụng model `google/gemini-2.0-flash-exp:free` (hoặc model tùy chọn) qua `OpenRouter Chat Model` và `Basic LLM Chain` để tóm tắt abstract.
- *(Tùy chọn)* Email cá nhân cho Unpaywall API để tăng độ ổn định khi gọi dữ liệu Open Access.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và thông số sau trong các node cốt lõi:
- **Telegram Trigger & Send a text message / Send a text message1**: Kết nối với credential tài khoản Telegram Bot của các sếp để nhận tin nhắn chứa DOI và gửi trả phản hồi.
- **HTTP Request (Zotero nodes)**: Điền Zotero User ID và Zotero API Key để hệ thống có quyền tạo item mới trong thư viện của các sếp.
- **HTTP Request2, 3, 4, 9 (Crossref, DataCite, Unpaywall)**: Kiểm tra cấu hình URL gọi API, đảm bảo truyền đúng DOI trích xuất từ tin nhắn Telegram qua node **Code**.
- **OpenRouter Chat Model**: Cung cấp OpenRouter API Key và chọn model AI (mặc định cấu hình sẵn `google/gemini-2.0-flash-exp:free`) để phục vụ node **Basic LLM Chain** tóm tắt abstract.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn chứa link DOI (hoặc mã định danh arXiv) tới Telegram Bot của các sếp để test dữ liệu.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Teams**: Mở rộng workflow bằng cách bắn thông báo bài báo mới và bản tóm tắt AI lên channel chung của nhóm nghiên cứu.
- **Lưu log vào Google Sheets**: Thêm node Google Sheets để ghi lại lịch sử các bài báo đã import kèm ngày giờ và link Zotero.
- **Phân loại tự động bằng AI**: Sử dụng thêm một node LLM để tự động sinh ra các `Tags` phù hợp dựa trên nội dung abstract trước khi đẩy vào Zotero.

### 📌 Kết luận
Việc quản lý tài liệu nghiên cứu chưa bao giờ mượt mà đến thế! Chỉ với vài phút thiết lập workflow n8n này, các sếp đã sở hữu một trợ lý AI đắc lực, tự động hóa toàn bộ quy trình từ Telegram vào Zotero. Chúc các sếp cài đặt thành công và "nâng cấp" năng suất nghiên cứu của mình!