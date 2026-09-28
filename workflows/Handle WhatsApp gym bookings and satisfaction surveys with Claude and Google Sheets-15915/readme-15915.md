---
title: "🚀 Tự động hóa Đặt lịch Phòng Gym & Khảo sát hài lòng qua WhatsApp với Claude AI & n8n"
description: "Xây dựng hệ thống chatbot WhatsApp thông minh cho phòng gym bằng n8n, Claude AI và Google Sheets, hỗ trợ đặt lịch, hủy lịch, xử lý tin nhắn thoại và khảo sát tự động."
slug: "tu-dong-hoa-dat-lich-gym-whatsapp-claude-ai-n8n"
tags: [n8n, automation, whatsapp, ai-agent, google-sheets, claude-ai]
keywords: [n8n workflow, whatsapp chatbot gym, tự động hóa phòng gym, claude ai n8n, google sheets booking]
---

# 🚀 Tự động hóa Đặt lịch Phòng Gym & Khảo sát hài lòng qua WhatsApp với Claude AI

Các chủ phòng gym và trung tâm thể hình thường đau đầu với việc xử lý tin nhắn đặt lịch, hủy lịch, giải đáp câu hỏi (FAQ) thủ công tốn hàng giờ đồng hồ mỗi ngày trên điện thoại. Việc bỏ lỡ tin nhắn khách hàng đồng nghĩa với việc mất đi doanh thu.

Giải pháp? Biến chiếc WhatsApp thành một trợ lý AI thông minh hoạt động 24/7. Workflow n8n này giúp tự động hóa toàn bộ quy trình chăm sóc khách hàng và đặt lịch qua WhatsApp mà không cần tốn tiền cho các phần mềm quản lý đắt đỏ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý tin nhắn realtime ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Khách hàng nhắn tin bằng ngôn ngữ tự nhiên (tiếng Anh, Ả Rập, Pháp...), AI sẽ tự hiểu và thao tác đặt/hủy lịch tập.
- **Xử lý tin nhắn thoại thông minh:** Tự động chuyển đổi tin nhắn voice note thành văn bản nhờ OpenAI Whisper.
- **Lưu trữ chủ động:** Toàn bộ dữ liệu hội viên, lịch đặt, trạng thái phiên làm việc đều lưu trực tiếp vào Google Sheets của các sếp.
- **Khảo sát tự động:** Gửi khảo sát độ hài lòng đến hội viên và nhận thông báo tức thì khi có phản hồi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (Cloud Starter hoặc Self-hosted)
- Tài khoản **UltraMsg** (nhận và gửi tin nhắn WhatsApp qua Webhook)
- **Anthropic API Key** (sử dụng model Claude Haiku)
- **OpenAI API Key** (dùng cho tính năng chuyển đổi giọng nói Whisper)
- **Google Sheets** (Lưu cấu hình, dữ liệu hội viên, trạng thái phiên)
- **Google Calendar** (Tạo lịch tự động cho các chi nhánh)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và paste toàn bộ JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Webhook Node**: Cấu hình URL trỏ từ tài khoản UltraMsg của sếp về webhook path `gymbot/conversation` trên n8n.
- **Anthropic Chat Model Node**: Chọn credentials API Key của Anthropic và đảm bảo model đang trỏ đúng `Claude Haiku`.
- **Transcribe (Whisper) Node**: Cấu hình OpenAI Credentials để xử lý tin nhắn âm thanh từ khách hàng.
- **Google Sheets Nodes (Lookup Session, Read Active Members, Read Config...)**: Kết nối tài khoản Google Sheets cá nhân, trỏ đến bảng tính quản lý phòng gym của sếp (bao gồm các sheet cấu hình `Gymbot_Config`, `Session_State`, `Members`).

#### 3. Kích hoạt ⚡️
- Gửi một tin nhắn thử nghiệm qua WhatsApp đến số cấu hình UltraMsg để kiểm tra log.
- Bật công tắc **Active** góc trên cùng bên phải để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo nội bộ:** Tích hợp thêm node Telegram hoặc Slack để gửi cảnh báo ngay cho quản lý khi khách hàng phàn nàn hoặc hủy lịch phút chót.
- **Tự động hóa Unanswered QA:** Các câu hỏi AI không trả lời được sẽ tự động lưu vào sheet riêng, giúp các sếp cập nhật thêm FAQ hàng tuần.
- **Mở rộng Sub-workflows:** Đảm bảo các tool sub-workflows phụ (Create Booking, Cancel Booking, FAQ...) đã được import và active đầy đủ trước khi chạy AI Agent chính.

### 📌 Kết luận
Hệ thống GymBot Pro trên n8n là vũ khí tối thượng giúp các phòng gym tiết kiệm nhân sự trực chat, tối ưu hóa trải nghiệm hội viên và gia tăng tỷ lệ giữ chân khách hàng một cách tự động. Lên đồ và áp dụng ngay hôm nay thôi các sếp!