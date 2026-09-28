---
title: "🚀 Trích xuất và xử lý Q&A từ URL tự động trên Telegram với Airtop, OpenRouter AI và Safety Guardrails"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất nội dung Q&A từ URL qua Telegram, kiểm duyệt an toàn bằng Guardrails và xử lý thông minh bằng OpenRouter AI."
slug: "trich-xuat-va-xu-ly-qa-tu-url-telegram-airtop-openrouter-ai"
tags: [n8n, automation, ai-agent, telegram, airtop, openrouter, safety-guardrails]
keywords: [n8n workflow, trích xuất url q&a, telegram bot ai, airtop ai, openrouter ai, safety guardrails]
---

# 🚀 Trích xuất và xử lý Q&A từ URL tự động trên Telegram với Airtop, OpenRouter AI & Safety Guardrails

Các sếp có bao giờ cảm thấy mệt mỏi khi phải đọc thủ công từng trang tài liệu dài lê thê, copy câu hỏi và tìm kiếm câu trả lời mỗi khi nhận được một đường link từ khách hàng hoặc đồng nghiệp trên Telegram? Việc xử lý thủ công này không chỉ tốn thời gian mà còn dễ bỏ sót thông tin quan trọng.

Giải pháp ở đây là gì? Hãy để **n8n workflow** này lo thay các sếp! Đây là một hệ thống tự động hóa 100% không cần code, kết hợp sức mạnh của **Telegram Bot**, công cụ trích xuất web **Airtop**, bộ lọc kiểm duyệt an toàn **Safety Guardrails**, mô hình ngôn ngữ thông minh **OpenRouter AI** và công cụ tìm kiếm web **Tavily**. Workflow sẽ tự động nhận diện URL từ Telegram, cào dữ liệu Q&A, kiểm tra bảo mật (chống nội dung độc hại/lộ thông tin cá nhân PII) và trả về kết quả an toàn ngay lập tức cho người dùng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Nhận link từ Telegram, xử lý và trả kết quả mà không cần sự can thiệp thủ công.
- **Bảo mật tuyệt đối:** Tích hợp bộ lọc *Safety Guardrails* tự động phát hiện và chặn các nội dung vi phạm NSFW hoặc rò rỉ dữ liệu cá nhân (PII).
- **Trích xuất thông minh:** Sử dụng *Airtop* và *OpenRouter AI* để lấy cấu trúc Q&A chính xác từ các trang web phức tạp.
- **Hoạt động 24/7:** Bot Telegram sẵn sàng phục vụ yêu cầu của người dùng bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Telegram Bot Token:** Tạo qua [@BotFather](https://t.me/BotFather) trên Telegram.
- **Airtop Account:** Đăng ký tại [airtop.ai](https://airtop.ai) để lấy API Key.
- **OpenRouter Account:** Đăng ký tại [openrouter.ai](https://openrouter.ai) để lấy API Key.
- **Tavily Account:** Đăng ký tại [tavily.com](https://app.tavily.com) để lấy API Key (cho phép AI search web bổ sung).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Mở n8n Editor của các sếp, chọn **Add workflow** -> **Import from File / Paste JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau trong n8n:

- **Telegram Trigger1 & Send Safe Response & Send Violation Alert:** 
  - Tạo Credentials loại **Telegram API** bằng cách nhập Token lấy từ `@BotFather`.
  - Gán credentials này cho cả 3 node liên quan đến Telegram.
- **Extract Q&A from URL (Node loại `airtop`):**
  - Tạo Credentials loại **Airtop API** từ dashboard của Airtop.
  - Kiểm tra lại prompt mặc định: *"Extract all questions and answers from this form or document"* để đảm bảo phù hợp với nhu cầu.
- **OpenRouter Model (Node loại `lmChatOpenRouter`):**
  - Cấu hình model sử dụng (mặc định là `openrouter/sherlock-dash-alpha` hoặc thay đổi sang model AI yêu thích của các sếp như Claude 3.5 Sonnet, GPT-4o...).
- **Tavily Web Search (Node loại `@tavily/n8n-nodes-tavily.tavilyTool`):**
  - Tạo Credentials loại **Tavily API** để cung cấp khả năng tìm kiếm web mở rộng cho AI Agent.
- **Apply Safety Guardrails (Node loại `guardrails`):**
  - Tùy chỉnh mức độ nhạy cảm của bộ lọc nếu cần để tránh việc bot chặn nhầm nội dung hợp lệ.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và gửi thử một đường link chứa tài liệu/Q&A đến Bot Telegram của các sếp để kiểm tra dữ liệu trả về.
- Nếu mọi thứ hoạt động trơn tru, hãy gạt công tắc sang chế độ **Active** để bot chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ lịch sử:** Kết nối thêm node **Google Sheets** hoặc **Airtable** sau bước xử lý của Agent để lưu lại toàn bộ các câu hỏi và URL mà người dùng đã tra cứu.
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể nhân bản nhánh gửi tin nhắn sang **Slack** hoặc **Discord** để phục vụ đội ngũ nội bộ công ty.
- **Tạo báo cáo định kỳ:** Thống kê số lượng URL được xử lý mỗi ngày và gửi báo cáo tổng hợp vào nhóm chat quản lý.

### 📌 Kết luận
Workflow trích xuất và xử lý Q&A từ URL này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa thời gian nghiên cứu tài liệu, tổng hợp kiến thức tự động và đảm bảo an toàn thông tin nhờ các lớp kiểm duyệt thông minh. Hãy "lên đồ" ngay cho hệ thống tự động hóa của các sếp ngày hôm nay!