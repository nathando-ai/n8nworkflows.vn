---
title: "🚀 Tự Động Hóa Xác Nhận Đơn Hàng Abacate Pay & Tặng Voucher Cho Khách Mới"
description: "Workflow n8n tự động gửi email xác nhận đơn hàng qua Abacate Pay, thông báo Slack cho đội ngũ và tặng voucher giảm giá 10% cho khách hàng mua lần đầu tiên."
slug: "tu-dong-hoa-xac-nhan-don-hang-abacate-pay"
tags: [n8n, automation, no-code, abacate-pay, crm, email-marketing]
keywords: [n8n workflow, abacate pay, tự động hóa đơn hàng, tặng voucher khách mới, tích hợp slack]
---

# 🚀 Tự Động Hóa Xác Nhận Đơn Hàng Abacate Pay & Tặng Voucher Cho Khách Mới

Trong kinh doanh thương mại điện tử, tốc độ phản hồi sau khi khách hàng thanh toán thành công là yếu tố sống còn. Việc xác nhận đơn hàng chậm trễ hoặc thiếu cá nhân hóa không chỉ gây trải nghiệm kém mà còn bỏ lỡ cơ hội vàng để tăng tỷ lệ quay lại mua hàng (retention).

Thay vì phải lập trình thủ công để kiểm tra xem khách hàng có phải là người mua lần đầu hay không, sau đó tạo voucher và gửi email, workflow này giúp các sếp tự động hóa toàn bộ quy trình chỉ với **Abacate Pay**, **Email** và **Slack**. Đặc biệt, workflow sẽ "thông minh" phát hiện khách hàng mới và tự động tạo mã giảm giá 10% cho đơn tiếp theo, gửi kèm trong email xác nhận.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tỷ lệ quay lại mua hàng:** Khách hàng mới nhận được voucher giảm giá 10% ngay lập tức, tạo động lực quay lại.
- **Trải nghiệm khách hàng liền mạch:** Email xác nhận được gửi tức thì sau khi thanh toán thành công, kèm thông tin đơn hàng chi tiết.
- **Đồng bộ nội bộ nhanh chóng:** Đội ngũ vận hành nhận thông báo chi tiết trên Slack ngay khi có đơn mới, giúp xử lý hàng hóa kịp thời.
- **Không cần code phức tạp:** Logic kiểm tra "khách hàng mới" và tạo voucher được xử lý tự động qua API Abacate Pay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Abacate Pay:** Cần có API Key và Secret Key để gọi API tra cứu đơn hàng và tạo voucher.
- **Tài khoản SMTP:** Để gửi email xác nhận (Gmail, SendGrid, Mailgun, hoặc SMTP server riêng).
- **Tài khoản Slack:** Cần có Webhook URL hoặc API Token để gửi thông báo vào channel nội bộ.
- **n8n Instance:** Chạy local hoặc trên VPS.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Nếu copy JSON, chọn **Import from Clipboard** và dán vào.
4. Workflow sẽ hiện ra với các node đã được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình để workflow hoạt động đúng:

**1. Node `Configs` (Set Node)**
Đây là node trung tâm chứa các biến cấu hình. Các sếp cần chỉnh sửa các trường sau:
- `companyName`: Tên công ty của bạn (hiển thị trong email).
- `siteUrl`: Link website của bạn.
- `webhookValidationToken`: Một chuỗi ký tự ngẫu nhiên để xác thực webhook (tránh spam). Hãy đặt một chuỗi mạnh như `my-secret-token-123`.
- `slackChannel`: Tên channel Slack cần nhận thông báo (ví dụ: `#orders`).
- `emailSubject`: Tiêu đề email mặc định.

**2. Node `Webhook`**
- Mặc định path là `1b27997e-c86e-4f3d-ac12-61a79400bb1d`. Các sếp có thể giữ nguyên hoặc đổi path tùy thích.
- **Quan trọng:** Sau khi cấu hình xong, copy **Production URL** của webhook này để cấu hình trong hệ thống Abacate Pay (tại phần cài đặt Webhook/Notification).

**3. Node `CheckToken` (If Node)**
- Node này kiểm tra xem token trong payload có khớp với `webhookValidationToken` ở node `Configs` không.
- Nếu khớp, luồng đi tiếp. Nếu không, sẽ đi sang `RespondError` và trả về lỗi 401.

