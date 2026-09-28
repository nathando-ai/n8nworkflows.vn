---
title: "🚀 Tự động gửi yêu cầu kết nối LinkedIn cá nhân hóa với Google Sheets và Unipile"
description: "Hướng dẫn tự động hóa gửi yêu cầu kết nối LinkedIn cá nhân hóa từ Google Sheets với n8n, giúp tiết kiệm thời gian và duy trì sự chuyên nghiệp trong quá trình kết nối."
slug: "tu-dong-gui-yeu-cau-ket-noi-linkedin-ca-nhan-hoa"
tags: [n8n, automation, no-code, linkedin, google-sheets]
keywords: [n8n workflow, tự động hóa, linkedin, google sheets, unipile]
---

# 🚀 Tự động gửi yêu cầu kết nối LinkedIn cá nhân hóa với Google Sheets và Unipile

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải gửi hàng trăm yêu cầu kết nối LinkedIn thủ công? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần code, giúp tiết kiệm thời gian quý giá và duy trì sự chuyên nghiệp trong quá trình kết nối.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi yêu cầu kết nối hàng loạt mà không cần can thiệp thủ công.
- Cá nhân hóa: Gửi tin nhắn kết nối cá nhân hóa cho từng người liên hệ.
- Theo dõi: Theo dõi trạng thái của từng yêu cầu kết nối trong Google Sheets.
- An toàn: Tự động tránh gửi yêu cầu liên tục, tránh bị LinkedIn chặn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được chia sẻ với n8n.
- Tài khoản Unipile đã kết nối với LinkedIn.
- API Key, DSN và Account ID từ Unipile.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào "Import from URL" và dán link: [https://n8n.io/workflows/14444](https://n8n.io/workflows/14444).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Schedule Trigger**: Cấu hình lịch chạy workflow (mỗi 4-8 giờ là an toàn).
- **Get Leads**: Cấu hình Google Sheets OAuth2 API và chọn sheet chứa danh sách liên hệ.
- **Filter**: Đảm bảo sheet có cột `connection_request_status` để lọc những liên hệ chưa được gửi yêu cầu.
- **Limit Connection Request**: Giới hạn số lượng yêu cầu gửi mỗi lần chạy (10-15 yêu cầu là an toàn).
- **Data Arrangement**: Điền các thông tin từ Unipile (DSN, API Key, Account ID).
- **Wait**: Đặt thời gian chờ giữa các yêu cầu (3-5 phút để tránh bị LinkedIn chặn).

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu gửi yêu cầu kết nối tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy.
- Lưu log hoạt động vào Google Sheets để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về số lượng yêu cầu kết nối đã gửi và trạng thái.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình gửi yêu cầu kết nối LinkedIn một cách chuyên nghiệp và an toàn. Bằng cách sử dụng Google Sheets để quản lý danh sách liên hệ và Unipile để gửi yêu cầu, các sếp có thể tiết kiệm thời gian và tập trung vào những việc quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!