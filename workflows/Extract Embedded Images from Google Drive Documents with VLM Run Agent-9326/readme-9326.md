---
title: "🚀 Trích xuất và Lưu trữ Hình ảnh Tự động từ Google Drive với VLM Run Agent trong n8n"
description: "Tự động hóa quy trình trích xuất hình ảnh nhúng từ tài liệu PDF, báo cáo trên Google Drive bằng VLM Run AI Agent và lưu ngược lại Drive một cách mượt mà."
slug: "trich-xuat-hinh-anh-google-drive-vlm-run-n8n"
tags: [n8n, automation, google-drive, vlm-run, ai-agent, image-extraction]
keywords: [n8n workflow, trích xuất ảnh google drive, vlm run agent, tự động hóa n8n, xu ly tai lieu ai]
---

# 🚀 Trích xuất và Lưu trữ Hình ảnh Tự động từ Google Drive với VLM Run Agent

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công mở từng file PDF hay báo cáo dài dằng dặc trên Google Drive, sau đó cắt, tải từng tấm hình ảnh nhúng bên trong để lưu trữ lại không? Việc này vừa tốn thời gian, dễ bỏ sót lại vừa cực kỳ nhàm chán. 

Giải pháp hoàn hảo là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: phát hiện file mới trên Google Drive, gọi AI Agent từ **VLM Run** để bóc tách hình ảnh thông minh, rồi tự động tải về và lưu vào thư mục chỉ định mà các sếp không cần đụng tay vào bất cứ khâu thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Ngay khi có tài liệu mới tải lên Google Drive, hệ thống tự kích hoạt xử lý.
- **Sử dụng AI thông minh:** VLM Run Agent nhận diện chính xác các hình ảnh, biểu đồ, hóa đơn ẩn trong tài liệu.
- **Tổ chức khoa học:** Tự động tách từng URL hình ảnh, tải về và gom gọn gàng vào thư mục đích trên Google Drive.
- **Tiết kiệm thời gian tuyệt đối:** Giải phóng hàng giờ đồng hồ làm việc tay chân cho đội ngũ vận hành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Google Drive Account** (Cần thiết lập OAuth2 Credentials để n8n có quyền đọc, tải và lưu file).
- **Tài khoản VLM Run** và API Key đi kèm để chạy Agent trích xuất hình ảnh (`@vlm-run/n8n-nodes-vlmrun`).
- Thư mục nguồn (Watch folder) trên Google Drive để theo dõi file mới và thư mục đích (Destination folder) để lưu ảnh trích xuất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo một workflow mới và copy/paste toàn bộ mã nguồn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Monitor Uploads (`googleDriveTrigger`):** 
  - Chọn Credentials Google Drive OAuth2.
  - Thiết lập thư mục nguồn cần theo dõi sự kiện file mới (`fileCreated`).
- **Download File (`googleDrive`):** 
  - Sử dụng chung Credentials Google Drive. Cấu hình operation là `download` để lấy file nhị phân từ ID do trigger truyền sang.
- **Extract Images (`@vlm-run/n8n-nodes-vlmrun.vlmRun`):**
  - Nhập thông tin `vlmRunApi` credentials.
  - Cấu hình Agent với prompt yêu cầu trích xuất hình ảnh.
  - Điền Webhook URL của n8n vào phần Callback URL trên hệ thống VLM Run để nhận dữ liệu trả về.
- **Receive Image Links (`webhook`):**
  - Đảm bảo đường dẫn path là `image-extract-via-agent` với phương thức `POST` để hứng dữ liệu kết quả từ VLM Run.
- **Split Out (`splitOut` & Download/Save):**
  - Node này sẽ tách mảng `body.response.extracted_images` thành từng đường dẫn riêng lẻ.
  - Node **Download Image (`httpRequest`)** sẽ tải file hình ảnh về.
  - Node **Save Image (`googleDrive`)** sẽ lưu các file ảnh này vào thư mục **Extracted Image** đã chuẩn bị sẵn trên Google Drive.

#### 3. Kích hoạt ⚡️
- Thực hiện một lượt Test Run thủ công bằng cách upload thử một file PDF có hình ảnh lên thư mục Google Drive được giám sát.
- Kiểm tra dữ liệu chạy qua từng node trên n8n để đảm bảo không có lỗi kết nối API.
- Bật công tắc **Active** để workflow chính thức vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo kèm số lượng ảnh đã trích xuất thành công về group chat cho team.
- **Quản lý Log:** Lưu lại lịch sử xử lý vào Google Sheets để dễ dàng tra cứu khi cần.
- **Xử lý linh hoạt định dạng:** Có thể mở rộng prompt trong VLM Run Agent để phân loại hình ảnh theo chủ đề (như hóa đơn, biểu đồ, ảnh minh họa) trước khi lưu vào các thư mục con tương ứng trên Google Drive.

### 📌 Kết luận
Quy trình trích xuất hình ảnh từ tài liệu bằng AI nay đã trở nên vô cùng đơn giản với sự kết hợp giữa Google Drive và VLM Run Agent trong n8n. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất làm việc ngay hôm nay!