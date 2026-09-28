---
title: "🛒 Tự Động Báo Cáo Giỏ Hàng Bỏ Rơi Shopify + Razorpay qua Telegram"
description: "Workflow n8n giúp các sếp tự động quét đơn hàng chưa thanh toán trên Razorpay (kết nối Shopify) và gửi cảnh báo chi tiết qua Telegram mỗi 6 giờ, không cần code."
slug: "bao-cao-gio-hang-bo-roi-shopify-razorpay-telegram"
tags: [n8n, automation, no-code, shopify, razorpay, telegram, crm]
keywords: [n8n workflow, tự động hóa bán hàng, giỏ hàng bỏ rơi, razorpay integration, telegram alert]
---

# 🛒 Tự Động Báo Cáo Giỏ Hàng Bỏ Rơi Shopify + Razorpay qua Telegram

Trong kinh doanh thương mại điện tử, "giỏ hàng bỏ rơi" (abandoned cart) là kẻ thù thầm lặng ăn mòn doanh thu. Khách hàng thêm sản phẩm vào giỏ, điền thông tin nhưng lại rời đi trước khi hoàn tất thanh toán. Nếu các sếp đang dùng Shopify kết hợp cổng thanh toán Razorpay, việc theo dõi thủ công những đơn hàng này là cực kỳ tốn thời gian và dễ sót.

Workflow này được thiết kế để giải quyết vấn đề đó một cách hoàn toàn tự động. Nó sẽ định kỳ quét hệ thống Razorpay, lọc ra các đơn hàng ở trạng thái "đã tạo nhưng chưa thanh toán" (created) trong một khung thời gian nhất định, và gửi ngay thông báo chi tiết vào Telegram của các sếp. Chỉ với 5 nodes đơn giản, các sếp có thể nắm bắt cơ hội "chốt đơn" lại mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian kiểm tra thủ công:** Hệ thống tự động quét và báo cáo, các sếp chỉ việc xem tin nhắn.
- **Tăng tỷ lệ chuyển đổi:** Nhận được cảnh báo sớm giúp các sếp kịp thời liên hệ khách hàng (qua email/SMS/Chat) để nhắc thanh toán.
- **Dữ liệu chính xác:** Chỉ lọc các đơn hàng thực sự chưa thanh toán trong khung thời gian gần nhất, tránh spam tin nhắn cũ.
- **Cá nhân hóa linh hoạt:** Dễ dàng chỉnh sửa tần suất quét và khung thời gian lọc theo chiến lược bán hàng của mình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Razorpay:** Có quyền truy cập API (Key ID và Key Secret).
2. **Tài khoản Telegram:** Tạo Bot qua @BotFather để lấy Bot Token.
3. **ID Telegram:** ID chat hoặc kênh mà các sếp muốn nhận thông báo.
4. **n8n Instance:** Đã cài đặt và chạy (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc [n8n.io/workflows/8092](https://n8n.io/workflows/8092) hoặc copy toàn bộ code JSON bên dưới, sau đó vào n8n Editor -> **Import from URL** hoặc **Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại 3 node chính sau đây:

**1. Node: `Cron (every 6h)`**
- Đây là node kích hoạt workflow. Mặc định chạy mỗi 6 giờ.
- Các sếp có thể chỉnh sửa biểu thức Cron nếu muốn tần suất khác (ví dụ: mỗi 1 giờ, mỗi 30 phút).
- *Gợi ý:* Nếu lưu lượng đơn hàng lớn, nên quét thường xuyên hơn (30-60 phút) để kịp thời can thiệp.

**2. Node: `HTTP → Razorpay Orders`**
- Đây là node gọi API Razorpay để lấy danh sách đơn hàng.
- **Credentials:** Chọn hoặc tạo mới credential type `httpBasicAuth`.
  - Username: `Key ID` của Razorpay.
  - Password: `Key Secret` của Razorpay.
- **URL:** Mặc định là `https://api.razorpay.com/v1/orders`.
- **Query Parameters:** Node này thường được cấu hình để lấy các đơn hàng gần nhất. Các sếp kiểm tra lại tham số `count` và `from`/`to` nếu cần, nhưng thường node Code bên dưới sẽ xử lý logic lọc thời gian nên node này chỉ cần lấy dữ liệu thô.

**3. Node: `Window (last 2h)` & `Filter status=created + Format`**
- **Node `Window (last 2h)`:** Node Code này tính toán khung thời gian (ví dụ: 2 giờ trước đó). Các sếp có thể sửa số `2` trong code nếu muốn mở rộng hoặc thu hẹp khung thời gian quét (ví dụ: `last 1h` hoặc `last 4h`).
- **Node `Filter status=created + Format`:** Node Code này lọc các đơn hàng có `status` là `created` (chưa thanh toán) và định dạng dữ liệu thành tin nhắn dễ đọc.
- *Lưu ý:* Thông thường không cần chỉnh sửa code trong 2 node này trừ khi các sếp muốn thay đổi logic lọc (ví dụ: chỉ lọc đơn hàng có giá trị > 500k).

**4. Node: `Telegram → Me`**
- **Credentials:** Chọn hoặc tạo mới credential type `Telegram`.
  - Bot Token: Token từ @BotFather.
- **Chat ID:** Điền ID Telegram của các sếp (hoặc ID kênh).
- **Message:** Kiểm tra phần template message. Workflow đã định dạng sẵn tên khách hàng, email, tổng tiền, và link chi tiết đơn hàng. Các sếp có thể tùy chỉnh thêm emoji hoặc lời chào.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** để chạy thử. Kiểm tra xem có nhận được tin nhắn Telegram không.
2. **Active Workflow:** Bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động theo lịch Cron đã thiết lập.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI để viết tin nhắn nhắc nợ:** Thay vì gửi tin nhắn tĩnh, các sếp có thể thêm node `OpenAI` hoặc `Claude` để tạo ra nội dung nhắc thanh toán cá nhân hóa, thân thiện hơn dựa trên lịch sử mua hàng của khách.
- **Gửi Email tự động:** Thêm node `Gmail` hoặc `SendGrid` sau khi nhận được cảnh báo Telegram để tự động gửi email nhắc thanh toán cho khách hàng.
- **Lưu log vào Google Sheets:** Thêm node `Google Sheets` để lưu lại lịch sử các đơn hàng bỏ rơi đã được cảnh báo, giúp các sếp phân tích xu hướng và hiệu quả của chiến dịch nhắc nợ.
- **Phân quyền theo nhân viên:** Nếu có nhiều nhân viên chăm sóc khách hàng, các sếp có thể tạo nhiều workflow hoặc sử dụng node `Switch` để phân bổ đơn hàng cho từng người dựa trên khu vực hoặc loại sản phẩm.

### 📌 Kết luận
Việc bỏ sót các đơn hàng chưa thanh toán là một thiệt hại không đáng có. Với workflow n8n này, các sếp có thể biến "giỏ hàng bỏ rơi" thành "doanh thu tiềm năng" chỉ với vài phút cấu hình. Hãy import, chỉnh sửa credentials và bật Active ngay hôm nay để bắt đầu tối ưu hóa quy trình bán hàng của mình!