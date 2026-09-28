---
title: "🚀 Tự Động Sửa & Gửi Lại Email Đơn Hàng Khách Lẻ (Guest Order) trong Magento 2 qua REST API"
description: "Giải pháp tự động hóa giúp các store owner sửa email đơn hàng cho khách vãng lai và gửi lại email xác nhận trên Magento 2 ngay lập tức mà không cần can thiệp thủ công."
slug: "sua-va-gui-lai-email-don-hang-magento-2-n8n"
tags: [n8n, automation, magento2, ecommerce, rest-api, crm]
keywords: [n8n workflow, magento 2 fix guest order email, resend order confirmation, tu dong hoa magento, n8n webhook rest api]
---

# 🚀 Tự Động Sửa & Gửi Lại Email Đơn Hàng Khách Lẻ (Guest Order) trong Magento 2 qua REST API

Trong quá trình vận hành cửa hàng thương mại điện tử trên nền tảng Magento 2, việc khách hàng (đặc biệt là khách vãng lai - guest checkout) gõ nhầm địa chỉ email khi đặt hàng là "nỗi đau" cực kỳ phổ biến. Hệ quả là họ không nhận được email xác nhận đơn hàng, dẫn đến hàng loạt ticket phàn nàn gửi về bộ phận chăm sóc khách hàng (CSKH). Việc đội ngũ support phải vào database sửa tay từng đơn rồi kích hoạt lại email vừa tốn thời gian, vừa dễ phát sinh sai sót bảo mật.

Giải pháp hoàn hảo được tác giả **Kanaka Kishore Kandregula** xây dựng chính là workflow n8n này: Tự động hóa 100% quy trình tiếp nhận yêu cầu, kiểm tra đơn hàng, cập nhật email chính xác vào cơ sở dữ liệu MySQL, gọi Magento 2 REST API để gửi lại email xác nhận cho khách hàng chỉ trong chớp mắt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian xử lý:** Đội ngũ CSKH không cần mò mẫm trong phpMyAdmin hay Admin Panel phức tạp.
- **Trải nghiệm khách hàng tuyệt vời:** Khách hàng nhận lại email xác nhận đơn hàng chính xác ngay lập tức sau vài giây.
- **Bảo mật và chuẩn xác:** Thao tác trực tiếp thông qua cơ sở dữ liệu và REST API chuẩn của Magento 2, loại bỏ hoàn toàn lỗi thao tác thủ công.
- **Hoạt động 24/7 tự động:** Workflow sẵn sàng xử lý mọi lúc, mọi nơi ngay khi có yêu cầu được gửi qua form nội bộ.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Magento 2 REST API Credentials:** Token hoặc tài khoản Admin tích hợp (Integration) có quyền truy cập Orders API.
- **MySQL Database Access:** Thông tin kết nối trực tiếp đến database của Magento 2 (Host, Port, User, Password, Database Name).
- **Form Interface:** Giao diện hoặc form nội bộ (n8n Form Trigger) để nhân viên CSKH nhập mã đơn hàng (Increment ID) và email mới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và paste trực tiếp vào n8n Editor của mình. Workflow gồm tổng cộng 7 nodes được bố trí mạch lạc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **On form submission (`formTrigger`):** Thiết kế form nội bộ cho đội ngũ CSKH với 2 trường dữ liệu bắt buộc: *Mã đơn hàng (Increment ID)* và *Địa chỉ email mới*.
- **Get Order By Increment ID (`httpRequest`):** Cấu hình gọi Magento 2 REST API (ví dụ: `/V1/orders?searchCriteria...`) để tìm kiếm thông tin đơn hàng dựa trên Increment ID do nhân viên vừa nhập ở form.
- **Checks If Order Exist (`if`):** Node điều kiện kiểm tra xem API có tìm thấy đơn hàng tồn tại trên hệ thống hay không. Nếu không, workflow sẽ dừng hoặc báo lỗi.
- **Code (`code`):** Xử lý logic bóc tách dữ liệu JSON từ Magento API, chuẩn bị câu lệnh SQL cập nhật dữ liệu và chuẩn bị payload cho bước gọi API tiếp theo.
- **Update Guest Order Email (`mySql`):** Kết nối trực tiếp vào database MySQL của Magento 2 để cập nhật email mới vào bảng `sales_order` (và các bảng liên quan như `sales_order_grid` nếu cần).
- **resend order confirmation (`httpRequest`):** Gọi Magento 2 REST API endpoint chuyên dụng để kích hoạt tính năng gửi lại email xác nhận đơn hàng cho khách.
- **Checks for Resend (`if`):** Node kiểm tra phản hồi từ API xem lệnh gửi lại email đã thành công hay chưa để thông báo kết quả cuối cùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nghiệm bằng một đơn hàng test trên môi trường Staging.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để đưa vào sử dụng thực tế.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình này hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
1. **Tích hợp Slack/Telegram:** Thêm node gửi thông báo về kênh chat nội bộ của team CSKH ngay khi email được sửa và gửi lại thành công.
2. **Lưu Log vào Google Sheets:** Ghi lại lịch sử ai là người yêu cầu sửa email, mã đơn hàng nào, thời gian nào để dễ dàng đối soát khi cần thiết.
3. **Xác thực tự động qua OTP:** Kết hợp thêm bước xác thực danh tính khách hàng trước khi cho phép thay đổi email để tăng cường tính bảo mật cho cửa hàng.

### 📌 Kết luận
Việc tự động hóa quy trình sửa và gửi lại email đơn hàng khách lẻ trong Magento 2 không chỉ giải phóng sức lao động cho đội ngũ vận hành mà còn nâng tầm chuyên nghiệp cho cửa hàng của các sếp. Hãy cài đặt ngay workflow này vào hệ thống n8n để cảm nhận sự khác biệt!