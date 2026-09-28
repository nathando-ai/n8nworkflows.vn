---
title: "🚀 Tự động ghi hóa đơn từ Telegram vào Google Sheets và tra cứu chi phí thông minh với Gemini AI & MCP"
description: "Hướng dẫn xây dựng hệ thống quản lý tài chính cá nhân tự động 100%: Chụp ảnh hóa đơn gửi Telegram, Gemini AI tự bóc tách dữ liệu vào Google Sheets và tích hợp MCP Server để chat hỏi tiền bạc với Claude/ChatGPT."
slug: "quan-ly-tai-chinh-ca-nhan-telegram-google-sheets-gemini-mcp"
tags: [n8n, automation, telegram, google-sheets, google-gemini, mcp, ai-agents]
keywords: [n8n workflow, tự động hóa tài chính, đọc hóa đơn telegram gemini, mcp server n8n, quản lý chi tiêu AI]
---

# 🚀 Tự động ghi hóa đơn từ Telegram vào Google Sheets và tra cứu chi phí thông minh với Gemini AI & MCP

Các sếp có cảm thấy mệt mỏi mỗi khi cuối tháng ngồi tổng hợp lại hóa đơn, nhẩm tính xem tiền đã bay đi đâu mất không? Việc ghi chép thủ công vừa tẻ nhạt, dễ bỏ sót lại mất rất nhiều thời gian. 

Workflow n8n tuyệt vời này sẽ giải quyết triệt để vấn đề đó bằng cách kết hợp sức mạnh của **Telegram Bot**, **Google Gemini Vision AI**, **Google Sheets** và giao thức **MCP (Model Context Protocol)**. Các sếp chỉ cần chụp ảnh hóa đơn vứt vào Telegram, phần còn lại hệ thống tự lo. Thậm chí, các sếp còn có thể hỏi Claude hoặc ChatGPT bằng ngôn ngữ tự nhiên kiểu: *"Tháng trước tôi tiêu bao nhiêu tiền ăn uống?"* và nhận kết quả ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% việc nhập liệu:** Không cần gõ phím, chỉ cần chụp ảnh hóa đơn gửi Telegram là xong.
- **AI thông minh bóc tách dữ liệu:** Gemini tự nhận diện số tiền, ngày tháng, nhà cung cấp, danh mục chi tiêu (`Groceries`, `Dining`, `Transport`, `Utilities`, `Shopping`, `Health`, `Entertainment`, `Travel`, `Other`).
- **Tra cứu bằng ngôn ngữ tự nhiên:** Tích hợp MCP Server để hỏi trực tiếp Claude Desktop hoặc ChatGPT về tình hình tài chính cá nhân.
- **Hoàn toàn miễn phí (Free Stack):** Tận dụng các gói miễn phí của Telegram, Google Sheets và Gemini Flash.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Google Gemini API Key** (dùng Google AI Studio).
- **Google Sheets** tài khoản để lưu trữ dữ liệu chi tiêu.
- (Tùy chọn) **Claude Desktop** hoặc **ChatGPT/Cursor** nếu muốn sử dụng tính năng tra cứu MCP.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Query Spending` & `Receive Query Parameters`:** Sau khi import, hãy mở node `Query Spending` (thuộc loại `toolWorkflow`) và **re-link (liên kết lại)** nó với bản sao sub-workflow *Personal Finance Query Spending (MCP Tool)* trên không gian làm việc của các sếp. ID mặc định đang trỏ về máy của tác giả gốc nên sẽ không chạy nếu không đổi!
- **Node `Read Expenses` & `Append to Expense Sheet` (Google Sheets):** Tạo sẵn một Google Sheet với các tiêu đề cột ở dòng 1: `Date`, `Amount`, `Currency`, `Vendor`, `Category`, `Note`, `LoggedAt`. Trỏ cả hai node này vào **cùng một Google Sheet** đó.
- **Node `Extract Receipt Data with Gemini`:** Điền Google Gemini API Credentials. *(Lưu ý bảo mật: Trên gói miễn phí của Gemini, Google có thể dùng ảnh của các sếp để cải thiện mô hình. Hãy dùng tài khoản trả phí nếu hóa đơn của các sếp có chứa thông tin cực kỳ nhạy cảm).*
- **Node `Download Photo` & `Receive Receipt Photo` (Telegram):** Thêm Telegram Bot Token vào credentials chung cho các node Telegram.
- **Node `MCP Server: Personal Finance`:** 
  - Mặc định server này để chế độ **No Authentication** để dễ test. Trước khi đưa vào production thực tế, hãy chuyển mục **Authentication** sang **Bearer Auth** và cấu hình token bảo mật.
  - Sau khi bật workflow, lấy **Production URL** để cấu hình vào file `claude_desktop_config.json` nếu muốn kết nối với Claude Desktop.

#### 3. Kích hoạt ⚡️
- Gửi thử một bức ảnh chụp hóa đơn bất kỳ vào Telegram Bot của các sếp để kiểm tra xem dữ liệu đã được đẩy chuẩn vào Google Sheets chưa.
- Bật (Active) workflow chính (**MCP Server / Telegram Ingestion**) lên. Sub-workflow *Query Spending* chỉ chạy theo yêu cầu khi MCP gọi tới nên **không cần bật active** sub-workflow đó.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng ghi hóa đơn để nhận thông báo tổng kết ngay lập tức sau khi lưu thành công.
- **Tích hợp cơ sở dữ liệu lớn:** Nếu lượng hóa đơn quá lớn, các sếp có thể thay thế Google Sheets bằng Supabase hoặc PostgreSQL để truy vấn nhanh hơn.
- **Cải thiện độ chính xác OCR:** Với những hóa đơn nhàu nát, có thể tích hợp thêm dịch vụ OCR phụ trợ trước khi đẩy qua Gemini.

### 📌 Kết luận
Hệ thống quản lý tài chính cá nhân kết hợp AI và MCP này sẽ giúp các sếp giải phóng hoàn toàn sức lao động khỏi việc nhập liệu thủ công. Hãy "lên đồ" ngay hôm nay để làm chủ tài chính một cách thông minh nhất!