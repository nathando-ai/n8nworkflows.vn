---
title: "🚀 Tóm tắt lịch trình Google Calendar qua SMS mỗi sáng với Claude AI & Twilio"
description: "Tự động hóa nhận bản tin tóm tắt lịch trình Google Calendar hàng ngày qua tin nhắn SMS lúc 7 giờ sáng bằng Claude AI và Twilio, giúp bạn nắm bắt ngày mới không bỏ lỡ sự kiện."
slug: "tom-tat-lich-trinh-google-calendar-qua-sms-claude-ai"
tags: [n8n, automation, no-code, google-calendar, claude-ai, twilio, productivity]
keywords: [n8n workflow, tóm tắt lịch calendar, claude ai, twilio sms, tự động hóa n8n, google calendar automation]
---

# 🚀 Nhận bản tóm tắt lịch trình Google Calendar qua SMS mỗi sáng với Claude AI

Các sếp có bao giờ cảm thấy buổi sáng đầu ngày vô cùng bận rộn, phải mở ứng dụng Lịch (Calendar) căng mắt xem hôm nay có những cuộc họp nào, sự kiện gì quan trọng để rồi dễ bị bỏ sót? Việc kiểm tra thủ công này vừa tốn thời gian lại vừa dễ sót việc.

Giải pháp đây rồi! Workflow n8n này sẽ hoạt động như một trợ lý ảo cá nhân đắc lực: tự động quét toàn bộ lịch Google Calendar của các sếp vào lúc **7 giờ sáng hàng ngày**, sử dụng **Claude AI (Anthropic)** để phân tích, tổng hợp thành một tin nhắn tóm tắt cực kỳ ngắn gọn, thân thiện và gửi thẳng vào điện thoại của các sếp qua **Twilio SMS**. Không cần code phức tạp, tự động hóa 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động mỗi ngày:** Nhận tin nhắn SMS tóm tắt lịch trình ngay khi vừa thức dậy (7h sáng) mà không cần mở app.
- **Cá nhân hóa thông minh:** Claude AI (model Claude 3.7 Sonnet) sẽ biến các sự kiện khô khan thành lời nhắc thân thiện như một trợ lý thực thụ.
- **Tiết kiệm thời gian:** Không bỏ lỡ bất kỳ cuộc họp hay sự kiện quan trọng nào trong ngày.
- **Hoạt động tự động 24/7:** Chạy ngầm ổn định trên n8n, không cần thao tác thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- [**Google Cloud Console**](https://cloud.google.com/cloud-console?hl=en): Kích hoạt Google Calendar API để lấy thông tin sự kiện.
- [**Twilio Account**](https://www.twilio.com/console): Mua một số điện thoại ảo và nạp sẵn một vài đô la để gửi tin nhắn SMS.
- **Anthropic API Key**: Để sử dụng sức mạnh của Claude AI (model `claude-3-7-sonnet-20250219`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình. Workflow gồm 8 nodes chính phối hợp nhịp nhàng:
- `Trigger workflow at 7AM` (Schedule Trigger)
- `Get events from Events Calendar` (Google Calendar)
- `Check if there are any events` (IF Node)
- `Format list of events and sender mobile num` (Code Node)
- `Basic LLM Chain` & `Anthropic Chat Model` (AI LangChain nodes)
- `Persist schema` (Set Node)
- `Twilio` (Gửi SMS)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đưa vào vận hành, các sếp nhớ cấu hình kỹ các node sau:
- **Trigger workflow at 7AM**: Kiểm tra lại múi giờ (Timezone) của các sếp để đảm bảo bot chạy đúng 7h sáng giờ địa phương.
- **Get events from Events Calendar**: Kết nối tài khoản Google Calendar (qua OAuth2) và chọn đúng Calendar cần lấy sự kiện.
- **Anthropic Chat Model**: Thêm Credentials chứa Anthropic API Key và chọn model mong muốn (`Claude 3.7 Sonnet`).
- **Twilio Node**: Điền thông tin Credentials của Twilio, thay thế số điện thoại gửi (`From`) bằng số điện thoại các sếp đã mua trên Twilio, và số điện thoại nhận (`To`) bằng số điện thoại cá nhân của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử xem SMS có bắn về điện thoại chưa.
- Sau khi test thành công, gạt công tắc **Active** góc trên bên phải để workflow tự động chạy mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài SMS qua Twilio, các sếp có thể nối thêm node Telegram hoặc Slack để nhận bản tóm tắt qua nhiều ứng dụng chat khác nhau.
- **Lưu log:** Thêm một node Google Sheets để lưu lại lịch sử các tin nhắn đã gửi nhằm phục vụ việc kiểm tra sau này.
- **Tùy chỉnh giọng văn AI:** Trong Prompt của LLM Chain, các sếp có thể tùy biến văn phong của trợ lý (hài hước, trang trọng, hoặc nói chuyện kiểu "chủ nhân và quản gia").

### 📌 Kết luận
Một workflow nhỏ nhưng mang lại sự tiện ích cực lớn cho những ai bận rộn. Hãy cài đặt ngay hôm nay để có một trợ lý AI nhắc lịch mỗi sáng, giúp các sếp luôn sẵn sàng năng lượng cho ngày mới!