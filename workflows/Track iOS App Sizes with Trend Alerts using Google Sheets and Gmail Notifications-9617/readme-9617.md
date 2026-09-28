---
title: "📊 Theo dõi kích thước ứng dụng iOS tự động với cảnh báo xu hướng và Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi kích thước ứng dụng iOS hàng ngày, lưu dữ liệu vào Google Sheets và nhận cảnh báo khi có thay đổi đáng kể"
slug: "theo-doi-kich-thuoc-ung-dung-ios-tu-dong"
tags: [n8n, automation, no-code, ios, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa, theo dõi ứng dụng, kích thước IPA, cảnh báo xu hướng]
---

# 📊 Theo dõi kích thước ứng dụng iOS tự động với cảnh báo xu hướng và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công kích thước ứng dụng iOS hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian theo dõi thủ công hàng ngày
- Dữ liệu lịch sử đầy đủ trong Google Sheets
- Nhận cảnh báo kịp thời khi kích thước ứng dụng thay đổi đáng kể
- Tự động hóa hoàn toàn quá trình theo dõi
- Dễ dàng tích hợp với các hệ thống khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets và Gmail API đã kích hoạt
- URL tải xuống IPA của ứng dụng cần theo dõi
- Google Sheets với bảng tính đã tạo sẵn (hoặc workflow sẽ tạo mới)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9617](https://n8n.io/workflows/9617)
2. Click vào nút "Import" ở góc trên bên phải
3. Đăng nhập vào tài khoản n8n của bạn (nếu chưa có, hãy tạo mới)
4. Chọn vị trí lưu workflow (thường là "My workflows")

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Daily size check"**:
   - Cấu hình lịch chạy hàng ngày (ví dụ: 8:00 AM mỗi ngày)

2. **Node "App Configuration"**:
   - Thêm các ứng dụng cần theo dõi vào mảng `appsToMonitor`
   - Mỗi ứng dụng cần có:
     ```json
     {
       "name": "Tên ứng dụng",
       "ipaUrl": "URL tải xuống IPA",
       "maxSize": "Kích thước tối đa cho phép (MB)"
     }
     ```

3. **Node "Append row in sheet"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền thông tin Spreadsheet ID (ID của Google Sheet)
   - Điền tên Sheet (Sheet Name) để lưu dữ liệu

4. **Node "Send Alert Email"**:
   - Chọn credentials Gmail OAuth2
   - Điền địa chỉ email nhận cảnh báo
   - Tùy chỉnh nội dung email theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test chạy dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheets và hộp thư đến
3. Sau khi test thành công, bật chế độ Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo Slack/Teams bằng cách thêm node tương ứng sau node "Send Alert Email"
- Tạo báo cáo định kỳ bằng cách thêm node gửi email hàng tuần/tuần
- Thêm nhiều hơn 1 ứng dụng vào danh sách theo dõi
- Tích hợp với các hệ thống CI/CD để tự động theo dõi phiên bản mới

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi kích thước ứng dụng iOS hàng ngày, lưu trữ dữ liệu lịch sử và nhận cảnh báo kịp thời khi có thay đổi đáng kể. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả quản lý ứng dụng!