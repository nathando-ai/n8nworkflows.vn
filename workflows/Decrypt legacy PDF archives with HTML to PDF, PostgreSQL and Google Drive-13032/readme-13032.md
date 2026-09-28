---
title: "🚀 Tự động giải mã tài liệu PDF cũ, kiểm tra bảo mật và lưu trữ với n8n"
description: "Hướng dẫn xây dựng quy trình tự động hóa giải mã hàng loạt file PDF bảo mật, đối soát mật khẩu từ PostgreSQL, xử lý lỗi và lưu trữ an toàn trên Google Drive."
slug: "giai-ma-pdf-cu-tu-dong-postgres-google-drive"
tags: [n8n, automation, no-code, postgresql, google-drive, security]
keywords: [n8n workflow, giải mã pdf tự động, html to pdf, postgresql key vault, google drive automation]
---

# 🚀 Tự động giải mã tài liệu PDF cũ, kiểm tra bảo mật và lưu trữ với n8n

Các doanh nghiệp, tổ chức pháp lý hoặc cơ quan lưu trữ thường đối mặt với hàng ngàn file PDF cũ được mã hóa bằng mật khẩu. Việc giải mã, kiểm tra tính toàn vẹn và phân loại thủ công tốn vô số thời gian và dễ xảy ra sai sót. 

Workflow này là một giải pháp cấp độ doanh nghiệp (Industrial-grade pipeline) giúp tự động hóa toàn bộ quá trình: tiếp nhận file, tra cứu mật khẩu từ cơ sở dữ liệu, giải mã, kiểm tra tính toàn vẹn (SHA-256), lưu trữ an toàn và gửi báo cáo qua Slack/Gmail. Tất cả chạy hoàn toàn tự động 100% không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Giải mã hàng loạt file PDF bảo mật mà không cần nhập mật khẩu thủ công.
- **Bảo mật & Kiểm soát toàn vẹn:** Tạo mã SHA-256 (Chain of Custody) để theo dõi trạng thái tài liệu trước và sau khi xử lý.
- **Xử lý lỗi thông minh (Quarantine Zone):** Các file lỗi, sai mật khẩu hoặc hỏng sẽ tự động được cách ly, ghi log vào cơ sở dữ liệu và cảnh báo qua Slack.
- **Đồng bộ đa nền tảng:** Lưu trữ file đã giải mã lên Google Drive, lưu vết kiểm toán (Audit Log) vào PostgreSQL và gửi báo cáo tổng hợp qua Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Hạ tầng n8n:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **PostgreSQL Database:** Các bảng lưu trữ khóa giải mã (`legacy_keys`), nhật ký kiểm toán (`audit_log`), và nhật ký cách ly (`quarantine_log`).
- **Tài khoản & API Keys:**
  - **HTML to PDF (Unlock Engine):** API key/credentials cho node xử lý PDF.
  - **Google Drive OAuth2:** Thư mục lưu trữ (Audit Vault và Quarantine Zone).
  - **Slack OAuth2:** Kênh thông báo cảnh báo và log tuân thủ.
  - **Gmail OAuth2:** Gửi email báo cáo pháp lý tóm tắt.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng 3 chấm ở góc trên bên phải -> Chọn **Import from File** và tải lên file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes được chia thành các phase rõ rệt. Các sếp cần cấu hình chính xác các node sau:

- **Node `Code: Forensic Intake1` & `IF: File Validator`:** Kiểm tra loại file, kích thước và tạo mã băm SHA-256 ban đầu. Hãy kiểm tra lại đoạn script trong code node nếu muốn thay đổi quy tắc lọc file đầu vào.
- **Node `Postgres: Key Vault1`:** Kết nối tới database PostgreSQL của các sếp. Đảm bảo câu lệnh SQL truy vấn đúng bảng `legacy_keys` để khớp tên file với mật khẩu tương ứng.
- **Node `HTML to PDF: Unlock Engine1`:** Node cốt lõi để gỡ bỏ mật khẩu PDF. Cần cấu hình đúng thông tin xác thực (`htmlcsstopdfApi`) và thiết lập thao tác `unlockPdf`.
- **Node `Google Drive: Audit Vault1` & `Google Drive: Quarantine Vault`:** Chọn đúng Folder ID trên Google Drive của các sếp để hệ thống tự động đẩy file sạch vào Vault hoặc đẩy file lỗi vào vùng Quarantine.
- **Node `Slack: Quarantine Alert` & `Slack: Compliance Log1`:** Kết nối Slack Credentials và chọn Channel nhận thông báo khi có file lỗi hoặc hoàn tất quy trình.
- **Node `Gmail: Legal Summary1`:** Cấu hình tài khoản Gmail gửi báo cáo tổng hợp (Legal Summary) cho đội ngũ pháp chế hoặc quản lý.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một vài file mẫu để kiểm tra luồng dữ liệu (đặc biệt là nhánh thành công và nhánh lỗi).
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook / Telegram:** Các sếp có thể nối thêm node Telegram để nhận thông báo tức thời ngay trên điện thoại thay vì chỉ dùng Slack.
- **Lưu trữ Log nâng cao:** Mở rộng bảng PostgreSQL để tracking thêm thời gian xử lý (`Processing_Latency`) nhằm tối ưu hiệu suất hệ thống.
- **Lên lịch chạy định kỳ (Schedule Trigger):** Kết hợp thêm node Schedule Trigger ở đầu workflow để hệ thống tự động quét thư mục chứa file cũ mỗi đêm lúc 00:00.

### 📌 Kết luận
Workflow "Decrypt legacy PDF archives with HTML to PDF, PostgreSQL and Google Drive" là một kiệt tác tự động hóa giúp giải quyết triệt để bài toán xử lý tài liệu cũ bảo mật. Hãy áp dụng ngay hôm nay để tiết kiệm hàng trăm giờ làm việc thủ công cho doanh nghiệp của các sếp!