---
title: "🚀 Tự động hóa tìm kiếm khách hàng tiềm năng trên LinkedIn với GPT-4o, Apify và PhantomBuster"
description: "Xây dựng hệ thống tự động quét khách hàng tiềm năng, tạo ice-breaker bằng AI và gửi lời mời kết nối LinkedIn tự động 100% không cần code với n8n."
slug: "tu-dong-hoa-tim-kiem-khach-hang-linkedin-gpt4o-apify"
tags: [n8n, automation, no-code, lead-generation, ai, apify, openai]
keywords: [n8n workflow, tự động hóa lead generation, linkedin automation, apify scraper, gpt-4o icebreaker, phantombuster]
---

# 🚀 Tự động hóa tìm kiếm khách hàng tiềm năng trên LinkedIn với GPT-4o, Apify và PhantomBuster

Các sếp có bao giờ cảm thấy kiệt sức khi phải ngồi hàng giờ lướt LinkedIn, tìm kiếm từng profile, đọc thông tin công ty rồi vắt óc suy nghĩ câu mở đầu (ice-breaker) để gửi lời mời kết nối không? Công việc thủ công này vừa tốn thời gian, tỷ lệ chuyển đổi lại thấp mà lại cực kỳ nhàm chán.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa toàn bộ quy trình: Từ việc nhập mô tả đối tượng mục tiêu vào Form, AI (GPT-4o) sẽ tạo URL tìm kiếm, Apify quét dữ liệu, AI viết câu chào cá nhân hóa, lưu vào Google Sheets và cuối cùng tự động gửi kết nối qua PhantomBuster. Tất cả chạy tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì tìm kiếm thủ công từng khách hàng, hệ thống tự động hóa từ A-Z chỉ sau một cú click điền Form.
- **Cá nhân hóa đỉnh cao:** Sử dụng GPT-4o để đọc dữ liệu LinkedIn và viết câu mở đầu (ice-breaker) siêu chuẩn xác dựa trên profile thực tế của khách hàng.
- **Đồng bộ dữ liệu thông minh:** Tự động lưu toàn bộ thông tin lead, profile URL và ice-breaker vào Google Sheets để dễ dàng theo dõi.
- **Tự động tiếp cận:** Kích hoạt PhantomBuster để gửi lời mời kết nối tự động, mở rộng mạng lưới networking không ngừng nghỉ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Key sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng GPT-4o tạo URL và viết ice-breaker.
- **Apify Account & API Token:** Dùng để chạy actor trích xuất dữ liệu khách hàng.
- **Google Sheets:** Một file Google Sheet chuẩn bị sẵn các cột nhận dữ liệu.
- **PhantomBuster Account & API Key:** Dùng để tự động hóa việc gửi lời mời kết nối trên LinkedIn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, vào n8n Editor chọn **Import từ file** (hoặc copy/paste trực tiếp đoạn JSON vào workspace) là xong phần khung.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp nhớ cấu hình kỹ các node sau:

- **Description of the audience you want to scrap (Form Trigger):** Đây là điểm khởi đầu. Các sếp tùy chỉnh các trường thông tin trong form để nhập mô tả đối tượng khách hàng muốn tìm (ví dụ: Chức vụ, ngành nghề, địa điểm...).
- **Genrating appolo Url for apify to scrap (OpenAI):** Node này sử dụng GPT-4o để chuyển đổi mô tả từ form thành một Apollo URL chuẩn xác. Các sếp cần kết nối **OpenAI Credentials** và kiểm tra lại System Prompt cho phù hợp.
- **Run apify actor to scrap the proscpect (HTTP Request):** Node gửi request để chạy Apify Actor quét dữ liệu lead. Các sếp cần điền API Key của Apify vào header hoặc cấu hình credential tương ứng.
- **Genrate ice breaker by scraping linkedin data (OpenAI):** Prompt cho GPT-4o đã được hard-code sẵn để tạo ice-breaker dựa trên dữ liệu LinkedIn quét được. Các sếp có thể tinh chỉnh lại prompt trong node này theo văn phong mong muốn.
- **Adding ice breaker to google sheets (Google Sheets):** 
  - Kết nối tài khoản Google của các sếp.
  - Chọn đúng file Spreadsheet và Sheet Name.
  - *Lưu ý:* Tạo sẵn các cột trong Google Sheet như: `Name`, `LinkedIn URL`, `Company Website`, `Description` cùng các trường do Apify và OpenAI trả về để map dữ liệu cho chính xác.
- **trigger phantom buster to send personlized connection request (HTTP Request):** Node kích hoạt PhantomBuster gửi kết nối LinkedIn. Các sếp cần lấy API Key từ PhantomBuster điền vào header, đồng thời thay thế Agent ID của các sếp vào URL của request.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và điền thử dữ liệu vào Form Trigger để test xem dữ liệu có đổ về Google Sheets và chạy mượt không.
- Nếu mọi thứ xanh đèn (success), các sếp bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram ngay sau Google Sheets để nhận thông báo tức thì mỗi khi có một lead mới được quét và tạo ice-breaker thành công.
- **Thêm bước lọc chất lượng (Filter Node):** Lọc bớt những lead không đủ điều kiện (thiếu website, không có số lượng nhân sự phù hợp) trước khi đẩy vào Google Sheets.
- **Mở rộng chuỗi Automation (Nurturing):** Kết hợp thêm các bước gửi tin nhắn Follow-up tự động sau khi khách hàng đồng ý kết nối trên LinkedIn.

### 📌 Kết luận
Workflow này là một vũ khí hạng nặng cho các đội ngũ Sales, Marketing và Founder muốn tối ưu hóa quy trình tìm kiếm khách hàng B2B trên LinkedIn. Thiết lập một lần, chạy tự động mãi mãi. Chúc các sếp áp dụng thành công và "chốt đơn" mỏi tay!