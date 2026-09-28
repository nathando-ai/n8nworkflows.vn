---
title: "🤖 Xây Dựng Trợ Lý Ảo Google Calendar Nhắc Lịch Thông Minh Với GPT-4o & Telegram"
description: "Tự động hóa lịch trình của bạn với n8n: Quét sự kiện Google Calendar sắp diễn ra, dùng GPT-4o-mini cá nhân hóa lời nhắc và gửi thẳng qua Telegram không lo bỏ lỡ."
slug: "tro-ly-ao-google-calendar-nhac-lich-gpt-4o-telegram"
tags: [n8n, automation, google-calendar, openai, telegram, ai-agent]
keywords: [n8n workflow, nhắc lịch google calendar, trợ lý ảo ai telegram, tự động hóa n8n, gpt-4o mini n8n]
---

# 🤖 Xây Dựng Trợ Lý Ảo Google Calendar Nhắc Lịch Thông Minh Với GPT-4o & Telegram

Các sếp có bao giờ gặp tình trạng quên lịch họp, hẹn khách hàng vì thông báo mặc định của Google Calendar quá khô khan và dễ bị trôi giữa hàng tá thông báo khác không? Việc bỏ lỡ các sự kiện quan trọng không chỉ gây mất uy tín mà còn làm gián đoạn dòng công việc.

Giải pháp ở đây chính là một trợ lý ảo chạy 24/7. Workflow n8n này sẽ tự động quét lịch trình sắp tới của bạn, nhờ **GPT-4o-mini** viết lại nội dung nhắc nhở thật tự nhiên, thân thiện và gửi trực tiếp qua **Telegram** trước khi sự kiện diễn ra đúng 1 tiếng. Tất cả tự động 100%, không tốn một xu phí thuê trợ lý ngoài!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bao giờ trễ hẹn**: Nhận thông báo thông minh trước 1 giờ qua Telegram cá nhân.
- **Lời nhắc cá nhân hóa bằng AI**: Thay vì thông báo cứng nhắc, GPT-4o-mini sẽ "biến hóa" nội dung lịch hẹn thành những lời nhắn nhủ lịch sự, dễ thương và đầy đủ chi tiết.
- **Chống spam hiệu quả**: Tích hợp bộ lọc trùng lặp (`Already sent?`) đảm bảo một sự kiện chỉ bắn tin nhắc duy nhất một lần.
- **Vận hành tự động hoàn toàn**: Chạy ngầm liên tục mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** (để kết nối Google Calendar).
- **OpenAI API Key** (để sử dụng mô hình GPT-4o-mini).
- **Telegram Bot Token** (tạo qua `@BotFather`) và **Chat ID** của cá nhân các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần cấu hình kỹ các điểm sau:

- **Schedule Trigger**: Node này quyết định tần suất n8n kiểm tra lịch của các sếp (mặc định có thể chạy mỗi giờ/mỗi ngày tùy ý).
- **Get upcoming event (Google Calendar)**: 
  - Kết nối tài khoản Google Calendar của các sếp qua OAuth2.
  - Cấu hình thời gian quét sự kiện (mặc định workflow đang được set lấy các sự kiện sắp diễn ra trong 1 giờ tới).
- **Already sent? (Remove Duplicates)**: Node này có sẵn nhiệm vụ lọc và loại bỏ các sự kiện đã được thông báo ở các lần chạy trước, giữ cho Telegram của các sếp không bị ngập rác.
- **Secretary Agent & OpenAI Chat Model**: 
  - Cấu hình credential cho **OpenAI Chat Model** (chọn model `gpt-4o-mini`).
  - **Secretary Agent** sẽ đóng vai trò tổng hợp thông tin sự kiện từ Google Calendar và điều phối AI viết nội dung nhắc nhở.
- **Send reminder (Telegram)**: 
  - Kết nối `telegramApi` bằng Bot Token của các sếp.
  - Thay thế `CHAT_ID` mặc định bằng Chat ID Telegram cá nhân của các sếp để bot biết đường gửi tin nhắn về máy.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử xem bot đã nhắn tin về Telegram chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow "xịn" hơn nữa, các sếp có thể tùy biến:
1. **Đa kênh thông báo**: Kết hợp thêm node Slack hoặc Discord nếu làm việc nhóm.
2. **Tùy chỉnh giọng văn AI**: Sửa System Prompt trong *Secretary Agent* để bắt bot nhắc nhở theo phong cách nghiêm túc, hài hước, hoặc nói chuyện như "chủ tịch".
3. **Thêm nút bấm tương tác**: Gắn thêm tính năng xác nhận "Tôi đã sẵn sàng" ngay trên tin nhắn Telegram.

### 📌 Kết luận
Một trợ lý AI nhắc lịch cá nhân hóa chưa bao giờ dễ thiết lập đến thế với n8n. Hãy cài đặt ngay để tối ưu hóa thời gian và không bao giờ bỏ lỡ bất kỳ cuộc họp quan trọng nào nữa các sếp nhé!