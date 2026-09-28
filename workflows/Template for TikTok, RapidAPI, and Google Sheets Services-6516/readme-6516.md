---
title: "🚀 Tự động hóa dữ liệu TikTok với n8n: Lấy thông tin người dùng và video từ RapidAPI vào Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc lấy dữ liệu TikTok (profile, video stats) từ RapidAPI và lưu vào Google Sheets bằng n8n. Giải pháp hoàn hảo cho quản lý nội dung và phân tích thị trường."
slug: "tu-dong-hoa-du-lieu-tiktok-voi-n8n"
tags: [n8n, automation, no-code, social-media, marketing]
keywords: [n8n workflow, tự động hóa TikTok, RapidAPI, Google Sheets, phân tích thị trường]
---

# 🚀 Tự động hóa dữ liệu TikTok với n8n: Lấy thông tin người dùng và video từ RapidAPI vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng phải mất hàng giờ mỗi ngày để theo dõi dữ liệu TikTok của nhiều tài khoản khác nhau. Từ việc kiểm tra số lượng người theo dõi, lượt xem video đến việc phân tích xu hướng nội dung - tất cả đều là công việc thủ công, tốn thời gian và dễ gây lỗi.

Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này trong vòng 15 phút, chỉ với kiến thức cơ bản về n8n. Workflow sẽ tự động:
- Lấy danh sách tài khoản TikTok từ Google Sheets
- Gửi yêu cầu API đến RapidAPI để lấy thông tin profile và video stats
- Lưu kết quả vào Google Sheets theo định dạng có thể đọc được
- Chạy tự động theo lịch trình đã đặt

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian làm việc hàng ngày
- Dữ liệu luôn được cập nhật tự động theo lịch trình
- Giảm thiểu lỗi do nhập liệu thủ công
- Có thể phân tích dữ liệu lớn với hàng nghìn tài khoản
- Tạo báo cáo tự động cho các cuộc họp quan trọng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ RapidAPI (dịch vụ TikTok Data API)
- Google Sheet chứa danh sách tài khoản TikTok cần theo dõi
- Google Sheet để lưu kết quả (có thể tạo mới)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/6516)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào menu "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Schedule Trigger**:
   - Chỉnh sửa lịch chạy (ví dụ: mỗi ngày lúc 8h sáng)
   - Đảm bảo thời gian server của bạn khớp với múi giờ mong muốn

2. **Node Google Sheets (Read)**:
   - Chọn credentials Google API đã được thiết lập
   - Nhập ID của Google Sheet chứa danh sách tài khoản TikTok
   - Chỉ định phạm vi dữ liệu (ví dụ: Sheet1!A2:A100)

3. **Node Fetch Profile và Fetch Videos**:
   - Đảm bảo đã thiết lập credentials RapidAPI trong n8n
   - Kiểm tra các tham số đầu vào (username, các trường dữ liệu cần lấy)
   - Thêm headers cần thiết cho API (Content-Type: application/json)

4. **Node Google Sheets (Write)**:
   - Chọn credentials Google API đã được thiết lập
   - Nhập ID của Google Sheet để lưu kết quả
   - Chỉ định phạm vi dữ liệu (ví dụ: Sheet2!A1)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Execute Node" trên mỗi node để test
2. Kiểm tra kết quả ở mỗi node để đảm bảo dữ liệu được xử lý đúng
3. Khi đã ổn định, click vào nút "Activate" để chạy workflow theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
1. **Xử lý lỗi**: Thêm node "Error Handling" để ghi lại các tài khoản không lấy được dữ liệu
2. **Báo cáo tự động**: Kết nối với node Email để gửi báo cáo hàng tuần
3. **Phân tích dữ liệu**: Sử dụng Google Data Studio để tạo dashboard từ dữ liệu đã thu thập
4. **Kết hợp với Slack**: Thêm node Slack để thông báo khi có sự thay đổi đáng chú ý

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa việc theo dõi dữ liệu TikTok, giúp các sếp tiết kiệm thời gian và tập trung vào những nhiệm vụ quan trọng hơn. Với cấu hình đơn giản và khả năng mở rộng, workflow này có thể được tùy chỉnh cho nhiều trường hợp sử dụng khác nhau trong lĩnh vực marketing và quản lý nội dung.