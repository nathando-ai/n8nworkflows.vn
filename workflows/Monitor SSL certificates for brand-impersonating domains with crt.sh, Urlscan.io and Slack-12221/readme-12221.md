---
title: "🚀 Giám sát chứng chỉ SSL & Cảnh báo giả mạo thương hiệu (Phishing Lookout) tự động với n8n"
description: "Tự động quét log chứng chỉ SSL hàng giờ qua crt.sh, phân tích URL độc hại với Urlscan.io và gửi cảnh báo kèm hình ảnh trực quan về Slack."
slug: "giam-sat-ssl-gia-mao-thuong-hieu-crt-sh-urlscan-slack"
tags: [n8n, automation, secops, cybersecurity, slack, urlscan]
keywords: [n8n workflow, giám sát ssl, chống giả mạo thương hiệu, phishing lookout, crt.sh urlscan, bảo mật tự động]
---

# 🚀 Tự động phát hiện và cảnh báo tên miền giả mạo thương hiệu với n8n

Trong thời đại số, các cuộc tấn công **Brand Impersonation** (giả mạo thương hiệu) hay **Typosquatting** ngày càng tinh vi. Kẻ xấu thường đăng ký các tên miền gần giống với thương hiệu của bạn (ví dụ: `mybrand-login.xyz` thay vì `mybrand.com`) để lừa người dùng cung cấp thông tin đăng nhập hoặc tải mã độc. 

Việc theo dõi thủ công là bất khả thi. Vì vậy, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hoàn toàn: Theo dõi log chứng chỉ SSL, quét tự động và gửi cảnh báo ngay lập tức lên Slack khi phát hiện dấu hiệu bất thường.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sớm 24/7**: Tự động quét log chứng chỉ SSL mới mỗi giờ từ cơ sở dữ liệu `crt.sh`.
- **Loại bỏ nhiễu (False Positives)**: Tự động lọc ra các tên miền chính chủ của công ty nhờ bộ lọc thông minh.
- **Bằng chứng trực quan**: Tự động chụp ảnh màn hình (screenshot) trang web khả nghi bằng Urlscan.io.
- **Cảnh báo tức thời**: Gửi thông tin chi tiết kèm hình ảnh trực tiếp lên kênh Slack của đội ngũ SecOps để xử lý nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Urlscan.io Account**: Đăng ký tài khoản miễn phí để lấy API Key thực hiện quét URL.
- **Slack Workspace**: Cần có Bot Token và quyền gửi tin nhắn vào kênh bảo mật (Security Channel).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ JSON của workflow từ n8n và dán trực tiếp vào n8n Editor của các sếp, hoặc import file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow hoạt động trơn tru:

- **Poll crt.sh (HTTP Request)**: 
  - Tại URL: `https://crt.sh/?q=%.testdomain.com&output=json`, hãy thay đổi `.testdomain.com` thành tên miền thực tế của doanh nghiệp (ví dụ: `%.yourbrand.com`).
  - Node này đã được cấu hình *Retry on Fail* để xử lý các lỗi 502/504 từ database công khai của `crt.sh`.
- **Filter & Deduplicate (Code Node)**:
  - Cập nhật danh sách `myDomains` trong code để loại trừ các tên miền chính thống của công ty, tránh báo động giả. 
  - *(Lưu ý: Nếu đang test, các sếp có thể bỏ qua bước này để hệ thống xem mọi tên miền phụ đều là khả nghi và đẩy lên Slack).*
- **Perform a scan & Get a scan (Urlscan.io Nodes)**:
  - Kết nối tài khoản Urlscan.io bằng API Key cá nhân.
- **Wait for Scan (Wait Node)**:
  - Giữ nguyên thời gian chờ **90 giây** để trình duyệt ảo của Urlscan.io kịp load trang và chụp ảnh màn hình, tránh lỗi thiếu dữ liệu (`resource not found`).
- **Alert Slack (Slack Node)**:
  - Kết nối Slack Credentials, chọn kênh nhận thông báo.
  - Bật tính năng **"Unfurl Media"** để hình ảnh chụp màn hình hiển thị trực tiếp trong đoạn chat Slack giúp đội ngũ triage nhanh chóng.
- **Looping**: Đảm bảo đầu ra của node *Alert Slack* được nối ngược lại vào đầu vào của node *Split In Batches* để hệ thống xử lý tuần tự tất cả các tên miền tìm được trong mỗi lần chạy.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với dữ liệu thủ công để kiểm tra kết nối Slack và Urlscan.io.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động chạy mỗi giờ theo lịch trình của node *Schedule (Every Hour)*.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin**: Ngoài Slack, các sếp có thể kết hợp thêm node Telegram hoặc Microsoft Teams để đa dạng hóa kênh cảnh báo sự cố.
- **Lưu trữ lịch sử**: Thêm node Google Sheets hoặc Airtable sau bước phân tích để lưu lại lịch sử các tên miền giả mạo phục vụ việc điều tra pháp lý về sau.
- **Tự động chặn (Blocking)**: Kết hợp thêm API của Cloudflare hoặc DNS provider để tự động đưa tên miền độc hại vào danh sách đen nếu độ tin cậy đạt mức nguy hiểm cao.

### 📌 Kết luận
Với workflow Phishing Lookout này, đội ngũ bảo mật của các sếp sẽ luôn đi trước kẻ tấn công một bước trong việc phát hiện các chiến dịch lừa đảo giả mạo thương hiệu. Triển khai ngay hôm nay để bảo vệ uy tín doanh nghiệp một cách tự động!