---
title: "🚀 Tự động phát hiện và di chuyển file Google Drive trùng lặp với Supabase và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động giám sát Google Drive, phát hiện file trùng lặp bằng mã băm MD5, dọn dẹp vào thư mục riêng, cảnh báo qua Slack và ghi log toàn bộ vào Supabase."
slug: "tu-dong-phat-hien-di-chuyen-file-google-drive-trung-lap"
tags: [n8n, automation, google-drive, supabase, slack, file-management]
keywords: [n8n workflow, tự động hóa google drive, phát hiện file trùng lặp, supabase dedup, slack notification]
---

# 🚀 Tự động phát hiện và di chuyển file Google Drive trùng lặp với Supabase và Slack

Các sếp có đau đầu khi thư mục Google Drive chung của công ty ngày càng phình to vì nhân sự upload nhầm các file trùng lặp (hình ảnh, tài liệu, hợp đồng...)? Việc kiểm tra thủ công vừa mất thời gian, vừa làm lãng phí dung lượng lưu trữ và gây rối loạn trong việc quản lý tài liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do chuyên gia **Shashwat Singh** thiết kế. Workflow này sẽ tự động giám sát Google Drive, tính toán mã băm nội dung file (MD5 Hash), đối chiếu với cơ sở dữ liệu Supabase để tự động dọn dẹp file trùng, bắn thông báo qua Slack và ghi log chi tiết mọi hoạt động mà không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Dọn dẹp dung lượng tự động:** Phát hiện và lập tức cô lập các file trùng lặp dựa trên nội dung thực tế (không phụ thuộc vào tên file).
- **Cảnh báo tức thời:** Bắn tin nhắn qua Slack ngay khi phát hiện file trùng lặp để các sếp hoặc đội ngũ nắm bắt.
- **Hệ thống log minh bạch:** Mọi sự kiện (file độc nhất, file trùng, lỗi thiếu binary, xung đột cơ sở dữ liệu) đều được ghi nhận vào bảng audit log của Supabase.
- **Vận hành 24/7:** Hoạt động ngầm liên tục, tự động bảo vệ kho dữ liệu Google Drive luôn gọn gàng, sạch sẽ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Account:** Tài khoản kết nối OAuth2 để theo dõi thư mục và quản lý file.
- **Supabase Account:** Dự án Supabase chuẩn bị sẵn 2 bảng: `file_hashes` và `dedup_audit_log`.
- **Slack Workspace:** Bot/Webhook để gửi thông báo cảnh báo file trùng lặp vào kênh chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào giao diện làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Google Drive Trigger & Download File:** 
  - Chọn tài khoản Google Drive OAuth2 credentials.
  - Chỉ định ID của thư mục Google Drive cần theo dõi file upload mới.
- **Crypto Node:** 
  - Cấu hình thuật toán tạo mã băm (`MD5`) dựa trên dữ liệu binary của file để đảm bảo nhận diện chính xác nội dung file.
- **Supabase Nodes (Check Hash Exists, Insert New Hash, Log Events...):**
  - Kết nối Supabase API credentials.
  - Đảm bảo các bảng `file_hashes` và `dedup_audit_log` đã được tạo sẵn trong cơ sở dữ liệu của các sếp.
- **Move to Duplicates (Google Drive):**
  - Cấu hình thao tác `move` và điền **ID của thư mục "Duplicates"** trên Google Drive để hệ thống tự động gom các file trùng về một chỗ.
- **Notify Duplicate (Slack):**
  - Chọn kênh Slack nhận thông báo và tùy chỉnh nội dung tin nhắn cảnh báo (tên file, thời gian, đường dẫn).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử upload một file mẫu lên Google Drive để test luồng xử lý (file độc nhất, sau đó upload lại chính file đó để kiểm tra luồng trùng lặp).
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Email:** Ngoài Slack, các sếp có thể nhân bản node thông báo để gửi cảnh báo qua Telegram Bot hoặc Email cho quản lý kho tài liệu.
- **Báo cáo định kỳ:** Tạo một Scheduled Trigger chạy mỗi tuần một lần để tổng hợp số lượng file trùng lặp đã được dọn dẹp từ bảng `dedup_audit_log` gửi về báo cáo cho sếp lớn.
- **Tự động xóa vĩnh viễn (Tùy chọn):** Nếu không muốn lưu trữ file trùng trong thư mục "Duplicates", các sếp có thể thay đổi node Move thành node Delete file sau một khoảng thời gian nhất định để tối ưu hoàn toàn dung lượng Drive.

### 📌 Kết luận
Workflow "Detect and move duplicate Google Drive files with Supabase and Slack" là giải pháp tự động hóa tuyệt vời giúp giải quyết triệt để vấn đề rác dữ liệu trên Google Drive của doanh nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa không gian lưu trữ và nâng cao hiệu suất làm việc!