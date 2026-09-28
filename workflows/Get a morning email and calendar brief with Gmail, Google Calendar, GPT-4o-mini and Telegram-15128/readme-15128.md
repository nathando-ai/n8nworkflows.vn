---
title: "🚀 Tự động hóa bản tin buổi sáng thông minh với Gmail, Google Calendar, GPT-4o-mini và Telegram"
description: "Xây dựng workflow n8n tự động tổng hợp email chưa đọc và lịch trình trong ngày, sử dụng AI lọc nhiễu và gửi bản tóm tắt sắc nét qua Telegram mỗi 8 giờ sáng."
slug: "tu-dong-hoa-ban-tin-buoi-sang-gmail-calendar-gpt-telegram"
tags: [n8n, automation, ai-agent, openai, telegram, productivity]
keywords: [n8n workflow, tóm tắt buổi sáng tự động, gpt-4o-mini telegram, tự động hóa gmail calendar]
---

# 🚀 Tự động hóa bản tin buổi sáng thông minh với Gmail, Google Calendar, GPT-4o-mini & Telegram

Các sếp có bao giờ cảm thấy mệt mỏi mỗi sáng thức dậy phải mở liền lúc chục tab: kiểm tra hộp thư rác ngập tràn email quảng cáo, soi lịch họp hôm nay và chuẩn bị cho ngày mai? Việc này ngốn không ít năng lượng trước khi ngày làm việc thực sự bắt đầu.

Giải pháp ở đây là để n8n lo! Workflow này tự động hóa 100% quy trình: gom email chưa đọc trong 24 giờ qua, lấy lịch hẹn hôm nay và ngày mai, đưa qua "bộ lọc thần thánh" **GPT-4o-mini** để loại bỏ rác, và gửi một bản tin (brief) siêu gọn gàng thẳng vào **Telegram** cá nhân của các sếp đúng 8h sáng các ngày trong tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian vàng:** Nắm bắt toàn bộ bức tranh công việc trong ngày chỉ với 1 tin nhắn duy nhất trên Telegram trước khi mở bất kỳ ứng dụng nào.
- **AI thông minh lọc nhiễu:** GPT-4o-mini tự động loại bỏ email quảng cáo, thông báo rác, chỉ giữ lại các email thực sự khẩn cấp.
- **Chuẩn bị trước cho ngày mai:** Không chỉ tóm tắt hôm nay, hệ thống còn nhắc nhở lịch hẹn và các việc cần chuẩn bị cho ngày mai.
- **Hoạt động tự động 24/7:** Chạy mượt mà vào mỗi sáng từ thứ Hai đến thứ Sáu mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google:** Quyền truy cập Gmail và Google Calendar (OAuth2).
- **Tài khoản OpenAI:** API Key có tích hợp model `gpt-4o-mini`.
- **Telegram Bot:** Tạo một Bot thông qua `@BotFather` và lấy Telegram Chat ID cá nhân thông qua `@userinfobot`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy/paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình lần lượt các node sau:

- **2. Set — Config Values:** Điền chính xác các thông số cá nhân hóa:
  - `PASTE_YOUR_TELEGRAM_CHAT_ID_HERE`: ID Telegram của sếp.
  - `PASTE_YOUR_GMAIL_ADDRESS_HERE`: Địa chỉ Gmail cá nhân/công việc.
  - `PASTE_YOUR_NAME_OR_COMPANY_HERE`: Tên hoặc tên doanh nghiệp của sếp.
  - Cấu hình múi giờ (Ví dụ: `Asia/Ho_Chi_Minh`, `Asia/Kolkata`, `America/New_York`).
- **3. Gmail — Fetch Unread Emails:** Kết nối tài khoản Gmail qua OAuth2 để node thực hiện lệnh lấy các email chưa đọc trong 24 giờ qua.
- **4. Google Calendar — Fetch Today and Tomorrow:** Kết nối Google Calendar OAuth2 để lấy toàn bộ sự kiện lịch trong ngày hôm nay và ngày mai.
- **7. OpenAI — GPT-4o-mini Model:** Kết nối OpenAI Credential và đảm bảo chọn đúng model `gpt-4o-mini`.
- **9. Telegram — Send Morning Brief:** Kết nối Telegram Bot API Credential để bot có quyền gửi tin nhắn vào tài khoản của sếp.

*💡 Mẹo nhỏ:* Trước khi chạy lần đầu, hãy mở ứng dụng Telegram, tìm đến con bot vừa tạo và nhắn `/start` để kích hoạt kết nối chat.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thử nghiệm dữ liệu mẫu xem tin nhắn có bắn về Telegram mượt mà không.
- Nếu mọi thứ hiển thị đẹp đẽ, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy vào 8h sáng mỗi ngày!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Telegram, các sếp có thể nhân bản node cuối để đẩy đồng thời bản tin này lên **Slack** hoặc **Discord** nhóm dự án.
- **Lưu trữ Log Notion/Google Sheets:** Thêm một node Google Sheets hoặc Notion để lưu lại lịch sử các bản brief mỗi ngày nhằm phục vụ việc review công việc cuối tuần.
- **Tùy chỉnh Prompt AI:** Tại node **6. AI Agent — Write Morning Brief**, các sếp có thể tinh chỉnh system prompt để AI dùng giọng điệu hài hước, nghiêm túc hoặc tập trung sâu vào một lĩnh vực cụ thể (như tài chính, Sales, Tech...).

### 📌 Kết luận
Một khởi đầu ngày mới hoàn hảo bắt đầu từ việc kiểm soát thông tin chứ không để thông tin kiểm soát bạn. Hãy cài đặt ngay workflow này để tối ưu hóa năng suất cá nhân và giải phóng thời gian cho các quyết định quan trọng hơn, các sếp nhé!