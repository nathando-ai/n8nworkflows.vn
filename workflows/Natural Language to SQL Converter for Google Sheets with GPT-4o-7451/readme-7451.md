---
title: "🚀 Chuyển đổi ngôn ngữ tự nhiên thành SQL truy vấn Google Sheets với GPT-4o"
description: "Hướng dẫn cài đặt workflow n8n sử dụng AI Agent và GPT-4o để tra cứu, phân tích dữ liệu Google Sheets thông qua câu lệnh chat tự nhiên cực kỳ thông minh."
slug: "chuyen-doi-ngon-ngu-tu-nhien-thanh-sql-google-sheets-gpt-4o"
tags: [n8n, automation, no-code, openai, google-sheets, ai-agent]
keywords: [n8n workflow, natural language to sql, google sheets ai, gpt-4o n8n, tự động hóa google sheets, ai agent n8n]
keywords: [n8n workflow, tự động hóa, natural language to sql, google sheets ai, gpt-4o]
---

# 🚀 Chuyển đổi ngôn ngữ tự nhiên thành SQL truy vấn Google Sheets với GPT-4o

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mò mẫm lọc dữ liệu, viết hàm phức tạp hay tìm kiếm thông tin thủ công trong các bảng Google Sheets khổng lồ chưa? Việc tra cứu báo cáo bằng tay không chỉ tốn thời gian mà còn dễ xảy ra nhầm lẫn.

Được thiết kế bởi chuyên gia tự động hóa **Robert Breen**, workflow n8n này sẽ biến bảng tính của các sếp thành một cơ sở dữ liệu thông minh. Nhờ sức mạnh của **GPT-4o** và **AI Agent**, hệ thống cho phép người dùng trò chuyện trực tiếp bằng ngôn ngữ tự nhiên để truy vấn dữ liệu, phân tích và trích xuất thông tin từ Google Sheets một cách nhanh chóng, chính xác 100% mà không cần biết viết code hay hàm phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu bằng ngôn ngữ tự nhiên:** Chỉ cần chat (ví dụ: *"Tháng trước sản phẩm nào bán chạy nhất?"*), AI sẽ tự động phân tích và trả về kết quả.
- **Tự động hóa hoàn toàn:** Kết hợp AI Agent, GPT-4o và Google Sheets Tool giúp xử lý mượt mà các yêu cầu phức tạp.
- **Tiết kiệm thời gian:** Không còn mất hàng giờ lọc dữ liệu thủ công hay nhớ các hàm Excel/Google Sheets phức tạp.
- **Hoạt động liên tục 24/7:** Giao diện chat trực quan tích hợp sẵn sàng phục vụ đội ngũ bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **OpenAI** (có sẵn API Key và đã nạp credit để sử dụng mô hình GPT-4o).
- Tài khoản **Google Cloud / Google Sheets** để tạo OAuth2 Credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc sao chép toàn bộ mã JSON, sau đó dán trực tiếp vào n8n Editor của các sếp thông qua tính năng Import từ clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **OpenAI Chat Model1 (GPT-4o)** & **OpenAI Chat Model2 (GPT-4.1 Mini)**:
  - Tạo hoặc chọn **OpenAI API Credential**.
  - Dán OpenAI API Key của các sếp vào để cấp quyền cho mô hình AI xử lý ngôn ngữ và định dạng kết quả.
- **Get Column Info2 (Google Sheets Tool)**:
  - Tạo **Google Sheets OAuth2 API Credential** bằng cách cấu hình Client ID và Client Secret trên Google Cloud Console (đừng quên bật Google Sheets API).
  - Điền **Document ID** của bảng Google Sheets và tên Sheet chứa metadata cột (`Columns`) để AI hiểu được cấu trúc dữ liệu.
- **AI Agent3**:
  - Cập nhật System Prompt, thay thế URL trong tin nhắn hệ thống bằng Google Sheet URL của các sếp (đảm bảo quyền chia sẻ *"Anyone with the link can view"*).
  - Điều chỉnh GID (sheet ID) khớp với bảng dữ liệu thực tế.

#### 3. Kích hoạt ⚡️
- Sử dụng tính năng chat trực tiếp trên node **When chat message received** để test thử các câu hỏi mẫu.
- Sau khi kiểm tra dữ liệu trả về chính xác, gạt công tắc sang trạng thái **Active workflow** để đưa hệ thống vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc:** Kết hợp thêm node Telegram hoặc Slack để đội ngũ sales/marketing có thể tra cứu số liệu ngay trên nhóm chat công ty mà không cần mở n8n.
- **Lưu lịch sử truy vấn:** Thêm một bước ghi lại các câu hỏi và kết quả vào một Google Sheet khác để phân tích nhu cầu tìm kiếm dữ liệu của nhân sự.
- **Mở rộng nguồn dữ liệu:** Có thể nhân bản cấu trúc AI Agent này để kết nối với các nguồn cơ sở dữ liệu khác như Airtable, PostgreSQL hoặc MySQL.

### 📌 Kết luận
Workflow chuyển đổi ngôn ngữ tự nhiên thành SQL cho Google Sheets với GPT-4o là một giải pháp đột phá giúp tối ưu hóa việc khai thác dữ liệu doanh nghiệp bằng AI. Hãy thiết lập ngay hôm nay để đưa sức mạnh tự động hóa vào mô hình vận hành của các sếp!