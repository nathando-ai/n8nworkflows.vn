---
title: "🚀 Tự động hóa làm giàu thông tin LinkedIn Profile không cần tài khoản với n8n"
description: "Hướng dẫn cấu hình workflow n8n giúp quét và cập nhật thông tin LinkedIn Profile tự động vào Google Sheets bằng Ghost Genius API một cách đơn giản, không cần tài khoản phức tạp."
slug: "enrich-linkedin-profiles-ghost-genius-google-sheets"
tags: [n8n, automation, linkedin, google-sheets, ghost-genius, ai]
keywords: [n8n workflow, enrich linkedin profile, ghost genius, google sheets automation, tự động hóa linkedin]
---

# 🚀 Tự động hóa làm giàu thông tin LinkedIn Profile không cần tài khoản với n8n

Các sếp đang đau đầu vì việc phải copy/paste thủ công từng đường link LinkedIn để tìm kiếm thông tin chi tiết (chức vụ, công ty, kinh nghiệm...) phục vụ cho các chiến dịch Sales hoặc tuyển dụng? Việc làm thủ công này vừa tốn hàng giờ đồng hồ, vừa dễ xảy ra sai sót dữ liệu.

Đừng lo! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa 100%. Workflow này sẽ lấy danh sách profile từ Google Sheets, gọi API trích xuất thông tin qua **Ghost Genius** (không cần tài khoản phức tạp) và tự động cập nhật ngược lại Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh tra cứu thủ công từng profile LinkedIn.
- **Dữ liệu đồng bộ & sạch:** Thông tin trả về được cập nhật chính xác trực tiếp vào Google Sheets.
- **Hoạt động linh hoạt:** Dễ dàng kích hoạt thủ công hoặc cấu hình chạy định kỳ theo lịch trình mong muốn.
- **Không cần cấu hình phức tạp:** Sử dụng dịch vụ Ghost Genius giúp lấy dữ liệu cookieless an toàn và nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Google Cloud / Google Sheets để kết nối và lưu trữ dữ liệu.
- Tài liệu mẫu Google Sheet: [Make a copy here](https://docs.google.com/spreadsheets/d/1oiV25COrTMP20nMgNvbtMo2LHcm7ehkqOxbAB-s6PhA/edit?usp=sharing).
- Tài khoản hoặc API Endpoint từ dịch vụ LinkedIn API cookieless: [Ghost Genius](https://ghostgenius.fr).
- Video hướng dẫn gốc từ tác giả Matthieu: [Xem Video Setup tại đây](https://youtu.be/kIOJeMoCfp4).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ hệ thống n8n, sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Start (manualTrigger):** Node khởi chạy thủ công. Các sếp có thể thay thế bằng Schedule Trigger nếu muốn workflow tự động chạy hàng ngày.
- **Recover Profiles (googleSheets):** 
  - Chọn tài khoản Google Sheets Credentials của các sếp.
  - Trỏ đến file Google Sheet mẫu đã copy (hướng dẫn kết nối chi tiết tại [Video Tutorial](https://www.youtube.com/watch?v=pWGXlZBGu4k)).
  - Thiết lập operation là `Get` hoặc `Get Many` để lấy danh sách các URL LinkedIn cần enrich.
- **Get Profile Info (httpRequest):**
  - Node này dùng để gọi API từ **Ghost Genius** nhằm cào thông tin profile LinkedIn.
  - Điền chính xác Endpoint URL cung cấp bởi [Ghost Genius](https://ghostgenius.fr) và đính kèm các Headers/Parameters yêu cầu (API Key nếu có) kèm theo URL LinkedIn lấy từ bước Google Sheets.
- **Update (googleSheets):**
  - Thiết lập `operation` là **update**.
  - Map các trường dữ liệu trả về từ node *Get Profile Info* (như tên, chức vụ, công ty, bio...) vào các cột tương ứng trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test chạy thử với một vài dòng dữ liệu mẫu xem thông tin có được cập nhật chuẩn xác vào Google Sheet hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để sẵn sàng đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa toàn diện:** Thay vì dùng `Manual Trigger`, các sếp có thể kết hợp thêm `Schedule Trigger` để hệ thống tự quét danh sách mới mỗi sáng.
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi quá trình enrich danh sách hoàn tất.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt các trường hợp link LinkedIn lỗi hoặc API phản hồi chậm, giúp hệ thống không bị ngắt quãng.

### 📌 Kết luận
Workflow "Enrich LinkedIn Profiles with Ghost Genius and Google Sheets" là trợ thủ đắc lực giúp tối ưu hóa công việc tìm kiếm thông tin khách hàng tiềm năng. Hãy áp dụng ngay vào quy trình của các sếp để bứt phá hiệu suất làm việc!