---
title: "🚀 Tự động trích xuất dữ liệu hợp đồng pháp lý & cảnh báo thông minh với VLM Run, Google Workspace và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình đọc hợp đồng, trích xuất dữ liệu bằng AI, lưu Google Sheets, tạo lịch Google Calendar và bắn thông báo Slack."
slug: "tu-dong-trich-xuat-du-lieu-hop-dong-vlm-run-google-workspace-slack"
tags: [n8n, automation, no-code, vlm-run, google-workspace, slack, ai]
keywords: [n8n workflow, trích xuất hợp đồng tự động, vlm run n8n, google drive trigger, google sheets automation, slack notification]
---

# 🚀 Tự động trích xuất dữ liệu hợp đồng pháp lý & cảnh báo thông minh với VLM Run, Google Workspace và Slack

Việc xử lý các hợp đồng pháp lý, hóa đơn hay tài liệu kinh doanh thủ công thường ngốn rất nhiều thời gian của đội ngũ pháp chế và vận hành. Từ việc đọc từng trang, nhập liệu thủ công vào Google Sheets, tính toán thời hạn hiệu lực cho đến việc tạo lịch nhắc nhở trên Google Calendar đều dễ xảy ra sai sót.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp giải phóng hoàn toàn sức lao động. Hệ thống sẽ tự động theo dõi Google Drive, sử dụng trí tuệ nhân tạo VLM Run để trích xuất dữ liệu hợp đồng, lưu trữ có cấu trúc, đồng thời tự động thông báo qua Slack và lên lịch nhắc nhở các mốc thời gian quan trọng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần nhập liệu thủ công từ file PDF hay ảnh chụp hợp đồng.
- **AI thông minh:** Sử dụng VLM Run để đọc chính xác ngay cả các tài liệu scan mờ hoặc chụp từ điện thoại.
- **Đồng bộ đa nền tảng:** Tự động cập nhật cơ sở dữ liệu vào Google Sheets, đẩy cảnh báo tức thì lên Slack.
- **Quản lý thời hạn hiệu quả:** Tự động tạo sự kiện và nhắc nhở ngày hiệu lực, ngày chấm dứt hợp đồng trên Google Calendar.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Google Drive & Google Sheets & Google Calendar Credentials** (OAuth2).
- **VLM Run API Key** (để kết nối với node `@vlm-run/n8n-nodes-vlmrun`).
- **Slack Bot Token / Webhook** để gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây, các sếp cần cấu hình chuẩn xác:
- **Monitor Contract Uploads (`googleDriveTrigger`)**: Chọn thư mục trên Google Drive chuyên dùng để lưu trữ hợp đồng đầu vào.
- **Download Contract File (`googleDrive`)**: Đảm bảo node này nhận đúng File ID truyền từ trigger để tải file về xử lý.
- **VLM Run ContractParser (`@vlm-run/n8n-nodes-vlmrun.vlmRun`)**: 
  - Cấu hình credentials với VLM Run API Key.
  - Thiết lập operation là `executeAgent` để trích xuất các trường dữ liệu: Mã hợp đồng (ID), Tiêu đề, Các bên tham gia, Ngày có hiệu lực và Ngày chấm dứt.
  - ⚠️ **Lưu ý quan trọng:** Hãy dán **Production URL** của node **Receive Contract (`webhook`)** vào trường *Callback URL* trong VLM Run để hệ thống trả dữ liệu về đúng workflow đang chạy. Không dùng URL `localhost`.
- **Save to Expense Database (`googleSheets`)**: Chọn file Google Sheets và sheet tương ứng để lưu thông tin hợp đồng được trích xuất (ID, Tiêu đề, Các bên, Ngày hiệu lực, Ngày kết thúc).
- **Send a message (`slack`)**: Cấu hình channel Slack (ví dụ: `#all-n8n-test`) để nhận thông báo chi tiết và tóm tắt hợp đồng từ AI.
- **Prepare Calendar Events (`code`) & Create an event (`googleCalendar`)**: Xử lý logic thời gian để tạo các sự kiện cả ngày (all-day events) trên Google Calendar bao gồm: Ngày hiệu lực, Ngày chấm dứt và nhắc nhở gia hạn trước 30 ngày.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một vài file hợp đồng mẫu (PDF hoặc ảnh) để kiểm tra luồng dữ liệu.
- Bật công tắc **Active** để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh chat:** Có thể bổ sung node Telegram hoặc Microsoft Teams để gửi thông báo song song với Slack.
- **Gửi bản tóm tắt qua Email:** Kết hợp thêm node Gmail để tự động gửi email xác nhận cho đối tác hoặc bộ phận pháp chế ngay khi hợp đồng được phê duyệt.
- **Lưu trữ tệp đính kèm:** Sau khi xử lý xong, có thể cấu hình thêm bước di chuyển file hợp đồng vào thư mục "Processed" trên Google Drive để tránh trùng lặp.

### 📌 Kết luận
Workflow tự động hóa xử lý hợp đồng pháp lý này sẽ giúp doanh nghiệp tiết kiệm hàng chục giờ làm việc mỗi tháng, loại bỏ hoàn toàn sai sót do nhập liệu thủ công và kiểm soát chặt chẽ thời hạn hợp đồng. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành!