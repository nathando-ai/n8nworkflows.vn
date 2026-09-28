---
title: "🚀 Tự động hóa trích xuất và phân loại hóa đơn, biên nhận từ Gmail với OpenAI và Google Drive"
description: "Hướng dẫn cài đặt workflow n8n giúp quét Gmail, dùng AI phân loại hóa đơn/biên nhận PDF, lưu trữ tự động lên Google Drive và gửi báo cáo cho kế toán."
slug: "tu-dong-hoa-trich-xuat-phan-loai-hoa-don-gmail-openai-google-drive"
tags: [n8n, automation, gmail, open-ai, google-drive, finance]
keywords: [n8n workflow, tự động hóa hóa đơn, trích xuất pdf gmail, openai phân loại hóa đơn, google drive automation]
---

# 🚀 Tự động hóa trích xuất và phân loại hóa đơn, biên nhận từ Gmail với OpenAI và Google Drive

Mỗi dịp cuối tháng hay tổng kết tài chính, việc phải "bới tung" hộp thư Gmail để tìm kiếm từng chiếc hóa đơn, biên nhận, sau đó tải về và phân loại thủ công lên Google Drive thực sự là một cơn ác mộng tốn thời gian. Chưa kể nguy cơ sót đơn, nhầm lẫn thông tin khiến việc báo cáo thuế trở nên cực kỳ căng thẳng.

Giải pháp là gì? Workflow n8n siêu việt này sẽ thay các sếp làm toàn bộ công việc nhàm chán đó: tự động quét email, trích xuất file PDF, sử dụng sức mạnh AI của **OpenAI** để đọc hiểu và phân loại đâu là hóa đơn/biên nhận, tự động tạo thư mục trên **Google Drive** để lưu trữ và thậm chí gửi gói tài liệu gọn gàng thẳng đến hòm thư của kế toán chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải tải xuống và sắp xếp thủ công hàng tá hóa đơn mỗi tháng.
- **Phân loại thông minh bằng AI:** OpenAI tự động đọc nội dung PDF để xác thực chính xác hóa đơn/biên nhận, loại bỏ rác hoặc file đính kèm không liên quan.
- **Tổ chức khoa học:** Tự động tạo thư mục theo dải ngày trên Google Drive với tên gọi rõ ràng (`invoices_YYYY-MM-DD_YYYY-MM-DD`).
- **Tự động hóa toàn diện:** Tích hợp tùy chọn gửi email tổng hợp trực tiếp cho kế toán hoặc quản lý tài chính một cách mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản Gmail** (Cấp quyền kết nối OAuth2 để đọc và gửi email).
- **Tài khoản Google Drive** (Cấp quyền OAuth2 để tạo thư mục và upload file).
- **OpenAI API Key** (Dùng cho model AI phân tích nội dung văn bản PDF).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chính thức (`n.io/workflows/3719`) hoặc copy toàn bộ JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Node `Configure` (Set):** Đây là trung tâm điều khiển các tham số quan trọng:
  - `maxTokenSize`: Giới hạn dung lượng chữ gửi lên OpenAI (Mặc định: `8000`) nhằm tối ưu chi phí và tránh lỗi token.
  - `Match on`: Từ khóa/tiêu chí để AI nhận diện (Mặc định: `"receipt or invoice"` - các sếp có thể đổi thành `"contract"` nếu muốn tìm hợp đồng).
  - `sendInvoicesTo`: Địa chỉ email nhận file tổng hợp (Ví dụ: `accounting@example.com`).
- **Node `OpenAI`:** Chọn credential API Key của OpenAI. Đảm bảo tài khoản có số dư API hoạt động.
- **Node `Get emails with attachments` & `Send to my accountant` (Gmail):** Kết nối tài khoản Gmail thông qua **Gmail OAuth2 API**.
- **Node `Create folder` & `Upload file to folder` (Google Drive):** Kết nối tài khoản Google Drive thông qua **Google Drive OAuth2 API**.
- **Node `Webhook`:** Cung cấp điểm đầu vào (Endpoint) để kích hoạt workflow từ các hệ thống bên ngoài hoặc công cụ lập lịch (Cron job).

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** bằng một request webhook chứa dải ngày (`start date`, `end date`) cùng tham số `sendEmail` (true/false) để kiểm tra luồng chạy.
- Sau khi kiểm tra mọi thứ trơn tru, hãy bật công tắc **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack:** Thêm một node thông báo qua Telegram hoặc Slack sau khi hoàn tất quá trình upload để team nắm được tổng số hóa đơn đã xử lý thành công.
- **Lưu log Google Sheets:** Bổ sung node Google Sheets để ghi lại lịch sử quét email, tên file hóa đơn và thời gian upload phục vụ việc đối soát sau này.
- **Tự động chạy định kỳ:** Thay vì kích hoạt bằng Webhook thủ công, các sếp có thể gắn thêm node **Schedule Trigger** để workflow tự động chạy vào ngày 1 hàng tháng.

### 📌 Kết luận
Tự động hóa hóa đơn chưa bao giờ dễ dàng và mượt mà đến thế với sự kết hợp giữa n8n, Gmail và AI. Hãy triển khai ngay hôm nay để giải phóng bản thân và đội ngũ khỏi những tác vụ thủ công vô nghĩa!