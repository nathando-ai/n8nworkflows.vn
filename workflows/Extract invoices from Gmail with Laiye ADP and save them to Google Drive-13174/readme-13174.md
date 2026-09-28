---
title: "🚀 Tự động trích xuất hóa đơn từ Gmail với Laiye ADP và lưu trữ vào Google Drive"
description: "Hướng dẫn tự động hóa quy trình nhận hóa đơn qua Gmail, xử lý trích xuất dữ liệu thông minh bằng Laiye ADP và tự động lưu file gọn gàng lên Google Drive."
slug: "trich-xuat-hoa-don-gmail-laiye-adp-google-drive"
tags: [n8n, automation, no-code, invoice-processing, google-drive, gmail, laiye-adp]
keywords: [n8n workflow, tự động hóa hóa đơn, laiye adp, trích xuất hóa đơn gmail, google drive automation]
keywords: [n8n workflow, tự động hóa, xử lý hóa đơn, trích xuất gmail, google drive, laiye adp]
---

# 🚀 Tự động trích xuất hóa đơn từ Gmail với Laiye ADP và Google Drive

Việc xử lý hóa đơn thủ công từ email mỗi dịp cuối tháng luôn là cơn ác mộng của bộ phận kế toán và vận hành. Nhân viên phải mất hàng giờ đồng hồ để tải file đính kèm từ Gmail, nhập liệu thủ công vào Excel hoặc phần mềm kế toán, rồi lại cặm cụi lưu trữ phân loại vào Google Drive. Quá trình này không chỉ tốn thời gian mà còn cực kỳ dễ xảy ra sai sót.

Giải pháp? Workflow n8n này sẽ tự động hóa **100%** quy trình từ A-Z: Nhận hóa đơn từ Gmail, gọi AI/công cụ trích xuất thông minh **Laiye ADP** để bóc tách dữ liệu, và tự động lưu trữ file gọn gàng lên **Google Drive**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh tải thủ công từng hóa đơn hay copy-paste dữ liệu mỏi tay.
- **Chính xác tuyệt đối:** Ứng dụng công nghệ Laiye ADP và các node xử lý thông minh giúp bóc tách dữ liệu sạch sẽ, chuẩn xác.
- **Lưu trữ khoa học:** Tự động đồng bộ và phân loại hóa đơn vào đúng thư mục trên Google Drive ngay khi email vừa đổ về.
- **Hoạt động 24/7:** Chạy ngầm liên tục không mệt mỏi, đảm bảo không bỏ sót bất kỳ hóa đơn nào từ nhà cung cấp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (để cấu hình Trigger nhận email chứa hóa đơn).
- **Tài khoản Google Drive** (để lưu trữ file hóa đơn đã xử lý).
- **Tài khoản Laiye ADP** cùng API Key/Credentials tương ứng để thực hiện trích xuất dữ liệu từ hóa đơn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy mã JSON cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl + V` để paste trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Gmail Trigger (`gmailTrigger`):** Kết nối tài khoản Gmail của doanh nghiệp. Thiết lập bộ lọc (như nhãn - label, tiêu đề chứa từ khóa "Hóa đơn", "Invoice") để chỉ bắt các email thực sự cần xử lý, tránh quét nhầm email rác.
- **Trích xuất file (`extractFromFile` & `HTTP Request` với Laiye ADP):** Cấu hình kết nối API tới Laiye ADP, truyền file hóa đơn đính kèm từ Gmail sang để hệ thống tiến hành bóc tách dữ liệu.
- **Xử lý điều kiện & dữ liệu (`if`, `code`, `merge`):** Kiểm tra xem file đính kèm có đúng định dạng (PDF, ảnh...) và kết quả trích xuất từ Laiye ADP có trả về thành công hay không trước khi chuyển bước tiếp theo.
- **Google Drive (`googleDrive`):** Kết nối tài khoản Google Drive và trỏ tới thư mục (`Folder ID`) cụ thể để lưu trữ các file hóa đơn đã được xử lý xong.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email mẫu chứa hóa đơn đến Gmail đã kết nối để kiểm tra xem dữ liệu có chạy qua từng node trơn tru không.
- Sau khi test thành công, gạt công tắc sang trạng thái **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Slack hoặc Telegram để gửi thông báo ngay về nhóm kế toán mỗi khi có một hóa đơn mới được xử lý và lưu trữ thành công.
- **Lưu log vào Google Sheets:** Kết hợp thêm node Google Sheets để ghi lại lịch sử (Tên nhà cung cấp, Số tiền, Ngày tháng, Link file trên Drive) giúp việc tra cứu dòng tiền trở nên dễ dàng hơn bao giờ hết.
- **Phân loại thư mục thông động:** Dùng node Code để đọc tên nhà cung cấp từ kết quả Laiye ADP và tự động tạo/lưu vào các thư mục con tương ứng trên Google Drive theo tháng hoặc theo tên công ty.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn với n8n, Gmail, Laiye ADP và Google Drive không chỉ giúp giải phóng sức lao động thủ công cho đội ngũ kế toán mà còn giúp doanh nghiệp bước đầu chuyển đổi số cực kỳ hiệu quả. Hãy áp dụng ngay hôm nay để tối ưu hóa vận hành cho doanh nghiệp của các sếp!