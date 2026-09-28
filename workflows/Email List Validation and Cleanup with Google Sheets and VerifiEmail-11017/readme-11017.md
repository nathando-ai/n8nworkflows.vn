---
title: "🚀 Tự động làm sạch và xác thực danh sách Email với Google Sheets và VerifiEmail"
description: "Giải pháp tự động hóa n8n giúp lọc sạch email rác, email tạm thời và email không hợp lệ từ Google Sheets, giữ lại danh sách khách hàng chất lượng cao."
slug: "tu-dong-lam-sach-va-xac-thuc-danh-sach-email-google-sheets-verifiemail"
tags: [n8n, automation, lead-generation, google-sheets, email-validation, no-code]
keywords: [n8n workflow, làm sạch email, xác thực email, verifiemail, google sheets automation, lọc email rác]
---

# 🚀 Tự động làm sạch và xác thực danh sách Email với Google Sheets và VerifiEmail

Các sếp có đang đau đầu vì danh sách email (subscriber list) ngày càng phình to nhưng tỷ lệ gửi vào Inbox lại thấp thảm hại? Gửi email nhầm vào các địa chỉ "ảo", email rác (disposable) hay email không tồn tại không chỉ làm tốn chi phí gửi mà còn khiến domain của các sếp bị đưa vào danh sách đen (Blacklist).

Việc kiểm tra thủ công hàng ngàn email là điều bất khả thi. Đó là lý do workflow n8n này ra đời – giải pháp tự động hóa 100 giúp đọc, chuẩn hóa, xác thực qua **VerifiEmail** và tự động dọn dẹp danh sách trên **Google Sheets** chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tỷ lệ Deliverability:** Loại bỏ hoàn toàn email rác, email tạm thời (disposable), bảo vệ uy tín tên miền gửi email.
- **Tiết kiệm 90% thời gian:** Không còn phải copy/paste thủ công từng dòng để check tool ngoài.
- **Tự động hóa toàn diện:** Nhận request qua Webhook, tự động đọc Google Sheets, phân loại và cập nhật kết quả (xóa email xấu, lưu email sạch vào bảng riêng).
- **Minh bạch dữ liệu:** Trả về kết quả JSON chi tiết cho từng email (`email`, `action`, `status`) để các sếp dễ dàng theo dõi qua Postman hoặc các hệ thống khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** có quyền truy cập Google Sheets.
- **Tài khoản VerifiEmail** (tại `verifi.email`) để lấy API Key xác thực sức khỏe email (MX record + disposable check).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:

- **Webhook - Receive EmailBatch**: Điểm tiếp nhận request khởi chạy quá trình làm sạch. Các sếp có thể cấu hình HTTP Method là `POST` với đường dẫn `/email-batch`.
- **Fetch Subscribers & Delete rows or columns from sheet & Append Clean Emails (Google Sheets)**: 
  - Kết nối tài khoản Google Sheets thông qua **Google Sheets OAuth2 API**.
  - Chỉ định đúng **Spreadsheet ID** và **Sheet Name** chứa danh sách người đăng ký của các sếp.
  - Đảm bảo cấu trúc cột có chứa các trường cần thiết như `email`, `row_number`, `name`, `tags`, `activity`.
- **Verifi Email**: 
  - Cần tạo credentials loại **VerifiEmail API** bằng cách nhập API Key lấy từ trang quản trị của `verifi.email`.
- **Normalize Subscriber & Classify Email (Code Nodes)**: 
  - Các node này chứa mã JavaScript xử lý logic chuẩn hóa định dạng email và phân loại (`keep` hoặc `remove` dựa trên kết quả trả về từ VerifiEmail).
- **Should Remove? (If Node)**: 
  - Phân nhánh luồng xử lý: Nếu email bị đánh dấu `remove` sẽ chạy qua node xóa dòng trên Google Sheets; nếu là `keep` sẽ được lưu vào danh sách email sạch (`Append Clean Emails`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** với một vài dữ liệu mẫu để kiểm tra xem quá trình đọc, lọc và ghi dữ liệu có hoạt động chính xác không.
- Sau khi test thành công, gạt công tắc **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi báo cáo tổng kết (Ví dụ: *"Đã quét xong 500 email, xóa 45 email rác, giữ lại 455 email sạch"*) ngay sau khi chạy xong.
- **Lưu log lịch sử:** Tạo thêm một Google Sheet riêng để lưu lại lịch sử mỗi lần chạy (Run notes, tổng số email xử lý, thời gian chạy) nhằm dễ dàngAudit về sau.
- **Lên lịch định kỳ (Cron):** Thay vì dùng Webhook kích hoạt thủ công, các sếp có thể kết hợp thêm node **Schedule Trigger** để hệ thống tự động dọn dẹp danh sách email hàng tuần/hàng tháng.

### 📌 Kết luận
Một danh sách email sạch là nền tảng cốt lõi của mọi chiến dịch Email Marketing thành công. Với workflow n8n kết hợp Google Sheets và VerifiEmail này, các sếp hoàn toàn có thể tự động hóa toàn bộ quy trình lọc rác mà không tốn một đồng chi phí thuê ngoài nào. Triển khai ngay thôi các sếp ơi!