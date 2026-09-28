---
title: "🚀 Tự động ghi chép chi tiêu từ Telegram vào Google Sheets bằng AI Voice & Text"
description: "Hướng dẫn cài đặt workflow n8n giúp ghi lại nhiều khoản chi tiêu qua tin nhắn văn bản hoặc ghi âm Telegram, tự động phân tích bằng OpenAI và lưu vào Google Sheets."
slug: "tu-dong-ghi-chep-chi-tieu-telegram-google-sheets-ai"
tags: [n8n, automation, ai, telegram, google-sheets, open-ai]
keywords: [n8n workflow, ghi chép chi tiêu tự động, telegram bot google sheets, ai expense tracker, open ai whisper n8n]
---

# 🚀 Tự động ghi chép chi tiêu từ Telegram vào Google Sheets bằng AI Voice & Text

Các sếp có cảm thấy mệt mỏi mỗi khi cuối tháng phải ngồi tổng hợp lại hóa đơn, mở Google Sheets lên nhập từng dòng chi tiêu thủ công? Việc ghi chép thủ công không chỉ tốn thời gian mà còn dễ bỏ sót. 

Giải pháp đây rồi! Workflow n8n này sẽ biến chiếc điện thoại của các sếp thành một trợ lý tài chính thông minh 100% tự động. Chỉ cần gửi một tin nhắn văn bản hoặc thậm chí là **tin nhắn thoại (voice note)** qua Telegram, AI sẽ tự động phân tích, tách từng khoản chi và lưu thẳng vào Google Sheets, sau đó gửi lại tin nhắn xác nhận. Không cần code, không cần app phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Không cần mở bảng tính hay app phức tạp, chỉ cần nhắn tin Telegram khi đang di chuyển.
- **Hỗ trợ giọng nói (Voice Note):** Vừa lái xe vừa đọc "Cà phê 35 nghìn, ăn trưa 50 nghìn" là hệ thống tự ghi nhận.
- **Xử lý thông minh:** AI tự động tách nhiều khoản chi tiêu trong cùng một tin nhắn thành các dòng riêng biệt.
- **Phản hồi tức thì:** Bot Telegram sẽ gửi lại báo cáo xác nhận ngay sau khi ghi dữ liệu thành công lên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua `@BotFather`).
- **Google Account** để kết nối Google Sheets.
- **OpenAI API Key** (Sử dụng cho mô hình GPT-4o-mini và Whisper audio transcription).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON tải từ trang quản trị.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:
- **Telegram Message Trigger & Get File & Send Telegram Confirmation:** Kết nối với tài khoản Telegram API và chọn Bot của các sếp.
- **Transcribe audio (OpenAI):** Chọn resource là `audio`, operation là `transcribe` và dùng mô hình Whisper để chuyển đổi giọng nói thành văn bản.
- **OpenAI Chat Model & Parse Expenses with AI:** Chọn model `gpt-4o-mini` (được khuyến nghị vì nhanh và tiết kiệm chi phí). Cấu hình Structured Output Parser để ép AI trả về đúng cấu trúc dữ liệu mong muốn.
- **Append to Google Sheet:** 
  - Tạo sẵn một Google Sheet với các tiêu đề cột: `Date | Category | Merchant | Amount | Note`.
  - Điền chính xác **Spreadsheet ID** và **Sheet Name** vào node.
  - Mapping các trường dữ liệu do AI trả về vào đúng các cột trong bảng.
- **Wait 0.5 seconds:** Giữ node này ở khoảng `500–1000 ms` để tránh lỗi xung đột API (rate limit) khi ghi nhiều dòng liên tục vào Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một tin nhắn mẫu tới Bot Telegram của sếp:  
  `Gas 34.67, Groceries 82.45, Coffee 6.25, Lunch 14.90`
- Kiểm tra xem Google Sheets đã tự động thêm 4 dòng tương ứng chưa và bot có phản hồi lại không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo qua Slack/Telegram nhóm:** Nếu quản lý quỹ chung của team, sếp có thể mở rộng workflow để bắn thông báo chi tiêu vào nhóm chat chung.
- **Tạo báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để chạy lệnh tổng hợp chi tiêu mỗi tuần/tháng rồi gửiสรุป (summary) về Telegram cho các sếp.
- **Phân loại tự động:** Tinh chỉnh prompt trong AI node để tự động gán nhãn danh mục (Ăn uống, Di chuyển, Mua sắm...) thông minh hơn dựa trên thói quen chi tiêu.

### 📌 Kết luận
Một workflow cực kỳ thực chiến giúp số hóa toàn bộ thói quen ghi chép tài chính cá nhân hoặc doanh nghiệp nhỏ chỉ bằng một vài câu lệnh qua Telegram. Hãy cài đặt ngay để tối ưu hóa thời gian cho bản thân các sếp nhé!