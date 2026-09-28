---
title: "🚀 Tự động gửi SMS nhắc lịch họp mỗi ngày từ Google Calendar với GPT-4o-mini và Alive5"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy lịch họp từ Google Calendar mỗi 9h sáng, dùng AI viết tin nhắn ngắn gọn và gửi SMS qua Alive5."
slug: "tu-dong-nhac-lich-hop-sms-google-calendar-gpt-4-alive5"
tags: [n8n, automation, google-calendar, openai, alive5, sms-reminder]
keywords: [n8n workflow, nhắc lịch họp sms, google calendar ai, gpt-4o-mini, alive5 automation]
---

# 🚀 Tự động gửi SMS nhắc lịch họp mỗi ngày từ Google Calendar với GPT-4o-mini và Alive5

Các sếp có bao giờ rơi vào tình trạng quên lịch họp vì có quá nhiều cuộc hẹn rải rác trong ngày? Việc mở đi mở lại Google Calendar để kiểm tra không chỉ tốn thời gian mà còn dễ bỏ sót. 

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: mỗi sáng quét lịch họp, nhờ AI (GPT-4o-mini) cô đọng lại thành một tin nhắn siêu ngắn dưới 160 ký tự, và bắn thẳng tin nhắn SMS về điện thoại của các sếp qua Alive5. Không cần code, hoạt động tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Đúng 9 giờ sáng mỗi ngày, hệ thống tự điểm danh các cuộc họp trong ngày mà không cần chạm tay.
- **Cô đọng & Chính xác**: Sử dụng GPT-4o-mini để viết tin nhắn chuẩn chỉnh dưới 160 ký tự, không chào hỏi rườm rà, không emoji, đi thẳng vào trọng tâm (Tiêu đề, thời gian, địa điểm).
- **Nhận tin qua SMS tiện lợi**: Gửi trực tiếp tin nhắn SMS về số điện thoại cá nhân (hỗ trợ số US) thông qua cổng Alive5.
- **Xử lý từng sự kiện tuần tự**: Dù có 1 hay 5 cuộc họp, hệ thống sẽ lần lượt gửi từng tin nhắn riêng biệt cho mỗi cuộc hẹn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Calendar Account**: Tài khoản Google để kết nối và lấy lịch họp.
- **OpenAI API Key**: Để sử dụng mô hình GPT-4o-mini viết nội dung SMS.
- **Alive5 Account**: Tài khoản Alive5 có tích hợp SMS (hỗ trợ số điện thoại US theo chuẩn E.164).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn hoặc tải file JSON, sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:

- **1. Schedule — Daily 9 AM**: 
  - Node này chạy mặc định lúc 9:00 sáng mỗi ngày (Cron: `0 9 * * *`). Các sếp có thể chỉnh lại giờ nếu muốn nhận tin sớm hoặc muộn hơn.
- **2. Google Calendar — Get Today's Meetings**: 
  - Kết nối tài khoản Google Calendar qua **OAuth2 credential**.
  - Thay thế `YOUR_CALENDAR_ID` thành `primary` hoặc chọn trực tiếp lịch chính của các sếp từ menu thả xuống.
- **3. Loop — Each Meeting (`splitInBatches`)**: 
  - Node này giúp lặp qua từng sự kiện lấy được. Không cần cấu hình phức tạp, nó sẽ tự động chạy vòng lặp.
- **4. Set — Extract Meeting Details**: 
  - Trích xuất các trường dữ liệu quan trọng như tiêu đề, thời gian, địa điểm, thời lượng và số lượng người tham dự từ JSON của lịch.
- **5. OpenAI — Generate SMS Text**: 
  - Kết nối **OpenAI API Key credential**.
  - Node này sử dụng `gpt-4o-mini` kèm theo hệ thống quy tắc ngầm (không chào hỏi, không emoji, dưới 160 ký tự) để tạo ra nội dung SMS tự nhiên nhất.
- **6. Alive5 — Send SMS**: 
  - Kết nối **Alive5 credential**.
  - Thay thế `+1XXXXXXXXXX` bằng số điện thoại nhận tin nhắn của các sếp (định dạng E.164, ví dụ: `+14155551234`). Lưu ý Alive5 hiện tại tối ưu tốt cho đầu số US.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test step** hoặc **Execute Workflow** để chạy thử với dữ liệu thực tế xem SMS có gửi về điện thoại không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin**: Ngoài Alive5 gửi SMS, các sếp có thể kết hợp thêm node Telegram hoặc Slack để nhận bản tổng hợp lịch họp ngay trên ứng dụng chat.
- **Tùy biến giọng văn AI**: Sửa đổi System Prompt trong node OpenAI nếu các sếp thích phong cách hài hước hơn hoặc muốn chèn thêm một số emoji sinh động.
- **Lưu log vào Google Sheets**: Thêm một bước ghi lại lịch sử các tin nhắn đã gửi vào bảng Google Sheets để tiện theo dõi.

### 📌 Kết luận
Một workflow cực kỳ gọn nhẹ nhưng mang lại hiệu suất cao cho những ai bận rộn. Hãy cài đặt ngay để không bao giờ bỏ lỡ bất kỳ cuộc họp quan trọng nào trong ngày nhé các sếp!