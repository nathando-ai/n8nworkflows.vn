---
title: "🚀 Tự động tóm tắt email Gmail gửi thẳng vào Telegram bằng OpenAI GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt email mới từ Gmail, sử dụng AI tóm tắt thông minh và gửi thông báo trực tiếp qua Telegram."
slug: "tu-dong-tom-tat-email-gmail-gui-telegram-openai"
tags: [n8n, automation, gmail, telegram, openai, ai-agent]
keywords: [n8n workflow, tóm tắt email gmail, openai gpt-4o, telegram automation, tự động hóa n8n]
---

# 🚀 Tự động tóm tắt email Gmail gửi thẳng vào Telegram bằng OpenAI GPT-4o

Các sếp có đang cảm thấy mệt mỏi mỗi khi mở hộp thư đến và thấy hàng tá email dài dằng dặc, email quảng cáo, hay những thông báo công việc rườm rà? Việc đọc thủ công từng email không chỉ ngốn rất nhiều thời gian mà còn khiến các sếp dễ bỏ lỡ các thông tin cốt lõi trong lúc di chuyển.

Giải pháp là đây! Workflow n8n này sẽ đóng vai trò như một thư ký AI riêng biệt: tự động theo dõi hộp thư Gmail, dùng sức mạnh của AI (OpenAI GPT-4o-mini) để chắt lọc những ý chính, và bắn thẳng bản tóm tắt súc tích vào Telegram cá nhân của các sếp ngay lập tức. 100% tự động, không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không cần đọc toàn bộ email dài, chỉ cần nắm bắt nội dung chính qua Telegram trong vài giây.
- **Không bỏ lỡ thông tin quan trọng:** Nhận thông báo tức thì ngay khi có email mới đến hộp thư.
- **Cá nhân hóa linh hoạt:** Dễ dàng thay đổi ngôn ngữ tóm tắt (Tiếng Việt, tiếng Anh...), giọng văn hoặc thậm chí đổi sang các mô hình AI khác (Claude, DeepSeek).
- **Hoạt động 24/7:** Chạy ngầm liên tục trên n8n mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản Gmail:** Có quyền kết nối OAuth2 để đọc email đến.
- **Telegram Bot:** Đã tạo sẵn Bot qua `@BotFather` và lấy được Chat ID của các sếp.
- **OpenAI API Key:** Tài khoản OpenAI có đủ số dư để gọi model GPT-4o-mini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **New** -> **Import from Clipboard** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:

- **Node `When a new email arrives` (Gmail Trigger):** 
  - Kết nối tài khoản Gmail của các sếp thông qua `gmailOAuth2`.
  - Chọn tài khoản email cần theo dõi.
- **Node `Set summary language` (Set):** 
  - Nơi cấu hình ngôn ngữ trả về. Các sếp có thể đặt giá trị là `Tiếng Việt` để AI luôn tóm tắt bằng tiếng mẹ đẻ cho dễ đọc.
- **Node `OpenAI Model` (OpenAI Chat Model):** 
  - Thêm `openAiApi` credentials của các sếp.
  - Model mặc định là `gpt-4o-mini` (nhanh, tiết kiệm và thông minh). Các sếp có thể đổi sang model khác nếu muốn.
- **Node `Summary generation agent` (AI Agent):** 
  - Node trung tâm điều phối, nhận nội dung email và ngôn ngữ yêu cầu để tiến hành tóm tắt.
- **Node `Send summary to Telegram` (Telegram):** 
  - Thêm `telegramApi` credentials (Token của Bot).
  - Điền **Chat ID** của các sếp vào ô cấu hình để bot biết gửi tin nhắn về đâu (có thể lấy Chat ID bằng cách nhắn tin với bot `@userinfobot` trên Telegram).

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** và gửi một email thử nghiệm đến tài khoản Gmail để kiểm tra kết quả.
- Nếu mọi thứ hoạt động mượt mà, hãy gạt nút **Active** ở góc trên bên phải để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi nhà cung cấp AI:** Nếu không thích OpenAI, các sếp có thể thay thế node `OpenAI Model` bằng Anthropic Claude hoặc DeepSeek một cách dễ dàng.
- **Phân loại email:** Kết hợp thêm logic rẽ nhánh (If Node) để chỉ tóm tắt các email có chứa từ khóa quan trọng (như "Hợp đồng", "Thanh toán", "Khẩn cấp") để tránh bị spam thông báo.
- **Lưu lịch sử:** Bổ sung thêm node Google Sheets hoặc Notion để lưu lại toàn bộ các bản tóm tắt email nhằm tra cứu về sau.

### 📌 Kết luận
Một workflow cực kỳ nhỏ gọn nhưng mang lại hiệu suất vượt trội cho dân văn phòng, lập trình viên hay các nhà quản lý thường xuyên bận rộn. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa thời gian xử lý email từ hôm nay!