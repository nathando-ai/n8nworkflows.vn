---
title: "🚀 Tự động tạo bản tóm tắt cuộc họp AI từ Google Calendar với SerpAPI, Azure OpenAI và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động nghiên cứu thông tin người tham dự họp qua SerpAPI, tổng hợp bằng Azure OpenAI và gửi báo cáo qua Slack trước giờ G."
slug: "tu-dong-tom-tat-cuoc-hop-ai-google-calendar-serpapi-azure-openai-slack"
tags: [n8n, automation, no-code, google-calendar, azure-openai, slack]
keywords: [n8n workflow, tự động hóa cuộc họp, AI meeting brief, serpapi azure openai, slack automation]
---

# 🚀 Tự động tạo bản tóm tắt cuộc họp AI từ Google Calendar với SerpAPI, Azure OpenAI và Slack

Mỗi khi có lịch họp mới xuất hiện trên Google Calendar, các sếp thường phải mất thời gian tra cứu Google, tìm hiểu thông tin về đối tác, khách hàng hoặc công ty của họ để chuẩn bị nội dung trao đổi. Việc làm thủ công này vừa tốn thời gian, vừa dễ bỏ sót các thông tin quan trọng.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: **Phát hiện lịch họp mới ➔ Nghiên cứu thông tin cá nhân và công ty qua SerpAPI ➔ Tổng hợp và phân tích bằng AI (Azure OpenAI) ➔ Gửi bản tóm tắt (briefing) trực tiếp qua Slack** ngay trước khi cuộc họp diễn ra. Các sếp sẽ luôn ở thế chủ động trong mọi cuộc gặp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Không cần tự tay search Google, LinkedIn hay tìm hiểu website đối tác trước mỗi cuộc họp.
- **Chuẩn bị kỹ lưỡng:** AI tự động cô đọng thông tin về background, vai trò và bối cảnh công ty của người tham dự thành một bản tóm tắt ngắn gọn.
- **Tương tác nhanh chóng qua Slack:** Nhận thông tin trực tiếp qua tin nhắn cá nhân (DM) trên Slack một cách mượt mà.
- **Hoạt động tự động 24/7:** Lắng nghe lịch sự kiện liên tục, chỉ xử lý các cuộc họp có khách mời thực tế và bỏ qua các sự kiện nội bộ trống.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Calendar Credentials** (OAuth2) để theo dõi lịch hẹn.
- **SerpAPI Account & API Key** để thực hiện tìm kiếm Google tự động.
- **Azure OpenAI Credentials** (với model `gpt-4o-mini` hoặc tương tự) để AI phân tích và viết tóm tắt.
- **Slack App / Credentials** (OAuth2) và Member ID của sếp để nhận tin nhắn DM.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **New Calendar Event Trigger:** Kết nối tài khoản Google Calendar qua OAuth2 và chọn đúng Calendar ID cần theo dõi. Node này sẽ quét lịch hẹn mỗi phút một lần.
- **Filter: Has Attendees & Extract Attendee & Company Info:** Node `Set` (`Extract Attendee & Company Info`) cần được tùy chỉnh lại để trích xuất đúng tên người tham dự và công ty từ tiêu đề hoặc mô tả sự kiện (tùy thuộc vào cách các sếp đặt lịch).
- **Search Person on Google & Search Company on Google (`SerpAPI`):** Điền SerpAPI Key vào cả hai node này. *Lưu ý:* Tránh lạm dụng với lịch họp quá dày đặc vì sẽ làm tiêu tốn hạn mức (quota) API hàng tháng của SerpAPI.
- **AI Meeting Briefing Agent & Azure OpenAI Chat Model1 (`Azure OpenAI`):** Kết nối Azure OpenAI credentials. Đảm bảo cấu hình deployment model là `gpt-4o-mini`. Prompt trong Agent sẽ kết hợp dữ liệu từ cả 2 nhánh tìm kiếm để tạo ra bản tóm tắt ngắn gọn.
- **Send Briefing via Slack DM (`Slack`):** Kết nối Slack OAuth2 credentials. **Đặc biệt lưu ý:** Thay thế `YOUR_SLACK_USER_ID` thành Member ID thực tế của sếp trên Slack (định dạng dạng `U0XXXXXXX`). Nếu để nguyên, tin nhắn sẽ không thể gửi đi.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và tạo một sự kiện lịch giả lập để test dữ liệu chạy qua từng node.
- Kiểm tra xem tin nhắn Slack đã bắn về tài khoản cá nhân chính xác chưa.
- Bật công tắc **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Thêm nhánh thứ ba gọi SerpAPI tìm kiếm profile LinkedIn của khách mời để AI có bức tranh toàn diện hơn về lịch sử công việc.
- **Gợi ý câu hỏi/Chủ đề (Talking Points):** Tinh chỉnh System Prompt trong AI Agent để yêu cầu đưa ra 3 câu hỏi gợi mở hoặc chủ đề phá băng (ice-breaker) phù hợp với lĩnh vực của đối tác.
- **Lưu lịch sử:** Bổ sung một node Google Sheets hoặc Airtable cuối luồng để lưu trữ toàn bộ lịch sử các buổi gặp và tóm tắt AI để tiện tra cứu sau này.

### 📌 Kết luận
Workflow "Get AI meeting briefs from Google Calendar with SerpAPI, Azure OpenAI and Slack" là trợ lý ảo hoàn hảo cho các nhà quản lý, sales và founder bận rộn. Hãy cài đặt ngay hôm nay để mỗi cuộc họp đều bắt đầu với sự chuẩn bị chuyên nghiệp nhất!