---
title: "🚀 Tự động gán CSM và gửi email chào mừng AI cho HubSpot khi giao dịch thành công"
description: "Hướng dẫn tự động hóa quy trình gán CSM ít bận rộn nhất và gửi email chào mừng AI khi giao dịch HubSpot được đánh dấu 'Đã thắng' - tiết kiệm thời gian và cá nhân hóa trải nghiệm khách hàng."
slug: "tu-dong-giao-dich-thanh-cong-hubspot-voi-ai"
tags: [n8n, automation, no-code, crm, ai]
keywords: [n8n workflow, tự động hóa, hubspot, email ai, csm]
---

# 🚀 Tự động gán CSM và gửi email chào mừng AI cho HubSpot khi giao dịch thành công

[Các sếp đang mệt mỏi với việc phải theo dõi thủ công từng giao dịch HubSpot, gán CSM và gửi email chào mừng? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý giao dịch ngay khi được đánh dấu 'Đã thắng' mà không cần can thiệp thủ công.
- **Cá nhân hóa hoàn hảo**: Email chào mừng được tạo bởi AI với nội dung phù hợp với từng khách hàng.
- **Phân bổ công việc hợp lý**: Gán CSM ít bận rộn nhất cho mỗi giao dịch mới.
- **Tăng hiệu quả hoạt động**: Giảm thiểu thời gian chờ đợi và tăng tốc độ xử lý giao dịch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản Gmail để gửi email
- Tài khoản OpenAI để sử dụng mô hình AI
- Dữ liệu CSM trong bảng dữ liệu n8n (chi tiết bên dưới)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/10398)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Tạo bảng dữ liệu CSM**:
   - Tạo bảng mới với tên `csm_assignments`
   - Thêm 2 cột: `csm_id` (String) và `deal_count` (Number)
   - Thêm một hàng cho mỗi CSM với ID HubSpot và `deal_count` ban đầu là 0

2. **Cấu hình các node quan trọng**:
   - **Trigger: Deal Is 'Closed Won'**: Thêm credentials HubSpot Developer API
   - **HubSpot: Get Deal Details**: Thêm credentials HubSpot
   - **HubSpot: Get Contact Details**: Thêm credentials HubSpot
   - **HubSpot: Assign Contact Owner**: Thêm credentials HubSpot
   - **AI Model**: Thêm credentials OpenAI
   - **Gmail: Send Welcome Email**: Thêm credentials Gmail

3. **Cấu hình biến template**:
   - Mở node **Configure Template Variables**
   - Điền thông tin sender: `company_name`, `sender_name`, `sender_email`

4. **Cập nhật bảng dữ liệu trong các node**:
   - Mở node **Get CSM List** và **Increment CSM Deal Count**
   - Trong trường **Table**, chọn bảng `csm_assignments` vừa tạo

5. **Tùy chỉnh prompt AI**:
   - Mở node **AI: Write Welcome Email**
   - Chỉnh sửa prompt để phù hợp với phong cách của công ty

6. **Cập nhật trường deal_count**:
   - Trong node **Increment CSM Deal Count**:
     - Chọn `deal_count` trong trường **Field**
     - Chuyển sang chế độ biểu thức (`f(x)`) và dán:
       `{{ $('Find Least Busy CSM').item.json.current_count + 1 }}`

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra email được gửi và CSM được gán
3. Bật Active workflow khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Teams**: Thêm node để thông báo khi giao dịch mới được xử lý
- **Lưu log hoạt động**: Thêm node để ghi lại lịch sử gán CSM và gửi email
- **Báo cáo định kỳ**: Tạo workflow phụ để tổng hợp và gửi báo cáo hàng tuần
- **Tích hợp với các hệ thống khác**: Kết nối với các công cụ khác như Salesforce, Zendesk...

### 📌 Kết luận
Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình gán CSM và gửi email chào mừng, tiết kiệm thời gian quý giá và cung cấp trải nghiệm khách hàng cá nhân hóa. Hãy áp dụng ngay để tối ưu hóa quy trình bán hàng của công ty!