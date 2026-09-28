---
title: "🚀 Tự động giám sát và tải xuống file thay đổi trên Google Drive"
description: "Hướng dẫn thiết lập workflow n8n tự động phát hiện, tải xuống các file mới hoặc được cập nhật trên Google Drive dựa trên file mốc thời gian (timestamp)."
slug: "tu-dong-giam-sat-tai-xuong-file-google-drive"
tags: [n8n, automation, google-drive, file-management, no-code]
keywords: [n8n workflow, tự động hóa google drive, quản lý file n8n, tải file google drive tự động, n8n google drive oauth2]
---

# 🚀 Tự động giám sát và tải xuống file thay đổi trên Google Drive

Việc kiểm tra thủ công các thư mục Google Drive để tìm kiếm tài liệu mới hoặc các file vừa được chỉnh sửa là một công việc tẻ nhạt, mất thời gian và rất dễ bỏ sót. Đặc biệt khi bạn cần đồng bộ dữ liệu định kỳ cho các hệ thống khác.

Workflow này sinh ra để giải quyết triệt để vấn đề đó. Nó hoạt động như một "thư ký" tự động 24/7, tự động quét Google Drive, phát hiện các file mới hoặc có thay đổi kể từ lần chạy cuối cùng, tiến hành tải về và cập nhật mốc thời gian mà không cần sự can thiệp thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Định kỳ kiểm tra file mới/thay đổi trên Google Drive mà không cần click chuột thủ công.
- **Thông minh với Timestamp:** Sử dụng file `n8n_last_run.txt` để ghi nhớ thời điểm chạy gần nhất, tránh tải lại các file cũ gây trùng lặp.
- **Xử lý linh hoạt:** Tự động fallback về mốc 24 giờ trước nếu đây là lần chạy đầu tiên (chưa có file timestamp).
- **Vận hành liên tục:** Đảm bảo dữ liệu luôn được đồng bộ và sẵn sàng phục vụ các bước xử lý tiếp theo trong chuỗi automation của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Self-hosted hoặc n8n Cloud).
- **Tài khoản Google:** Cần có quyền truy cập Google Drive.
- **Google Drive OAuth2 API Credentials:** Để n8n có thể đọc, ghi, tải xuống và xóa file trên tài khoản Drive của bạn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ trang nguồn.
- Mở giao diện n8n Editor, nhấn vào nút **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các điểm sau:

- **Google Drive Nodes (`Search for Timestamp File1`, `Download Timestamp File1`, `Download New Files2`, `Upload New Timestamp2`, `Search for New Files2`, `Delete Old Timestamp File1`):**
  - Tất cả các node này đều yêu cầu cấu hình **Credentials**. Hãy chọn hoặc tạo mới kết nối `Google Drive OAuth2 API`.
  - Tại các node tìm kiếm/tải file (`Search for Timestamp File1`, `Search for New Files2`), các sếp cần cấu hình **Folder ID** (thư mục đích trên Google Drive mà n8n sẽ theo dõi).

- **Cơ chế hoạt động của Timestamp:**
  - Workflow sẽ tìm file có tên `n8n_last_run.txt` trên Google Drive.
  - Nếu file này chưa tồn tại (chạy lần đầu), hệ thống sẽ tự động mặc định quét các file thay đổi trong vòng 24 giờ qua.
  - Sau khi hoàn tất, workflow sẽ tự động xóa file timestamp cũ (`Delete Old Timestamp File1`), tạo nội dung thời gian mới (`Create Timestamp File`) và tải lên lại (`Upload New Timestamp2`) để chuẩn bị cho lần chạy tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử nghiệm thủ công với một vài file mẫu để kiểm tra kết nối Google Drive.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch của `Schedule Trigger1`.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Nối thêm node Telegram hoặc Slack ngay sau bước tải file thành công để nhận ngay thông báo khi có tài liệu mới được thêm vào Drive.
- **Lưu trữ vào Database:** Thay vì chỉ tải xuống Google Drive, các sếp có thể đẩy thông tin file mới vào Google Sheets, Notion hoặc Airtable để quản lý tập trung.
- **Xử lý file chuyên sâu:** Kết hợp các node AI (như OpenAI) để tự động đọc nội dung file vừa tải về, tóm tắt và phân loại tài liệu.

### 📌 Kết luận
Workflow giám sát và tải file Google Drive tự động này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình quản lý tài liệu, loại bỏ thao tác thủ công rườm rà. Hãy áp dụng ngay vào hệ thống của các sếp để tiết kiệm hàng giờ làm việc mỗi tuần!