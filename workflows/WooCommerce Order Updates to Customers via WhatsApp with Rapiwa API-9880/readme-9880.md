---
title: "🚀 Tự động hóa thông báo đơn hàng WooCommerce qua WhatsApp với Rapiwa API"
description: "Hướng dẫn tự động gửi thông báo trạng thái đơn hàng WooCommerce đến khách hàng qua WhatsApp bằng n8n và Rapiwa API, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-hoa-thong-bao-don-hang-woocommerce-qua-whatsapp-voi-rapiwa-api"
tags: [n8n, automation, no-code, WooCommerce, WhatsApp]
keywords: [n8n workflow, tự động hóa, WooCommerce, WhatsApp, Rapiwa API]
---

# 🚀 Tự động hóa thông báo đơn hàng WooCommerce qua WhatsApp với Rapiwa API

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý đơn hàng thủ công
- Nâng cao trải nghiệm khách hàng với thông báo tức thì
- Tăng độ chính xác trong việc gửi thông tin đơn hàng
- Tự động hóa quá trình theo dõi trạng thái đơn hàng
- Giảm thiểu lỗi trong quá trình gửi thông báo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API/webhook
- Tài khoản Rapiwa với API key hợp lệ
- Tài khoản Google với Google Sheets và quyền OAuth2
- Tài khoản n8n với các nodes: Webhook, HTTP Request, Code, SplitInBatches, IF, Google Sheets, Wait
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấp vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/9880`
4. Nhấp vào nút "Import" để hoàn tất quá trình import

Hoặc bạn cũng có thể:
1. Truy cập link workflow: [WooCommerce Order Updates to Customers via WhatsApp with Rapiwa API](https://n8n.io/workflows/9880)
2. Nhấp vào nút "Download" để tải file JSON về máy
3. Trong n8n Editor, nhấp vào nút "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

1. **Webhook Node**:
   - Cấu hình webhook để nhận các sự kiện đơn hàng từ WooCommerce
   - Đảm bảo đường dẫn webhook là duy nhất và bảo mật
   - Kiểm tra xem webhook có hoạt động đúng không bằng cách gửi một yêu cầu thử nghiệm

2. **Format Webhook Response Data Node**:
   - Kiểm tra và điều chỉnh mã JavaScript để phù hợp với cấu trúc dữ liệu đơn hàng của bạn
   - Đảm bảo các trường thông tin khách hàng, sản phẩm và liên kết hóa đơn được trích xuất đúng cách

3. **Clean WhatsApp Number Node**:
   - Kiểm tra và điều chỉnh mã JavaScript để đảm bảo số điện thoại được làm sạch đúng cách
   - Đảm bảo số điện thoại được định dạng đúng để sử dụng với Rapiwa API

4. **Check valid whatsapp number Using Rapiwa Node**:
   - Cấu hình credentials cho Rapiwa API
   - Kiểm tra xem URL API có hoạt động đúng không
   - Đảm bảo bạn có quyền truy cập vào endpoint `/api/verify-whatsapp`

5. **If Node**:
   - Kiểm tra điều kiện để phân luồng cho các số điện thoại đã xác thực và chưa xác thực
   - Đảm bảo logic điều kiện hoạt động đúng

6. **Rapiwa Sender Node**:
   - Cấu hình credentials cho Rapiwa API
   - Kiểm tra xem URL API có hoạt động đúng không
   - Đảm bảo bạn có quyền truy cập vào endpoint `/api/send-message`
   - Kiểm tra và điều chỉnh template tin nhắn để phù hợp với nhu cầu của bạn

7. **Store State of Rows in Verified & Sent Node**:
   - Cấu hình credentials cho Google Sheets
   - Kiểm tra xem ID bảng tính có chính xác không
   - Đảm bảo các cột trong bảng tính được định dạng đúng

8. **Store State of Rows in Unverified & Not Sent Node**:
   - Cấu hình credentials cho Google Sheets
   - Kiểm tra xem ID bảng tính có chính xác không
   - Đảm bảo các cột trong bảng tính được định dạng đúng

9. **Loop Over Items Node**:
   - Điều chỉnh kích thước batch để phù hợp với giới hạn tốc độ của Rapiwa API
   - Kiểm tra xem số lượng đơn hàng được xử lý trong mỗi batch có phù hợp không

10. **Wait Node**:
    - Điều chỉnh thời gian chờ để phù hợp với giới hạn tốc độ của Rapiwa API
    - Kiểm tra xem thời gian chờ có đủ để tránh bị chặn không

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình và kiểm tra tất cả các node, bạn có thể kích hoạt workflow bằng cách:

1. Nhấp vào nút "Activate" trên thanh công cụ
2. Kiểm tra xem workflow có hoạt động đúng không bằng cách gửi một yêu cầu thử nghiệm
3. Theo dõi quá trình xử lý đơn hàng trong Google Sheets

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm các node để gửi thông báo đến các kênh Slack hoặc Telegram khi có đơn hàng mới.
2. **Lưu log chi tiết**: Mở rộng bảng tính Google Sheets để lưu trữ thêm thông tin chi tiết về các đơn hàng.
3. **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp về các đơn hàng đã xử lý hàng ngày.
4. **Tích hợp với các hệ thống khác**: Kết nối với các hệ thống CRM khác để cập nhật thông tin khách hàng sau khi gửi thông báo.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hoàn chỉnh để gửi thông báo trạng thái đơn hàng WooCommerce đến khách hàng qua WhatsApp. Bằng cách tích hợp với Rapiwa API và Google Sheets, workflow giúp các sếp tiết kiệm thời gian, nâng cao trải nghiệm khách hàng và tối ưu hóa quá trình quản lý đơn hàng. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của bạn!