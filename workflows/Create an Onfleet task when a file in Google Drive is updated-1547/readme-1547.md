---
title: "🚀 Tự Động Tạo Task Onfleet Khi File Google Drive Thay Đổi"
description: "Giải pháp tự động hóa 100%: Khi file trong Google Drive được cập nhật, hệ thống sẽ tự động tạo task giao hàng/logistics trên Onfleet mà không cần thao tác thủ công."
slug: "tu-dong-tao-task-onfleet-google-drive"
tags: [n8n, automation, no-code, onfleet, google-drive, logistics]
keywords: [n8n workflow, tự động hóa logistics, onfleet api, google drive trigger, quản lý vận chuyển]
---

# 🚀 Tự Động Tạo Task Onfleet Khi File Google Drive Thay Đổi

Trong các quy trình vận hành logistics hoặc bán hàng, việc đồng bộ dữ liệu giữa kho file (Google Drive) và hệ thống quản lý vận chuyển (Onfleet) thường là một "nỗi đau" lớn. Các nhân viên vận hành thường phải mở file Excel/PDF trong Drive, kiểm tra thông tin đơn hàng, rồi chuyển sang tab Onfleet để nhập liệu thủ công. Quy trình này không chỉ tốn thời gian mà còn dễ xảy ra lỗi do con người (nhầm mã vận đơn, sai địa chỉ, quên cập nhật trạng thái).

Workflow này giải quyết triệt để vấn đề đó bằng cách sử dụng **n8n**. Chỉ cần một file trong thư mục Google Drive được cập nhật (ví dụ: file danh sách đơn hàng mới), hệ thống sẽ tự động kích hoạt và tạo ngay một task giao hàng trên Onfleet. Toàn bộ quá trình diễn ra tức thời, chính xác và hoàn toàn không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian vận hành:** Loại bỏ hoàn toàn bước nhập liệu thủ công giữa Google Drive và Onfleet.
- **Độ chính xác 100%:** Dữ liệu được truyền trực tiếp từ file sang API, tránh lỗi do con người.
- **Phản hồi tức thời:** Task được tạo ngay lập tức khi file thay đổi, giúp đội ngũ giao hàng cập nhật lịch trình sớm nhất.
- **Dễ dàng mở rộng:** Có thể dễ dàng thêm các bước xử lý dữ liệu (làm sạch, validate) trước khi gửi sang Onfleet.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
2. **Tài khoản Google Drive:** Đã kết nối với n8n (OAuth2).
3. **Tài khoản Onfleet:** Có API Key để tạo task.
4. **File mẫu trong Google Drive:** Một file (Excel, CSV, hoặc JSON) chứa thông tin cần thiết để tạo task (địa chỉ, tên người nhận, mô tả...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n của mình theo 2 cách:
- **Cách 1 (Khuyên dùng):** Tải file JSON của workflow từ link gốc [n8n.io/workflows/1547](https://n8n.io/workflows/1547) và chọn **Import from File** trong n8n.
- **Cách 2:** Copy toàn bộ code JSON của workflow và dán vào **Import from URL** hoặc tạo workflow mới rồi dán JSON vào editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này khá gọn gàng với 2 node chính, nhưng các sếp cần cấu hình kỹ các tham số sau để nó chạy đúng ý đồ:

**Node 1: Google Drive Trigger**
- **Credentials:** Chọn hoặc tạo mới credentials Google Drive (OAuth2).
- **Folder ID:** Đây là phần quan trọng nhất. Các sếp cần tìm ID của thư mục Google Drive mà workflow sẽ "lắng nghe".
    - *Cách lấy Folder ID:* Mở thư mục trong Google Drive, nhìn vào URL. Phần sau `folders/` chính là Folder ID.
- **Event:** Chọn loại sự kiện cần theo dõi. Mặc định thường là `file.updated` (khi file được sửa) hoặc `file.created` (khi file mới được tạo). Tùy vào quy trình của sếp mà chọn cho phù hợp.

**Node 2: Onfleet**
- **Credentials:** Chọn hoặc tạo mới credentials Onfleet (API Key).
- **Operation:** Đã được đặt sẵn là `create` (tạo task mới).
- **Mapping Data (Ánh xạ dữ liệu):** Đây là bước "chốt hạ". Các sếp cần ánh xạ các trường dữ liệu từ file Google Drive sang các trường yêu cầu của Onfleet:
    - `origin`: Địa chỉ điểm xuất phát (có thể là cố định hoặc lấy từ file).
    - `destination`: Địa chỉ điểm đến (lấy từ cột địa chỉ trong file).
    - `description`: Mô tả đơn hàng (lấy từ cột ghi chú/mô tả trong file).
    - `driver_id`: ID của tài xế (nếu muốn gán sẵn tài xế) hoặc để trống để Onfleet tự phân công.
    - *Lưu ý:* Đảm bảo cấu trúc dữ liệu trong file Google Drive khớp với các trường mà Onfleet yêu cầu. Nếu file là Excel/CSV, các sếp có thể cần thêm một node "Code" hoặc "Set" để chuyển đổi dữ liệu trước khi gửi sang Onfleet nếu cấu trúc không khớp trực tiếp.

#### 3. Kích hoạt ⚡️
- **Test Run:** Trước khi bật Active, các sếp hãy tạo một file mẫu trong thư mục Google Drive đã cấu hình. Chạy thử workflow (Execute Workflow) để xem dữ liệu có được truyền sang Onfleet không. Kiểm tra xem task có xuất hiện trong dashboard Onfleet không.
- **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n. Từ giờ, mọi thay đổi trong thư mục Google Drive sẽ tự động tạo task Onfleet.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước Validate:** Chèn một node "IF" hoặc "Code" giữa Google Drive và Onfleet để kiểm tra dữ liệu. Ví dụ: Nếu địa chỉ trống, không tạo task mà gửi email báo lỗi cho nhân viên.
- **Gửi thông báo qua Slack/Telegram:** Sau khi tạo task thành công, thêm một node Slack hoặc Telegram để gửi thông báo cho đội ngũ vận hành: "Đã tạo task #123 cho địa chỉ X".
- **Xử lý nhiều loại file:** Nếu file là Excel, các sếp có thể dùng node "Google Sheets" thay vì "Google Drive Trigger" nếu muốn theo dõi từng dòng thay vì cả file. Tuy nhiên, với workflow này, việc theo dõi file update phù hợp hơn cho các file danh sách tổng hợp.
- **Log hoạt động:** Thêm một node "Google Sheets" hoặc "Postgres" để lưu lại lịch sử các task đã tạo, giúp đối soát sau này.

### 📌 Kết luận
Việc tự động hóa quy trình từ Google Drive sang Onfleet là một bước tiến nhỏ nhưng mang lại hiệu quả lớn trong vận hành logistics. Với workflow này, các sếp có thể giải phóng nhân sự khỏi các công việc lặp lại, tập trung vào những việc quan trọng hơn. Hãy thử áp dụng ngay để trải nghiệm sự khác biệt!