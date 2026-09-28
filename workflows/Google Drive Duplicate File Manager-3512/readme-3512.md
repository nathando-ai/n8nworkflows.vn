---
title: "🚀 Tự động phát hiện và dọn dẹp file trùng lặp trên Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét, phát hiện và xử lý các file trùng lặp trên Google Drive bằng cách chuyển vào thùng rác hoặc gắn cờ đổi tên."
slug: "quan-ly-file-trung-lap-google-drive-n8n"
tags: [n8n, automation, google-drive, file-management, no-code]
keywords: [n8n workflow, google drive duplicate, tự động hóa google drive, dọn dẹp file trùng lặp, no-code automation]
---

# 🚀 Tự động phát hiện và dọn dẹp file trùng lặp trên Google Drive với n8n

Các sếp có đang đau đầu vì Google Drive ngày càng cạn kiệt dung lượng lưu trữ chỉ vì nhân viên hoặc chính mình vô tình tải lên hàng loạt file trùng lặp? Việc rà soát và xóa thủ công từng file tốn rất nhiều thời gian và cực kỳ nhàm chán.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh do **Ventsislav Minev** chia sẻ, giúp tự động hóa 100% quy trình quét, phát hiện và xử lý file trùng lặp trên Google Drive một cách an toàn và hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm dung lượng lưu trữ:** Tự động loại bỏ các file thừa thãi, tối ưu không gian Google Drive.
- **Tùy biến linh hoạt:** Cho phép chọn giữ lại file đầu tiên (`first`) hoặc file cuối cùng (`last`) được tải lên.
- **An toàn tuyệt đối:** Tùy chọn chuyển file trùng vào Thùng rác (giữ lại 30 ngày có thể khôi phục) hoặc chỉ gắn cờ đổi tên (`DUPLICATE-`).
- **Hoạt động tự động 24/7:** Chạy ngầm định kỳ qua trigger mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Google Drive và cấu hình **Google Drive OAuth2 API Credentials** trong n8n để cấp quyền đọc/ghi file.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes, trong đó có một số node cốt lõi các sếp cần lưu ý cấu hình:

- **Google Drive Trigger**: 
  - Cấu hình tần suất quét (Poll times) - mặc định là kiểm tra file mới mỗi 15 phút.
  - Chọn thư mục (Folder) cần giám sát. *Lưu ý quan trọng:* Nếu chọn thư mục gốc (`/`), workflow sẽ quét toàn bộ file trong mọi thư mục con, hãy cẩn trọng để tránh nhầm lẫn!
- **Config & Edit Fields**: 
  - Thiết lập thông số `keep` (giá trị: `first` hoặc `last` - mặc định là `last`).
  - Thiết lập thông số `action` (giá trị: `trash` để chuyển vào thùng rác, hoặc `flag` để đổi tên thêm tiền tố `DUPLICATE-` - mặc định là `flag`).
- **Working Folder**: Node này lọc các file nằm trực tiếp tại cấp độ 1 của thư mục được chỉ định (không quét sâu vào các thư mục con nếu giữ nguyên bộ lọc mặc định).
- **Send Duplicates to Trash / Google Drive (Update)**: Các node thực thi hành động xóa hoặc đổi tên file trùng dựa theo cấu hình của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu hiện tại trên Drive và kiểm tra kết quả.
- Bật công tắc **Active** để workflow tự động chạy ngầm theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo:** Kết hợp thêm node **Slack** hoặc **Telegram** sau bước xử lý file trùng để gửi báo cáo tổng kết xem hôm nay hệ thống đã dọn dẹp được bao nhiêu file thừa.
- **Lưu log:** Đẩy thông tin các file bị phát hiện trùng lặp vào **Google Sheets** để dễ dàng tra cứu lịch sử dọn dẹp.
- **Mở rộng phạm vi:** Tùy chỉnh node Filter nếu các sếp muốn áp dụng quét cho toàn bộ Drive thay vì chỉ một thư mục cố định.

### 📌 Kết luận
Với workflow **Google Drive Duplicate File Manager**, việc quản lý không gian lưu trữ đám mây chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay hôm nay để giải phóng dung lượng và giữ cho Google Drive của doanh nghiệp luôn gọn gàng, ngăn nắp!