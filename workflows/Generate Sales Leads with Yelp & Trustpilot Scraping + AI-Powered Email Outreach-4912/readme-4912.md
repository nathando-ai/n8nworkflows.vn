---
title: "🚀 Tự động quét Lead từ Yelp & Trustpilot kèm Email Outreach bằng AI"
description: "Khám phá workflow n8n giúp tự động tìm kiếm khách hàng tiềm năng chất lượng cao từ Yelp và Trustpilot, đánh giá qua AI và gửi email chăm sóc tự động hoàn toàn."
slug: "tu-dong-quet-lead-yelp-trustpilot-ai-email-outreach"
tags: [n8n, automation, no-code, sales, ai, yelp, trustpilot]
keywords: [n8n workflow, quét lead yelp trustpilot, ai email outreach, tự động hóa sales, n8n scraper]
---

# 🚀 Tự động quét Lead từ Yelp & Trustpilot kèm Email Outreach bằng AI

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) và gửi email tiếp cận thủ công thường ngốn rất nhiều thời gian của đội ngũ sales. Các sếp thường phải mất hàng giờ lướt Yelp, tổng hợp thông tin, tìm website, kiểm tra độ uy tín và soạn từng chiếc email cá nhân hóa.

Workflow này sinh ra để giải quyết triệt để nỗi đau đó! Với sự kết hợp giữa **n8n**, **AI (Gemini & Claude)** và các công cụ scraping, hệ thống sẽ tự động hóa toàn bộ quy trình: từ việc phân tích vị trí, quét dữ liệu doanh nghiệp trên Yelp, lọc qua Trustpilot cho đến việc viết nội dung email siêu cá nhân hóa và gửi đi tự động qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% từ A-Z**: Không còn cảnh copy-paste thủ công từ Yelp hay Trustpilot vào Excel.
- **AI thông minh**: Sử dụng Gemini để phân tích khu vực/ngành nghề và Claude Sonnet để viết nội dung email outreach cực kỳ tự nhiên, tỷ lệ phản hồi cao.
- **Quản lý dữ liệu tập trung**: Toàn bộ thông tin doanh nghiệp, website và email được lưu trữ ngăn nắp trên Google Sheets.
- **Hoạt động liên tục**: Kích hoạt bằng Form Trigger đơn giản, chạy ngầm mượt mà và gửi email trực tiếp qua Gmail cá nhân/doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Google Sheets (Cần copy [Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1hX0MD_BLVWuEaXwOjKtwrWsjsBzc32ZtFVjP7wVGQYI/edit?usp=drive_link)).
- API Key của Google Gemini (`googlePalmApi`).
- API Key của Anthropic Claude (`anthropicApi`).
- Tài khoản Gmail đã kết nối OAuth2 (`gmailOAuth2`).
- Dịch vụ Scraper tích hợp (được gọi qua HTTP Request nodes như BrightData hoặc tương đương).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow này, vào giao diện n8n chọn **New Workflow**, nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ 30 nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Form Trigger - Get User Input**: Nơi nhập yêu cầu tìm kiếm đầu vào (vị trí, ngành nghề). Các sếp có thể mở form này để test trực tiếp.
- **Gemini - Location AI Model** & **AI Location Analyzer**: Kết nối credential của Google Gemini để AI bóc tách khu vực tìm kiếm thành các tiểu khu vực tối ưu.
- **Claude - Email AI Model** & **AI Generate Email Content**: Chọn model `Claude 4 Sonnet` và cấu hình API key của Anthropic để hệ thống viết email outreach dựa trên dữ liệu thu thập được.
- **Google Sheets Nodes** (`Save Yelp Data to Sheet`, `Read Yelp Sheet Websites`, `Save Trustpilot Data to Sheet`, `Read Emails from Trustpilot Sheet`): 
  - Yêu cầu kết nối tài khoản Google Sheets OAuth2.
  - Trỏ đúng đến file Google Sheet mà các sếp đã sao chép từ [link mẫu này](https://docs.google.com/spreadsheets/d/1hX0MD_BLVWuEaXwOjKtwrWsjsBzc32ZtFVjP7wVGQYI/edit?usp=drive_link).
- **Send Outreach Email**: Cấu hình tài khoản Gmail (`gmailOAuth2`) để workflow có quyền gửi email tự động tới danh sách lead đã lọc.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một từ khóa nhỏ trên Form Trigger để kiểm tra quá trình gọi API Yelp, Trustpilot và AI phản hồi.
- Sau khi thấy dữ liệu đổ về Google Sheets và email nháp/gửi đi chính xác, hãy bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động hóa hoàn toàn.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo**: Gắn thêm node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi AI gửi xong loạt email outreach trong ngày.
- **Quản lý trạng thái Lead**: Thêm cột "Status" trong Google Sheets để đánh dấu những lead đã được gửi email, tránh việc gửi trùng lặp nếu chạy lại workflow.
- **Tùy chỉnh Prompt cho AI**: Tinh chỉnh prompt trong node AI Generate Email Content để cá nhân hóa sâu hơn theo sản phẩm/dịch vụ riêng của công ty các sếp.

### 📌 Kết luận
Workflow quét lead kết hợp AI Email Outreach này là thứ vũ khí hạng nặng giúp đội ngũ sales tối ưu hóa năng suất, khai thác triệt để nguồn dữ liệu khổng lồ từ Yelp và Trustpilot mà không tốn nhiều sức lao động thủ công. Hãy triển khai ngay hôm nay trên hệ thống n8n của các sếp nhé!