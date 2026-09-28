---
title: "🚀 Trích xuất dữ liệu website tự động với Form, Gemini AI và Gmail trong n8n"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu từ bất kỳ website nào dựa trên yêu cầu từ Form, sử dụng Google Gemini AI và gửi báo cáo qua Gmail."
slug: "trich-xuat-du-lieu-website-voi-gemini-ai-va-gmail"
tags: [n8n, automation, ai-summarization, multimodal-ai, google-gemini, web-scraping]
keywords: [n8n workflow, trích xuất dữ liệu website, web scraper form, gemini ai n8n, tự động hóa gmail]
---

# 🚀 Trích xuất dữ liệu website tự động với Form, Gemini AI và Gmail

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công truy cập vào các website, đọc qua hàng ngàn dòng code HTML hoặc văn bản để tìm kiếm và copy những thông tin cụ thể? Công việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót khi làm thủ công với số lượng lớn.

Đừng lo, workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên hoàn toàn tự động! Hệ thống kết hợp giữa **Web Form**, **Google Gemini AI thông minh**, và **Gmail** để cào dữ liệu, phân tích theo đúng yêu cầu và gửi kết quả về email ngay lập tức mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ việc nhận yêu cầu qua Form đến khi trả kết quả qua email.
- **AI thông minh:** Sử dụng Google Gemini để bóc tách chính xác thông tin theo đúng yêu cầu tùy chỉnh của người dùng từ cấu trúc HTML phức tạp.
- **Định dạng chuẩn JSON:** Kết quả được cấu trúc sạch sẽ, dễ dàng tích hợp tiếp vào các hệ thống khác.
- **Báo cáo tức thì:** Gửi toàn bộ kết quả phân tích chi tiết qua Gmail ngay khi hoàn thành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Tài khoản Google PaLM/Gemini API để kết nối với mô hình AI.
- **Gmail Account:** Tài khoản Gmail đã cấu hình OAuth2 trong n8n để gửi email kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor (hoặc import file JSON thông qua giao diện n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để workflow chạy mượt mà:

- **Web Scraper form submission (`formTrigger`):** Đây là điểm khởi đầu, cung cấp giao diện web form để người dùng nhập URL website cần cào và yêu cầu trích xuất dữ liệu.
- **Get HTML from source url (`httpRequest`):** Node này thực hiện gọi HTTP để lấy toàn bộ mã nguồn của URL mà người dùng đã nhập.
- **HTML Extractor (`html`):** Xử lý mã nguồn HTML thô và trích xuất phần `body` nội dung chính để chuẩn bị đưa vào AI.
- **Google Gemini Chat Model (`lmChatGoogleGemini`):** Kết nối với credentials **Google Gemini API Key** của các sếp.
- **Data Extractor LLM Chain (`chainLlm`) & Structured Output Parser (`outputParserStructured`):** 
  - Tùy chỉnh câu lệnh (Prompt) và JSON Schema tại đây nếu các sếp muốn thay đổi cấu trúc dữ liệu đầu ra (ví dụ: chỉ lấy giá sản phẩm, tiêu đề bài viết, hay thông tin liên hệ...).
- **Gmail - Send Result (`gmail`):** 
  - Chọn credentials **Gmail OAuth2**.
  - **Quan trọng:** Thay đổi địa chỉ email nhận kết quả (mặc định đang để `template_data_extactor_replace_me@yopmail.com`) thành email thực tế của các sếp.
  - Tùy chỉnh tiêu đề và nội dung email thông báo cho phù hợp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một request mẫu qua Web Form để kiểm tra dữ liệu trả về.
- Nếu mọi thứ hoạt động chính xác, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node Slack hoặc Telegram sau bước AI để bắn thông báo ngay lập tức về nhóm chat thay vì chỉ nhận qua email.
- **Lưu trữ vào Google Sheets:** Thêm một node Google Sheets để tự động lưu lại lịch sử các lần trích xuất dữ liệu nhằm phục vụ tra cứu sau này.
- **Xử lý URL hàng loạt:** Nâng cấp form hoặc kết hợp với Google Sheets Trigger để cào dữ liệu hàng loạt nhiều website cùng lúc thay vì từng URL đơn lẻ.

### 📌 Kết luận
Workflow trích xuất dữ liệu website kết hợp Form, Gemini AI và Gmail là một công cụ cực kỳ mạnh mẽ giúp tiết kiệm hàng đống thời gian nghiên cứu và thu thập dữ liệu thủ công. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tối ưu hóa hiệu suất làm việc ngay hôm nay!