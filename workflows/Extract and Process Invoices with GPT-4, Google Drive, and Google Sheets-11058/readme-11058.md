---
title: "🚀 Tự động hóa xử lý hóa đơn PDF thông minh với AI, Google Drive và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin hóa đơn PDF bằng GPT-4, phân loại tài khoản kế toán, lưu trữ trên Google Drive và cập nhật Google Sheets."
slug: "tu-dong-hoa-xu-ly-hoa-don-pdf-voi-ai-google-drive-sheets"
tags: [n8n, automation, no-code, ai, google-drive, google-sheets, invoice-processing]
keywords: [n8n workflow, tự động hóa hóa đơn, xử lý invoice ai, gpt-4o-mini, google drive trigger, trích xuất hóa đơn pdf]
---

# 🚀 Tự động hóa xử lý hóa đơn PDF thông minh với AI, Google Drive và Google Sheets

Các sếp có đang mệt mỏi mỗi cuối tháng khi phải đối mặt với hàng đống hóa đơn PDF gửi đến, ngồi cặm cụi đọc từng cái, gõ lại tên nhà cung cấp, số tiền, ngày tháng vào Excel, rồi lại tìm thư mục để lưu và đổi tên file thủ công không? Việc này vừa tốn thời gian, vừa dễ dẫn đến sai sót số liệu.

Đừng lo nữa! Hôm nay tụi mình sẽ "lên đồ" một workflow n8n cực xịn sò do tác giả **Wolfgang Renner** chia sẻ, giúp tự động hóa 100% quy trình xử lý hóa đơn. Từ việc nhận file PDF mới trên Google Drive, dùng AI (GPT-4o-mini) đọc hiểu thông tin, phân loại tài khoản kế toán, đổi tên file chuẩn chỉnh, lưu trữ gọn gàng cho đến việc cập nhật thẳng vào Google Sheets. Tất cả diễn ra mượt mà không cần một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhập liệu thủ công, AI sẽ thay các sếp "cân" hết từ đọc file đến phân loại.
- **Dữ liệu chuẩn xác 100%:** Trích xuất thông tin nhất quán (Nhà cung cấp, mã giao dịch, số tiền, tiền tệ...) và map đúng tài khoản kế toán.
- **Tổ chức khoa học:** File hóa đơn tự động được đổi tên theo chuẩn `YYMMDD Nhà cung cấp.pdf` và lưu vào đúng thư mục trên Google Drive.
- **Báo cáo tức thì:** Bảng kê booking (Booking List) trên Google Sheets được cập nhật dòng mới ngay khi có hóa đơn vừa xử lý xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Account:** Tạo sẵn thư mục chứa hóa đơn đầu vào (Input) và các thư mục lưu trữ đầu ra (Output theo tài khoản kế toán).
- **Google Sheets Account:** Chuẩn bị sẵn 1 Sheet danh mục tài khoản (Chart of Accounts) và 1 Sheet ghi nhận danh sách booking (Booking List).
- **OpenAI API Key:** Tài khoản OpenAI có quyền gọi mô hình GPT-4o-mini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON về máy.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào menu 3 chấm ở góc trên bên phải -> Chọn **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` để dán trực tiếp vào màn hình workflow trống).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 12 nodes phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các node quan trọng sau:

- **Google Drive Trigger:** 
  - Chọn Credentials tài khoản Google Drive của các sếp.
  - Chọn đúng thư mục đầu vào (`Input Folder`) nơi các sếp sẽ upload các file hóa đơn PDF lên.
- **Download file:** 
  - Node này nhận tín hiệu từ Trigger để tải file PDF nhị phân về chuẩn bị cho bước đọc file.
- **Extract from File:** 
  - Cấu hình operation là `pdf` để bóc tách dữ liệu thô từ file PDF vừa tải.
- **Invoice Agent & OpenAI Chat Model:**
  - Chọn Credentials cho OpenAI API.
  - Tại node **OpenAI Chat Model**, đảm bảo model đang chọn là `gpt-4o-mini` (hoặc model GPT-4 phù hợp).
  - AI Agent sẽ đóng vai trò đọc thông tin thông minh (Vendor, booking text, amount, currency...).
- **Structured Output Parser:** 
  - Định nghĩa cấu trúc dữ liệu đầu ra mà AI cần trả về (như tên nhà cung cấp, số tiền, ngày tháng, mã tài khoản...) để các node phía sau dễ dàng sử dụng.
- **Chart of Accounts (Google Sheets Tool):**
  - Kết nối Credentials Google Sheets.
  - Trỏ đến file Google Sheet chứa danh mục tài khoản kế toán của công ty để AI tham chiếu và gán đúng mã tài khoản cho hóa đơn.
- **Edit Fields & Save to Drive / Move file:**
  - Cấu hình quy tắc đặt tên mới cho file theo định dạng `YYMMDD Vendor`.
  - Chọn thư mục lưu trữ tương ứng trên Google Drive dựa trên tài khoản kế toán đã phân loại.
- **Update Booking List (Google Sheets):**
  - Kết nối Credentials Google Sheets.
  - Chọn file Google Sheet quản lý booking và cấu hình operation `append` để tự động thêm một dòng mới chứa toàn bộ thông tin hóa đơn vừa xử lý.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test Workflow** và thử upload một file PDF hóa đơn mẫu vào thư mục Google Drive Input để kiểm tra xem AI đọc đúng không, file có được đổi tên và chuyển đi đúng chỗ không.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để workflow tự động chiến đấu 24/7!

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tự động hóa này trở nên "ba đầu sáu tay" hơn, các sếp có thể mở rộng thêm:
- **Thêm thông báo Telegram / Slack:** Gắn thêm node thông báo ngay vào nhóm chat nội bộ của phòng kế toán mỗi khi có một hóa đơn mới được xử lý thành công kèm link file trên Drive.
- **Xử lý ngoại lệ (Error Handling):** Thêm nhánh **Error Trigger** để bắt lỗi nếu hóa đơn mờ, AI không đọc được, sau đó gửi email cảnh báo về cho bộ phận hành chính.
- **Tạo bảng tổng hợp chi phí:** Kết hợp thêm các node định kỳ để gửi báo cáo tổng hợp chi phí theo tuần/tháng vào email của sếp lớn.

### 📌 Kết luận
Xử lý hóa đơn thủ công đã là chuyện của thế kỷ trước. Với workflow n8n kết hợp GPT-4o-mini và Google Workspace này, các sếp vừa tiết kiệm được nguồn lực nhân sự, vừa tối ưu hóa tốc độ làm việc cho cả bộ phận kế toán. Hãy setup ngay hôm nay để tận hưởng sức mạnh tuyệt vời từ tự động hóa no-code nhé!