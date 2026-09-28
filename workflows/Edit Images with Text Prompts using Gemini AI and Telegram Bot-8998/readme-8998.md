---
title: "🚀 Tự động chỉnh sửa ảnh bằng AI qua Telegram Bot với Google Gemini và n8n"
description: "Xây dựng chatbot Telegram thông minh tự động nhận ảnh và chỉnh sửa theo yêu cầu văn bản của bạn nhờ sức mạnh của Google Gemini AI và n8n."
slug: "chinh-sua-anh-ai-telegram-bot-gemini-n8n"
tags: [n8n, automation, telegram-bot, google-gemini, ai-image-editor]
keywords: [n8n workflow, telegram bot ai, chỉnh sửa ảnh bằng ai, google gemini api, tự động hóa n8n]
---

# 🚀 Tự động chỉnh sửa ảnh bằng AI qua Telegram Bot với Google Gemini

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở Photoshop hay các phần mềm phức tạp chỉ để chỉnh sửa nhanh một bức ảnh? Hoặc việc dùng các web app AI tốn kém thời gian chuyển đổi qua lại giữa các ứng dụng? 

Hãy tưởng tượng bạn chỉ cần gửi một bức ảnh kèm theo lời nhắn (caption) như *"thêm hiệu ứng siêu anh hùng"* hoặc *"làm sáng bức ảnh này lên"* vào chính chiếc Telegram quen thuộc, và lập tức nhận lại bức ảnh đã được AI "phù phép" hoàn hảo. Workflow n8n này sẽ giúp các sếp biến ý tưởng đó thành hiện thực 100% tự động mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và phản hồi Telegram tức thì, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ thần tốc**: Xử lý và trả kết quả ảnh chỉnh sửa trực tiếp trên Telegram chỉ trong vài giây.
- **Tiết kiệm chi phí**: Tận dụng Google Gemini API mạnh mẽ với chi phí tối ưu thay vì mua các gói phần mềm đắt đỏ.
- **Trải nghiệm mượt mà**: Tương tác tự nhiên qua chat, không cần giao diện phức tạp, phù hợp cho cả cá nhân lẫn đội ngũ làm việc nhóm.
- **Hoạt động 24/7**: Bot luôn túc trực trên Telegram sẵn sàng nhận yêu cầu bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản Telegram để tạo Bot.
- Tài khoản Google AI Studio để lấy khóa API Gemini.
- Một n8n instance (Self-hosted hoặc n8n Cloud) đã bật các node Telegram và Google Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo một workflow mới và dán toàn bộ mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 5 nodes chính phối hợp nhịp nhàng:

- **Telegram Trigger**: Lắng nghe tin nhắn mới từ người dùng. Các sếp cần cấu hình **Credentials** cho node này bằng cách kết nối tài khoản `Telegram API` (lấy token từ `@BotFather`).
- **Filter: Has Caption and File**: Node logic điều kiện (AND) giúp kiểm tra xem tin nhắn gửi đến có đồng thời chứa file ảnh và caption (prompt) hay không. Nếu thiếu, workflow sẽ tự động bỏ qua để tránh lỗi.
- **Download Image**: Sử dụng `file_id` từ trigger để tải file ảnh về dưới dạng binary data (lưu ý: file trên Telegram tự động xóa sau 1 giờ, vì vậy trigger cần hoạt động ngay lập tức).
- **Edit Image with AI (Google Gemini)**: Node cốt lõi xử lý hình ảnh. Các sếp cần cấu hình **Credentials** `Google Gemini API` (Google Palm API). Tại ô `Prompt`, hệ thống sẽ tự động lấy nội dung từ caption của tin nhắn: `={{ $('Telegram Trigger').item.json.message.caption }}`.
- **Send Edited Image**: Node Telegram thực hiện gửi bức ảnh đã được AI xử lý xong trả ngược lại cho người dùng với thao tác `sendPhoto`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một bức ảnh kèm caption cho bot trên Telegram để test thử.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để bot chính thức hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho công việc thực tế, các sếp có thể mở rộng thêm:
1. **Lưu lịch sử**: Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử người dùng đã gửi ảnh gì và prompt nào.
2. **Thông báo nhóm (Slack/Telegram Group)**: Gửi bản sao của bức ảnh đã chỉnh sửa vào một nhóm nội bộ để quản lý chất lượng hoặc kiểm duyệt.
3. **Xử lý lỗi thông minh**: Thêm nhánh Error Trigger để bot tự động phản hồi lại người dùng bằng tin nhắn văn bản nếu prompt quá dài hoặc ảnh không hợp lệ thay vì đứng im lặng.

### 📌 Kết luận
Workflow này là một minh họa tuyệt vời cho việc ứng dụng AI vào tự động hóa công việc hàng ngày một cách cực kỳ thiết thực. Hãy triển khai ngay hôm nay để sở hữu một "trợ lý thiết kế" ngay trong khung chat Telegram của các sếp!