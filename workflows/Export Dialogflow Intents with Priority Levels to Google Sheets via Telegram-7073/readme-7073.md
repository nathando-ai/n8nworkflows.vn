---
title: "🚀 Xuất Intent Dialogflow kèm Mức độ Ưu tiên vào Google Sheets qua Telegram"
description: "Tự động hóa quy trình backup và quản lý Intent từ Dialogflow, phân loại theo mức ưu tiên và lưu trữ trực tiếp vào Google Sheets thông qua bot Telegram cực kỳ tiện lợi."
slug: "xuat-dialogflow-intents-google-sheets-telegram"
tags: [n8n, automation, no-code, dialogflow, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa dialogflow, backup intents google sheets, bot telegram n8n, quản lý chatbot]
---

# 🚀 Tự động Backup Dialogflow Intents vào Google Sheets qua Telegram

Việc quản lý và kiểm tra hàng loạt **Intent** trong chatbot Dialogflow thủ công thường tốn rất nhiều thời gian, đặc biệt khi cần đánh giá mức độ ưu tiên để tối ưu hóa trải nghiệm người dùng. 

Giải pháp? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: chỉ cần gửi một lệnh qua Telegram, hệ thống sẽ tự động quét toàn bộ Intent từ Dialogflow, phân loại mức độ ưu tiên kèm emoji sinh động, lưu trữ gọn gàng vào Google Sheets và gửi tin nhắn báo cáo kết quả ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần truy cập vào Dialogflow Console phức tạp để kiểm tra thủ công.
- **Phân loại thông minh:** Tự động gán mức ưu tiên (Highest, High, Normal, Low, Ignore) kèm biểu tượng trực quan.
- **Bảo mật và kiểm soát:** Tích hợp xác thực ID người dùng và câu lệnh bảo mật (`backup`).
- **Báo cáo tức thì:** Nhận ngay thông báo xác nhận qua Telegram ngay khi quá trình hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Google Sheets** đã tạo sẵn file và cấu hình cột (Intent Name, Priority, Timestamp...).
- **Dialogflow Agent** và quyền truy cập API/Credentials tương ứng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc copy trực tiếp mã nguồn JSON, sau đó dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với hệ thống của các sếp, hãy chú ý cấu hình các node sau:
- **Telegram Trigger**: Kết nối với Telegram Bot Credentials của các sếp để lắng nghe tin nhắn đến.
- **Validación de usuario por ID** (Node IF): Thay thế chuỗi ID mặc định bằng Telegram User ID thực tế của các sếp để giới hạn quyền truy cập bot.
- **Validación del comando** (Node IF): Thiết lập từ khóa kích hoạt (mặc định là từ **"backup"**).
- **Obtiene datos de los intents** (Node HTTP Request): Cấu hình Endpoint và thông tin xác thực API của Dialogflow Agent.
- **Mapear intents con su prioridad** (Node Code): Xử lý JSON trả về từ Dialogflow để trích xuất `displayName`, `priority` và gắn nhãn ưu tiên:
  - 🔴 Highest
  - 🟠 High
  - 🔵 Normal
  - 🟢 Low
  - 🚫 Ignore
- **Añadir fila en la hoja** (Node Google Sheets): Chọn đúng tài liệu Google Sheet và Sheet Name để lưu dữ liệu.
- **Mensaje de confirmación** (Node Telegram): Đảm bảo cấu hình tùy chọn `Execute Once` để tin nhắn tổng kết chỉ gửi đi một lần duy nhất.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách gửi tin nhắn chứa từ khóa `backup` tới bot Telegram.
- Kiểm tra dữ liệu đổ về Google Sheets và thông báo trả về.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Có thể bổ sung thêm node gửi thông báo về kênh/group Telegram nội bộ của team thay vì chỉ chat cá nhân.
- **Lịch chạy tự động (Cron):** Thay vì dùng Telegram Trigger, các sếp có thể kết hợp thêm node `Schedule Trigger` để hệ thống tự động backup hàng tuần/hàng tháng mà không cần gõ lệnh.
- **Lưu log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để cảnh báo kịp thời nếu API Dialogflow hoặc Google Sheets gặp sự cố kết nối.

### 📌 Kết luận
Workflow này là một công cụ cực kỳ hữu ích giúp các nhà phát triển chatbot và đội ngũ vận hành tiết kiệm hàng giờ thao tác thủ công. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý dự án chatbot của các sếp!