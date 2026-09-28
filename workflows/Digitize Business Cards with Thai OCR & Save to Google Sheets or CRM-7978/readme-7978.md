---
title: "🚀 Số hóa danh thiếp thông minh với Thai OCR & AI, tự động lưu Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n sử dụng Typhoon OCR và LLM để quét danh thiếp tiếng Thái/Anh, làm giàu thông tin và tự động đồng bộ vào Google Sheets."
slug: "so-hoa-danh-thiep-thai-ocr-google-sheets-n8n"
tags: [n8n, automation, ai-ocr, google-sheets, typhoon-ai, business-cards]
keywords: [n8n workflow, số hóa danh thiếp, thai ocr, typhoon ai, google sheets automation]
---

# 🚀 Số hóa danh thiếp thông minh với Thai OCR & AI, tự động lưu Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi đi hội thảo, sự kiện về và ôm một cục danh thiếp (name card) giấy, sau đó phải cặm cụi gõ tay từng thông tin vào file Excel hoặc CRM không? Việc này không chỉ tốn thời gian, dễ sai sót mà còn làm giảm tốc độ tiếp cận khách hàng tiềm năng (lead).

Giải pháp hoàn hảo cho các sếp đây! Workflow n8n này sẽ tự động hóa 100% quy trình: **Nhận ảnh danh thiếp -> Đọc chữ (OCR kể cả tiếng Thái/Anh) nhờ Typhoon AI -> Phân tích cấu trúc dữ liệu -> Làm giàu thông tin -> Lưu thẳng vào Google Sheets và gửi email chào hỏi tự động**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần nhập liệu thủ công, chỉ cần upload ảnh danh thiếp lên form.
- **Hỗ trợ đa ngôn ngữ (Đặc biệt tiếng Thái & Anh):** Khai thác tối đa công nghệ OCR tiên tiến từ Typhoon AI.
- **Làm giàu thông tin thông minh:** Tự động phân loại cấp bậc, ngành nghề hoặc tìm kiếm thông tin bổ sung qua SerpAPI.
- **Tự động hóa chăm sóc khách hàng:** Tùy chọn gửi email chào hỏi (Greeting Email) ngay lập tức sau khi quét danh thiếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Typhoon AI / OpenAI API Key:** Tài khoản API từ Typhoon (xem tài liệu cấu hình tại [opentyphoon.ai](https://opentyphoon.ai/blog/en/n8n-typhoon-integration-guide)).
- **Google Sheets Account:** Tài khoản Google để lưu trữ thông tin danh bạ.
- **SerpAPI (Tùy chọn):** Nếu sử dụng phiên bản có tích hợp Search API để làm giàu thông tin profile.
- **Gmail Account (Tùy chọn):** Nếu muốn kích hoạt bước gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON tương ứng, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này cung cấp 2 phiên bản (Có hoặc không có Search API). Các sếp cần chú ý cấu hình các node quan trọng sau:
- **On form submission / On form submission1 (Form Trigger):** Nơi người dùng tải ảnh danh thiếp lên. Đảm bảo cấu hình Form đúng giao diện các sếp mong muốn.
- **Edit Image / Edit Image1:** Xử lý sơ bộ thông tin ảnh trước khi đẩy vào OCR.
- **Typhoon OCR / Typhoon OCR1 (lmChatOpenAi):** Chọn đúng model `typhoon-ocr-preview` hoặc `typhoon-ocr-preview-techsauce-workshop` và điền credentials OpenAI/Typhoon API Key.
- **Contact Info Parser / Enricher (ChainLLM):** Sử dụng các model như `typhoon-v2.1-12b-instruct` để chuyển văn bản thô thành JSON chuẩn hóa. Các sếp có thể tùy chỉnh Prompt trong các node này để trích xuất đúng trường dữ liệu theo nhu cầu kinh doanh.
- **Add Contact to Google Sheet / Google Sheet1:** Kết nối tài khoản Google Sheets OAuth2, chọn file Google Sheet đích và mapping các trường dữ liệu JSON vào các cột tương ứng.
- **Send a message (Gmail):** Nếu muốn dùng tính năng gửi email, kết nối credentials Gmail và nối node `Text to JSON` với node Gmail. Nếu không dùng, có thể ngắt kết nối phần này.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách upload một vài ảnh danh thiếp mẫu lên form.
- Kiểm tra xem dữ liệu đã được đẩy chuẩn xác vào Google Sheets chưa.
- Nếu mọi thứ mượt mà, bật công tắc **Active** để chính thức đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì dùng Form Trigger, các sếp có thể kết nối workflow này với **Telegram Bot** hoặc **Zalo OA**, cho phép nhân viên sales chụp ảnh danh thiếp gửi thẳng vào chat là hệ thống tự xử lý.
- **Bổ trợ CRM chuyên sâu:** Thay vì lưu Google Sheets, các sếp có thể thay thế node Google Sheets bằng **HubSpot**, **Notion**, hoặc **Pipedrive** node để quản lý khách hàng chuyên nghiệp hơn.
- **Lưu log lỗi:** Thêm nhánh Error Trigger để thông báo về Telegram/Slack nếu ảnh danh thiếp quá mờ hoặc AI không đọc được dữ liệu.

### 📌 Kết luận
Số hóa danh thiếp chưa bao giờ dễ dàng và thông minh đến thế nhờ sự kết hợp giữa n8n và Typhoon AI. Hãy "lên đồ" ngay workflow này để tối ưu hóa đội ngũ sales và tăng tốc độ tiếp cận khách hàng của doanh nghiệp các sếp nhé!