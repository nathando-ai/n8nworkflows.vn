---
title: "🚀 Tự động sao lưu tệp đính kèm Gmail lên Google Drive cực nhanh với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động bắt email mới từ Gmail, trích xuất tệp đính kèm và lưu trữ an toàn vào Google Drive mà không cần tốn một phút thao tác thủ công."
slug: "tu-dong-sao-luu-tep-dinh-kem-gmail-len-google-drive"
tags: [n8n, automation, no-code, gmail, google-drive, it-ops]
keywords: [n8n workflow, tự động hóa gmail, lưu file gmail vào google drive, backup gmail attachment, n8n gmail trigger]
keywords: [n8n workflow, tự động hóa, sao lưu gmail, google drive automation, gmail to google drive]
---

# 🚀 Tự động sao lưu tệp đính kèm Gmail lên Google Drive cực nhanh với n8n

Mỗi ngày, các sếp phải nhận hàng tá email công việc chứa hóa đơn, hợp đồng, tài liệu từ đối tác và khách hàng? Việc phải tải thủ công từng tệp đính kèm (attachment) xuống máy tính rồi upload lên Google Drive vừa mất thời gian, lại rất dễ sót việc hoặc lộn xộn thư mục.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động bằng n8n workflow **"Gmail Attachment Backup to Google Drive"**. Chỉ cần có email mới đến, toàn bộ file đính kèm sẽ được cất gọn gàng vào thư mục Google Drive chỉ định!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần đụng tay tải và đẩy file thủ công.
- **Lưu trữ khoa học:** Tệp đính kèm tự động phân loại và gom về đúng thư mục Google Drive mong muốn.
- **Hoạt động 24/7:** Bắt trọn mọi email ngay khi vừa đổ về hộp thư đến (Inbox).
- **Mở rộng linh hoạt:** Dễ dàng thêm bước thông báo qua Telegram/Slack hoặc ghi log sau khi upload xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n đang hoạt động.
- Tài khoản **Gmail** (Cần cấp quyền OAuth2 để n8n đọc email).
- Tài khoản **Google Drive** (Cần cấp quyền OAuth2 để n8n tạo và lưu file).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này, sau đó dán trực tiếp vào n8n Editor của mình (hoặc import file JSON đã tải từ n8n.io/workflows/4243).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy cấu hình các node quan trọng sau đây để workflow chạy đúng ý đồ:

- **Node `Gmail Trigger`**:
  - Chọn Credentials tài khoản Gmail của các sếp.
  - **Change sender filter**: Sửa đổi bộ lọc người gửi hoặc từ khóa trong node này để chỉ quét những email thực sự cần thiết (tránh lưu rác từ email quảng cáo).
- **Node `Gmail` (get)**:
  - Dùng để lấy chi tiết nội dung email và tệp đính kèm dựa trên sự kiện kích hoạt từ Trigger.
- **Node `Google Drive`**:
  - Chọn Credentials Google Drive.
  - **Change destination folder**: Cập nhật chính xác `folderId` của thư mục trên Google Drive nơi các sếp muốn lưu trữ file.
  - **Modify filename format**: Chỉnh sửa biểu thức định dạng tên file (`name expression`) nếu muốn đổi cấu trúc tên file khi lưu (ví dụ: gắn thêm thời gian, tên người gửi...).
- **Node `Code` & `Replace Me` (noOp)**:
  - **Add post-upload logic**: Node `Replace Me` đang ở dạng chờ (NoOp). Các sếp có thể giữ nguyên, thay thế hoặc mở rộng nó bằng các node gửi thông báo qua Slack/Telegram hoặc ghi nhận dữ liệu vào Google Sheets sau khi upload thành công.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** và gửi một email mẫu có đính kèm file đến Gmail đã cấu hình để kiểm tra kết quả.
- Nếu file đã nằm ngoan ngoãn trong Google Drive, hãy gạt công tắc sang **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo:** Nối thêm node Telegram hoặc Slack sau node Google Drive để nhận thông báo ngay lập tức: *"Vừa lưu thành công file [Tên file] vào thư mục X!"*.
- **Quản lý log:** Kết nối thêm node Google Sheets để ghi lại lịch sử: Ai gửi, tên file gì, thời gian lưu lúc mấy giờ để tiện tra cứu về sau.
- **Phân loại thư mục thông minh:** Dùng node `If` trước Google Drive để lọc loại file (PDF, hình ảnh, tài liệu Word) và chuyển vào các thư mục Google Drive khác nhau.

### 📌 Kết luận
Workflow **Gmail Attachment Backup to Google Drive** là một "trợ lý ảo" cực kỳ hữu ích giúp tự động hóa khâu quản lý tài liệu đầu vào của cá nhân lẫn doanh nghiệp. Hãy thiết lập ngay hôm nay để tối ưu hóa thời gian và không bao giờ bỏ lỡ hay thất lạc tệp quan trọng nào nữa nhé các sếp!