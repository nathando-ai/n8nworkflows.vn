---
title: "🚀 Tự động nhận thông báo qua Telegram khi số dư Meta Ads cạn kiệt bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động kiểm tra số dư tài khoản quảng cáo Facebook (Meta Ads) định kỳ và gửi cảnh báo qua Telegram để tránh gián đoạn chiến dịch."
slug: "tu-dong-thong-bao-so-du-meta-ads-qua-telegram-n8n"
tags: [n8n, automation, meta-ads, facebook-marketing, telegram, marketing-automation]
keywords: [n8n workflow, tự động hóa meta ads, kiểm tra số dư facebook ads, cảnh báo số dư ads telegram, facebook graph api n8n]
---

# 🚀 Tự động nhận thông báo qua Telegram khi số dư Meta Ads cạn kiệt

Trong quá trình chạy quảng cáo Facebook (Meta Ads), việc tài khoản bất ngờ hết tiền dẫn đến chiến dịch bị dừng đột ngột là "nỗi đau" của không ít nhà quảng cáo và doanh nghiệp. Điều này làm lỡ nhịp tiếp cận khách hàng và lãng phí thời gian kiểm tra thủ công mỗi ngày. 

Giải pháp tuyệt vời cho các sếp đây: Workflow n8n tự động hóa 100% giúp kiểm tra số dư tài khoản Meta Ads định kỳ và ngay lập tức bắn tin nhắn cảnh báo qua Telegram khi số dư tụt xuống mức nguy hiểm. Không cần code phức tạp, setup một lần chạy mượt mà mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động 24/7:** Hệ thống tự động quét số dư tài khoản quảng cáo đều đặn mỗi 12 giờ mà không cần con người nhúng tay.
- **Phản ứng tức thì:** Nhận thông báo trực tiếp qua Telegram ngay khi số dư thấp hơn ngưỡng cho phép (ví dụ: dưới 400).
- **Tránh gián đoạn chiến dịch:** Giúp nạp tiền kịp thời, giữ cho quảng cáo chạy liên tục không bị bóp tương tác hay đứt quãng.
- **Tiết kiệm thời gian:** Dẹp bỏ hoàn toàn thói quen phải truy cập Meta Ads Manager thủ công mỗi ngày chỉ để check tiền trong tài khoản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn:
- Một instance **n8n** đang hoạt động ổn định.
- **Meta (Facebook) Developer Account & Access Token** có quyền truy cập vào Facebook Graph API (để lấy thông tin tài khoản quảng cáo).
- **Telegram Bot Token** và **Chat ID** (tạo qua BotFather) để nhận tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn gốc hoặc tạo mới, sau đó paste trực tiếp vào n8n Editor của mình. Workflow gồm 8 nodes được bố trí mạch lạc từ kích hoạt lịch trình đến gọi API và gửi cảnh báo.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình kỹ các node sau:
- **Every 12h (`scheduleTrigger`):** Node này mặc định kích hoạt chạy 12 tiếng một lần. Các sếp có thể tuỳ chỉnh lại tần suất chạy (ví dụ: 6 tiếng/lần hoặc theo giờ hành chính) nếu muốn kiểm tra dày hơn.
- **Method 1 & Method 2 (`facebookGraphApi`):** Đây là hai node cốt lõi gọi đến Facebook Graph API để truy vấn thông tin tài khoản quảng cáo và số dư. Các sếp cần cấu hình **Credentials** (Facebook Graph API Token) và điền đúng **Ad Account ID**.
- **Lower than 400 ? (`if`):** Node điều kiện để kiểm tra số dư thực tế. Mặc định đang đặt mốc so sánh là `400`. Các sếp hãy thay đổi con số này thành mức tiền tối thiểu phù hợp với ngân sách của doanh nghiệp (ví dụ: 500,000 VNĐ hoặc tùy loại tiền tệ tài khoản).
- **Send message (`telegram`):** Kết nối với tài khoản Telegram Bot của sếp. Điền chính xác **Chat ID** của cá nhân hoặc nhóm chat nội bộ để bot gửi tin nhắn hú còi khi tài khoản đói vốn.
- **Edit Fields / Edit Fields1 (`set`):** Dùng để chuẩn hóa dữ liệu đầu ra từ API trước khi đẩy qua bước kiểm tra điều kiện hoặc gửi thông báo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử nghiệm xem dữ liệu từ Facebook Graph API có trả về chính xác hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow chính thức vào ca trực 24/7.

### ✍️ Nâng cao & Gợi ý mở rộng
Để hệ thống xịn xò hơn nữa, các sếp có thể tùy biến:
- **Đa kênh thông báo:** Kết hợp thêm node Slack hoặc Discord bên cạnh Telegram để team Marketing và Kế toán cùng nắm tình hình tài chính ads.
- **Lưu log Google Sheets:** Đưa lịch sử kiểm tra số dư vào Google Sheets để tracking biến động chi tiêu quảng cáo theo ngày/tuần.
- **Cảnh báo nhiều tài khoản:** Nhân bản nhánh API để theo dõi cùng lúc nhiều Ad Account của công ty chỉ trên một workflow duy nhất.

### 📌 Kết luận
Việc kiểm soát số dư quảng cáo chưa bao giờ dễ dàng đến thế với sức mạnh của tự động hóa n8n. Hãy cài đặt ngay workflow này để bảo vệ các chiến dịch marketing của doanh nghiệp khỏi việc "cháy tài khoản" bất ngờ các sếp nhé!