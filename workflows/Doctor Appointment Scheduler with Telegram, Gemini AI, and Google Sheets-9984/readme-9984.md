---
title: "🚀 Xây dựng Trợ lý AI Đặt Lịch Khám Bệnh qua Telegram với Gemini và Google Sheets"
description: "Tự động hóa toàn bộ quy trình đặt lịch khám bác sĩ qua Telegram sử dụng AI Agent, Google Gemini và Google Sheets mà không cần viết code."
slug: "tro-ly-ai-dat-lich-kham-benh-telegram-gemini"
tags: [n8n, automation, no-code, ai-agent, telegram, google-sheets, gemini]
keywords: [n8n workflow, chatbot đặt lịch khám, telegram bot ai, google gemini n8n, tự động hóa n8n]
---

# 🚀 Tự động hóa Đặt lịch Khám Bệnh thông minh qua Telegram với AI Agent & Google Sheets

Các sếp có đang gặp tình trạng phòng khám, bệnh viện hoặc dịch vụ y tế cá nhân ngập đầu vì tin nhắn hỏi lịch khám của bệnh nhân? Việc nhân viên phải túc trực trả lời khung giờ trống, kiểm tra lịch hẹn thủ công trên Excel và xác nhận lại rất dễ dẫn đến nhầm lẫn, trùng lịch hoặc bỏ sót khách hàng.

Giải pháp đây rồi! Bài viết này sẽ hướng dẫn các sếp thiết lập một **Trợ lý AI Đặt lịch Khám bệnh** tự động 100% trên **Telegram**. Trợ lý này tích hợp **Google Gemini AI**, có khả năng trò chuyện tự nhiên (cả văn bản và tin nhắn thoại), tự động tra cứu thông tin bác sĩ, kiểm tra lịch trống và ghi nhận lịch hẹn trực tiếp vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi 24/7 tức thì**: Bệnh nhân nhắn tin bất kể ngày đêm, AI tiếp nhận và xử lý ngay lập tức.
- **Hỗ trợ tin nhắn thoại (Voice Note)**: Bệnh nhân có thể gửi audio, AI sẽ tự động phiên âm (transcribe) và hiểu ý định.
- **Đồng bộ Google Sheets thông minh**: Tự động check lịch trống, tránh trùng lặp khung giờ và ghi nhận lịch hẹn mới chính xác.
- **Thông minh như người thật**: Sử dụng Gemini AI để tư vấn chuyên khoa, chi phí khám và lịch làm việc của từng bác sĩ (Dr. Karan Singh, Dr. Arjun Mehta...).
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua [@BotFather](https://t.me/BotFather)).
- **Google Gemini API Key** (Google AI Studio).
- **Google Sheets** chứa dữ liệu mẫu về thông tin bác sĩ và lịch hẹn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy file JSON của workflow hoặc import trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 16 nodes kết hợp linh hoạt giữa Telegram, Google Gemini và Google Sheets. Các sếp cần cấu hình các điểm cốt lõi sau:

- **Telegram Trigger & Send nodes (`Telegram Trigger`, `Send a text message`, `Send a chat action`, `Get a file`)**:
  - Kết nối với `telegramApi` credentials bằng Bot Token của các sếp.
  - Node `Telegram Trigger` sẽ nhận tin nhắn từ người dùng.
- **Google Gemini & Chat Model (`Google Gemini Chat Model`, `Transcribe a recording`)**:
  - Cấu hình credentials `googlePalmApi` bằng Google Gemini API Key.
  - Node `Transcribe a recording` dùng để chuyển đổi file âm thanh (giọng nói của bệnh nhân gửi qua Telegram) thành văn bản để AI xử lý.
- **AI Agent & Memory (`AI Agent`, `Simple Memory`)**:
  - Đóng vai trò bộ não điều phối, giữ ngữ cảnh hội thoại (`Simple Memory`) giúp bệnh nhân có thể trao đổi qua lại mượt mà.
- **Google Sheets Tools (`Doctor_Info`, `Dr Karan Singh`, `Dr Arjun Mehta`, `Dr Karan Singh Append Row`, `Dr Arjun Mehta Append Row`)**:
  - Kết nối `googleSheetsOAuth2Api`.
  - Liên kết với file Google Sheets của các sếp theo schema chuẩn:
    - **Schema Doctor_Info**: `Doctor name` | `Department` | `Fees`
    - **Schema Doctor Scheduler** (cho từng bác sĩ): `Doctor Name` | `Patient Name` | `Booked Date` | `Booked Time`
- **Switch & Edit Fields (`Switch`, `Edit Fields`, `Edit Fields1`)**:
  - Xử lý phân loại luồng dữ liệu đầu vào (tin nhắn văn bản hay file âm thanh) trước khi đẩy vào AI Agent.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một tin nhắn tới bot Telegram của các sếp (ví dụ: *"Tôi muốn đặt lịch khám với bác sĩ Karan Singh vào ngày mai lúc 10h sáng"*).
- Kiểm tra xem AI đã phản hồi chính xác và dữ liệu đã được ghi vào Google Sheets chưa.
- Nếu mọi thứ mượt mà, gạt nút **Active** để đưa bot vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi email/SMS xác nhận**: Thêm node Gmail hoặc Twilio sau bước "Append Row" để gửi phiếu khám bệnh tự động cho bệnh nhân.
- **Thông báo cho bác sĩ/Lễ tân**: Thêm một node Telegram gửi tin nhắn về group nội bộ của phòng khám mỗi khi có lịch hẹn mới thành công.
- **Xử lý nhắc lịch (Reminder)**: Kết hợp Schedule Trigger để quét Google Sheets hàng ngày và gửi tin nhắn nhắc nhở bệnh nhân trước giờ hẹn 2 tiếng.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một hệ thống đặt lịch khám tự động chuẩn AI với chi phí gần như bằng 0. Hãy triển khai ngay để tối ưu hóa vận hành và mang lại trải nghiệm chuyên nghiệp nhất cho khách hàng của mình nhé!