---
title: "🚀 Tự động quét Lead từ Google Maps, cào Email Website và lưu Airtable với n8n & Apify"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa tìm kiếm khách hàng tiềm năng từ Google Maps bằng Apify, trích xuất email từ website doanh nghiệp và lưu trữ vào Airtable."
slug: "tu-dong-quet-lead-google-maps-apify-airtable"
tags: [n8n, automation, no-code, lead-generation, apify, airtable]
keywords: [n8n workflow, quét lead google maps, apify n8n, cào email website, lưu airtable tự động]
---

# 🚀 Tự động quét Lead từ Google Maps, cào Email Website và lưu Airtable

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi hàng giờ lướt Google Maps, copy thủ công tên doanh nghiệp, số điện thoại, website rồi lại lọ mọ tìm email của từng công ty để làm chiến dịch sales? Công việc thủ công này không chỉ ngốn thời gian mà còn cực kỳ nhàm chán, dễ sai sót.

Đừng lo nữa! Bài viết này sẽ giới thiệu một siêu workflow n8n được thiết kế bởi chuyên gia **Ezema Kingsley Chibuzo**, giúp tự động hóa 100% quy trình: **Nhận yêu cầu từ Form -> Quét thông tin doanh nghiệp trên Google Maps qua Apify -> Truy cập website cào dữ liệu & trích xuất Email -> Lọc và lưu trữ tự động vào Airtable**. Không cần code phức tạp, các sếp chỉ cần "lắp ráp" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng ngày, hệ thống quét hàng trăm lead chỉ trong vài phút.
- **Dữ liệu chất lượng cao:** Kết hợp Google Maps (thông tin chính thống) và trích xuất email trực tiếp từ website doanh nghiệp.
- **Tự động hóa thông minh:** Cơ chế phân đoạn (Batching) và độ trễ ngẫu nhiên (Random Wait) giúp tránh bị chặn IP khi cào website.
- **Đồng bộ hóa mượt mà:** Tự động Upsert (cập nhật/thêm mới) dữ liệu sạch vào cơ sở dữ liệu Airtable.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Apify:** Lấy Apify API Key để kết nối với Google Maps Scraper Actor.
- **Tài khoản Airtable:** Tạo sẵn một Base/Table với các trường cơ bản như: `Email`, `Website`, `Phone`, `Company Name`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow (hoặc copy toàn bộ mã nguồn JSON) và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 20 nodes được sắp xếp logic theo các khối chức năng. Các sếp cần chú ý cấu hình các điểm sau:
- **On form submission:** Node kích hoạt dạng Form, các sếp có thể tùy chỉnh các trường đầu vào (như từ khóa tìm kiếm, vị trí địa lý...).
- **Run an Actor & Get dataset items (Apify):** Chọn credentials `apifyApi` và trỏ tới Actor quét Google Maps phù hợp trên Apify.
- **Grab Desired Fields & Parse url/website:** Node `set` và `code` giúp lọc các thông tin cần thiết và làm sạch URL (loại bỏ query parameters không cần thiết).
- **Website Scraping & Extract Email Address:** Thực hiện HTTP Request đến website của từng doanh nghiệp, kết hợp đoạn mã lấy ra các địa chỉ Email hợp lệ.
- **Filter Leads with Email only:** Node `filter` đảm bảo chỉ giữ lại những doanh nghiệp có thông tin email để tiến hành chăm sóc.
- **Database (Airtable):** Chọn credentials `airtableTokenApi`, cấu hình thao tác `upsert` để đẩy dữ liệu sạch vào bảng Airtable đã chuẩn bị.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một từ khóa mẫu (ví dụ: *"Coffee shop in Ho Chi Minh"*).
- Kiểm tra dữ liệu đổ về Airtable xem đã chính xác chưa.
- Bật công tắc **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào sau node `Database` để nhận tin nhắn thông báo mỗi khi có một mẻ lead mới được quét xong.
- **Gửi Email tự động:** Kết hợp thêm node Gmail hoặc Resend để tự động gửi email giới thiệu dịch vụ ngay khi lead mới được lưu vào Airtable.
- **Mở rộng lưu trữ:** Nếu không dùng Airtable, các sếp hoàn toàn có thể thay thế bằng Google Sheets chỉ với vài thao tác đổi node.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" cực kỳ đắt giá cho các đội ngũ Sales và Marketing muốn xây dựng phễu khách hàng tự động với chi phí tối ưu. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất kinh doanh của các sếp nhé!