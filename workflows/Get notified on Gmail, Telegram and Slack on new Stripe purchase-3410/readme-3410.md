---
title: "🚀 Tự động thông báo đơn hàng Stripe qua Gmail, Telegram và WhatsApp"
description: "Hướng dẫn cài đặt workflow n8n tự động bắt sự kiện thanh toán thành công trên Stripe, lấy thông tin sản phẩm và bắn thông báo đa kênh lập tức."
slug: "tu-dong-thong-bao-don-hang-stripe-gmail-telegram-whatsapp"
tags: [n8n, automation, stripe, finance, telegram, whatsapp, gmail]
keywords: [n8n workflow, stripe trigger, tự động hóa thanh toán, thông báo đơn hàng stripe, n8n stripe telegram gmail]
---

# 🚀 Tự động thông báo đơn hàng Stripe qua Gmail, Telegram và WhatsApp

Các sếp kinh doanh online chắc chắn đều hiểu cảm giác "hồi hộp" chờ đơn, nhưng việc phải liên tục vào trang quản trị Stripe hay kiểm tra email thủ công vừa mất thời gian lại dễ bỏ lỡ khoảnh khắc chốt đơn quan trọng. Khi có khách hàng thanh toán thành công, việc đội ngũ sale hoặc bản thân các sếp nhận được thông báo ngay lập tức trên điện thoại là cực kỳ cần thiết để chăm sóc khách hàng kịp thời.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động lắng nghe sự kiện từ Stripe, bóc tách thông tin sản phẩm chi tiết và bắn thông báo đa kênh đồng thời qua **Gmail (thiết kế HTML đẹp mắt)**, **Telegram** và **WhatsApp Business** 100% tự động mà không tốn một đồng chi phí vận hành thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nhận thông báo tức thì**: Biến điện thoại thành "tiếng kèn reo" mỗi khi có tiền về tài khoản Stripe từ khách hàng.
- **Đa kênh linh hoạt**: Gửi đồng thời qua Gmail, Telegram và WhatsApp giúp team không bao giờ bỏ sót thông tin đơn hàng dù ở bất cứ đâu.
- **Thông tin chi tiết rõ ràng**: Tự động tổng hợp tên sản phẩm, giá tiền, thông tin khách hàng từ Stripe mà không cần tra cứu thủ công.
- **Hoạt động 24/7 bền bỉ**: Chạy tự động hoàn toàn trên nền tảng n8n, không lo bỏ lỡ đơn hàng kể cả ban đêm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Stripe** (đã có quyền cấu hình Webhook).
- Tài khoản **Telegram Bot** (tạo qua BotFather để lấy Token và Chat ID).
- Tài khoản **WhatsApp Business Cloud** (hoặc Meta Business API credentials).
- Tài khoản **Gmail** (hoặc Google Workspace để gửi email tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này hoặc tải file từ nguồn gốc, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File/Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Stripe Trigger**: 
  - Kết nối tài khoản Stripe của các sếp.
  - Cấu hình lắng nghe sự kiện thanh toán thành công (thường là sự kiện `checkout.session.completed` hoặc `payment_intent.succeeded`).
- **Filter by paid only**: 
  - Đảm bảo điều kiện lọc chỉ nhận các giao dịch đã thanh toán thành công (paid = true) để tránh bắn thông báo nhầm với các đơn hàng lỗi/chưa thanh toán.
- **Stripe | Get checkout line items** & **Stripe | Get product info** (Node HTTP Request): 
  - Kiểm tra lại các endpoint API của Stripe để đảm bảo n8n lấy đúng thông tin chi tiết sản phẩm và giỏ hàng của phiên thanh toán.
- **Telegram** & **WhatsApp Business Cloud**: 
  - Nhập **Bot Token** và **Chat ID / Phone Number ID** chính xác của các sếp để bot có thể gửi tin nhắn thành công.
- **Email with HTML design (Gmail)**: 
  - Chọn credential tài khoản Gmail cá nhân hoặc doanh nghiệp.
  - Tùy chỉnh tiêu đề và mẫu HTML nội dung email gửi cho khách hàng hoặc cho chính nội bộ team quản lý.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thực hiện một giao dịch test trên Stripe (hoặc sử dụng tính năng Test Event của Stripe) để kiểm tra luồng chạy dữ liệu qua các node.
- Nếu dữ liệu chảy xanh mướt từ đầu đến cuối, các sếp chỉ cần gạt công tắc sang **Active** để hệ thống chính thức hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu vào Google Sheets**: Thêm một node Google Sheets vào sau bước `Set Fields` để lưu toàn bộ lịch sử đơn hàng phục vụ cho việc thống kê doanh thu.
- **Bắn tin nhắn vào nhóm nội bộ Slack**: Thay vì chỉ gửi cá nhân qua Telegram/WhatsApp, các sếp có thể kết hợp thêm node Slack để đẩy thông báo vào channel chung của team Sale & CSKH.
- **Gửi email tự động cảm ơn khách hàng**: Tách luồng email thành 2 nhánh: một gửi cho nội bộ (như hiện tại) và một gửi hóa đơn/thư cảm ơn tự động cho chính khách hàng vừa mua sản phẩm.

### 📌 Kết luận
Workflow tự động hóa thông báo đơn hàng Stripe qua Gmail, Telegram và WhatsApp này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình vận hành kinh doanh số. Hãy cài đặt ngay hôm nay để quản lý dòng tiền và đơn hàng một cách chuyên nghiệp, nhanh chóng nhất!