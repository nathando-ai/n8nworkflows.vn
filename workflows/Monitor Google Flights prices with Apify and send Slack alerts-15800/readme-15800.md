---
title: "🚀 Tự động săn vé máy bay giá rẻ Google Flights với Apify và n8n"
description: "Hướng dẫn xây dựng hệ thống tự động theo dõi giá vé máy bay qua Google Flights bằng Apify và n8n, gửi cảnh báo tức thì qua Slack khi có deal hời."
slug: "tu-dong-san-ve-may-bay-gia-re-google-flights-voi-apify-va-n8n"
tags: [n8n, automation, no-code, apify, slack, market-research]
keywords: [n8n workflow, tự động hóa google flights, apify scraper, săn vé máy bay giá rẻ, slack alert]
---

# 🚀 Tự động săn vé máy bay giá rẻ Google Flights với Apify và n8n

Việc thủ công tra cứu giá vé máy bay trên Google Flights mỗi ngày cho nhiều ngày khởi hành khác nhau cực kỳ tốn thời gian, và các đợt giảm giá chớp nhoáng (flash sale) thường trôi qua trước khi các sếp kịp nhận ra. 

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa toàn bộ quy trình: cào dữ liệu giá vé thời gian thực qua **Apify**, phân tích và so sánh giá thông minh, sau đó tự động bắn thông báo chi tiết qua **Slack** ngay khi xuất hiện vé rẻ hoặc có biến động giá.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần tốn công tra cứu thủ công từng ngày trên Google Flights.
- **Cảnh báo tức thì:** Nhận thông báo qua Slack ngay khi tìm thấy chuyến bay có giá thấp hơn ngưỡng kỳ vọng (ví dụ: dưới $1,400).
- **Lịch trình thông minh:** Tự động điều chỉnh tần suất quét (quét dày hơn vào ban đêm, thưa hơn vào ban ngày) để tối ưu hiệu suất và chi phí API.
- **Báo cáo toàn diện:** Gửi lịch trình giá vé đầy đủ của 18 ngày khởi hành thẳng vào Slack để tiện theo dõi xu hướng giá.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Apify** kèm API Key / OAuth2 để chạy Google Flights Scraper Actor.
- **Workspace Slack** có quyền tích hợp, tạo sẵn các kênh (channels) nhận thông báo như `#price-drop`, `#regular-update`, `#sales-team`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc sao chép mã JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Run an Actor and get dataset` (Apify):** Kết nối tài khoản Apify thông qua `Apify OAuth2 API` và kiểm tra cấu hình Actor chuyên cào dữ liệu Google Flights (chọn tuyến bay, điểm đi/đến, cửa sổ ngày về).
- **Các node Slack (`price drop Alert`, `normal update`, `all dates full report`):** Xác thực tài khoản qua `Slack OAuth2 API` và điền chính xác ID của các kênh Slack nhận tin nhắn tương ứng.
- **Node `Find Cheapest & Decide` / `Below $1,400?`:** Điều chỉnh mức giá mục tiêu (`$1,400`) trong mã code hoặc điều kiện IF cho phù hợp với nhu cầu thực tế của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công lần đầu, kiểm tra dữ liệu trả về từ Apify và định dạng tin nhắn trên Slack.
- Bật công tắc **Active** để workflow tự động chạy theo lịch trình thông minh.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi kênh nhận tin:** Có thể tích hợp thêm Telegram Bot hoặc Email (Gmail node) nếu đội ngũ hoặc cá nhân các sếp không sử dụng Slack thường xuyên.
- **Lưu lịch sử giá:** Kết nối thêm Google Sheets hoặc Airtable sau node `Find Cheapest & Decide` để lưu trữ dữ liệu giá vé theo thời gian, phục vụ việc phân tích xu hướng dài hạn.
- **Mở rộng tuyến bay:** Nhân bản nhánh cào dữ liệu để theo dõi đồng thời nhiều hành trình bay khác nhau cùng lúc.

### 📌 Kết luận
Với workflow n8n này, việc săn vé máy bay giá rẻ trở nên hoàn toàn tự động và chuyên nghiệp. Triển khai ngay hôm nay để không bỏ lỡ bất kỳ đợt giảm giá vé máy bay nào các sếp nhé!