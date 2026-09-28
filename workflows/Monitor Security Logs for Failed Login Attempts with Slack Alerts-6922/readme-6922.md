---
title: "🚀 Giám sát log bảo mật & Cảnh báo đăng nhập thất bại qua Slack với n8n"
description: "Tự động phát hiện sớm các cuộc tấn công brute-force và đăng nhập bất thường từ hệ thống log, gửi cảnh báo chi tiết qua Slack ngay lập tức."
slug: "giam-sat-log-bao-mat-canh-bao-dang-nhap-that-bai-slack"
tags: [n8n, automation, secops, slack, security, log-monitoring]
keywords: [n8n workflow, giám sát bảo mật, cảnh báo slack, phát hiện xâm nhập, security automation, siem lightweight]
---

# 🚀 Tự động Giám sát Log Bảo mật & Cảnh báo Đăng nhập Thất bại qua Slack

Các sếp có đang đau đầu vì việc kiểm tra log hệ thống thủ công mỗi ngày để tìm kiếm các dấu hiệu tấn công như brute-force hay dò mật khẩu? Việc bỏ sót các mẫu dữ liệu bất thường (như hàng loạt lần đăng nhập thất bại trong thời gian ngắn) có thể tạo cơ hội cho kẻ xấu xâm nhập hệ thống mà không hề hay biết.

Giải pháp thủ công vừa tốn thời gian, vừa kém hiệu quả. Đó chính là lý do workflow n8n **Simple Log Anomaly Detector** ra đời – giúp tự động hóa 100% quá trình kiểm tra log, phát hiện bất thường và bắn tin cảnh báo ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sớm mối đe dọa:** Tự động quét log theo lịch trình (ví dụ: mỗi 15 phút) mà không cần con người can thiệp.
- **Cảnh báo tức thì:** Gửi thông tin chi tiết (số lần thất bại, danh sách IP nghi vấn) thẳng vào kênh Slack của đội ngũ kỹ thuật.
- **Giảm thiểu rủi ro bảo mật:** Xây dựng hệ thống SIEM thu nhỏ với chi phí 0 đồng, cực kỳ phù hợp cho SMEs và đội ngũ SysAdmin.
- **Hoạt động bền bỉ 24/7:** Chạy ngầm liên tục, đảm bảo không bỏ sót bất kỳ hành vi đáng ngờ nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- API Endpoint cung cấp log hệ thống (server, ứng dụng...).
- Slack Workspace và quyền tạo/kết nối Bot để gửi tin nhắn thông báo (Slack API Credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính hoạt động nhịp nhàng:

- **Schedule Trigger:** Node khởi chạy định kỳ. Các sếp hãy cấu hình thời gian chạy phù hợp (ví dụ: chạy mỗi 15 phút một lần).
- **Fetch Logs (HTTP Request Node):** Cấu hình URL endpoint của API log hệ thống, kèm theo các header/token xác thực nếu API yêu cầu bảo mật.
- **Count Failed Logins (Code Node):** Node JavaScript xử lý logic đếm số lần `login_failure` và lọc ra các địa chỉ IP độc hại. Các sếp có thể tùy chỉnh đoạn code bên trong nếu cấu trúc log của bên mình khác biệt.
- **Failed Logins > Threshold? (If Node):** Thiết lập ngưỡng cảnh báo (Threshold). Ví dụ: nếu số lần đăng nhập thất bại vượt quá 5 lần trong khung thời gian quét, workflow sẽ cho phép đi tiếp.
- **Send Anomaly Alert (Slack Node):** Kết nối với tài khoản Slack của công ty (`slackApi`), chọn kênh (Channel) nhận cảnh báo và tùy chỉnh nội dung tin nhắn hiển thị số lượng lỗi cùng danh sách IP.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu mẫu xem log có được fetch và xử lý chính xác không.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow chính thức gác cổng cho hệ thống 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống bảo mật trở nên "xịn sò" hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng:
- **Tích hợp thêm Telegram/Discord:** Song song với Slack, gửi thêm cảnh báo vào nhóm Telegram riêng của đội DevOps.
- **Lưu lịch sử cảnh báo:** Đẩy thông tin các cuộc tấn công vào Google Sheets hoặc Database để làm báo cáo kiểm tra định kỳ hàng tuần.
- **Tự động hóa chặn IP (Nâng cao):** Kết hợp thêm một HTTP Request gọi tới Firewall API (như Cloudflare hoặc Fail2ban) để tự động đưa IP tấn công vào danh sách đen (Blacklist).

### 📌 Kết luận
Bảo mật hệ thống chưa bao giờ là việc dễ dàng nhưng với n8n, các sếp hoàn toàn có thể tự động hóa khâu giám sát ban đầu chỉ với vài phút cài đặt. Hãy áp dụng ngay workflow này để bảo vệ hệ thống của doanh nghiệp trước các cuộc tấn công dò mật khẩu!