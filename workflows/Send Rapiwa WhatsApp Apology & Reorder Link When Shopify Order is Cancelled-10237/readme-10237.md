---
title: "🚀 Tự động gửi tin nhắn lỗi lỗ và liên kết đặt hàng lại khi đơn hàng Shopify bị hủy"
description: "Tự động hóa hoàn toàn quá trình gửi tin nhắn lỗi lỗ và liên kết đặt hàng lại cho khách hàng khi đơn hàng Shopify bị hủy, tiết kiệm thời gian và tăng trải nghiệm khách hàng"
slug: "tu-dong-gui-tin-nhan-loi-lo-va-lien-ket-dat-hang-lai-khi-don-hang-shopify-bi-huy"
tags: [n8n, automation, no-code, shopify, whatsapp]
keywords: [n8n workflow, tự động hóa, shopify, whatsapp, tin nhắn lỗi lỗ]
---

# 🚀 Tự động gửi tin nhắn lỗi lỗ và liên kết đặt hàng lại khi đơn hàng Shopify bị hủy

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình gửi tin nhắn lỗi lỗ và liên kết đặt hàng lại
- Tiết kiệm thời gian xử lý thủ công cho nhân viên
- Tăng trải nghiệm khách hàng với tin nhắn cá nhân hóa
- Theo dõi hiệu quả gửi tin nhắn qua hệ thống báo cáo trên Google Sheets
- Tự động xử lý hàng loạt đơn hàng bị hủy trong cùng một phiên
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với webhook đơn hàng bị hủy đã được kích hoạt
- Tài khoản Rapiwa và API token
- Một instance n8n (cloud hoặc self-hosted)
- Google Sheet đã được thiết lập để ghi lại trạng thái tin nhắn
- Shopify Access Token (Private App hoặc Admin API)
- Số WhatsApp đã được xác minh của Rapiwa và có đủ tin nhắn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấp vào nút "Import from URL" ở góc trên bên phải
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/10237`
4. Nhấp vào nút "Import" để tải workflow vào n8n của bạn

Hoặc bạn cũng có thể:
1. Truy cập vào trang workflow gốc: [https://n8n.io/workflows/10237](https://n8n.io/workflows/10237)
2. Nhấp vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, nhấp vào nút "Import from JSON" và dán nội dung đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Shopify Trigger** (Order Cancelled):
   - Đảm bảo bạn đã thiết lập webhook đơn hàng bị hủy trong Shopify
   - Cấu hình credentials "shopifyAccessTokenApi" với token truy cập Shopify của bạn

2. **Code** (Simplify Order Data):
   - Node này sẽ tự động trích xuất và định dạng dữ liệu đơn hàng
   - Không cần cấu hình thêm, nhưng bạn có thể chỉnh sửa mã để phù hợp với cấu trúc dữ liệu đơn hàng của bạn

3. **Clean WhatsApp Number**:
   - Node này sẽ làm sạch số điện thoại của khách hàng
   - Đảm bảo bạn đã cấu hình đúng mã quốc gia (ví dụ: 880 cho Bangladesh)

4. **Check valid whatsapp number Using Rapiwa**:
   - Cấu hình credentials "httpBearerAuth" với token Rapiwa của bạn
   - Đảm bảo endpoint API là `https://app.rapiwa.com/api/verify-whatsapp`

5. **Send Message Using Rapiwa**:
   - Cấu hình credentials "httpBearerAuth" với token Rapiwa của bạn
   - Đảm bảo endpoint API là `https://app.rapiwa.com/api/send-message`
   - Chỉnh sửa nội dung tin nhắn lỗi lỗ và liên kết đặt hàng lại theo nhu cầu của bạn

6. **Save State of Rows in Verified & Sent**:
   - Cấu hình credentials "googleSheetsOAuth2Api" với thông tin xác thực Google Sheets
   - Chỉnh sửa ID của Google Sheet và tên sheet phù hợp với cấu trúc của bạn
   - Đảm bảo các cột trong Google Sheet phù hợp với dữ liệu được ghi lại

7. **Save State of Rows in Verified & Sent1**:
   - Tương tự như node trên, nhưng dành cho các đơn hàng không thể gửi tin nhắn
   - Cấu hình credentials và thông tin Google Sheet phù hợp

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình tất cả các node quan trọng:

1. Kiểm tra workflow bằng cách nhấp vào nút "Execute Workflow" với dữ liệu mẫu
2. Đảm bảo tất cả các node hoạt động như mong đợi
3. Khi đã sẵn sàng, nhấp vào nút "Activate" để kích hoạt workflow
4. Đảm bảo workflow đang chạy bằng cách kiểm tra trạng thái trên giao diện n8n

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo qua Slack hoặc Telegram để theo dõi hiệu quả gửi tin nhắn
- Tích hợp với hệ thống CRM để cập nhật trạng thái khách hàng sau khi gửi tin nhắn
- Thiết lập báo cáo định kỳ để theo dõi hiệu quả của chiến dịch gửi tin nhắn
- Tùy chỉnh nội dung tin nhắn dựa trên ngôn ngữ hoặc sản phẩm để tăng độ tương tác
- Thêm node xử lý lỗi để ghi lại và thông báo khi có vấn đề xảy ra trong quá trình gửi tin nhắn

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn toàn cho việc gửi tin nhắn lỗi lỗ và liên kết đặt hàng lại khi đơn hàng Shopify bị hủy. Bằng cách tích hợp với Rapiwa và Google Sheets, bạn có thể tiết kiệm thời gian, tăng trải nghiệm khách hàng và theo dõi hiệu quả của chiến dịch một cách dễ dàng. Hãy áp dụng ngay workflow này để nâng cao chất lượng dịch vụ khách hàng của bạn!