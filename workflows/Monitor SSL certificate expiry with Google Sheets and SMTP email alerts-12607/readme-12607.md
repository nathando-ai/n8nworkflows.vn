---
title: "🛡️ Tự động giám sát hạn SSL và cảnh báo qua Email với n8n và Google Sheets"
description: "Giải pháp SecOps tự động kiểm tra thời hạn chứng chỉ SSL của website, ghi log vào Google Sheets và gửi email cảnh báo kịp thời để tránh gián đoạn dịch vụ."
slug: "giam-sat-han-ssl-tu-dong-google-sheets-smtp"
tags: [n8n, automation, no-code, secops, ssl-monitoring, google-sheets, smtp]
keywords: [n8n workflow, giám sát SSL, tự động hóa SecOps, kiểm tra chứng chỉ SSL, cảnh báo SSL hết hạn]
---

# 🛡️ Tự động giám sát hạn SSL và cảnh báo qua Email với n8n

Việc chứng chỉ SSL đột ngột hết hạn không chỉ làm gián đoạn trải nghiệm của khách hàng, hiển thị cảnh báo bảo mật "Not Secure" đáng sợ mà còn làm tổn hại nghiêm trọng đến uy tín thương hiệu và thứ hạng SEO của doanh nghiệp. Thông thường, việc kiểm tra thủ công danh sách dài các tên miền là một công việc nhàm chán và rất dễ bỏ sót.

Với workflow n8n **Monitor SSL certificate expiry with Google Sheets and SMTP email alerts**, các sếp có thể tự động hóa 100% quy trình này. Hệ thống sẽ chủ động quét thời hạn SSL, cập nhật trạng thái vào Google Sheets và tự động gửi email cảnh báo trước khi chứng chỉ hết hạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động 100%:** Phát hiện sớm chứng chỉ SSL sắp hết hạn trước khi gây ra sự cố downtime.
- **Quản lý tập trung:** Toàn bộ danh sách tên miền và trạng thái SSL được đồng bộ tự động vào Google Sheets.
- **Cảnh báo thông minh:** Tự động gửi email thông báo chi tiết qua giao thức SMTP đến đội ngũ kỹ thuật.
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn các00% thao tác kiểm tra thủ công hàng tuần/hàng tháng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đã được cài đặt và hoạt động.
- Tài khoản Google tích hợp (Google Sheets Credentials).
- Thông tin máy chủ SMTP (Gmail, SendGrid, Amazon SES, v.v.) để gửi email cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp (hoặc lấy từ n8n template ID `12607`), sau đó chọn **Import from File** hoặc copy và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình các thành phần sau:
- **Schedule Trigger:** Cài đặt lịch chạy tự động (ví dụ: chạy mỗi ngày một lần vào lúc 8:00 sáng để kiểm tra SSL).
- **Google Sheets Node:** Kết nối với tài khoản Google của các sếp, trỏ tới file Google Sheets quản lý tên miền (nơi lưu danh sách các URL cần kiểm tra).
- **Execute Command / Code Node:** Xử lý logic kiểm tra thời gian hết hạn của chứng chỉ SSL thông qua lệnh hệ thống hoặc đoạn mã script.
- **If Node:** Bộ lọc điều kiện để xác định xem chứng chỉ nào sắp hết hạn (ví dụ: còn dưới 15 hoặc 30 ngày) để chuyển hướng sang luồng cảnh báo.
- **Email Send (SMTP) Node:** Điền chính xác thông tin máy chủ SMTP, cổng, tài khoản và mật khẩu ứng dụng để gửi email cảnh báo đến người quản trị.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với một vài tên miền mẫu, đảm bảo Google Sheets cập nhật đúng và email gửi đi thành công.
- Bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp ChatOps:** Kết hợp thêm node **Telegram** hoặc **Slack** để bắn thông báo trực tiếp vào nhóm chat kỹ thuật ngay khi phát hiện SSL sắp hết hạn.
- **Báo cáo định kỳ hàng tuần:** Tạo thêm một nhánh gửi báo cáo tổng hợp trạng thái toàn bộ SSL vào đầu tuần để ban quản lý nắm bắt.
- **Tự động gia hạn:** Nếu sử dụng Let's Encrypt, có thể mở rộng workflow để gọi API tự động renew chứng chỉ luôn khi gần hết hạn.

### 📌 Kết luận
Đừng để sự cố SSL làm gián đoạn kinh doanh và mất lòng tin từ khách hàng. Hãy thiết lập ngay workflow tự động hóa này để hệ thống hạ tầng của các sếp luôn trong trạng thái an toàn và chuyên nghiệp nhất!