---
title: "🚀 Tự động tạo trợ lý giọng nói AI cho doanh nghiệp địa phương với Claude, VAPI và Google Maps qua n8n"
description: "Hướng dẫn xây dựng hệ thống tự động quét Google Maps, phân tích website, tạo kịch bản thông minh bằng Claude và triển khai trợ lý giọng nói VAPI tự động 100%."
slug: "tao-tro-ly-giong-noi-ai-cho-doanh-nghiep-dia-phuong-vapi-claude-n8n"
tags: [n8n, automation, vapi, claude, apify, ai-voice-agent, google-maps]
keywords: [n8n workflow, trợ lý giọng nói ai, vapi ai, apify google maps scraper, claude ai automation, tự động hóa n8n]
---

# 🚀 Tự động tạo trợ lý giọng nói AI cho doanh nghiệp địa phương với Claude, VAPI và Google Maps

Các sếp đang làm dịch vụ marketing, agency hay tư vấn giải pháp AI chắc hẳn đều đau đầu khi muốn tiếp cận các doanh nghiệp địa phương (local businesses) bằng các giải pháp tổng đài thông minh (Voice AI). Việc thủ công tìm kiếm khách hàng, nghiên cứu website từng nơi, viết kịch bản hội thoại rồi cấu hình lên hệ thống tổng đài tốn rất nhiều thời gian và công sức.

Với workflow n8n cực kỳ mạnh mẽ này, mọi thứ sẽ được tự động hóa hoàn toàn! Chỉ cần nhập thông tin khu vực và ngành nghề qua một form đơn giản, hệ thống sẽ tự động quét Google Maps, phân tích website, dùng sức mạnh của Claude để viết kịch bản hội thoại cá nhân hóa, tự động tạo trợ lý giọng nói trên VAPI và lưu lại toàn bộ thông tin vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình**: Từ khâu tìm kiếm khách hàng tiềm năng trên Google Maps đến khi tạo xong trợ lý AI trên VAPI.
- **Cá nhân hóa sâu sắc**: Claude và OpenRouter sẽ phân tích trực tiếp website của từng doanh nghiệp để tạo system prompt, lời chào (greeting) và tin nhắn thoại (voicemail) phù hợp tuyệt đối với dịch vụ của họ.
- **Tiết kiệm thời gian tối đa**: Thay vì mất hàng giờ cấu hình thủ công cho từng khách hàng, hệ thống xử lý hàng loạt trong vài phút.
- **Quản lý tập trung**: Mọi thông tin trợ lý giọng nói vừa tạo được tự động lưu trữ gọn gàng trong Google Sheets để tiện theo dõi, chăm sóc khách hàng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Apify Account & API Key** (Dùng cho actor Google Maps Scraper).
- **Anthropic API Key** (Dùng cho node Claude tạo kịch bản agent).
- **OpenRouter API Key** (Dùng cho mô hình ngôn ngữ phân tích website).
- **VAPI Account & API Key** (Nền tảng tạo trợ lý giọng nói AI).
- **Google Sheets Account** (Cấp quyền OAuth2 để lưu log).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn dấu ba chấm ở góc trên bên phải chọn **Import from File** hoặc dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Form Trigger - Business Location Input**: Nơi người dùng nhập từ khóa ngành nghề, thành phố, quốc gia. Các sếp nhớ cấu hình `countryCode`, `language` và `locationQuery` cho phù hợp với quốc gia muốn quét dữ liệu (ví dụ: `"vn"`, `"vi"`, `"Hanoi, Vietnam"`).
- **Scrape Local Businesses**: Kết nối với tài khoản **Apify** để chạy tác vụ quét dữ liệu doanh nghiệp từ Google Maps.
- **Extract Website Text / Clean & Grok-4-fast**: Kết nối **OpenRouter** để trích xuất và làm sạch nội dung từ website doanh nghiệp.
- **Generate Agent Messages**: Kết nối **Anthropic** (Claude) để tạo lời thoại thông minh cho agent dựa trên dữ liệu thu thập được.
- **Create Vapi Assistant**: Node **HTTP Request** bắt buộc phải cấu hình **Authorization Header** chứa VAPI API Key của các sếp để hệ thống tự động tạo voice assistant trên nền tảng VAPI.
- **Log Agent to Sheet & Sync to Google Sheet**: Kết nối tài khoản **Google Sheets OAuth2**, chọn file Sheet chuẩn bị sẵn để lưu trữ thông tin các agent vừa tạo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử bằng cách điền thông tin vào form thu thập dữ liệu.
- Sau khi kiểm tra dữ liệu chạy trơn tru qua các node, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Telegram/Slack**: Thêm node Telegram ngay sau bước tạo Vapi Assistant thành công để nhận thông báo tức thì về điện thoại mỗi khi có trợ lý giọng nói mới được tạo.
- **Gửi email tự động cho khách hàng**: Kết nối thêm Gmail node để tự động gửi thông tin demo trợ lý giọng nói vừa tạo cho chủ doanh nghiệp đó nhằm chốt sales.
- **Mở rộng giới hạn (Limit)**: Trong workflow có node `Limit to 1st result for preview`, các sếp có thể bỏ node này khi đã test xong để hệ thống quét toàn bộ danh sách hàng loạt.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp các agency tự động hóa toàn bộ phễu từ tìm kiếm khách hàng đến tạo sản phẩm demo Voice AI. Hãy cài đặt ngay hôm nay để bứt phá hiệu suất kinh doanh cùng n8n và AI các sếp nhé!