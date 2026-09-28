---
title: "🚀 Tự động hóa Upload Nhiều File Đính Kèm từ Gmail lên Google Drive - Không Cần Code"
description: "Hướng dẫn chi tiết cách tự động hóa việc upload nhiều file đính kèm từ Gmail lên Google Drive bằng n8n, tiết kiệm thời gian và công sức cho các sếp quản lý dữ liệu."
slug: "tu-dong-hoa-upload-nhieu-file-gmail-len-google-drive"
tags: [n8n, automation, no-code, google-drive, gmail]
keywords: [n8n workflow, tự động hóa, google drive, gmail, upload file]
---

# 🚀 Tự động hóa Upload Nhiều File Đính Kèm từ Gmail lên Google Drive - Không Cần Code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải đối mặt với tình trạng phải tải tay từng file đính kèm từ email lên Google Drive, đặc biệt là khi nhận được nhiều email cùng lúc. Việc này không chỉ tốn thời gian mà còn dễ gây lỗi và mất tập trung. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi tự động hóa việc tải file từ Gmail lên Google Drive.
- Giảm thiểu lỗi do thao tác thủ công.
- Tự động xử lý các file đính kèm lớn và bỏ qua các file nhỏ như biểu tượng.
- Hoạt động liên tục 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ.
- Tài khoản Google Drive với quyền truy cập đầy đủ.
- API keys hoặc credentials cho Gmail và Google Drive.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/2966`.
4. Nhấn "OK" để hoàn tất quá trình import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Gmail Trigger**:
   - Chọn credentials cho Gmail OAuth2.
   - Cấu hình các tham số như folder, label, hoặc từ khóa để lọc email.

2. **Google Drive**:
   - Chọn credentials cho Google Drive OAuth2 API.
   - Cấu hình thư mục đích trên Google Drive để lưu file.

3. **Split Out**:
   - Không cần cấu hình gì thêm, node này sẽ tự động tách các file đính kèm thành các item riêng biệt.

4. **Switch**:
   - Cấu hình điều kiện để xử lý các file đính kèm lớn và bỏ qua các file nhỏ.
   - Ví dụ: `{{ $binary.size > 1000000 }}` để xử lý các file lớn hơn 1MB.

5. **Send "Too Big" Notification (for example)**:
   - Cấu hình thông báo khi file quá lớn (ví dụ: gửi email hoặc thông báo trên Slack).

6. **Ignore Little Graphics / Icons (for example)**:
   - Cấu hình để bỏ qua các file nhỏ như biểu tượng.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi có file mới được tải lên.
- Lưu log các file đã tải lên để theo dõi và quản lý.
- Gửi báo cáo định kỳ về các file đã tải lên để kiểm tra và quản lý.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình tải file từ Gmail lên Google Drive một cách dễ dàng và hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và công sức cho các công việc quản lý dữ liệu hàng ngày.