**4. Node `GetOrders` (HTTP Request)**
- Đây là node gọi API Abacate Pay để lấy chi tiết đơn hàng.
- **Authentication:** Chọn `Header Auth` hoặc `Basic Auth` tùy theo tài liệu API của Abacate Pay.
- **Headers/Body:** Điền `API Key` và `Secret Key` của Abacate Pay vào đây.
- **URL:** Kiểm tra URL API tra cứu đơn hàng (thường là endpoint `GET /orders/{id}`).

**5. Node `CheckFirstOrder` (Code Node)**
- Node này xử lý logic: So sánh số lượng đơn hàng của khách hàng.
- Nếu đây là đơn hàng đầu tiên, nó sẽ set flag `isFirstOrder = true`.
- Các sếp không cần sửa code này trừ khi logic nghiệp vụ thay đổi (ví dụ: tặng voucher cho 3 đơn đầu tiên).

**6. Node `CreateCustomCoupon` (HTTP Request)**
- Chỉ chạy khi `isFirstOrder` là `true`.
- Gọi API Abacate Pay để tạo một voucher giảm giá 10% mới.
- **Authentication:** Tương tự node `GetOrders`, cần điền API Key/Secret.
- **Body:** Cấu hình giá trị giảm giá (10%), thời hạn sử dụng, và điều kiện áp dụng.

**7. Node `MakeBodyEmail` (Code Node)**
- Node này tổng hợp thông tin đơn hàng, thông tin khách hàng và mã voucher (nếu có) để tạo nội dung email HTML.
- Các sếp có thể chỉnh sửa template HTML trong code node này để phù hợp với thương hiệu (thêm logo, màu sắc, font chữ).

**8. Node `Send Email` (Email Send)**
- **Credentials:** Chọn hoặc tạo credentials SMTP mới.
- **To:** Lấy từ biến `customerEmail` (đã được extract từ API Abacate Pay).
- **Subject & HTML:** Đã được map từ node `MakeBodyEmail`.

**9. Node `Slack` (Slack Node)**
- **Credentials:** Chọn credentials Slack API.
- **Channel:** Điền tên channel (ví dụ: `#orders`).
- **Message:** Node này sẽ gửi một block message chi tiết bao gồm: Tên khách, ID đơn, Tổng tiền, và trạng thái "KHÁCH MỚI" (nếu có voucher).

**10. Node `If` (Cuối luồng)**
- Kiểm tra lại trạng thái gửi email và Slack. Nếu thành công, workflow kết thúc. Nếu lỗi, có thể thêm node `Error Trigger` để xử lý.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Tạo một đơn hàng test trên Abacate Pay (hoặc dùng sandbox mode nếu có).
   - Đảm bảo webhook từ Abacate Pay được gửi đến URL Production của n8n.
   - Quan sát luồng chạy: Webhook -> Check Token -> Get Orders -> Check First Order -> (Tạo Voucher nếu cần) -> Send Email -> Slack.
   - Kiểm tra hộp thư email và kênh Slack xem thông tin có chính xác không.
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n.
   - Workflow sẽ sẵn sàng xử lý mọi đơn hàng thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh Voucher:** Thay vì cố định 10%, các sếp có thể dùng node `Code` để tính toán voucher dựa trên giá trị đơn hàng (ví dụ: đơn > 1 triệu tặng 15%).
- **Tích hợp CRM:** Thêm node `HubSpot` hoặc `Salesforce` để tự động cập nhật trạng thái khách hàng thành "Active" hoặc thêm tag "First Buyer" vào hồ sơ CRM.
- **Gửi SMS:** Thêm node `Twilio` hoặc `Viettel SMS` để gửi tin nhắn xác nhận đơn hàng, tăng tỷ lệ mở thông tin lên 90% so với email.
- **Báo cáo định kỳ:** Thêm node `Cron` để tổng hợp số lượng đơn hàng mới và voucher đã phát ra mỗi tuần, gửi báo cáo cho quản lý.

### 📌 Kết luận
Workflow này không chỉ giải quyết bài toán xác nhận đơn hàng mà còn là một công cụ marketing tự động hóa cực kỳ hiệu quả. Bằng cách tặng voucher cho khách hàng mới, các sếp đang đầu tư vào việc xây dựng lòng trung thành ngay từ lần chạm đầu tiên. Hãy import, cấu hình và bật Active ngay hôm nay để trải nghiệm sự khác biệt trong quy trình vận hành!