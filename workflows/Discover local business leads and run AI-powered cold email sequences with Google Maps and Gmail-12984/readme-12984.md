---
title: "🚀 Tự động quét khách hàng tiềm năng Google Maps và chạy chiến dịch Cold Email bằng AI"
description: "Hướng dẫn xây dựng hệ thống tìm kiếm khách hàng địa phương tự động từ Google Maps, cào email website, viết nội dung bằng AI Gemini và gửi chuỗi 3 email chăm sóc tự động hoàn toàn."
slug: "tu-dong-quet-lead-google-maps-cold-email-ai"
tags: [n8n, automation, no-code, lead-generation, google-maps, ai-email, gmail]
keywords: [n8n workflow, quét lead google maps, cold email ai, google sheets automation, tự động hóa marketing, gemini ai n8n]
---

# 🚀 Tự động hóa toàn diện: Quét Lead Google Maps & Chạy Chuỗi Cold Email AI

Các sếp có đang tốn hàng giờ mỗi tuần để thủ công tìm kiếm khách hàng địa phương trên Google Maps, copy số điện thoại, mò mẫm website tìm email và soạn từng bức thư chào hàng? Quá trình này không chỉ cực kỳ tẻ nhạt, mất thời gian mà còn dễ bỏ sót những cơ hội kinh doanh vàng.

Workflow n8n "khủng" với 62 nodes này sẽ giải quyết triệt để nỗi đau đó! Hệ thống tự động hóa 100% không cần code này sẽ thay thế hoàn toàn đội ngũ sales thủ công: từ việc quét danh sách doanh nghiệp theo mã ZIP, cào email từ website, sử dụng AI (Google Gemini) để viết email cá nhân hóa siêu đỉnh, cho đến việc tự động gửi chuỗi email chăm sóc (Intro + 2 Follow-ups) qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động tìm kiếm nguồn Lead chất lượng**: Khai thác dữ liệu doanh nghiệp chính xác từ Google Maps dựa trên mã ZIP và ngành nghề mục tiêu.
- **Cá nhân hóa nội dung bằng AI**: Sử dụng sức mạnh của Google Gemini để tạo ra các email chào hàng (intro và follow-up) cực kỳ tự nhiên, trúng "nỗi đau" của từng khách hàng.
- **Chuỗi chăm sóc tự động 3 bước**: Gửi email giới thiệu ban đầu, sau đó tự động phản hồi (reply) chuỗi 2 email follow-up theo đúng lịch trình (ngày 7 và ngày 11) mà không cần can thiệp thủ công.
- **Hoạt động bền bỉ, an toàn**: Tích hợp sẵn cơ chế xử lý lỗi (Retry logic), quản lý giới hạn tốc độ (Rate-limit handling) và theo dõi trạng thái chi tiết qua Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets**: Tài khoản Google để quản lý dữ liệu danh sách mã ZIP, ngành nghề và kết quả quét (Sử dụng [mẫu Google Sheets có sẵn](https://docs.google.com/spreadsheets/d/1BRPF4IHoxtAIE5gBQMNP_qIux_XNDXTnmIEHYcl5kEk/edit?usp=sharing)).
- **Google Maps API Key**: Khóa API để truy xuất dữ liệu địa điểm từ Google.
- **Google Gemini (Vertex AI / Google Palm API)**: Credentials để node AI Writer tạo nội dung email.
- **Gmail Account (OAuth2)**: Tài khoản Gmail để gửi chuỗi email outreach.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một workflow nâng cao với 62 nodes, các sếp cần chú ý cấu hình kỹ các thành phần cốt lõi sau:
- **Google Sheets Nodes (`Get Zip Codes`, `Get Category`, `Add rows in Google Sheets`, v.v.)**: Kết nối tài khoản `Google Sheets OAuth2 API` và trỏ đúng đến file Google Sheet quản lý lead của các sếp.
- **GMaps API (`GMaps API`)**: Điền Google Maps API Key vào header hoặc tham số của HTTP Request node để cho phép quét vị trí.
- **AI Email Writer (`Email Writer`)**: Kết nối tài khoản Google Gemini / Palm API. Các sếp có thể tinh chỉnh Prompt bên trong node này để nội dung email phù hợp với văn phong sản phẩm/dịch vụ của công ty mình.
- **Gmail Nodes (`Send Intro Mail`, `Follow Up Mail 1`, `Follow Up Mail 2`)**: Kết nối tài khoản Gmail cá nhân hoặc Workspace qua `Gmail OAuth2` để hệ thống tự động gửi và reply thư.
- **Schedule Triggers**: Kiểm tra lại các lịch chạy tự động (`Trigger: Generate AI Emails`, `Trigger: Send Follow Up 1`, v.v.) để đảm bảo thời gian chạy khớp với múi giờ mong muốn (mặc định các follow-up chạy lúc 8 giờ sáng hàng ngày).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) từng phần (Lead Discovery trước, sau đó đến AI Generation và Email Sending) để kiểm tra luồng dữ liệu.
- Sau khi mọi thứ mượt mà, bật công tắc **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Telegram/Slack**: Thêm một node Telegram hoặc Slack ở bước sau khi gửi email thành công để team sales nhận được thông báo ngay lập tức khi có lead phản hồi.
- **Lọc trùng lớp Lead**: Tối ưu hóa các node Filter để tránh quét trùng lặp các doanh nghiệp đã có trong cơ sở dữ liệu cũ.
- **A/B Testing nội dung AI**: Tách nhánh Prompt trong node AI Writer để thử nghiệm các tiêu đề email khác nhau, từ đó tìm ra tỷ lệ mở (Open rate) cao nhất.

### 📌 Kết luận
Workflow quét lead và chạy cold email tự động này chính là "vũ khí bí mật" giúp tối ưu hóa phễu sales, tiết kiệm hàng chục giờ làm việc tay chân mỗi tuần. Hãy thiết lập ngay hôm nay để dòng khách hàng tiềm năng liên tục đổ về doanh nghiệp của các sếp một cách hoàn toàn tự động!