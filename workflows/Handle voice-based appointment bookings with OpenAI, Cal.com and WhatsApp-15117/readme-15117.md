---
title: "🚀 Tự động hóa đặt lịch hẹn bằng giọng nói với OpenAI, Cal.com và WhatsApp trong n8n"
description: "Hướng dẫn xây dựng trợ lý AI xử lý tin nhắn thoại và cuộc gọi, tự động trích xuất ý định, kiểm tra lịch trống và đặt lịch hẹn 24/7."
slug: "tu-dong-hoa-dat-lich-hen-giong-noi-openai-calcom-whatsapp"
tags: [n8n, automation, ai-agent, openai, cal.com, whatsapp]
keywords: [n8n workflow, đặt lịch hẹn tự động, giọng nói thành văn bản, OpenAI Whisper, Cal.com automation]
---

# 🚀 Tự động hóa đặt lịch hẹn bằng giọng nói với OpenAI, Cal.com và WhatsApp

Các doanh nghiệp dịch vụ (như phòng khám, salon, spa, đơn vị tư vấn) thường xuyên đối mặt với tình trạng bỏ lỡ cuộc gọi hoặc tin nhắn thoại đặt lịch ngoài giờ làm việc. Việc tuyển nhân sự trực tổng đài 24/7 tốn kém chi phí, trong khi xử lý thủ công rất dễ xảy ra sai sót hoặc trùng lịch. 

Workflow n8n này từ **Oneclick AI Squad** chính là giải pháp tự động hóa 100% không cần code (No-code): Nhận diện tin nhắn thoại/cuộc gọi, chuyển đổi thành văn bản bằng AI, trích xuất thông tin, kiểm tra lịch trống trên Cal.com/Google Calendar, tiến hành đặt lịch tự động và gửi thông báo xác nhận qua WhatsApp hoặc Email.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7**: Không bao giờ bỏ lỡ một khách hàng tiềm năng nào gọi đến hoặc gửi tin nhắn thoại ngoài giờ hành chính.
- **Xử lý thông minh**: AI tự động hiểu ngày giờ, dịch vụ khách hàng mong muốn qua giọng nói mà không cần biểu mẫu phức tạp.
- **Đồng bộ lịch trình thời gian thực**: Tránh tuyệt đối việc trùng lịch hẹn nhờ tích hợp trực tiếp với Cal.com và Google Calendar.
- **Chăm sóc khách hàng tức thì**: Tự động gửi thông tin xác nhận qua WhatsApp, SMS hoặc Email ngay sau khi đặt lịch thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key**: Dùng cho Whisper STT (chuyển giọng nói thành văn bản) và GPT (trích xuất ý định).
- **Cal.com API Key** hoặc **Google Calendar OAuth** để quản lý lịch hẹn.
- **Tài khoản WhatsApp Business / Twilio** hoặc dịch vụ gửi tin nhắn/email (SendGrid) để gửi xác nhận.
- **Google Sheets** để lưu trữ log danh sách đặt lịch.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy đoạn mã JSON tương ứng.
- Vào n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **Webhook - Incoming Voice or Audio**: Điểm tiếp nhận dữ liệu đầu vào. Các sếp cấu hình đường dẫn (path) `voice-booking-inbound` và trỏ tổng đài điện thoại hoặc ứng dụng WhatsApp của mình về URL webhook này.
- **Set Business Config**: Node này lưu cấu hình doanh nghiệp. Các sếp cần cập nhật tên doanh nghiệp, danh sách dịch vụ cung cấp và múi giờ (timezone) chuẩn (ví dụ: `Asia/Ho_Chi_Minh`).
- **Whisper STT - Transcribe Audio / ElevenLabs STT**: Nhập OpenAI API Key để mô hình xử lý file âm thanh nhận được thành văn bản một cách chính xác.
- **AI - Extract Booking Intent**: Cấu hình prompt cho AI để trích xuất các trường dữ liệu quan trọng như: Tên khách hàng, Ngày hẹn, Giờ hẹn, Loại dịch vụ.
- **Cal.com - Check Available Slots / Google Calendar - Check Busy Times**: Kết nối tài khoản Cal.com hoặc Google Calendar để hệ thống tự động quét lịch trống.
- **Send WhatsApp Confirmation / Send Email Confirmation**: Điền thông tin kết nối tài khoản gửi tin nhắn (HTTP Basic Auth hoặc API tương ứng của nhà cung cấp dịch vụ WhatsApp/SMS/Email).
- **Log Booking to Google Sheets**: Trỏ tới file Google Sheets quản lý lịch hẹn của doanh nghiệp để lưu vết mọi đơn hàng thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một file âm thanh mẫu (hoặc gọi test webhook) để kiểm tra luồng chạy từ đầu đến cuối.
- Kiểm tra xem lịch có được tạo trên Cal.com và thông báo có gửi về WhatsApp/Email thành công hay không.
- Gạt công tắc sang **Active** để đưa hệ thống vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack**: Bổ sung một node thông báo qua Telegram hoặc Slack để đội ngũ sale nhận được cảnh báo ngay khi có khách hàng đặt lịch mới qua giọng nói.
- **Xử lý lịch bận thông minh**: Ở node AI tạo phản hồi khi trùng lịch (`AI - Generate Conflict Response`), các sếp có thể yêu cầu AI tự động đề xuất 3 khung giờ trống tiếp theo một cách tự nhiên và lịch sự nhất.
- **Lưu log chi tiết**: Kết hợp thêm cơ sở dữ liệu (như Airtable hoặc PostgreSQL) thay vì chỉ dùng Google Sheets để lưu trữ thông tin khách hàng lâu dài và phục vụ việc remarketing sau này.

### 📌 Kết luận
Việc tự động hóa quy trình đặt lịch bằng giọng nói với AI không chỉ giúp doanh nghiệp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn mang lại trải nghiệm chuyên nghiệp, tức thì cho khách hàng. Hãy triển khai ngay hôm nay để nâng tầm hệ thống vận hành của các sếp!