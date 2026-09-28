---
title: "🚀 Tự động hóa chuyển file từ FTP lên Google Drive với n8n - Giải pháp tiết kiệm thời gian 100%"
description: "Hướng dẫn chi tiết cách tự động chuyển file từ máy chủ FTP lên Google Drive bằng n8n. Tiết kiệm thời gian, tự động hóa hoàn toàn, không cần code."
slug: "tu-dong-chuyen-file-ftp-google-drive-n8n"
tags: [n8n, automation, no-code, ftp, google-drive]
keywords: [n8n workflow, tự động hóa, ftp, google drive, tự động hóa file]
---

# 🚀 Tự động hóa chuyển file từ FTP lên Google Drive với n8n - Giải pháp tiết kiệm thời gian 100%

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải chuyển hàng loạt file từ máy chủ FTP lên Google Drive mỗi ngày không? Việc này tốn thời gian, dễ xảy ra lỗi và không thể thực hiện liên tục 24/7. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể: Không cần can thiệp thủ công mỗi khi chuyển file.
- Tự động hóa hoàn toàn: Workflow chạy liên tục 24/7 mà không cần giám sát.
- Tăng độ chính xác: Giảm thiểu lỗi do thao tác thủ công.
- Tích hợp dễ dàng: Kết nối liền mạch với các dịch vụ khác trong hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản FTP với thông tin đăng nhập (server, username, password).
- Tài khoản Google Drive với quyền truy cập đầy đủ.
- Thư mục đích trên Google Drive để lưu file.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Click vào "Import from URL" và dán link sau: [https://n8n.io/workflows/6244](https://n8n.io/workflows/6244)
3. Hoặc các sếp có thể tải file JSON về và import thủ công.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Manual Trigger**:
   - Node này dùng để kích hoạt workflow thủ công.
   - Không cần cấu hình gì thêm.

2. **List FTP Directory**:
   - Cấu hình credentials FTP với thông tin đăng nhập của các sếp.
   - Đảm bảo đường dẫn `/` là thư mục gốc cần scan.

3. **Filter Files Only**:
   - Node này lọc ra chỉ các file (không phải thư mục).
   - Có thể điều chỉnh logic lọc nếu cần.

4. **Download File from FTP**:
   - Sử dụng biến `={{ $json.path }}` để lấy đường dẫn file từ node trước.
   - Không cần cấu hình gì thêm.

5. **Upload to Google Drive**:
   - Cấu hình credentials Google Drive.
   - Chỉ định thư mục đích trên Google Drive.

6. **No Operation, do nothing**:
   - Hai node này không làm gì cả, chỉ dùng để kết nối các node khác.
   - Có thể xóa nếu không cần thiết.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, các sếp có thể test workflow bằng cách click "Execute Workflow".
2. Đảm bảo workflow chạy thành công trước khi kích hoạt.
3. Bật "Active" để workflow chạy tự động khi có file mới trên FTP.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log hoạt động của workflow để theo dõi.
- Tự động hóa báo cáo định kỳ về các file đã được chuyển.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình chuyển file từ FTP lên Google Drive, tiết kiệm thời gian và giảm thiểu lỗi. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!