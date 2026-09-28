---
title: "🚀 Tự động tạo và xác thực hàng loạt mã QR với Google Sheets và Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc tạo mã QR hàng loạt, lưu trữ trên Google Drive và xác thực quét mã QR theo thời gian thực."
slug: "tao-va-xac-thuc-ma-qr-hang-loat-n8n"
tags: [n8n, automation, no-code, google-sheets, google-drive, qr-code]
keywords: [n8n workflow, tạo mã QR hàng loạt, xác thực QR code, google sheets n8n, google drive automation]
---

# 🚀 Tự động tạo và xác thực hàng loạt mã QR với Google Sheets và Google Drive

Việc quản lý sự kiện, vé tham dự hoặc mã định danh bằng mã QR (QR Code) thủ công thường rất tốn thời gian, dễ xảy ra sai sót khi tạo mã, lưu trữ file hình ảnh rời rạc và khó kiểm soát trạng thái quét mã (đã dùng hay chưa). 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: từ việc đọc dữ liệu từ Google Sheets, sinh mã QR chứa URL xác thực, lưu trữ file ảnh vào Google Drive, cho đến việc xử lý webhook xác thực khi người dùng quét mã.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Tạo hàng loạt mã QR chỉ với 1 cú click hoặc tự động định kỳ.
- **Lưu trữ khoa học:** Hình ảnh QR được sinh ra và lưu thẳng vào thư mục Google Drive chỉ định, đính kèm thông tin trên Google Sheets.
- **Xác thực thông minh (Check-in/Validation):** Tự động kiểm tra trạng thái ID, chống quét trùng lặp (chỉ cho phép dùng 1 lần) thông qua Webhook.
- **Hoạt động 24/7:** Vận hành trơn tru trên nền tảng n8n không cần sự can thiệp thủ công liên tục.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google có kết nối **Google Sheets** và **Google Drive**.
- Một file Google Sheets chuẩn bị sẵn gồm các cột thông tin cơ bản (ví dụ: `email`, `status_qr`,...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sao chép toàn bộ mã nguồn JSON và dán (Paste) vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 17 nodes được chia thành 2 phần chính (Tạo mã & Xác thực mã). Các sếp cần cấu hình kỹ các node sau:

- **Google Sheets Nodes (`Get List`, `Get List ID`, `Update QR used`, `Update Row Status QR Generated`):** Kết nối tài khoản Google của các sếp, trỏ tới file Google Sheets quản lý dữ liệu và cấu hình đúng tên Sheet/Range.
- **Google Drive Node (`Upload file`):** Chọn thư mục đích trên Google Drive để lưu trữ các hình ảnh mã QR được tạo ra.
- **HTTP Request Node (`QR Generator`):** Thay đổi Webhook Base URL thành URL production thực tế của n8n instance khi workflow được kích hoạt để đảm bảo liên kết mã QR dẫn đúng về hệ thống xác thực.
- **Webhook Node (`QR Validation Webhook`):** Đảm bảo đường dẫn path (`read-qr`) đã chính xác để nhận các request quét mã từ bên ngoài.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`When clicking ‘Execute workflow’`** (`manualTrigger`) để test thử nghiệm với dữ liệu mẫu trên Google Sheets.
- Kiểm tra kết quả trên Google Drive và Google Sheets xem hệ thống đã sinh ảnh và cập nhật trạng thái (`QR_GENERATED`) hay chưa.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau node `QR OK` hoặc `QR ID Already Used` để gửi thông báo real-time mỗi khi có người check-in quét mã thành công hoặc thất bại.
- **Tự động hóa qua Cron:** Thay thế node `manualTrigger` bằng node `Schedule Trigger` để hệ thống tự quét danh sách mới và tạo mã QR tự động hàng ngày/hàng tuần.
- **Bảo mật Webhook:** Thêm bước xác thực token hoặc API Key ở phần Webhook nhận diện quét mã để tránh bị spam request giả mạo.

### 📌 Kết luận
Với workflow này, việc quản lý và phát hành mã QR hàng loạt không còn là nỗi ám ảnh thủ công. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình vận hành sự kiện, quản lý nhân sự hay phân phối mã ưu đãi một cách chuyên nghiệp nhất!