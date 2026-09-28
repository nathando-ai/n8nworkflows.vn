---
title: "🚀 Quản lý Lịch Google tự động bằng AI Agent với n8n và OpenAI"
description: "Hướng dẫn xây dựng Sub-workflow tự động quản lý Google Calendar (Lấy, Tạo, Xóa sự kiện) thông qua OpenAI Assistant và n8n AI Agent siêu thông minh."
slug: "quan-ly-google-calendar-voi-openai-assistant-n8n"
tags: [n8n, automation, ai-agent, openai, google-calendar, no-code]
keywords: [n8n workflow, quản lý lịch google, openai assistant, google calendar automation, ai agent n8n]
---

# 🚀 Quản lý Lịch Google tự động bằng AI Agent với n8n và OpenAI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải liên tục mở Google Calendar để tìm kiếm lịch trống, tạo sự kiện thủ công hay xóa lịch hẹn bị hủy? Việc quản lý thời gian thủ công không chỉ tốn thời gian mà còn dễ dẫn đến sai sót, trùng lịch. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ: Sử dụng **AI Agent kết hợp OpenAI và Google Calendar Tools**, hoạt động như một trợ lý ảo thông minh nhận lệnh qua text để tự động **Xem (Get), Tạo (Create) và Xóa (Delete)** sự kiện trên lịch của các sếp một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Trợ lý AI tự động phân tích yêu cầu ngôn ngữ tự nhiên để gọi đúng công cụ (Get, Create, Delete) mà không cần lập trình phức tạp.
- **Tiết kiệm thời gian**: Thay vì click nhiều bước trên giao diện Calendar, chỉ cần gửi một câu lệnh là xong việc.
- **Duy trì ngữ cảnh (Memory)**: Hệ thống sử dụng `sessionid` để ghi nhớ lịch sử hội thoại, giúp các sếp trò chuyện mượt mà như với trợ lý con người.
- **Linh hoạt tích hợp**: Thiết kế dưới dạng Sub-workflow, dễ dàng gọi từ các workflow chính như chatbot Telegram, Slack hoặc Webhook bất kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Khuyên dùng bản self-hosted hoặc n8n Cloud).
- **OpenAI API Key**: Tài khoản OpenAI có quyền truy cập vào các mô hình GPT (Workflow sử dụng `gpt-4.1-mini`).
- **Google Account**: Tài khoản Google có quyền truy cập Google Calendar để cấu hình OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này (hoặc tải file JSON từ n8n.io/workflows/7787) và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính được cấu hình mạch lạc. Các sếp cần chú ý các điểm sau:

- **When Executed by Another Workflow (`executeWorkflowTrigger`)**: Node nhận dữ liệu đầu vào bao gồm `text` (nội dung câu lệnh) và `sessionid` (mã phiên làm việc).
- **OpenAI Chat Model (`lmChatOpenAi`)**: 
  - Chọn Credentials OpenAI của các sếp.
  - Đảm bảo model được chọn là `gpt-4.1-mini` (hoặc thay đổi sang model khác tùy nhu cầu).
- **Simple Memory (`memoryBufferWindow`)**: Giúp lưu trữ ngữ cảnh hội thoại dựa theo `sessionid`.
- **Google Calendar Tools (Create, Get, Delete)**:
  - Cấu hình **Google Calendar OAuth2 API credentials** cho cả 3 node này để cấp quyền truy cập lịch của các sếp.
  - Node **Get**: Mặc định cấu hình `operation` là `getAll` (lấy danh sách sự kiện theo khoảng thời gian).
  - Node **Create**: Yêu cầu cung cấp thông tin `start`, `end`, và `summary`.
  - Node **Delete**: Yêu cầu cung cấp `eventId` để xóa chính xác sự kiện.
- **AI Agent (`agent`)**: Đóng vai trò bộ não trung tâm, điều phối các công cụ (tools) dựa trên yêu cầu từ `text` được truyền vào và trả về xác nhận ngắn gọn cho Parent workflow.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với dữ liệu giả lập (`text`: "Kiểm tra lịch ngày mai", `sessionid`: "test-123").
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot**: Kết nối Sub-workflow này với một Parent workflow nhận tin nhắn từ **Telegram Bot** hoặc **Slack**, giúp các sếp quản lý lịch trực tiếp khi đang chat trên điện thoại.
- **Lưu Log hoạt động**: Thêm node Google Sheets hoặc Airtable sau AI Agent để lưu lại lịch sử các thao tác tạo/xóa lịch phục vụ việc kiểm tra sau này.
- **Bổ sung công cụ**: Các sếp có thể mở rộng thêm các Google Calendar Tool khác như `Update` (Cập nhật sự kiện) nếu cần thiết.

### 📌 Kết luận
Với workflow n8n kết hợp OpenAI Assistant và Google Calendar này, các sếp đã sở hữu ngay một trợ lý thời gian biểu siêu việt, hoạt động 24/7 mà không tốn chi phí thuê nhân sự. Hãy import ngay vào hệ thống và trải nghiệm sức mạnh của AI Automation nhé!