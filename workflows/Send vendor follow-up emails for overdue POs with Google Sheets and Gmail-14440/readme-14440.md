---
title: "📅 Tự động nhắc nhở nhà cung cấp đơn hàng quá hạn với Google Sheets & Gmail"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp các sếp theo dõi và nhắc nhở nhà cung cấp đơn hàng quá hạn hàng ngày, tiết kiệm thời gian và tránh quên nhắc."
slug: "tu-dong-nhac-nho-nha-cung-cap-don-hang-qua-han"
tags: [n8n, automation, no-code, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa đơn hàng, nhắc nhở nhà cung cấp, quản lý mua hàng]
---

# 📅 Tự động nhắc nhở nhà cung cấp đơn hàng quá hạn với Google Sheets & Gmail

[Nhắc nhở nhà cung cấp đơn hàng quá hạn thủ công là một công việc tốn thời gian và dễ bị quên. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, đảm bảo không bỏ sót bất kỳ đơn hàng nào.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động theo dõi và nhắc nhở hàng ngày mà không cần can thiệp thủ công.
- **Tránh quên nhắc**: Đảm bảo không bỏ sót bất kỳ đơn hàng quá hạn nào.
- **Chính xác cao**: Lọc và xử lý dữ liệu một cách tự động, giảm thiểu lỗi con người.
- **Chuyên nghiệp**: Gửi email nhắc nhở với thông tin chi tiết và chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets và Gmail.
- Google Sheets chứa dữ liệu đơn hàng (Purchase Order Log) và danh sách nhà cung cấp (Vendor Base).
- Cài đặt và cấu hình n8n trên VPS (tự host) hoặc sử dụng dịch vụ n8n cloud.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/14440](https://n8n.io/workflows/14440)
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Trigger Node**: Đảm bảo lịch trình chạy đúng giờ (mặc định là 9:00 AM hàng ngày).
- **Read PO Node**:
  - Chọn credentials Google Sheets OAuth2 API.
  - Nhập ID của Google Sheet chứa dữ liệu đơn hàng.
  - Đảm bảo tên các cột (Vendor ID, Delivery Date, Status) khớp với dữ liệu thực tế.
- **Filter + Normalize Node**:
  - Kiểm tra và điều chỉnh hàm parseDate nếu định dạng ngày tháng trong Google Sheets không chuẩn.
- **Read Vendors Node**:
  - Chọn credentials Google Sheets OAuth2 API.
  - Nhập ID của Google Sheet chứa danh sách nhà cung cấp.
  - Đảm bảo tên các cột (Vendor ID, Supplier Email) khớp với dữ liệu thực tế.
- **Send Email Node**:
  - Chọn credentials Gmail OAuth2.
  - Kiểm tra và điều chỉnh template email nếu cần.
- **Update PO Sheet Node**:
  - Chọn credentials Google Sheets OAuth2 API.
  - Kiểm tra lại ID của Google Sheet và tên cột để cập nhật ngày nhắc nhở.

#### 3. Kích hoạt ⚡️
1. Chạy thử workflow với dữ liệu mẫu để kiểm tra kết quả.
2. Sau khi đảm bảo hoạt động đúng, bật chế độ Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo qua Slack hoặc Telegram khi có đơn hàng quá hạn.
- **Lưu log hoạt động**: Thêm node để lưu log các email đã gửi để theo dõi lịch sử nhắc nhở.
- **Gửi báo cáo định kỳ**: Tạo workflow phụ để tổng hợp và gửi báo cáo hàng tuần về tình trạng đơn hàng.
- **Xử lý lỗi tự động**: Thêm node để xử lý các trường hợp lỗi và gửi thông báo cảnh báo.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình nhắc nhở nhà cung cấp đơn hàng quá hạn, tiết kiệm thời gian và đảm bảo không bỏ sót bất kỳ đơn hàng nào. Hãy áp dụng ngay để nâng cao hiệu quả quản lý mua hàng của bạn!