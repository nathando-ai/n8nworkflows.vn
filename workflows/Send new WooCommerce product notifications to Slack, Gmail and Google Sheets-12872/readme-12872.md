---
title: "🚀 Tự động thông báo sản phẩm mới WooCommerce tới Slack, Gmail và Google Sheets"
description: "Hướng dẫn tự động hóa thông báo sản phẩm mới WooCommerce tới Slack, Gmail và Google Sheets bằng n8n. Tiết kiệm thời gian và đảm bảo đồng bộ thông tin giữa các kênh."
slug: "tu-dong-thong-bao-san-pham-moi-woocommerce"
tags: [n8n, automation, no-code, WooCommerce, Google Sheets]
keywords: [n8n workflow, tự động hóa, WooCommerce, Google Sheets, Slack, Gmail]
---

# 🚀 Tự động thông báo sản phẩm mới WooCommerce tới Slack, Gmail và Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi và thông báo thủ công mỗi khi có sản phẩm mới trên WooCommerce. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ phát hiện sản phẩm mới đến thông báo và lưu trữ dữ liệu.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công mỗi khi có sản phẩm mới.
- **Đồng bộ thông tin**: Thông báo đồng thời tới Slack, Gmail và Google Sheets.
- **Dễ dàng quản lý**: Lưu trữ dữ liệu sản phẩm mới trong Google Sheets để theo dõi và báo cáo.
- **Tăng tính chuyên nghiệp**: Thông báo sản phẩm mới một cách tự động và chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API.
- Tài khoản Slack với quyền gửi tin nhắn.
- Tài khoản Gmail với quyền gửi email.
- Tài khoản Google với quyền truy cập Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [Workflow này trên n8n.io](https://n8n.io/workflows/12872).
2. Click vào nút "Import" để tải xuống file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON đã tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "WooCommerce – New Product Created"**:
   - Cấu hình credentials cho WooCommerce API.
   - Đảm bảo tài khoản WooCommerce có quyền truy cập API.

2. **Node "Notify Team on Slack"**:
   - Cấu hình credentials cho Slack API.
   - Chỉnh sửa thông điệp Slack theo nhu cầu (ví dụ: thêm hoặc bớt thông tin sản phẩm).

3. **Node "Send Product Launch Email"**:
   - Cấu hình credentials cho Gmail OAuth2.
   - Chỉnh sửa nội dung email theo nhu cầu (ví dụ: thêm hoặc bớt thông tin sản phẩm).

4. **Node "Log Product in Google Sheets"**:
   - Cấu hình credentials cho Google Sheets OAuth2 API.
   - Chỉnh sửa tên sheet và định dạng dữ liệu theo nhu cầu.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thêm node Telegram để nhận thông báo sản phẩm mới.
- **Lưu log chi tiết**: Thêm node để lưu log chi tiết các hoạt động của workflow.
- **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp sản phẩm mới hàng tuần.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình thông báo sản phẩm mới WooCommerce tới Slack, Gmail và Google Sheets. Với việc tự động hóa, các sếp có thể tiết kiệm thời gian và đảm bảo đồng bộ thông tin giữa các kênh. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh!