---
title: "🚀 Tự động tải nhiều tệp đính kèm từ Gmail lên Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt email mới có tệp đính kèm từ Gmail và lưu trữ toàn bộ file vào Google Drive một cách mượt mà, không cần code."
slug: "tu-dong-tai-tep-dinh-kem-gmail-len-google-drive-n8n"
tags: [n8n, automation, no-code, gmail, google-drive, building-blocks]
keywords: [n8n workflow, tải tệp đính kèm gmail, tự động hóa gmail google drive, n8n gmail trigger, google drive upload n8n]
---

# 🚀 Tự động tải nhiều tệp đính kèm từ Gmail lên Google Drive

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi nhận được email có hàng loạt tệp đính kèm (hóa đơn, hợp đồng, báo cáo,...) từ khách hàng hay đối tác, rồi lại phải lọ mọ tải từng file về máy tính và thủ công upload lên Google Drive? Việc này không chỉ tốn thời gian mà còn rất dễ bỏ sót file quan trọng.

Giải pháp ở đây là gì? Hãy để n8n lo! Workflow tự động hóa này sẽ giúp các sếp gom trọn toàn bộ tệp đính kèm từ mỗi email mới đến và đẩy thẳng lên Google Drive chỉ trong một nốt nhạc, hoạt động 24/7 hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối**: Không còn cảnh tải xuống và tải lên thủ công từng file đính kèm rườm rà.
- **Không bao giờ bỏ lỡ file**: Mọi tệp đính kèm từ email mới đều được quét và xử lý chính xác 100%.
- **Lưu trữ khoa học**: Đồng bộ hóa toàn bộ tài liệu từ email vào đúng thư mục Google Drive chỉ định.
- **Vận hành tự động 24/7**: Hệ thống tự chạy ngầm, các sếp chỉ việc nhận báo cáo kết quả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** có quyền truy cập qua API (để cấu hình Trigger).
- **Tài khoản Google Drive** để lưu trữ các tệp đính kèm được tải lên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON từ template gốc hoặc dùng file JSON của workflow này để paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 node chính cực kỳ tinh gọn, các sếp cần cấu hình chuẩn xác các thông số sau:

- **Node `Trigger - New Email` (Gmail Trigger):**
  - Kết nối tài khoản Gmail của các sếp bằng **OAuth2**.
  - Thiết lập điều kiện lọc email (ví dụ: chỉ bắt email có tệp đính kèm `Has Attachment: True` hoặc lọc theo nhãn/thư mục cụ thể) để tối ưu hóa hiệu suất.

- **Node `attach binary data outputs` (Function):**
  - Node này sử dụng mã JavaScript để xử lý và định dạng lại các tệp đính kèm nhị phân (binary data) từ email, đảm bảo n8n có thể nhận diện và tách từng file một cách chính xác khi một email chứa nhiều tệp đính kèm cùng lúc. Các sếp có thể giữ nguyên mã nguồn trong function node này.

- **Node `upload files to google drive` (Google Drive):**
  - Kết nối tài khoản Google Drive bằng **OAuth2**.
  - Chọn thao tác (Operation): **Upload**.
  - Chỉ định thư mục đích (Parent Folder ID) trên Google Drive nơi các sếp muốn lưu trữ các file tải lên.
  - Map trường dữ liệu binary từ node trước vào phần nội dung file để tiến hành upload.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để thử nghiệm với một email mẫu có sẵn tệp đính kèm trong hộp thư.
- Kiểm tra lại trên Google Drive xem file đã được đẩy lên đúng thư mục chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow "xịn xò" hơn nữa, các sếp có thể mở rộng thêm các tính năng sau:
- **Gửi thông báo Telegram/Slack**: Thêm node thông báo mỗi khi có bộ tệp đính kèm mới được upload thành công kèm theo tên file và link Google Drive.
- **Phân loại thư mục thông minh**: Dùng thêm các node điều kiện (If/Switch) để phân chia file vào các thư mục Google Drive khác nhau dựa trên tiêu đề email hoặc định dạng file (`.pdf`, `.xlsx`, `.jpg`,...).
- **Ghi log vào Google Sheets**: Lưu lại lịch sử ai đã gửi email, thời gian nhận và tên file đã lưu để dễ tra cứu về sau.

### 📌 Kết luận
Chỉ với 3 node đơn giản trong n8n, bài toán quản lý và lưu trữ tệp đính kèm từ Gmail đã được giải quyết triệt để. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình làm việc và giải phóng thời gian cho những công việc quan trọng hơn các sếp nhé!