---
title: "🚀 Tự động tìm số điện thoại từ LinkedIn qua ScraperCity và gửi thông báo Sales trên Slack"
description: "Hướng dẫn tự động hóa quy trình tìm kiếm số điện thoại di động từ profile LinkedIn bằng ScraperCity API, lọc trùng lặp và bắn thông báo nóng hổi về Slack cho đội ngũ Sales."
slug: "tim-so-dien-thoai-linkedin-scrapercity-slack"
tags: [n8n, automation, no-code, lead-generation, scrapercity, slack, sales-automation]
keywords: [n8n workflow, tìm số điện thoại linkedin, scrapercity api, sales automation slack, trích xuất lead linkedin]
---

# 🚀 Tự động tìm số điện thoại từ LinkedIn qua ScraperCity và bắn thông báo cho Sales trên Slack

Việc tìm kiếm số điện thoại di động (mobile numbers) chất lượng từ LinkedIn để phục vụ chiến dịch Cold Calling hay Sales Outreach thủ công thường cực kỳ mất thời gian và tốn kém nhân lực. Các sếp thường phải copy từng profile, tra cứu qua các công cụ ngoài, rồi lại thủ công copy số điền vào CRM hay nhắn cho đội ngũ sales. 

Quá trình thủ công này không chỉ làm giảm năng suất của đội ngũ kinh doanh mà còn khiến doanh nghiệp bỏ lỡ "thời điểm vàng" để tiếp cận khách hàng tiềm năng.

Workflow n8n này sẽ tự động hóa toàn bộ quy trình: Nhận danh sách LinkedIn, gửi yêu cầu đến ScraperCity API, tự động lặp (polling) kiểm tra trạng thái, tải về file kết quả CSV, lọc bỏ trùng lặp, chọn ra các contact có số điện thoại và bắn thông báo trực tiếp vào kênh Slack của đội Sales ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần copy-paste thủ công từ LinkedIn sang các công cụ tra cứu số điện thoại.
- **Tối ưu thời gian cho Sales:** Đội ngũ kinh doanh nhận được số điện thoại trực tiếp trên Slack ngay khi dữ liệu được xử lý xong.
- **Dữ liệu sạch & chính xác:** Tự động lọc bỏ các bản ghi trùng lặp (duplicates) và chỉ giữ lại các contact có chứa số điện thoại hợp lệ.
- **Hoạt động linh hoạt:** Cơ chế kiểm tra trạng thái thông minh (Polling Loop) giúp xử lý các job quét dữ liệu lớn mà không lo timeout.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản ScraperCity:** API Key hợp lệ từ nền tảng ScraperCity (của Alex Berman) để gọi các endpoint tìm mobile.
- **Slack Workspace:** Đã tạo Bot/App với quyền `chat:write` và add vào channel Sales nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy toàn bộ mã JSON của workflow này, paste trực tiếp vào n8n Editor hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau:
- **Configure Inputs (Node `set`):** Mở node này và điền danh sách các URL LinkedIn mục tiêu (`linkedinProfiles`), email công việc (`workEmails`), và kênh Slack đích (`slackChannel`).
- **HTTP Request Nodes (`Submit Mobile Finder Job`, `Check Job Status`, `Download Mobile Finder Results`):** 
  - Tạo Credentials loại **Header Auth** với ScraperCity API Key của các sếp.
  - Xác nhận lại các endpoint URL trong các node này khớp với phiên bản API hiện tại của tài khoản ScraperCity.
- **Alert Sales Team in Slack (Node `slack`):** 
  - Kết nối Credentials loại **Slack API**.
  - Đảm bảo bot có quyền gửi tin nhắn vào channel đã cấu hình.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** chạy thủ công lần đầu để test với dữ liệu mẫu trong `Configure Inputs`.
- Kiểm tra logs tại các node `Poll Loop Controller`, `Parse CSV Results` và `Alert Sales Team in Slack` để chắc chắn dữ liệu trả về chuẩn chỉnh.
- Bật công tắc **Active** để sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Đẩy dữ liệu về CRM:** Thay vì chỉ bắn tin nhắn lên Slack, các sếp có thể gắn thêm node **HubSpot**, **Notion** hoặc **Google Sheets** sau bước `Filter Records With Phone Numbers` để lưu trữ data tự động.
- **Tùy biến tin nhắn Slack:** Chỉnh sửa code trong node `Format Slack Message` để làm đẹp giao diện thông báo, thêm các nút bấm hoặc gắn trực tiếp link dẫn về profile LinkedIn của khách hàng.
- **Tối ưu thời gian chờ:** Điều chỉnh thời gian ở các node `Wait 30 Seconds Before First Poll` và `Wait 60 Seconds Before Retry` tùy thuộc vào khối lượng công việc quét dữ liệu trung bình trên ScraperCity.

### 📌 Kết luận
Workflow này là vũ khí cực kỳ mạnh mẽ giúp các đội ngũ Sales và Growth Hacker tự động hóa khâu tìm kiếm thông tin liên lạc chất lượng từ LinkedIn. Triển khai ngay hôm nay để tối ưu hóa hiệu suất đội ngũ kinh doanh của các sếp!