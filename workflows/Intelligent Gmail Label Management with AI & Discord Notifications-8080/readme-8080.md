---
title: "🚀 Tự động phân loại nhãn Gmail thông minh bằng AI & thông báo Discord"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc email đến, sử dụng AI LangChain để phân tích nội dung, tự động tạo nhãn mới hoặc gán nhãn cũ trong Gmail và gửi tóm tắt qua Discord."
slug: "tu-dong-phan-loai-nhan-gmail-thong-minh-ai-discord"
tags: [n8n, automation, gmail, discord, ai, langchain, openai]
keywords: [n8n workflow, tự động hóa gmail, phân loại email bằng ai, discord notification, langchain n8n]
---

# 🚀 Tự động phân loại nhãn Gmail thông minh bằng AI & thông báo Discord

Hộp thư đến (Inbox) của các sếp lúc nào cũng ngập tràn email từ công việc, quảng cáo, hóa đơn cho đến thông báo hệ thống? Việc ngồi lọc thủ công, gắn nhãn (label) rồi phân loại từng email ngốn rất nhiều thời gian quý báu mỗi ngày. 

Đừng lo, workflow n8n tuyệt vời này do tác giả **Albert Ho** thiết kế sẽ thay các sếp giải quyết triệt để vấn đề trên. Sử dụng sức mạnh của **AI (LangChain & OpenAI/LLM)** kết hợp với **Gmail** và **Discord**, hệ thống sẽ tự động đọc email mới, thông minh nhận diện nội dung để tự tạo nhãn mới (nếu cần) hoặc gắn nhãn phù hợp, đồng thời bắn thông báo trực quan ngay lập tức vào kênh Discord của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Email vừa đến là được AI phân tích và gán nhãn ngay lập tức mà không cần động tay.
- **AI thông minh tự thích ứng:** Hệ thống tự động quét các nhãn sẵn có trong Gmail để AI lựa chọn. Nếu xuất hiện chủ đề hoàn toàn mới, AI tự động tạo nhãn mới trong Gmail.
- **Báo cáo tức thì:** Nhận ngay bản tóm tắt email và trạng thái gắn nhãn gọn gàng qua kênh Discord cá nhân hoặc nhóm làm việc.
- **Tiết kiệm hàng giờ mỗi ngày:** Dẹp bỏ hoàn toàn nỗi ám ảnh dọn dẹp hộp thư đến thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Tài khoản Google / Gmail** (Cần cấp quyền OAuth2 để n8n đọc email, lấy danh sách nhãn, tạo nhãn mới và thêm nhãn vào thư).
- **OpenAI API Key** hoặc LLM tương thích (để chạy các node `Basic LLM Chain`, `OpenAI Chat`).
- **Discord Bot Token & Webhook/Channel** (để gửi tin nhắn thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào trình soạn thảo n8n (n8n Editor) của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các credentials và tham số quan trọng sau:

- **Gmail Trigger & Các node Gmail (`Get many labels`, `Create a label`, `Add label to message`):**
  - Kết nối tài khoản Gmail thông qua **Gmail OAuth2**.
  - Đảm bảo cấp đủ quyền (Scopes) cho phép n8n đọc, sửa nhãn và quản lý email của sếp.
- **OpenAI Chat Nodes (`OpenAI Chat 10000`, `OpenAI Chat 10001`) & Basic LLM Chain:**
  - Nhập **OpenAI API Key** của các sếp vào phần credentials.
  - Kiểm tra lại model LLM được chọn (có thể điều chỉnh sang `gpt-4o-mini` hoặc các model phù hợp để tối ưu chi phí và tốc độ).
- **Structured Output Parser:**
  - Node này đảm bảo AI trả về kết quả đúng định dạng JSON chuẩn xác để các bước sau (tạo nhãn, gắn nhãn) thực thi mượt mà không bị lỗi cú pháp.
- **Send a message (Discord node):**
  - Kết nối bằng **Discord Bot API**.
  - Chỉ định đúng Channel ID nơi các sếp muốn bot gửi thông báo tóm tắt email.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một email giả lập đến tài khoản Gmail của sếp để test quá trình xử lý của AI.
- Kiểm tra kết quả trên Gmail (xem email đã được gán nhãn chưa) và Discord (xem tin nhắn thông báo đã bắn về chưa).
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Discord, các sếp có thể nối thêm node Telegram hoặc Slack để nhận thông báo trên nhiều nền tảng khác nhau cùng lúc.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets trước hoặc sau bước xử lý để lưu lại toàn bộ log email đã phân loại, tiện cho việc thống kê báo cáo cuối tuần.
- **Tinh chỉnh Prompt cho AI:** Tùy biến prompt trong `Basic LLM Chain` để AI đặt tên nhãn theo tiếng Việt có dấu gọn gàng, phù hợp với văn hóa công ty của các sếp.

### 📌 Kết luận
Với workflow thông minh này, việc quản lý hộp thư Gmail không bao giờ dễ dàng và thú vị đến thế. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc cá nhân và doanh nghiệp của các sếp nhé!