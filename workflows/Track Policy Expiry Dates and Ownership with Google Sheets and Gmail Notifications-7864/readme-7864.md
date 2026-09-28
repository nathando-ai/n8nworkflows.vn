---
title: "🚀 Theo dõi hạn sử dụng và chủ sở hữu chính sách với Google Sheets và thông báo qua Gmail"
description: "Tự động hóa theo dõi hạn sử dụng chính sách và thông báo chủ sở hữu khi chính sách sắp hết hạn hoặc thiếu thông tin chủ sở hữu"
slug: "theo-doi-han-su-dung-chinh-sach-google-sheets-gmail"
tags: [n8n, automation, no-code, secops, google-sheets]
keywords: [n8n workflow, tự động hóa, secops, google sheets, gmail]
---

# 🚀 Theo dõi hạn sử dụng và chủ sở hữu chính sách với Google Sheets và thông báo qua Gmail

[Các sếp đang làm việc với nhiều chính sách và tài liệu quan trọng thường gặp khó khăn khi phải theo dõi thủ công hạn sử dụng và thông tin chủ sở hữu. Việc này tốn thời gian, dễ bỏ sót và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này chỉ trong vài phút.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động theo dõi hạn sử dụng chính sách hàng ngày
- Giảm rủi ro: Nhận thông báo kịp thời khi chính sách sắp hết hạn
- Tăng hiệu quả: Không bỏ sót bất kỳ chính sách nào cần cập nhật
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace với quyền truy cập vào Google Sheets và Gmail
- Google Sheets chứa dữ liệu chính sách (cột "Policy Name", "Expiry Date", "Owner")
- Thiết lập OAuth cho Google Sheets và Gmail trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/7864
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Policy Data"**:
   - Chọn Google Sheets credentials đã thiết lập
   - Nhập ID của Google Sheet chứa dữ liệu chính sách
   - Đảm bảo Sheet có các cột: "Policy Name", "Expiry Date", "Owner"

2. **Node "Is Policy Expiring Soon?"**:
   - Thiết lập điều kiện kiểm tra hạn sử dụng (ví dụ: chính sách hết hạn trong 30 ngày)
   - Điều chỉnh ngày cảnh báo theo nhu cầu của tổ chức

3. **Node "Is Owner Missing?"**:
   - Thiết lập điều kiện kiểm tra trường "Owner" có giá trị hay không

4. **Node "Notify Missing Owner"**:
   - Chọn Gmail credentials đã thiết lập
   - Nhập địa chỉ email nhận thông báo
   - Tùy chỉnh nội dung email theo mẫu có sẵn

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn "Activate" để chạy workflow tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập lịch chạy workflow hàng ngày để cập nhật thông tin mới nhất
- Kết hợp với Slack để nhận thông báo tức thời
- Thêm node để lưu log các thông báo đã gửi
- Tạo báo cáo định kỳ về trạng thái chính sách

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn việc theo dõi hạn sử dụng chính sách và thông báo chủ sở hữu, giảm thiểu rủi ro và tiết kiệm thời gian đáng kể. Hãy áp dụng ngay để nâng cao hiệu quả quản lý chính sách của tổ chức!