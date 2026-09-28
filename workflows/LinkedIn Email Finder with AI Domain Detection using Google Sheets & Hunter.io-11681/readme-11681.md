---
title: "🚀 Tìm kiếm email LinkedIn tự động thông minh bằng AI Agent và Google Sheets"
description: "Tự động hóa hoàn toàn quy trình tìm kiếm email từ profile LinkedIn sử dụng AI Agent thông minh, Google Gemini, Google Sheets và Hunter.io."
slug: "tim-kiem-email-linkedin-tu-dong-voi-ai-va-hunter-io"
tags: [n8n, automation, no-code, lead-generation, ai-agent, google-sheets]
keywords: [n8n workflow, tìm email linkedin, hunter.io automation, google gemini ai agent, lead generation tự động]
---

# 🚀 Tìm kiếm email LinkedIn tự động thông minh bằng AI Agent và Google Sheets

Các sếp làm sales, marketing hay tuyển dụng chắc chắn hiểu được nỗi khổ khi phải ngồi dò tìm thủ công email từ các profile LinkedIn. Công việc này vừa tốn hàng tá thời gian, vừa dễ gây nhàm chán và hiệu suất thấp.

Giải pháp ở đây là gì? Workflow n8n siêu việt được phát triển bởi **Pixcels Themes** này sẽ tự động hóa 100% quy trình: đọc dữ liệu từ Google Sheets, dùng AI Agent phân tích công ty/domain, tra cứu qua Hunter.io (và Google Custom Search nếu thiếu domain), sau đó tự động cập nhật lại kết quả vào Google Sheets. Các sếp chỉ việc ngồi nhâm nhi cà phê và nhận data chất lượng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải copy-paste thủ công tên và công ty lên Google hay Hunter.io nữa.
- **Thông minh vượt trội:** AI Agent tự động nhận diện domain công ty hoặc tự tìm kiếm qua web nếu thiếu thông tin đầu vào.
- **Cập nhật liền mạch:** Dữ liệu email và domain tìm được sẽ được ghi đè/cập nhật thẳng vào Google Sheets một cách ngăn nắp.
- **Hoạt động không nghỉ:** Xử lý hàng loạt danh sách lead một cách mượt mà, tự động chạy theo lịch trình hoặc kích hoạt thủ công.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** (đã chuẩn bị sẵn file danh sách lead gồm Tên, Chức vụ, Mô tả...).
- **Google Gemini API Key** (cho các node AI Agent).
- **Hunter.io API Key** (để tra cứu email doanh nghiệp).
- **Google Custom Search API Key & CX** (để tìm kiếm web trong trường hợp thiếu domain).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n template hoặc copy đoạn JSON và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các thông số quan trọng sau:
- **Node `Get row(s) in sheet` & `Append or update row in sheet` (Google Sheets):** Kết nối tài khoản Google Sheets của các sếp, điền đúng Document ID và Sheet Name chứa danh sách lead.
- **Node `Google Gemini Chat Model` & `Google Gemini Chat Model1` (AI Model):** Thêm Credentials API Key của Google Gemini (PaLM/Gemini) để AI có đủ "trí tuệ" phân tích dữ liệu.
- **Node `HTTP Request` (Hunter.io):** Cấu hình Bearer Auth với API Key từ tài khoản Hunter.io để thực hiện gọi API tìm email.
- **Node `HTTP Request1` (Google Custom Search):** Cấu hình thông tin API Key và Custom Search Engine ID (CX) để hỗ trợ tìm kiếm domain công ty trong trường hợp dữ liệu ban đầu chưa có.
- **Node `Switch` & các node `Code in JavaScript`:** Các node logic này được thiết lập sẵn để phân nhánh dòng dữ liệu (nếu có sẵn domain vs. nếu cần tìm kiếm domain mới), các sếp giữ nguyên cấu trúc code đã được tối ưu sẵn.

#### 3. Kích hoạt ⚡️
- Nhấn **`Execute workflow`** bằng node `When clicking ‘Execute workflow’` với một vài dòng dữ liệu mẫu để test xem hệ thống chạy có mượt không.
- Sau khi kiểm tra thấy kết quả trả về Google Sheets chính xác, hãy gạt nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook/Trigger tự động:** Thay vì dùng nút bấm thủ công, các sếp có thể đổi trigger thành *Webhook* hoặc *Google Sheets Trigger* để mỗi khi thêm dòng mới vào bảng là hệ thống tự tìm email ngay lập tức.
- **Bắn thông báo qua Telegram/Slack:** Thêm một node thông báo để mỗi khi tìm được email thành công, hệ thống sẽ gửi tóm tắt về group chat cho đội sales nắm bắt.
- **Lưu log lỗi:** Thêm nhánh Error Handling để bắt các trường hợp Hunter.io không tìm thấy email, giúp dễ dàng lọc ra các lead cần xử lý thủ công.

### 📌 Kết luận
Workflow "LinkedIn Email Finder with AI Domain Detection" là một vũ khí cực kỳ lợi hại giúp tối ưu hóa phễu lọc khách hàng (Lead Generation) mà không tốn chi phí thuê tool đắt đỏ. Hãy cài đặt ngay hôm nay để tăng tốc độ làm việc cho đội ngũ của các sếp!