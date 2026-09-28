---
title: "🚀 Tự động lập chỉ mục file Google Drive vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét thư mục Google Drive, lọc file mới và cập nhật vào Google Sheets không lo trùng lặp."
slug: "tu-dong-lap-chi-muc-google-drive-vao-google-sheets-bang-n8n"
tags: [n8n, automation, no-code, google-drive, google-sheets, file-management]
keywords: [n8n workflow, tự động hóa google drive, lưu file drive vào sheets, quản lý file n8n, google drive to google sheets]
---

# 🚀 Tự động lập chỉ mục file Google Drive vào Google Sheets

Các sếp có đang đau đầu mỗi khi phải quản lý hàng trăm, hàng ngàn file tài liệu nằm rải rác trong các thư mục Google Drive? Việc kiểm tra thủ công xem file nào mới được thêm vào, file nào chưa được ghi nhận vào danh sách quản lý chung tốn rất nhiều thời gian và dễ xảy ra sai sót. 

Giải pháp ở đây chính là workflow n8n tự động hóa 100%: Quét sạch thư mục Google Drive, đối chiếu với danh sách hiện có và tự động "bơm" các file mới tinh vào Google Sheets mà không lo bị trùng lặp (duplicate).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy/paste tên file hay link thủ công vào bảng quản lý.
- **Không bao giờ trùng lặp:** Hệ thống tự động thông minh đối chiếu file cũ/mới, chỉ thêm những file hoàn toàn mới.
- **Dữ liệu đồng bộ, chuẩn chỉnh:** Tự động ghi lại Tên file, Loại file (MIME Type), Định dạng, Link Google Drive, File ID và Thời gian lập chỉ mục chính xác tới từng giây.
- **Hoạt động linh hoạt:** Có thể chạy thủ công theo ý muốn hoặc cấu hình lịch trình tự động quét định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- **Google Drive OAuth2 Credentials** để n8n có quyền đọc dữ liệu thư mục.
- **Google Sheets OAuth2 Credentials** để n8n ghi dữ liệu vào bảng tính.
- Một Google Sheet chuẩn bị sẵn với hàng tiêu đề (Row 1): `File Name`, `MIME Type`, `File Extension`, `Google Drive URL`, `File ID`, `Indexed At`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình là xong phần khung xương.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được thiết kế cực kỳ gọn gàng với **Node Config** là trung tâm điều khiển. Các sếp chỉ cần tập trung cấu hình tại đây và một vài node chính sau:
- **Node `Config` (Set):** Điền chính xác 3 tham số quan trọng gồm: ID thư mục Google Drive mục tiêu (`Folder ID`), ID của bảng Google Sheets (`Spreadsheet ID`), và tên tab chứa dữ liệu (mặc định là `Sheet1`).
- **Node `List files and folders` (Google Drive):** Kết nối tài khoản Google Drive OAuth2 của các sếp.
- **Node `Get Existing Index Rows` & `Append Row to Index Sheet` (Google Sheets):** Kết nối tài khoản Google Sheets OAuth2 và trỏ đúng đến file Google Sheet quản lý index.
- **Các node xử lý trung gian (`Filter Already Indexed Files`, `Prepare Index Row`, `Merge`):** Đã được lập trình sẵn logic code tối ưu, các sếp không cần can thiệp sâu trừ khi muốn tùy biến thêm cột dữ liệu.

#### 3. Kích hoạt ⚡️
- Bấm nút **`When clicking ‘Execute workflow’` (Manual Trigger)** để chạy thử nghiệm lần đầu (Test Run).
- Kiểm tra xem dữ liệu trong Google Sheets đã được đổ về đầy đủ và chuẩn xác chưa.
- Gạt công tắc **Active** góc trên cùng bên phải để bật workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này theo nhu cầu thực tế của doanh nghiệp, các sếp có thể áp dụng ngay các mẹo sau:
- **Tự động hóa theo lịch:** Thay thế node `Manual Trigger` bằng node `Schedule Trigger` để n8n tự động quét file mới mỗi giờ, mỗi ngày hoặc mỗi tuần.
- **Bắn thông báo về Slack/Telegram:** Thêm một node Telegram hoặc Slack ngay sau node `Append Row to Index Sheet` để gửi thông báo sếp biết ngay khi có nhân sự tải tài liệu mới lên Drive.
- **Lọc theo loại file:** Thêm một node `Filter` để chỉ định chỉ index các file có định dạng cụ thể (ví dụ: chỉ nhận file PDF hoặc Google Docs, bỏ qua hình ảnh/video).
- **Chia mẻ xử lý (Batching):** Với các thư mục chứa hàng nghìn file, hãy thêm node `Limit` để xử lý ngầm theo từng đợt, tránh quá tải timeout.

### 📌 Kết luận
Việc tự động hóa lập chỉ mục Google Drive vào Google Sheets giúp các sếp giải phóng hoàn toàn sức lao động chân tay, quản lý tài nguyên số khoa học và minh bạch hơn. Hãy áp dụng ngay vào hệ thống của mình nhé! Chúc các sếp thao tác thành công!