---
title: "🚀 Tự động trích xuất hóa đơn PDF từ Gmail vào Google Sheets với Cradl AI và Human Review"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình đọc hóa đơn PDF từ Gmail, trích xuất dữ liệu bằng AI và lưu trữ vào Google Sheets kèm cơ chế kiểm duyệt."
slug: "tu-dong-trich-xuat-hoa-don-pdf-gmail-google-sheets-n8n"
tags: [n8n, automation, no-code, ai, google-sheets, gmail, invoice-processing]
keywords: [n8n workflow, trích xuất hóa đơn, tự động hóa gmail google sheets, cradl ai, xử lý hóa đơn ai]
---

# 🚀 Tự động trích xuất hóa đơn PDF từ Gmail vào Google Sheets với Cradl AI và Human Review

Các sếp có đang cảm thấy mệt mỏi mỗi cuối tháng khi phải ngồi "soi" từng tờ hóa đơn PDF gửi đến email, gõ thủ công từng dòng tiền, tên nhà cung cấp, mã số thuế vào Google Sheets không? Công việc này không chỉ tốn hàng giờ đồng hồ mà còn cực kỳ dễ sai sót số liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n hoàn toàn tự động: Hóa đơn vừa vào Gmail sẽ được AI đọc hiểu, tách từng dòng chi tiết, cho phép nhân sự kiểm duyệt (Human-in-the-loop) trước khi tự động "đẩy" thẳng vào Google Sheets. Tiết kiệm 99% thời gian nhập liệu thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ hoàn toàn khâu tải file PDF và gõ Excel thủ công.
- **Độ chính xác cao nhờ AI:** Sử dụng Cradl AI chuyên biệt cho bài toán bóc tách hóa đơn, nhận diện linh hoạt mọi định dạng.
- **Kiểm soát an toàn (Human-in-the-loop):** Có cơ chế review, phê duyệt hoặc chỉnh sửa dữ liệu trực quan trước khi ghi nhận chính thức.
- **Đồng bộ tức thì:** Dữ liệu từng dòng hàng (line items) được bóc tách và phân rã gọn gàng vào Google Sheets để làm báo cáo tài chính ngay lập tức.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Gmail** (hoặc Workspace) để nhận hóa đơn.
- Tài khoản **Cradl AI** (Tạo tài khoản miễn phí [tại đây](https://rc.app.cradl.ai/login?redirect=signup&template=n8n%2Finvoices-gmail-to-sheets.json)).
- File **Google Sheets** chuẩn bị sẵn các cột tương ứng để lưu thông tin hóa đơn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của template [15011](https://n8n.io/workflows/15011) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Gmail Trigger (`Gmail Trigger`):** Kết nối tài khoản Gmail của các sếp. Tinh chỉnh bộ lọc tìm kiếm (Search filter) để chỉ quét các email có hóa đơn. Ví dụ: nếu nhận hóa đơn qua email chung, hãy thêm `to:invoices@mycompany.com has:attachment filename:pdf`.
- **Lọc file PDF (`Filter PDF attachments` - Code Node):** Node này dùng để lọc các tệp đính kèm đảm bảo đúng định dạng PDF trước khi gửi sang AI xử lý.
- **Trích xuất thông tin AI (`Extract invoice details with AI` - Cradl AI Node):** 
  - Kết nối tài khoản Cradl AI của các sếp.
  - Định nghĩa các trường dữ liệu cần trích xuất (Tên nhà cung cấp, Tổng tiền, Mã số thuế, Chi tiết từng dòng hàng...).
  - Kích hoạt tính năng Human-in-the-loop trên giao diện Cradl AI để đội ngũ kế toán có thể kiểm duyệt dữ liệu khi cần.
- **Tách từng dòng hàng (`Split out each invoice line` - Split Out Node):** Giúp bóc tách các dòng sản phẩm/dịch vụ riêng lẻ trong một hóa đơn ra thành các bản ghi độc lập.
- **Ghi vào Google Sheets (`Add invoice line to Google Sheets` - Google Sheets Node):** 
  - Kết nối tài khoản Google Drive/Sheets.
  - Chọn file Spreadsheet và Sheet Name chính xác.
  - Map (ánh xạ) các trường dữ liệu mà Cradl AI vừa bóc tách vào đúng các cột tương ứng trên Google Sheets.
- **Đánh dấu đã đọc (`Mark a message as read` - Gmail Node):** Tự động đánh dấu email chứa hóa đơn đã được xử lý để tránh bị quét lặp lại ở các lần chạy sau.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với một email hóa đơn mẫu để kiểm tra xem dữ liệu có chảy mượt mà từ Gmail sang Cradl AI rồi vào Google Sheets hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động túc trực 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node **Slack** hoặc **Telegram** sau bước ghi vào Google Sheets để bắn thông báo ngay về group công ty: *"Vừa nhận và cập nhật thành công hóa đơn từ [Tên Nhà Cung Cấp] tổng tiền [Số tiền]"*.
- **Mở rộng đích đến:** Ngoài Google Sheets, các sếp hoàn toàn có thể thay thế bằng các phần mềm kế toán chuyên dụng như Xero, MISA, QuickBooks thông qua API hoặc các node hỗ trợ sẵn của n8n.
- **Lưu trữ file PDF:** Kết hợp lưu bản gốc file PDF hóa đơn vào Google Drive/OneDrive tương ứng với từng dòng dữ liệu trên bảng tính để tiện đối soát thuế sau này.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn không chỉ giúp giải phóng kế toán khỏi đống giấy tờ, file PDF nhàm chán mà còn giúp doanh nghiệp quản trị tài chính theo thời gian thực một cách chính xác tuyệt đối. Hãy áp dụng ngay workflow này vào hệ thống của các sếp ngay hôm nay nhé!