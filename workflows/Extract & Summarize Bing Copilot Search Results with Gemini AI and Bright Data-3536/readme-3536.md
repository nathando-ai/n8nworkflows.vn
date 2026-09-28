---
title: "🚀 Trích xuất và Tóm tắt Kết quả Bing Copilot cực đỉnh với Gemini AI và Bright Data trong n8n"
description: "Hướng dẫn tự động hóa quy trình tìm kiếm Bing Copilot, trích xuất dữ liệu thông minh qua Bright Data Web Scraper API và tóm tắt bằng Google Gemini AI trong n8n."
slug: "trich-xuat-tom-tat-bing-copilot-gemini-bright-data-n8n"
tags: [n8n, automation, ai, gemini, bright-data, web-scraping]
keywords: [n8n workflow, bing copilot, gemini ai, bright data, web scraper api, tóm tắt dữ liệu tự động]
---

# 🚀 Trích xuất và Tóm tắt Kết quả Bing Copilot cực đỉnh với Gemini AI và Bright Data

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công tìm kiếm thông tin trên Bing Copilot, sau đó copy, phân loại và tóm tắt từng trang kết quả dài dằng dặc? Quy trình này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ sót các thông tin cốt lõi.

Đừng lo, workflow n8n này sinh ra để giải quyết triệt để vấn đề đó cho các sếp! Bằng cách kết hợp sức mạnh của **Bright Data Web Scraper API** để cào dữ liệu Bing Copilot và **Google Gemini AI** để phân tích, trích xuất cấu trúc dữ liệu cũng như tóm tắt nội dung, các sếp sẽ có ngay một hệ thống nghiên cứu thông tin tự động 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ việc gửi yêu cầu tìm kiếm đến Bing Copilot, chờ xử lý, tải snapshot dữ liệu cho đến khi tạo ra bản tóm tắt gọn gàng.
- **Trích xuất thông minh:** Sử dụng Google Gemini AI kết hợp Structured Output Parser để trả về dữ liệu chuẩn cấu trúc (JSON) sẵn sàng cho các bước xử lý tiếp theo.
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mất hàng giờ đọc và tổng hợp tài liệu, các sếp chỉ cần bấm nút và nhận kết quả tinh gọn trong tích tắc.
- **Tích hợp linh hoạt:** Dễ dàng bắn kết quả (webhook) về Slack, Telegram, Google Sheets hoặc CRM của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **Bright Data Account:** Tài khoản Bright Data để sử dụng Web Scraper API (cần có API Key/Token cấu hình cho `httpHeaderAuth`).
- **Google Gemini API Key:** Tài khoản Google AI Studio để lấy API Key kết nối với các node Google Gemini.
- **Webhook Endpoint (Tùy chọn):** URL nhận dữ liệu (ví dụ: webhook của Make, Zapier, Slack, hoặc server riêng) để hứng kết quả trích xuất và tóm tắt.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào menu 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:
- **Perform a Bing Copilot Request (`httpRequest`):** Cần điền thông tin xác thực (`httpHeaderAuth`) cho Bright Data API và cấu hình Endpoint, payload tìm kiếm phù hợp.
- **Check Snapshot Status & Download Snapshot (`httpRequest`):** Các node này dùng để kiểm tra trạng thái render của Bright Data và tải file snapshot về. Hãy đảm bảo header xác thực được thiết lập đúng.
- **Google Gemini Chat Model & Google Gemini Chat Model1 (`lmChatGoogleGemini`):** Cần kết nối credential (`googlePalmApi`) bằng Google Gemini API Key của các sếp. Model được khuyến nghị sử dụng là *Google Gemini Flash Exp*.
- **Structured Data Extractor (`chainLlm`) & Concise Summary Creator (`chainSummarization`):** Nơi cấu hình prompt hướng dẫn AI cách trích xuất dữ liệu theo dạng cấu trúc mong muốn và tóm tắt ngắn gọn.
- **Structured Data Webhook Notifier & Summary Webhook Notifier (`httpRequest`):** ⚠️ **CỰC KỲ QUAN TRỌNG:** Các sếp nhớ thay đổi `Webhook Notification URL` thành địa chỉ endpoint thực tế của mình để hệ thống bắn dữ liệu về đúng nơi.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** tại node `When clicking ‘Test workflow’` để chạy thử nghiệm và kiểm tra dữ liệu đầu ra ở từng node.
- Sau khi kiểm tra mọi thứ chạy xanh mướt (success), hãy bật công tắc **Active** ở góc trên bên phải để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Thay vì chỉ gửi qua Webhook, các sếp có thể nối thêm node **Google Sheets** hoặc **Notion** để tự động lưu lại toàn bộ các bản tóm tắt thành một kho tri thức (Knowledge Base) riêng.
- **Thông báo qua Chat:** Kết hợp thêm node **Telegram** hoặc **Slack** để nhận trực tiếp các bản tóm tắt cực gọn ngay trên điện thoại khi đang di chuyển.
- **Lập lịch chạy định kỳ:** Thay thế node `manualTrigger` bằng `Schedule Trigger` để tự động cào và tóm tắt các chủ đề hot mỗi ngày vào một khung giờ cố định.

### 📌 Kết luận
Workflow *Extract & Summarize Bing Copilot Search Results with Gemini AI and Bright Data* là một mẫu ví dụ tuyệt vời về sức mạnh kết hợp giữa Web Scraping hiện đại và Trí tuệ nhân tạo trong n8n. Hãy áp dụng ngay vào quy trình nghiên cứu thị trường hoặc tổng hợp tin tức của các sếp để tối ưu hóa năng suất làm việc gấp nhiều lần!