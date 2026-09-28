---
title: "🚀 Tự Động Sao Chép File FTP Lên Google Drive Định Kỳ (Không Code)"
description: "Giải pháp tự động hóa 100% để đồng bộ file từ máy chủ FTP lên Google Drive theo lịch. Đảm bảo backup an toàn, tiết kiệm thời gian quản trị."
slug: "tu-dong-sao-kep-ftp-len-google-drive"
tags: [n8n, automation, no-code, ftp, google-drive, backup]
keywords: [n8n workflow, tự động hóa backup, sync ftp google drive, sao chép file định kỳ, n8n file management]
---

# 🚀 Tự Động Sao Chép File FTP Lên Google Drive Định Kỳ (Không Code)

Các sếp có bao giờ phải đau đầu vì việc kiểm tra thủ công xem file trên máy chủ FTP đã được backup chưa? Hay tình trạng file bị mất, lỗi do quên sao chép định kỳ? Đây là nỗi đau chung của nhiều đội ngũ kỹ thuật và vận hành khi phải quản lý dữ liệu phân tán giữa nhiều hệ thống.

Workflow **"Automatic FTP File Backup to Google Drive with Scheduled Sync"** chính là giải pháp "chữa cháy" hoàn hảo. Nó hoạt động như một người gác cổng tự động, liên tục quét thư mục FTP, tải file về và đẩy lên Google Drive theo đúng lịch trình mà các sếp đã thiết lập. Không cần viết một dòng code, không cần lo lắng về việc quên backup, mọi thứ diễn ra trơn tru và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Backup An Toàn & Liên Tục:** Dữ liệu quan trọng luôn được sao lưu lên đám mây Google Drive, giảm thiểu rủi ro mất dữ liệu do sự cố máy chủ.
- **Tiết Kiệm 100% Thời Gian Thủ Công:** Không cần vào server để kéo file hay chạy script phức tạp. Hệ thống tự động chạy theo lịch (mỗi giờ, mỗi ngày...).
- **Đồng Bộ Dữ Liệu Nhanh Chóng:** File mới xuất hiện trên FTP sẽ được phát hiện và chuyển lên Drive ngay trong chu kỳ quét tiếp theo.
- **Quản Lý Tập Trung:** Tất cả file backup được lưu vào một thư mục Google Drive duy nhất, dễ dàng truy cập và chia sẻ khi cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy instance n8n (cloud hoặc self-hosted).
2. **Thông tin kết nối FTP:**
   - Host, Port, Username, Password của máy chủ FTP.
   - Đường dẫn thư mục (Path) trên FTP cần sao chép (ví dụ: `/backups`, `/reports`).
3. **Tài khoản Google Drive:**
   - Tài khoản Google đã đăng nhập.
   - ID của thư mục đích trên Google Drive (nơi muốn lưu file backup).
4. **Quyền truy cập:** Đảm bảo tài khoản FTP có quyền đọc (read) thư mục nguồn và tài khoản Google có quyền ghi (write) vào thư mục đích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** (hoặc dán JSON workflow vào editor).
3. Workflow sẽ hiển thị 4 node chính: Cron Trigger, FTP List, FTP Download, và Google Drive Upload.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ từng node để tránh lỗi:

**Node 1: `Start: Every Hour` (Cron Trigger)**
- Mặc định workflow chạy mỗi 1 giờ.
- **Cách chỉnh:** Click vào node, thay đổi biểu thức Cron.
  - Chạy mỗi ngày lúc 2h sáng: `0 2 * * *`
  - Chạy mỗi 30 phút: `*/30 * * * *`
  - Chạy mỗi tuần vào thứ 2: `0 0 * * 1`

**Node 2: `FTP: List Files`**
- **Credentials:** Chọn hoặc tạo mới credentials FTP (điền Host, User, Pass).
- **Path:** Mặc định là `/{{FTP_FOLDER}}`. Các sếp cần thay `{{FTP_FOLDER}}` bằng đường dẫn thực tế của thư mục trên FTP.
  - *Ví dụ:* Nếu thư mục tên là `logs`, hãy đổi thành `/logs`.
  - *Lưu ý:* Nếu muốn quét đệ quy (sub-folders), hãy kiểm tra tùy chọn "Recursive" trong node nếu n8n hỗ trợ, hoặc tạo thêm logic lọc.

**Node 3: `FTP: Download File`**
- Node này tự động lấy đường dẫn file từ node trước đó (`={{$json["path"]}}`).
- **Credentials:** Sử dụng cùng credentials FTP với node List Files.
- **Lưu ý quan trọng:** Node này sẽ chạy cho **mỗi file** được tìm thấy. Đảm bảo dung lượng file không quá lớn gây timeout nếu không cấu hình thêm timeout trong credentials.

**Node 4: `Google Drive: Upload`**
- **Credentials:** Chọn credentials Google Drive OAuth2.
- **Folder ID:** Tìm trường `Folder ID` (hoặc `Parent ID`).
  - Cách lấy ID: Mở thư mục đích trên Google Drive, nhìn vào URL trình duyệt. Phần cuối URL sau `/folders/` chính là **Folder ID**.
  - Thay `{{GDRIVE_FOLDER_ID}}` bằng ID thực tế này.
- **File Name:** Có thể giữ nguyên tên file từ FTP hoặc tùy chỉnh thêm timestamp để tránh trùng tên (nếu file cũ bị ghi đè).

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** (hoặc Test) để chạy thử một lần.
   - Kiểm tra xem file có xuất hiện trên Google Drive không.
   - Kiểm tra log để xem có lỗi kết nối FTP hay quyền truy cập Drive không.
2. **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động theo lịch Cron đã thiết lập.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo khi lỗi:** Thêm node **Slack** hoặc **Telegram** sau node Google Drive (hoặc dùng Error Trigger) để báo ngay cho các sếp khi quá trình backup thất bại.
- **Xóa file cũ trên FTP:** Nếu FTP chỉ dùng làm trung gian, các sếp có thể thêm node FTP Delete sau khi upload thành công để tiết kiệm dung lượng máy chủ.
- **Lọc loại file:** Thêm node **IF** hoặc **Filter** sau bước List Files để chỉ backup các file có đuôi `.csv`, `.log`, `.pdf`... tránh tải lên những file tạm không cần thiết.
- **Lưu log chi tiết:** Kết nối thêm node **Google Sheets** hoặc **Database** để ghi lại lịch sử backup (tên file, thời gian, kích thước, trạng thái) giúp dễ dàng kiểm tra và audit.

### 📌 Kết luận
Việc quản lý backup thủ công không chỉ tốn thời gian mà còn tiềm ẩn rủi ro cao. Với workflow **FTP to Google Drive Sync** này, các sếp có thể an tâm ngủ ngon vì dữ liệu luôn được bảo vệ và đồng bộ tự động. Hãy import ngay, cấu hình 5 phút và để n8n làm việc thay cho bạn!