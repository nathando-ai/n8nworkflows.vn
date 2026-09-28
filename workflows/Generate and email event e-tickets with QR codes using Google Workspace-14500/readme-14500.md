---
title: "🚀 Tự động tạo và gửi vé điện tử kèm mã QR bằng Google Workspace trong n8n"
description: "Hướng dẫn tự động hóa quy trình tạo vé sự kiện, chèn mã QR động vào Google Docs, xuất file PDF và gửi email cho người tham dự ngay khi có đăng ký mới."
slug: "tu-dong-tao-va-gui-ve-dien-tu-kem-ma-qr-google-workspace"
tags: [n8n, automation, google-workspace, google-docs, google-sheets, qr-code, event-management]
keywords: [n8n workflow, tạo vé điện tử tự động, tự động gửi vé qrcode, google docs automation, n8n viet nam]
---

# 🚀 Tự động tạo và gửi vé điện tử kèm mã QR với Google Workspace

Chào các sếp! Việc tổ chức sự kiện, hội thảo, workshop hay cuộc thi chạy (marathon) thường đi kèm với một cơn ác mộng mang tên: **Thủ công hóa việc làm vé tham dự**. Ngồi copy-paste tên từng người, tạo mã QR thủ công, xuất PDF rồi gửi email từng chiếc một không chỉ tốn hàng giờ đồng hồ mà còn cực kỳ dễ sai sót.

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia *Scale On Fajar*. Hệ thống này sẽ tự động hóa từ A-Z: Nhận thông tin đăng ký 👉 Tạo mã QR độc nhất 👉 Điền thông tin vào mẫu Google Doc 👉 Xuất file PDF 👉 Lưu trữ Google Drive và Gửi email vé điện tử cho khách ngay lập tức. 100% không cần code tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Xử lý hàng trăm, hàng ngàn vé sự kiện chỉ trong vài phút mà không cần nhân sự ngồi làm thủ công.
- **Cá nhân hóa chuyên nghiệp:** Mỗi khách tham dự nhận được một chiếc vé riêng biệt với tên tuổi, thông tin cá nhân và mã QR check-in độc nhất (Ticket ID).
- **Vận hành trơn tru 24/7:** Hệ thống tự động kích hoạt ngay khi có người đăng ký mới qua Google Sheets.
- **Lưu trữ khoa học:** Tự động sao lưu toàn bộ file PDF vé vào Google Drive để dễ dàng tra cứu khi check-in tại sự kiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** (có quyền truy cập Google Sheets, Google Docs, Google Drive).
- **Mẫu Google Doc Template** dùng làm phôi vé (đã thiết kế sẵn các trường như `{{nama_lengkap}}`, `{{ticket_id}}`,...).
- **Cấu hình SMTP hoặc dịch vụ gửi email** (SMTP credentials) để gửi email tự động cho người tham dự.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ n8n.io/workflows/14500) và paste trực tiếp vào n8n Editor của mình. Workflow này gồm tổng cộng **7 nodes** phối hợp nhịp nhàng với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Google Sheets Trigger:** Kết nối tài khoản Google Sheets và chọn đúng file/sheet chứa danh sách người đăng ký sự kiện. Đảm bảo bảng dữ liệu có các cột thông tin như Họ tên, Email, Mã vé (Ticket ID).
- **Insert image (HTTP Request):** Node này gọi API để tạo mã QR động dựa trên `Ticket ID` của người tham dự dưới dạng binary image.
- **Make Copy of Template (Google Drive):** Cần cung cấp **Google Doc Template ID** của phôi vé mẫu để n8n tạo một bản sao mới cho mỗi người tham dự.
- **Change Custom Variables (Google Docs) & Insert image:** Cấu hình để thay thế các biến văn bản (ví dụ: `{{nama_lengkap}}`) bằng dữ liệu thật từ Google Sheets và chèn hình ảnh mã QR vào đúng vị trí trên tài liệu.
- **Generate PDF & Add PDF To Drive (Google Drive):** Chuyển đổi Google Doc thành file PDF hoàn chỉnh và lưu vào một thư mục chỉ định trên Google Drive. *(Mẹo: Hãy đảm bảo thư mục Google Drive để chế độ chia sẻ phù hợp để file đính kèm gửi đi tải xuống được mượt mà).*
- **Send an Email (SMTP):** Điền thông tin SMTP của các sếp để gửi email chứa file vé PDF đính kèm đến thẳng hộp thư của người tham dự.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một dòng dữ liệu mẫu trên Google Sheets để kiểm tra xem email và vé PDF xuất ra có đúng định dạng chưa.
- Sau khi test ngon lành, các sếp gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống chuyên nghiệp hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng:
1. **Tích hợp Telegram/Slack:** Gửi một thông báo nhỏ vào nhóm ban tổ chức (Admin) mỗi khi có khách hàng đăng ký thành công và nhận vé.
2. **Cập nhật trạng thái:** Sau khi gửi email thành công, thêm một bước cập nhật cột "Trạng thái gửi vé: Đã gửi" ngược lại vào Google Sheets để dễ kiểm soát.
3. **Mã hóa Check-in:** Kết hợp quét mã QR bằng điện thoại thông minh tại cửa sự kiện để điểm danh nhanh chóng.

### 📌 Kết luận
Việc tự động hóa tạo và gửi vé sự kiện chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Google Workspace. Hãy áp dụng ngay workflow này để giải phóng bản thân khỏi các tác vụ thủ công lặp đi lặp lại và nâng tầm chuyên nghiệp cho sự kiện của các sếp! Chúc các sếp thao tác thành công! 🚀