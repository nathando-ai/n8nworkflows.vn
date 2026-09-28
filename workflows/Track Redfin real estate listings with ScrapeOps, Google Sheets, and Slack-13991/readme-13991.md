---
title: "🏡 Tự động theo dõi danh sách bất động sản Redfin với ScrapeOps, Google Sheets và Slack"
description: "Hướng dẫn tự động hóa theo dõi danh sách bất động sản Redfin hàng ngày với n8n, tiết kiệm thời gian và tối ưu hóa quy trình tìm kiếm bất động sản"
slug: "tu-dong-theo-doi-danh-sach-bat-dong-san-redfin"
tags: [n8n, automation, no-code, real estate, scrapeops]
keywords: [n8n workflow, tự động hóa bất động sản, scrapeops, google sheets, slack]
---

# 🏡 Tự động theo dõi danh sách bất động sản Redfin với ScrapeOps, Google Sheets và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp trong ngành bất động sản khi phải theo dõi hàng chục trang web bất động sản hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động cập nhật danh sách bất động sản hàng ngày mà không cần can thiệp thủ công.
- Dữ liệu chuẩn xác: Sử dụng ScrapeOps Proxy và Parser API để đảm bảo dữ liệu được lấy chính xác và đầy đủ.
- Tích hợp liền mạch: Lưu dữ liệu vào Google Sheets và nhận thông báo qua Slack, tạo chuỗi công việc liên tục.
- Cá nhân hóa: Có thể tùy chỉnh theo nhu cầu tìm kiếm cụ thể của từng sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeOps API key (đăng ký miễn phí tại [https://scrapeops.io/app/register/n8n](https://scrapeops.io/app/register/n8n))
- Tài khoản Google Sheets với quyền chỉnh sửa
- Tài khoản Slack (tùy chọn)
- URL tìm kiếm bất động sản Redfin cụ thể (ví dụ: [https://www.redfin.com/city/12345/CA/San-Francisco](https://www.redfin.com/city/12345/CA/San-Francisco))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13991](https://n8n.io/workflows/13991)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow vào
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **ScrapeOps: Fetch Redfin Page (Proxy)**
   - Thêm credentials ScrapeOps API key
   - Đảm bảo URL tìm kiếm Redfin được đặt chính xác trong node "Set Search Parameters"

2. **ScrapeOps: Parse Redfin Listings**
   - Thêm credentials ScrapeOps API key
   - Đảm bảo cấu hình parser phù hợp với trang web Redfin

3. **Save Listings to Google Sheets**
   - Thêm credentials Google Sheets OAuth2
   - Sao chép [Google Sheet template](https://docs.google.com/spreadsheets/d/1FYbt_m8nUdlkSmCzwZeBjgp4js6sdIKpiyyTIPBsigQ/edit?gid=0#gid=0) và dán Sheet ID vào node này

4. **Send Slack Summary** (tùy chọn)
   - Thêm credentials Slack API
   - Cấu hình kênh Slack nhận thông báo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách click vào nút "Execute Workflow" ở góc trên bên phải
2. Kiểm tra kết quả trên Google Sheets và Slack
3. Bật Active workflow bằng cách click vào nút "Activate" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh tìm kiếm**: Thay đổi URL tìm kiếm trong node "Set Search Parameters" để phù hợp với nhu cầu tìm kiếm cụ thể của từng sếp
2. **Thay đổi tần suất cập nhật**: Điều chỉnh thời gian trong node "Schedule Trigger" để cập nhật dữ liệu theo nhu cầu (hàng ngày, hàng tuần, hàng tháng)
3. **Thêm bộ lọc nâng cao**: Sử dụng node "Filter Valid Properties" để thêm các tiêu chí lọc bổ sung như diện tích, số phòng ngủ, giá bán
4. **Tích hợp với các công cụ khác**: Kết nối với các công cụ phân tích dữ liệu khác như Google Data Studio để tạo báo cáo trực quan

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa theo dõi danh sách bất động sản Redfin hàng ngày. Với tích hợp liền mạch với Google Sheets và Slack, các sếp có thể quản lý và theo dõi dữ liệu bất động sản một cách hiệu quả và chuyên nghiệp. Hãy áp dụng ngay để tiết kiệm thời gian và tối ưu hóa quy trình tìm kiếm bất động sản của bạn!