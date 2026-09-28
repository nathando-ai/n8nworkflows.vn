---
title: "🚀 Tự động phát hiện hóa đơn trùng lặp từ Gmail, easybits và Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét email Gmail, trích xuất dữ liệu hóa đơn PDF qua easybits API, kiểm tra trùng lặp trên Google Sheets và cảnh báo qua Slack."
slug: "tu-dong-phat-hien-hoa-don-trung-lap-gmail-easybits-google-sheets"
tags: [n8n, automation, no-code, invoice-processing, google-sheets, gmail, slack]
keywords: [n8n workflow, tu dong hoa hoa don, easybits extractor, gmail trigger google sheets, phat hien hoa don trung lap]
---

# 🚀 Tự động phát hiện hóa đơn trùng lặp từ Gmail, easybits và Google Sheets

Các sếp có đang đau đầu vì bộ phận kế toán thường xuyên phải kiểm tra thủ công từng hóa đơn PDF nhận được qua email để tránh việc thanh toán trùng lặp? Việc này vừa mất thời gian, vừa dễ dẫn đến sai sót nhầm lẫn tốn kém cho doanh nghiệp.

Giải pháp ở đây là gì? Hãy để workflow n8n này làm thay các sếp! Quy trình tự động hóa 100% không cần code này sẽ giúp rà soát email, trích xuất thông tin, đối chiếu dữ liệu lịch sử và tự động cảnh báo nếu phát hiện hóa đơn đã từng được xử lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần nhân sự mở từng file PDF đọc số hóa đơn và tra cứu sổ sách thủ công.
- **Loại bỏ sai sót:** Tránh hoàn toàn tình trạng thanh toán trùng lặp hóa đơn do con người sơ suất.
- **Cảnh báo tức thì:** Nhận thông báo trực tiếp qua Slack ngay lập tức khi phát hiện hóa đơn trùng.
- **Đồng bộ tự động:** Tự động ghi nhận hóa đơn mới hợp lệ vào Google Sheets Master liên tục 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Gmail** (OAuth2 Credentials) có cấu hình nhãn (Label) hóa đơn.
- **Tài khoản easybits Extractor** (Lấy API Key và Pipeline ID tại `extractor.easybits.tech`).
- **Google Sheets** (OAuth2 Credentials) với file quản lý tài chính chuẩn bị sẵn các cột cần thiết.
- **Slack Workspace & App** (Bot Token) để nhận thông báo cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc hoặc tạo mới, sau đó copy toàn bộ cấu trúc JSON và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính, các sếp cần cấu hình kỹ các điểm sau:
- **Gmail Trigger (`Gmail Trigger`):** Kết nối tài khoản qua OAuth2. Tạo một nhãn (Label) tên là `invoice` trong Gmail và cấu hình node chỉ quét các email có nhãn này, đồng thời bật tính năng tải xuống tệp đính kèm (Download Attachments).
- **Trích xuất file & API (`Extract from File`, `HTTP Request`, `Code in JavaScript`):** 
  - Node `Extract from File` thực hiện chuyển đổi file PDF đính kèm sang định dạng base64.
  - Tại node `HTTP Request`, các sếp thay thế Pipeline ID trong URL bằng pipeline của mình tại easybits và thêm Bearer Auth credential với API Key.
  - Node `Code in JavaScript` sẽ xử lý bóc tách dữ liệu cấu trúc như số hóa đơn (`invoice_number`) và tổng tiền (`total_amount`).
- **Kiểm tra trùng lặp (`Check Google Sheets`, `Already Exists?`, `Add to Master List`):**
  - Kết nối Google Sheets qua OAuth2. Chọn file Master Finance của doanh nghiệp.
  - File cần có các cột: **Invoice Number** và **Final Amount (EUR)** (hoặc VNĐ tùy chỉnh).
  - Node `Already Exists?` (IF node) sẽ đối chiếu số hóa đơn mới với danh sách sẵn có trong sheet và trả về kết quả `duplicate: true/false`.
- **Cảnh báo qua Slack (`Slack: Alert Finance`):**
  - Tạo một Slack App tại `api.slack.com/apps` với các quyền (scopes): `chat:write`, `chat:write.public`, `channels:read`, `groups:read`, `users:read`, `users.profile:read`.
  - Cài đặt vào workspace và lấy Bot Token cấu hình vào n8n để node gửi tin nhắn trực tiếp (DM) cho bộ phận tài chính khi phát hiện hóa đơn trùng lặp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một vài hóa đơn mẫu để đảm bảo dữ liệu chạy thông suốt từ Gmail qua easybits đến Google Sheets.
- Gửi thử một hóa đơn 2 lần liên tục để kiểm tra tính năng cảnh báo trùng lặp hoạt động chính xác.
- Bật công tắc **Active** để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Slack DM, các sếp có thể tích hợp thêm node Telegram hoặc gửi email cảnh báo cho quản lý.
- **Lưu trữ file PDF:** Kết hợp lưu trữ file PDF gốc lên Google Drive hoặc OneDrive theo từng thư mục tháng/năm để tiện đối soát thuế sau này.
- **Báo cáo định kỳ:** Thêm một Schedule Trigger để tổng hợp danh sách hóa đơn mới trong tuần và gửi báo cáo tóm tắt vào kênh Slack chung của công ty.

### 📌 Kết luận
Việc tự động hóa quy trình kiểm tra và nhập liệu hóa đơn chưa bao giờ dễ dàng đến thế với sự kết hợp của n8n, easybits và Google Sheets. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tiết kiệm thời gian và tối ưu hóa vận hành tài chính ngay hôm nay!