---
title: "🚀 Tự động trích xuất và phân loại tài liệu pháp lý với Claude Sonnet và Google Sheets"
description: "Xây dựng hệ thống tự động hóa xử lý, đọc hiểu, phân tích rủi ro tài liệu pháp lý và tài chính bằng Claude Sonnet, Google Sheets, Slack và Email."
slug: "trich-xuat-phan-loai-tai-lieu-phap-ly-claude-sonnet-google-sheets"
tags: [n8n, automation, no-code, ai-extraction, claude-sonnet, google-sheets]
keywords: [n8n workflow, trích xuất tài liệu pháp lý, Claude Sonnet, AI automation, Google Sheets, quản lý rủi ro tài liệu]
---

# 🚀 Tự động trích xuất và phân loại tài liệu pháp lý với Claude Sonnet và Google Sheets

Các sếp trong lĩnh vực pháp lý, tài chính hay hành chính chắc chắn hiểu rõ nỗi đau khi phải đối mặt với hàng đống hợp đồng, tài liệu dài dằng dặc. Việc đọc thủ công từng trang, tóm tắt nội dung, đối chiếu rủi ro và nhập liệu vào Google Sheets không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót chết người.

Được thiết kế bởi **Mychel Garzon** (n8n Verified Creator & Nhà vô địch Thử thách Kỹ thuật n8n Junction 2025), workflow cấp độ doanh nghiệp này sẽ tự động hóa toàn bộ quy trình: từ tiếp nhận tài liệu (URL hoặc văn bản thô), kiểm tra bảo mật SSRF, trích xuất thông tin qua **Claude Sonnet 4.6**, phân loại mức độ rủi ro, cho đến ghi log vào Google Sheets và cảnh báo thông minh qua Slack/Email. Tất cả diễn ra chỉ trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tệp tài liệu lớn mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Xử lý tài liệu PDF hoặc văn bản ngay khi gửi đến Webhook mà không cần can thiệp thủ công.
- **Trích xuất thông minh bằng AI**: Sử dụng Claude Sonnet để phân tích cấu trúc, bóc tách các điều khoản, các bên liên quan và đánh giá mức độ rủi ro chính xác.
- **Bảo mật và chống trùng lặp**: Tích hợp các bộ lọc chống trùng lặp (Deduplication), kiểm tra bảo mật URL (SSRF Guard) và giới hạn dung lượng tệp tin.
- **Cảnh báo thời gian thực**: Tự động bắn thông báo khẩn cấp qua Slack và Email khi phát hiện tài liệu có rủi ro cao (HIGH) hoặc vượt định mức token.
- **Đồng bộ hóa dữ liệu tập trung**: Tự động ghi kết quả bóc tách vào Google Sheets để tra cứu và kiểm toán bất cứ lúc nào.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted bản mới nhất).
- **Tài khoản Anthropic (Claude API)** kèm API Key.
- **Tài khoản Google** để kết nối Google Sheets (OAuth2).
- **Webhook Slack** (để nhận thông báo rủi ro, cảnh báo token và lỗi hệ thống).
- **Cấu hình SMTP** hoặc dịch vụ gửi Email (để gửi cảnh báo rủi ro cao).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ kho lưu trữ n8n chính thức (Link gốc: [n8n.io/workflows/15790](https://n8n.io/workflows/15790)), sau đó chọn **Import from File** hoặc sao chép toàn bộ mã nguồn JSON dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 31 nodes được chia thành các phân đoạn rõ ràng. Các sếp cần cấu hình chính xác các thành phần sau:

- **Anthropic Chat Model**: Kết nối credentials `Anthropic API` và đảm bảo biến model được trỏ tới `claude-sonnet-4-6`.
- **Log to Google Sheets**: 
  - Chọn tài khoản Google Sheets Credentials (OAuth2).
  - Thiết lập biến môi trường cho Sheet ID (`GSHEETS_SPREADSHEET_ID`) và Tên Sheet (`GSHEETS_SHEET_NAME`).
- **Slack Nodes** (`Slack: High Risk Alert`, `Slack: High Token Alert`, `Slack: Pipeline Error`): Cấu hình URL Webhook Slack thông qua biến môi trường `SLACK_WEBHOOK_URL`.
- **Email: High Risk Alert**: 
  - Kết nối thông tin SMTP credentials.
  - Cấu hình các biến môi trường người gửi/nhận (`ALERT_FROM_EMAIL` và `ALERT_TO_EMAIL`).
- **Workflow Config (model + settings)**: Tinh chỉnh các tham số cấu hình hệ thống, tên model hoặc giới hạn nếu cần thiết.
- **Biến bảo mật tùy chọn**: Cấu hình `ALLOWED_DOWNLOAD_DOMAINS` nếu muốn giới hạn các nguồn tải tài liệu PDF qua URL.

#### 3. Kích hoạt ⚡️
- Gửi một Payload thử nghiệm (Test Payload) đến đường dẫn Webhook của node **Receive Document** (đường dẫn dạng: `POST /webhook/process-document`).
- Kiểm tra kết quả trả về từ node `Respond 202 Accepted`.
- Sau khi kiểm tra dữ liệu trên Google Sheets và các kênh thông báo hoạt động trơn tru, các sếp hãy bật công tắc **Active workflow** để đưa vào vận hành thực tế.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp của mình, các sếp có thể cân nhắc mở rộng:
- **Tích hợp đa kênh thông báo**: Thay vì chỉ Slack và Email, có thể kết nối thêm Telegram Bot hoặc Microsoft Teams để đội ngũ pháp chế nhận tin tức nhanh hơn.
- **Lưu trữ file gốc**: Thêm bước lưu trữ tệp PDF nguồn từ URL vào Google Drive hoặc AWS S3 kèm theo mã Job ID để tiện đối chiếu.
- **Báo cáo định kỳ**: Tạo thêm một nhánh chạy lịch (Schedule Trigger) hàng tuần để tổng hợp số lượng tài liệu đã xử lý và gửi báo cáo tóm tắt qua Email cho ban quản lý.

---

### 📌 Kết luận
Việc tự động hóa quy trình phân tích và xử lý tài liệu pháp lý với Claude Sonnet và n8n không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn giảm thiểu tối đa rủi ro pháp lý cho doanh nghiệp. Hãy thiết lập ngay hôm nay để đưa hệ thống tự động hóa của các sếp lên một tầm cao mới!