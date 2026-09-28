---
title: "🚀 Tự động hóa tìm kiếm Lead LinkedIn & Viết thư cá nhân hóa bằng Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm khách hàng tiềm năng trên LinkedIn và soạn nội dung outreach siêu cá nhân hóa bằng Google Gemini AI."
slug: "linkedin-lead-finder-gemini-personalized-outreach"
tags: [n8n, automation, ai, lead-generation, google-gemini, google-sheets, linkedin]
keywords: [n8n workflow, tìm kiếm lead linkedin, google gemini ai, outreach tự động, n8n việt nam, tự động hóa marketing]
---

# 🚀 Tự động hóa tìm kiếm Lead LinkedIn & Viết thư cá nhân hóa bằng Gemini AI

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) và viết thông điệp tiếp cận (outreach message) thủ công trên LinkedIn thường ngốn rất nhiều thời gian và công sức của đội ngũ Sales. Việc này không chỉ nhàm chán mà còn khó duy trì sự cá nhân hóa ở quy mô lớn. 

Được thiết kế bởi chuyên gia **Cong Nguyen**, workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Nhận yêu cầu từ Form -> Dùng AI tạo từ khóa Boolean -> Quét thông tin LinkedIn -> Lưu trữ Google Sheets -> AI viết thư tiếp cận riêng biệt -> Gửi email thông báo. Tất cả diễn ra hoàn toàn tự động mà không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì ngồi tra cứu từng profile và nghĩ cách viết thư, hệ thống tự động xử lý hàng loạt.
- **Cá nhân hóa đỉnh cao:** Sử dụng Google Gemini AI để phân tích thông tin công ty/cá nhân và soạn thảo nội dung outreach cực kỳ trúng trọng tâm.
- **Quản lý tập trung:** Mọi dữ liệu lead và nội dung tin nhắn đều được lưu trữ gọn gàng trên Google Sheets.
- **Hoạt động liên tục:** Vận hành trơn tru, gửi email thông báo ngay khi quy trình hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Dùng cho các node AI tạo từ khóa và viết tin nhắn.
- **Google Sheets Account:** Chuẩn bị sẵn một Google Sheet để lưu thông tin lead.
- **Google Custom Search API & CX:** Để tìm kiếm profile/công ty trên LinkedIn thông qua HTTP Request.
- **SMTP Credentials:** Tài khoản gửi email (Gmail SMTP, SendGrid, Resend...) để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, sau đó dán trực tiếp vào n8n Editor của mình hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **Form submit (`formTrigger`):** Thiết lập form đầu vào để thu thập từ khóa mục tiêu và mục đích tìm kiếm lead từ người dùng.
- **Create boolean search strings (`googleGemini`):** Kết nối với `Google Palm/Gemini API` để AI tự động tạo chuỗi tìm kiếm Boolean tối ưu dựa trên input của Form.
- **Get Linkedin Company (`httpRequest`):** Cấu hình Google Custom Search Engine ID (`cx`) và API Key. Đồng thời, nhớ tinh chỉnh các tham số `hl` (ngôn ngữ) và `gl` (quốc gia) cho phù hợp với khu vực mục tiêu của các sếp.
- **Writing message (`googleGemini`):** Cấu hình lại Gemini API để AI tiến hành phân tích thông tin mô tả (`des`) và viết nội dung outreach hấp dẫn.
- **Append row in sheet & Update sheet (`googleSheets`):** Kết nối tài khoản Google Sheets OAuth2, chọn đúng file Google Sheet và mapping các trường dữ liệu theo đúng chuẩn:
  - `name` → Tên Công ty/Cá nhân
  - `linkedin_url` → Đường dẫn LinkedIn profile/company
  - `des` → Mô tả hoặc tagline
  - `message` → Nội dung outreach do AI tạo ra
- **Send email (`emailSend`):** Điền thông tin SMTP của các sếp để nhận email thông báo khi lead đã được xử lý và lưu xong.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền thông tin vào form để kiểm tra toàn bộ luồng dữ liệu.
- Nếu dữ liệu đổ về Google Sheets chuẩn chỉnh và email thông báo hoạt động, hãy bật công tắc **Active** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay trên điện thoại thay vì chỉ nhận qua email.
- **Mở rộng lưu trữ:** Thay vì Google Sheets, các sếp có thể đồng bộ lead trực tiếp vào CRM như HubSpot, Notion hoặc Airtable.
- **Tự động gửi tin nhắn:** Kết hợp thêm các công cụ tự động hóa trình duyệt (như Puppeteer hoặc API bên thứ ba) để tự động gửi kết nối/tin nhắn trực tiếp lên LinkedIn.

### 📌 Kết luận
Workflow "LinkedIn Lead Finder & Gemini-Powered Personalized Outreach with Google Sheets" là một cỗ máy tự động hóa tuyệt vời giúp tối ưu hóa phễu tìm kiếm khách hàng. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ sales và bứt phá doanh số!