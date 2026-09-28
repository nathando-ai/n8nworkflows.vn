---
title: "🚀 Mở rộng tính năng n8n với Telegram Bot: Tích hợp Thời tiết & Chạy tập lệnh nâng cao"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Telegram Bot để tra cứu thời tiết, xử lý file và chạy mã lệnh R script tự động 100% không cần code."
slug: "mo-rong-tinh-nang-n8n-telegram-bot-thoi-tiết-r-script"
tags: [n8n, automation, no-code, telegram, workflow, api]
keywords: [n8n workflow, tự động hóa telegram, n8n telegram bot, run r script n8n, api thời tiết n8n]
---

# 🚀 Mở rộng tính năng n8n với Telegram Bot: Tích hợp Thời tiết & Chạy tập lệnh nâng cao

Các sếp có bao giờ cảm thấy các công cụ tự động hóa thông thường đôi khi bị giới hạn bởi các node có sẵn? Việc kết hợp n8n với một giao diện chat quen thuộc như **Telegram** cùng khả năng thực thi các tập lệnh phức tạp (như R script) sẽ mở ra một thế giới tự động hóa hoàn toàn mới. 

Workflow này được thiết kế bởi **Eduard** nhằm biến bot Telegram của các sếp thành một trợ lý đa năng: vừa có thể tra cứu thông tin thời tiết trực quan qua hình ảnh/dữ liệu, vừa có khả năng xử lý dữ liệu và chạy các lệnh hệ thống (Execute Command) một cách mượt mà. Tất cả được tự động hóa 100% không cần viết code cồng kềnh!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác thông minh qua Telegram:** Nhận tin nhắn chào mừng, xử lý câu lệnh sai và hiển thị trạng thái "đang xử lý" (`msg_pleasewait`) cực kỳ chuyên nghiệp.
- **Tra cứu thời tiết tự động:** Kết nối API thời tiết thông qua HTTP Request, chuyển đổi dữ liệu và gửi hình ảnh/thông tin chi tiết về thành phố qua Telegram.
- **Xử lý dữ liệu & Chạy R Script:** Tự động tạo file dữ liệu (Spreadsheet/CSV), thực thi mã lệnh phân tích qua node `Run R script` và gửi kết quả ngược lại cho người dùng.
- **Kiểm soát lỗi chặt chẽ:** Các node điều kiện (`If`) giúp phát hiện lỗi từ API hoặc quá trình chạy script để thông báo kịp thời cho người quản trị.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo một bot mới thông qua `@BotFather` trên Telegram để lấy API Token (`telegramApi` credentials).
- **Môi trường Server (cho Self-hosted):** Cài đặt sẵn R nếu các sếp muốn sử dụng tính năng chạy R script (`executeCommand`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc của tác giả Eduard (Workflow #1605) hoặc copy toàn bộ mã nguồn JSON của workflow và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Telegram Trigger & các node Telegram (`msg_greet`, `msg_wrongcommand`, `msg_getweather`, v.v.):** 
  - Cần tạo và chọn đúng **Credentials** loại `telegramApi` bằng Bot Token đã lấy từ BotFather.
  - Node `Telegram Trigger` sẽ lắng nghe các tin nhắn từ người dùng gửi đến bot.
- **Switch:** 
  - Đóng vai trò bộ định tuyến, phân loại các lệnh (commands) mà người dùng nhắn qua Telegram để chuyển đến nhánh xử lý tương ứng (ví dụ: xem thời tiết, chạy R script, hoặc báo lỗi lệnh không hợp lệ `msg_wrongcommand`).
- **Get weather data (HTTP Request):** 
  - Cấu hình endpoint API thời tiết mà các sếp muốn sử dụng. Node `Convert API response` (Function) sẽ giúp chuẩn hóa dữ liệu trả về trước khi gửi qua node `msg_getweather` (với tùy chọn `sendPhoto` hoặc tin nhắn văn bản).
- **Spreadsheet File & Write csv / Read Binary File:** 
  - Xử lý việc xuất dữ liệu dạng bảng thành file CSV hoặc đọc/ghi file nhị phân để chuẩn bị dữ liệu đầu vào cho quá trình chạy lệnh.
- **Run R script (Execute Command):** 
  - Node này thực thi câu lệnh gọi R trên server. Các sếp cần đảm bảo môi trường VPS đã cài đặt ngôn ngữ R và các thư viện cần thiết.
- **Any errors API? & R successful? (If):** 
  - Kiểm tra xem API thời tiết hoặc quá trình chạy R script có gặp lỗi hay không. Nếu có, các node `msg_errorAPI` hoặc `msg_errorR` sẽ lập tức bắn thông báo cảnh báo về Telegram cho các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhắn tin cho Telegram Bot của các sếp để test từng luồng (gửi lệnh thời tiết, lệnh sai, v.v.).
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng danh sách thành phố:** Tùy chỉnh node `City List` (Function) để thêm các thành phố mà doanh nghiệp hoặc cá nhân các sếp thường xuyên quan tâm.
- **Tích hợp thêm thông báo:** Kết hợp thêm node Slack hoặc Discord song song với Telegram để đội ngũ kỹ thuật cùng theo dõi log lỗi.
- **Lưu lịch sử:** Thêm node Google Sheets hoặc PostgreSQL để lưu lại lịch sử các câu lệnh mà người dùng đã tương tác với Bot.

### 📌 Kết luận
Việc mở rộng n8n kết hợp cùng Telegram Bot và các công cụ dòng lệnh (như R script) giúp các sếp tối ưu hóa quy trình làm việc, biến n8n không chỉ là công cụ nối API đơn thuần mà thành một trung tâm điều hành thu nhỏ. Hãy "lên đồ" ngay cho bot của các sếp và trải nghiệm sức mạnh tự động hóa này nhé!