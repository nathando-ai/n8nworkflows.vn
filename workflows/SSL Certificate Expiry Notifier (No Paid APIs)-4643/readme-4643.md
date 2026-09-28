---
title: "🚀 Hướng dẫn tự động cảnh báo hết hạn SSL bằng n8n (Không cần API trả phí)"
description: "Hướng dẫn chi tiết cách tự động theo dõi và cảnh báo hết hạn SSL cho nhiều domain bằng n8n, Google Sheets và email - giải pháp hoàn toàn miễn phí"
slug: "huong-dan-tu-dong-can-bao-het-han-ssl-bang-n8n"
tags: [n8n, automation, no-code, devops, ssl]
keywords: [n8n workflow, tự động hóa, ssl expiry, devops, google sheets]
---

# 🚀 Tự động cảnh báo hết hạn SSL bằng n8n (Không cần API trả phí)

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý nhiều domain và phải theo dõi thủ công hết hạn SSL. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý thủ công
- Nhận cảnh báo tự động trước khi SSL hết hạn
- Theo dõi nhiều domain từ một bảng Google Sheets
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Giải pháp hoàn toàn miễn phí (không cần API trả phí)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets
- Thông tin SMTP để gửi email cảnh báo
- Danh sách các domain cần theo dõi (đã lưu trong Google Sheets)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4643)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "URLs to Monitor" và "Fetch URLs"**:
   - Cấu hình credentials Google Sheets OAuth2
   - Chỉnh sửa URL của Google Sheet trong tham số "resource"
   - Đảm bảo bảng có cột "URL" chứa danh sách domain cần theo dõi

2. **Node "Send Email"**:
   - Cấu hình credentials SMTP
   - Chỉnh sửa địa chỉ email nhận cảnh báo trong tham số "to"
   - Tùy chỉnh nội dung email trong tham số "body"

3. **Node "Daily Trigger"**:
   - Điều chỉnh thời gian chạy hàng ngày (mặc định là 8:00 AM)
   - Có thể thay đổi thành tần suất khác nếu cần

4. **Node "Expiry Alert"**:
   - Điều chỉnh ngưỡng cảnh báo (mặc định là 7 ngày)
   - Thay đổi biểu thức điều kiện nếu muốn cảnh báo sớm hơn

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra email để đảm bảo nhận được cảnh báo thử nghiệm
3. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Teams để nhận cảnh báo qua kênh chat
2. Thêm node lưu log để theo dõi lịch sử kiểm tra SSL
3. Tự động gửi báo cáo hàng tuần về trạng thái SSL của tất cả domain
4. Thêm chức năng tự động gia hạn SSL khi sắp hết hạn

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh để tự động theo dõi và cảnh báo hết hạn SSL cho nhiều domain mà không cần can thiệp thủ công. Với cấu hình đơn giản và hoạt động liên tục 24/7, đây là công cụ lý tưởng cho các sếp quản lý nhiều website và ứng dụng. Hãy thử ngay và tiết kiệm thời gian quý giá của mình!