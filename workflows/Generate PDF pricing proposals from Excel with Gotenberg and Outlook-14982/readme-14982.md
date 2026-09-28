---
title: "🚀 Tự Động Tạo Báo Giá PDF Từ Excel Bằng Gotenberg và Microsoft Outlook"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo file báo giá PDF từ dữ liệu Excel và gửi trực tiếp qua Microsoft Outlook bằng Gotenberg một cách chuyên nghiệp."
slug: "tao-bao-gia-pdf-tu-excel-gotenberg-outlook"
tags: [n8n, automation, no-code, microsoft-excel, microsoft-outlook, gotenberg, pdf-generation]
keywords: [n8n workflow, tạo pdf tự động, gotenberg n8n, microsoft excel outlook automation, tự động hóa báo giá]
keywords: [n8n workflow, tạo pdf tự động, gotenberg n8n, microsoft excel outlook automation, tự động hóa báo giá]
---

# 🚀 Tự Động Tạo Báo Giá PDF Từ Excel Bằng Gotenberg và Microsoft Outlook

Trong môi trường kinh doanh hiện đại, việc gửi báo giá (pricing proposals) nhanh chóng và chính xác cho khách hàng là chìa khóa chốt sale. Tuy nhiên, nếu đội ngũ sales vẫn đang làm thủ công: copy dữ liệu từ Excel, điền vào file Word/PDF, xuất file và mở Outlook để gửi, các sếp chắc chắn sẽ mất rất nhiều thời gian và dễ xảy ra sai sót.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: lấy dữ liệu từ **Microsoft Excel**, sử dụng **Gotenberg** để biên dịch thành file PDF chuyên nghiệp, và gửi thẳng qua **Microsoft Outlook** mà không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn thao tác thủ công từ khâu đọc dữ liệu Excel đến gửi email.
- **Tốc độ chớp nhoáng:** Tạo và gửi hàng loạt bản báo giá chỉ trong vài giây ngay khi có yêu cầu.
- **Chuyên nghiệp & Chuẩn xác:** Sử dụng Gotenberg để render file PDF đẹp mắt, không lo lệch định dạng hay sai sót số liệu.
- **Tích hợp liền mạch:** Hoạt động trơn tru với hệ sinh thái Microsoft 365 (Excel & Outlook) mà doanh nghiệp đang sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
1. **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
2. **Microsoft Account:** Đã cấu hình Credentials cho **Microsoft Excel** và **Microsoft Outlook** trong n8n.
3. **Gotenberg Server:** Một instance Gotenberg đang chạy (thường chạy qua Docker) để chuyển đổi HTML/Markdown sang PDF.
4. **File Template Excel:** Bảng tính Excel chứa danh sách thông tin khách hàng và giá sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp sao chép mã JSON của workflow (hoặc tải file JSON từ nguồn gốc).
- Vào giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình lại các node cốt lõi sau để hệ thống nhận đúng dữ liệu:
- **Webhook Node (`webhook`):** Điểm khởi đầu nhận tín hiệu kích hoạt quy trình tạo báo giá (có thể trigger từ CRM, form hoặc thủ công).
- **Microsoft Excel Node (`microsoftExcel`):** 
  - Chọn đúng Credentials tài khoản Microsoft của công ty.
  - Trỏ đến đúng File ID và Sheet Name chứa dữ liệu báo giá sản phẩm/khách hàng.
- **Code Node (`code`):** Dùng để xử lý dữ liệu thô từ Excel, chuyển đổi định dạng và chuẩn bị cấu trúc HTML/dữ liệu truyền vào Gotenberg.
- **HTTP Request Node (`httpRequest` - Gotenberg):** 
  - Cấu hình endpoint kết nối đến server Gotenberg của các sếp (ví dụ: `http://gotenberg:3000/forms/chromium/html/convert`).
  - Đảm bảo cấu hình đúng body dạng `multipart/form-data` để đẩy file HTML/Template sang dịch vụ Gotenberg render ra PDF.
- **Microsoft Outlook Node (`microsoftOutlook`):** 
  - Chọn Credentials Outlook.
  - Cấu hình người nhận (To), tiêu đề email (Subject), nội dung (Body) và đính kèm file PDF vừa được tạo từ bước Gotenberg.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một bản ghi dữ liệu mẫu để kiểm tra xem file PDF có được tạo đúng định dạng và email đã gửi đi thành công chưa.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối workflow để bắn thông báo về cho đội ngũ sales biết ngay khi báo giá đã được gửi thành công cho khách.
- **Lưu trữ lịch sử:** Thêm một bước lưu file PDF vừa tạo vào Google Drive hoặc OneDrive theo từng thư mục tên khách hàng để dễ đối soát.
- **Xử lý lỗi (Error Trigger):** Cấu hình thêm Error Workflow để nếu lỗi mạng Gotenberg hoặc lỗi tài khoản Outlook, hệ thống sẽ tự động ping cảnh báo vào nhóm chat kỹ thuật.

### 📌 Kết luận
Tự động hóa quy trình tạo báo giá từ Excel sang PDF chưa bao giờ dễ dàng đến thế với sự kết hợp của n8n, Gotenberg và Microsoft Outlook. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tối ưu hóa thời gian và bứt phá doanh số trong hôm nay!