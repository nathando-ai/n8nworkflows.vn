---
title: "🚀 Tự động giám sát tên miền .my với MYNIC RDAP và gửi cảnh báo qua Gmail, Discord"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra trạng thái tên miền .my thông qua RDAP, cập nhật Google Sheets và gửi thông báo tức thì qua Gmail, Discord."
slug: "giam-sat-ten-mien-mynic-rdap-n8n"
tags: [n8n, automation, no-code, monitoring, google-sheets, gmail, discord]
keywords: [n8n workflow, giám sát tên miền, MYNIC RDAP, tự động hóa n8n, check domain .my]
---

# 🚀 Tự động giám sát tên miền .my với MYNIC RDAP và gửi cảnh báo qua Gmail, Discord

Việc theo dõi các tên miền tiềm năng (đặc biệt là các tên miền .my) để săn domain vừa hết hạn hoặc kiểm tra trạng thái đăng ký thủ công là một công việc tẻ nhạt, tốn nhiều thời gian và rất dễ bỏ lỡ cơ hội. Nếu các sếp đang ôm mộng sở hữu những cái tên đẹp nhưng lại không muốn ngồi F5 liên tục, workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp giải quyết trọn vẹn bài toán đó.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7**: Hệ thống tự động kiểm tra định kỳ mỗi 30 phút mà không cần con người can thiệp.
- **Cảnh báo tức thì**: Nhận ngay thông báo qua cả Gmail và kênh Discord ngay khi tên miền vừa "thả tự do".
- **Đồng bộ dữ liệu mượt mà**: Tự động cập nhật trạng thái `isAvailable` vào Google Sheets để không bao giờ check trùng lặp.
- **Không tốn phí API**: Tận dụng hoàn toàn cổng RDAP công khai của MYNIC mà không cần mua hay cấu hình API Key phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets**: Tài khoản Google chứa danh sách tên miền cần theo dõi.
- **Gmail Account**: Tài khoản Gmail để gửi email cảnh báo.
- **Discord Bot**: Bot hoặc Webhook kết nối với kênh Discord nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON) vào không gian làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Schedule: Every 30 Minutes**: Node này quyết định tần suất quét. Các sếp có thể thay đổi thời gian chạy nếu muốn kiểm tra nhanh hơn hoặc chậm hơn.
- **Fetch Target Domains from Sheet**: Kết nối tài khoản `googleSheetsOAuth2Api`, chọn file Google Sheets và sheet tương ứng chứa danh sách tên miền cần theo dõi (`isAvailable = no`).
- **RDAP: Check Domain Status (`httpRequest`)**: Sử dụng Endpoint công khai: `https://rdap.mynic.my/rdap/domain/{domain}`. Node này sẽ gọi API để lấy dữ liệu trạng thái thực tế của tên miền.
- **Domain Available? (`if`)**: Kiểm tra phản hồi từ RDAP xem có chứa chuỗi `"is available for registration"` hay không để phân nhánh xử lý.
- **Gmail: Send Availability Alert**: Kết nối `gmailOAuth2` để cấu hình người nhận email thông báo khi domain sẵn sàng đăng ký.
- **Discord: Notify Available Domain**: Kết nối `discordBotApi` để đẩy tin nhắn thông báo trực tiếp vào channel Discord đã định trước.
- **Update Sheet: Mark Available**: Kết nối lại Google Sheets để cập nhật trạng thái cột tương ứng thành `yes` sau khi phát hiện domain đã tự do, tránh bị spam thông báo ở các lần quét sau.
- **Wait 10 Seconds**: Giúp giãn cách thời gian giữa các request trong vòng lặp, tránh việc bị giới hạn tốc độ (rate limit) từ server MYNIC.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài dòng dữ liệu mẫu trong Google Sheets để đảm bảo luồng chạy từ kiểm tra RDAP đến gửi Gmail, Discord và cập nhật Sheet diễn ra hoàn hảo.
- Bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Gmail và Discord, các sếp có thể tích hợp thêm Telegram Bot hoặc Slack để nhận tin nhắn ngay trên điện thoại cực kỳ tiện lợi.
- **Quản lý lịch sử**: Thêm một bước ghi log (ghi thời gian check, kết quả phản hồi) vào một sheet phụ để thống kê và phân tích lịch sử biến động của tên miền.
- **Lọc thông minh**: Kết hợp thêm các điều kiện lọc ký tự hoặc độ dài tên miền trước khi đưa vào vòng lặp check.

### 📌 Kết luận
Với workflow này, việc săn lùng các tên miền .my đẹp chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy cài đặt ngay để không bỏ lỡ bất kỳ cơ hội sở hữu tên miền vàng nào các sếp nhé!