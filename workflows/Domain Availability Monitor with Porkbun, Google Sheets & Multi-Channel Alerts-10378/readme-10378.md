---
title: "🚀 Tự động giám sát tên miền với Porkbun, Google Sheets và Đa kênh thông báo trên n8n"
description: "Hướng dẫn xây dựng hệ thống tự động kiểm tra trạng thái tên miền từ Porkbun, lưu trữ qua Google Sheets và gửi cảnh báo tức thì qua Gmail, Discord khi tên miền khả dụng."
slug: "tu-dong-giam-sat-ten-mien-porkbun-google-sheets-n8n"
tags: [n8n, automation, no-code, porkbun, google-sheets, discord, gmail]
keywords: [n8n workflow, tự động hóa tên miền, kiểm tra domain porkbun, google sheets automation, discord alert n8n]
---

# 🚀 Tự động giám sát tên miền với Porkbun, Google Sheets và Đa kênh thông báo

Các sếp đang săn lùng những tên miền đẹp nhưng bị người khác "xí phần"? Việc cứ vài tiếng lại phải vào trang kiểm tra domain thủ công vừa tốn thời gian, lại vừa dễ bỏ lỡ khoảnh khắc vàng khi tên miền hết hạn và nhả ra.

Đừng lo, workflow n8n này sẽ thay các sếp "trực chiến" 24/7. Hệ thống sẽ tự động quét danh sách tên miền từ Google Sheets thông qua Porkbun API, kiểm tra tính khả dụng và ngay lập tức gửi báo cáo qua Gmail, Discord đồng thời cập nhật trạng thái ngược lại vào Google Sheet ngay khi domain sẵn sàng để đăng ký!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần canh me thủ công, hệ thống tự động kiểm tra định kỳ (ví dụ: mỗi 30 phút).
- **Cảnh báo đa kênh tức thì**: Nhận thông báo ngay lập tức qua Gmail và Discord khi có tên miền "rơi tự do".
- **Đồng bộ dữ liệu mượt mà**: Tự động cập nhật trạng thái "Available" vào Google Sheets để dễ dàng theo dõi.
- **Vận hành an toàn**: Cơ chế ngắt quãng thông minh (`Wait 10 Seconds`) giúp tránh việc bị Porkbun chặn API do gửi request quá dày đặc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Porkbun** kèm API Keys (`API Key` và `Secret API Key`).
- **Google Sheets**: File chứa danh sách các tên miền cần theo dõi.
- **Tài khoản Gmail** (hoặc Credentials Gmail OAuth2).
- **Discord Bot** kèm Webhook/Token để bắn thông báo lên kênh chat.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy ngon lành, các sếp cần cấu hình chính xác các node sau:

- **Node `Check every 30 Minutes` (Schedule Trigger)**: 
  - Thiết lập chu kỳ thời gian chạy kiểm tra (mặc định là 30 phút hoặc tùy chỉnh theo nhu cầu săn domain của các sếp).
- **Node `Get Domains from Sheet` (Google Sheets)**: 
  - Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`.
  - Chỉ định đúng **Document ID** và **Sheet Name** chứa danh sách domain cần check.
- **Node `Validate API KEY` & `Check Domain Availability` (HTTP Request)**: 
  - Cần lấy thông tin API từ Porkbun theo hướng dẫn:
    1. Đăng nhập vào [Porkbun API Settings](https://porkbun.com/account/api).
    2. Click **"Create API Key"**, copy **API Key** (bắt đầu bằng `pk1_`) và **Secret API Key** (bắt đầu bằng `sk1_`).
    3. Đưa thông tin này vào phần Header/Body của các HTTP Request node trong n8n.
- **Node `Send Email Alert` (Gmail)**: 
  - Chọn Credentials Gmail OAuth2 và cấu hình nội dung email gửi đến khi phát hiện domain trống.
- **Node `Send Discord Notification` (Discord)**: 
  - Thiết lập `discordBotApi` và điền Channel ID để bot bắn tin nhắn cảnh báo.
- **Node `Update Sheet: Mark Available` (Google Sheets)**: 
  - Cấu hình thao tác `update` để ghi nhận lại trạng thái tên miền đã có thể mua vào Google Sheets.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) với 1-2 domain mẫu trong Google Sheets để kiểm tra luồng chạy từ HTTP Request đến Discord/Gmail.
- Sau khi mọi thứ mượt mà, bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram**: Thêm node Telegram Bot bên cạnh Discord để nhận thông báo nhanh ngay trên điện thoại cá nhân.
- **Lưu lịch sử log**: Tạo thêm một tab "History" trong Google Sheets để ghi lại lịch sử mỗi lần quét (kể cả lúc domain chưa available).
- **Tự động mua hộ (Advanced)**: Nếu Porkbun hỗ trợ API đăng ký (hoặc qua bên thứ 3), các sếp có thể nâng cấp workflow để auto-checkout khi domain vừa nhả ra (cân nhắc kỹ về bảo mật tài chính).

### 📌 Kết luận
Săn domain hụt nay chỉ là quá khứ! Với workflow n8n tự động hóa kết hợp giữa Porkbun, Google Sheets và đa kênh thông báo, các sếp sẽ luôn là người đầu tiên biết tên miền yêu thích sẵn sàng để sở hữu. Triển khai ngay thôi nào!