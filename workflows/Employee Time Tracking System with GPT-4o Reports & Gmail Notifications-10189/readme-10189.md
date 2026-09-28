---
title: "🚀 Xây dựng Hệ thống Chấm công Nhân viên Tự động với GPT-4o và Gmail"
description: "Tự động hóa toàn bộ quy trình chấm công, tính giờ làm việc, phân tích báo cáo bằng AI GPT-4o và gửi thông báo qua Gmail hoàn toàn không cần code."
slug: "he-thong-cham-cong-nhan-vien-gpt4o-gmail"
tags: [n8n, automation, hr, openai, gmail, no-code]
keywords: [n8n workflow, chấm công tự động, time tracking n8n, openai gpt-4o hr, tự động hóa nhân sự]
---

# 🚀 Xây dựng Hệ thống Chấm công Nhân viên Tự động với GPT-4o và Gmail

Việc quản lý thời gian làm việc, chấm công (Check-in/Check-out), tính toán giờ nghỉ giải lao (Break) và tổng hợp báo cáo nhân sự thủ công thường tốn rất nhiều thời gian của bộ phận HR và quản lý. Thậm chí, sai sót trong bảng lương hay báo cáo tháng rất dễ xảy ra. 

Giải pháp? Workflow n8n siêu việt này do chuyên gia **Jose Castillo** xây dựng sẽ giúp các sếp thiết lập một **Hệ thống Chấm công Tự động 100%**. Hệ thống tích hợp Webhook để nhận dữ liệu chấm công thời gian thực, sử dụng **OpenAI (GPT-4o)** để phân tích hiệu suất làm việc theo ngày/tháng, kết hợp **n8n Data Table** lưu trữ dữ liệu và tự động gửi email báo cáo chi tiết qua **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chấm công liền mạch:** Nhân viên có thể gửi dữ liệu check-in/check-out/break trực tiếp thông qua Webhook API một cách nhanh chóng.
- **Báo cáo thông minh bằng AI:** Sử dụng sức mạnh của GPT-4o để tổng hợp, phân tích thời gian làm việc hàng ngày và toàn bộ tháng một cách chuyên nghiệp.
- **Tự động hóa thông báo:** Tự động gửi email thông báo kết quả, nhắc nhở hoặc báo cáo cho cả nhân viên và ban quản lý qua Gmail.
- **Lưu trữ chuẩn chỉnh:** Quản lý toàn bộ dữ liệu chấm công tự động trên n8n Data Table mà không cần phụ thuộc vào Google Sheets phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance:** Đã cài đặt n8n (khuyến nghị bản Self-hosted hoặc n8n Cloud).
- **OpenAI API Key:** Để kết nối với node AI phân tích báo cáo (`Message a model`, `Message a model1`).
- **Gmail Account / Credentials:** Tài khoản Gmail được cấu hình OAuth2 để gửi email tự động qua node `EMAIL TO EMPLOYEE` và `EMAIL TO MANAGEMENT`.
- **n8n Data Table:** Các bảng dữ liệu (Data Table) được thiết lập sẵn trong n8n để hứng dữ liệu chấm công (`Get row(s)`, `Insert row`, `Update row(s)`...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó dán trực tiếp vào giao diện n8n Editor (hoặc Import file JSON thông qua menu tuỳ chọn của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các thành phần sau để hệ thống chạy mượt mà:
- **Webhook - Track Time:** Cấu hình đường dẫn endpoint (`path: track-time`) để hệ thống ngoài (như App nội bộ, Bot Telegram, Web form) gửi request `POST` ghi nhận thời gian chấm công.
- **Switch & Set Break Duration:** Tùy chỉnh các nhánh logic (Check-in, Break, Check-out, End) và thời gian nghỉ giải lao mặc định cho phù hợp với nội quy công ty.
- **n8n Data Tables (Các node Get/Insert/Update row):** Liên kết chính xác với các bảng dữ liệu (Data Table) lưu trữ thông tin nhân sự và lịch sử chấm công trong n8n của các sếp.
- **OpenAI Nodes (`Message a model` & `Message a model1`):** Kết nối thông tin OpenAI API Credentials, kiểm tra lại system prompt để đảm bảo GPT-4o trả về định dạng báo cáo tiếng Việt rõ ràng, mạch lạc.
- **Gmail Nodes (`EMAIL TO EMPLOYEE` & `EMAIL TO MANAGEMENT`):** Chọn OAuth2 Credentials của Gmail, thiết lập người nhận (Dynamic từ dữ liệu chấm công) và nội dung email thông báo lấy từ các node `MESSAGE`, `MESSAGE1`, `MESSAGE2`.
- **Schedule Triggers (`EVERY DAY` & `EVERY MONTH`):** Cài đặt khung giờ chạy định kỳ để hệ thống tự động tổng hợp báo cáo ngày và báo cáo tháng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và bắn một request `POST` giả lập vào **Webhook - Track Time** để test luồng dữ liệu.
- Kiểm tra kết quả trả về ở các node Data Table, OpenAI và Gmail xem đã chuẩn xác chưa.
- Gạt công tắc sang **Active** để chính thức đưa hệ thống vào vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack bên cạnh Gmail để bắn tin nhắn nhắc nhở chấm công (Clock-in reminder) ngay lập tức cho nhân viên.
- **Bảng điều khiển (Dashboard):** Dùng dữ liệu trong n8n Data Table để dựng một trang Dashboard mini (qua Retool hoặc Appsmith) giúp sếp theo dõi chấm công trực quan.
- **Xử lý ngoại lệ:** Thêm nhánh thông báo riêng vào node `ERROR` và `ERROR1` để cảnh báo cho quản trị viên nếu có lỗi phát sinh trong quá trình ghi nhận thời gian.

### 📌 Kết luận
Hệ thống chấm công tích hợp AI GPT-4o và Gmail này là bước tiến tuyệt vời giúp doanh nghiệp tối ưu hóa quy trình nhân sự, tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng. Hãy triển khai ngay hôm nay để đưa doanh nghiệp lên một tầm cao tự động hóa mới!