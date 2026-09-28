---
title: "🚀 Trích xuất dữ liệu có cấu trúc từ Brave Search với Bright Data MCP và Google Gemini"
description: "Tự động hóa quy trình tìm kiếm thông tin trên Brave Search thông qua Bright Data MCP Client và trích xuất dữ liệu chuẩn hóa bằng Google Gemini AI trên n8n."
slug: "trich-xuat-du-lieu-brave-search-bright-data-mcp-google-gemini"
tags: [n8n, automation, no-code, AI, Google Gemini, Bright Data MCP, Web Scraping]
keywords: [n8n workflow, trích xuất dữ liệu, Brave Search, Bright Data MCP, Google Gemini, AI automation, structured data]
---

# 🚀 Trích xuất dữ liệu có cấu trúc từ Brave Search với Bright Data MCP và Google Gemini

Trong thời đại số, việc thu thập thông tin và dữ liệu thị trường thủ công từ các công cụ tìm kiếm chiếm rất nhiều thời gian của các nhà làm marketing và nghiên cứu. Việc copy-paste dữ liệu thô rồi phân tích bằng tay vừa chậm chạp lại dễ sai sót. 

Bài viết này sẽ hướng dẫn các sếp cách thiết lập và sử dụng một workflow n8n cực mạnh mẽ, kết hợp giữa **Bright Data MCP Client**, **Brave Search**, và sức mạnh AI thông minh từ **Google Gemini** để tự động tìm kiếm, trích xuất và lưu trữ dữ liệu có cấu trúc một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted). *Lưu ý: Workflow này bắt buộc chạy trên môi trường Self-hosted vì sử dụng Community Node cho MCP Client.*
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Tìm kiếm và lọc dữ liệu (Hình ảnh, Video, Tin tức hoặc Tìm kiếm tổng hợp) theo từ khóa tùy chỉnh.
- **Trích xuất thông minh:** Sử dụng Google Gemini kết hợp Structured Output Parser để bóc tách dữ liệu theo đúng định dạng JSON chuẩn.
- **Lưu trữ linh hoạt:** Tự động đồng bộ dữ liệu vào Google Sheets, ghi file trực tiếp xuống ổ cứng hoặc bắn webhook sang hệ thống khác.
- **Tiết kiệm 90% thời gian:** Không còn cảnh tra cứu thủ công hàng chục tab trình duyệt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted instance** (đã cài đặt community node cho MCP Client).
- **Google Gemini API Key** (thông qua `Google Gemini Chat Model`).
- **Bright Data MCP Client API Credentials** (để kết nối với công cụ tìm kiếm Brave Search qua Bright Data).
- **Google Sheets account** (nếu muốn lưu dữ liệu vào bảng tính).
- **Webhook endpoint** (tùy chọn, nếu muốn đẩy dữ liệu sang CRM/Slack/Telegram).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON tải từ trang template n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình kỹ các node sau:
- **Set the search criteria's**: Thiết lập từ khóa tìm kiếm và chọn loại tìm kiếm phù hợp (`videos`, `images`, `news`, hoặc `all`) thông qua node `Switch`.
- **Bright Data MCP Client (Image/Video/News/All Search)**: Cấu hình credentials cho MCP Client API của Bright Data để gọi công cụ Brave Search tương ứng với nhu cầu.
- **Google Gemini Chat Model & Structured Output Parser**: Kết nối tài khoản Google Palm/Gemini API và cấu hình schema đầu ra để AI hiểu cách bóc tách dữ liệu.
- **Google Sheets**: Chọn file Google Sheets và cấu hình Sheet Name, ánh xạ các trường dữ liệu muốn lưu với operation `appendOrUpdate`.
- **Write the structured content to disk**: Đảm bảo đường dẫn thư mục trên ổ cứng của server n8n có quyền ghi file (`readWriteFile`).
- **Initiate a Webhook Notification for the Structured Data**: Thay thế URL webhook mặc định bằng Endpoint nhận dữ liệu của hệ thống các sếp (nếu có nhu cầu bắn thông báo).

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với từ khóa mẫu, kiểm tra kỹ dữ liệu trả về ở Google Sheets và file log.
- Sau khi kiểm tra mọi thứ hoạt động ổn định, gạt công tắc sang **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm node Telegram ngay sau bước trích xuất thành công để bắn tin nhắn tóm tắt kết quả tìm kiếm ngay vào điện thoại.
- **Lưu lịch sử tìm kiếm:** Kết hợp thêm node Date & Time để gắn mốc thời gian (Timestamp) cho mỗi lần tra cứu dữ liệu.
- **Chạy định kỳ:** Thay thế node `When clicking ‘Test workflow’` bằng node `Schedule Trigger` để hệ thống tự động quét thông tin thị trường mỗi ngày một lần.

### 📌 Kết luận
Workflow tích hợp Bright Data MCP và Google Gemini này là một vũ khí cực kỳ lợi hại cho các nhà nghiên cứu, marketer và các nhà phát triển muốn tự động hóa việc thu thập tin tức, hình ảnh hoặc dữ liệu từ web. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!