---
title: "🚀 Tự động trích xuất tài liệu và phân tích tổ chức với Foxit & Diffbot trên n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa quy trình xử lý tài liệu PDF mới từ Google Drive, trích xuất văn bản bằng Foxit API, phân tích thực thể qua Diffbot và gửi báo cáo qua Gmail."
slug: "tu-dong-trich-xuat-tai-lieu-foxit-diffbot-n8n"
tags: [n8n, automation, no-code, foxit, diffbot, google-drive, gmail]
keywords: [n8n workflow, trích xuất tài liệu pdf, foxit api, diffbot n8n, tự động hóa google drive gmail, trích xuất tổ chức]
---

# 🚀 Tự động trích xuất tài liệu và phân tích tổ chức với Foxit & Diffbot

Các sếp có bao giờ cảm thấy ngợp thở khi mỗi ngày có hàng tá tài liệu, hợp đồng, hay báo cáo PDF đổ về Google Drive nhưng lại phải mất hàng giờ để đọc, bóc tách thông tin các tổ chức/doanh nghiệp liên quan và tổng hợp nội dung thủ công? 

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ mạnh mẽ do chuyên gia **Raymond Camden** thiết kế. Workflow này sẽ tự động hóa từ A-Z: nhận tài liệu mới, đẩy lên **Foxit API** để trích xuất văn bản (xử lý bất đồng bộ thông minh qua vòng lặp), gọi **Diffbot API** để phân tích và tóm tắt thực thể, sau đó tự động định dạng và gửi email báo cáo chi tiết qua **Gmail**. Tất cả diễn ra tự động 100% không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận diện file PDF mới ngay lập tức mà không cần kiểm tra thủ công.
- **Trích xuất thông minh:** Ứng dụng Foxit API xử lý các tài liệu nặng, phức tạp và Diffbot phân tích sâu các tổ chức, thực thể có trong văn bản.
- **Tiết kiệm 90% thời gian:** Không còn cảnh đọc thủ công từng trang tài liệu để tổng hợp thông tin.
- **Báo cáo chuyên nghiệp:** Kết quả được định dạng HTML sạch sẽ và gửi thẳng tới hòm thư Gmail của các sếp hoặc đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Drive & Gmail** (kết nối qua OAuth2).
- **Foxit API Account & Credentials** (để upload và trích xuất văn bản).
- **Diffbot API Key** (để phân tích thực thể và tóm tắt nội dung).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n.io workflows 6286](https://n8n.io/workflows/6286), sau đó copy toàn bộ mã nguồn JSON và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes được chia thành 4 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Giai đoạn Ingestion (Nhập liệu):**
  - **Fire on New File in Google Drive Folder (`googleDriveTrigger`):** Chọn tài khoản Google Drive OAuth2 và trỏ tới thư mục (`Folder`) cụ thể nơi các sếp sẽ upload các file tài liệu PDF cần xử lý.
  - **Download File (`googleDrive`):** Cấu hình lấy file vừa kích hoạt trigger để tải nội dung xuống n8n.

- **G giai đoạn Uploading and Extracting (Trích xuất văn bản với Foxit):**
  - **Upload to Foxit, Kick off Foxit Extract, Check Task, Download Extracted Text (`httpRequest`):** Các node này sử dụng `httpCustomAuth` để kết nối với Foxit API. Các sếp cần điền Endpoint API chính xác của Foxit theo tài liệu nhà phát triển của họ.
  - **Is the job done? (`if`) & Wait (`wait`):** Do quá trình trích xuất của Foxit diễn ra bất đồng bộ (async), workflow sử dụng vòng lặp kiểm tra trạng thái (`Check Task`) kết hợp node `Wait` để chờ đến khi tác vụ hoàn thành.

- **Giai đoạn Analyzing (Phân tích với Diffbot):**
  - **Get Diffbot Entities (`httpRequest`):** Sử dụng `httpQueryAuth` với Diffbot API Key để gửi văn bản đã trích xuất từ Foxit sang Diffbot, yêu cầu hệ thống phân tích và tóm tắt các tổ chức (Organizations) và nội dung chính.

- **G giai đoạn Shaping and Emailing (Định dạng & Gửi email):**
  - **Shape Data & Make Email Contents (`code`):** Các node JavaScript này nhận dữ liệu thô từ Diffbot, xử lý và tạo chuỗi HTML hoàn chỉnh để làm nội dung email.
  - **Gmail (`gmail`):** Kết nối tài khoản Gmail qua `gmailOAuth2`, cấu hình người nhận (To), tiêu đề (Subject) và sử dụng biến HTML từ bước trước để gửi email.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử upload một file PDF mẫu lên thư mục Google Drive đã cấu hình để test run.
- Kiểm tra kết quả trả về ở các node và hòm thư Gmail xem email đã được gửi thành công chưa.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để workflow hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để bắn thông tin tóm tắt lên nhóm chat nội bộ ngay khi có tài liệu mới.
- **Lưu lịch sử:** Thêm một node **Google Sheets** hoặc **Airtable** trước bước gửi email để lưu lại log tên file, thời gian xử lý và danh sách các tổ chức được trích xuất.
- **Tùy biến Prompt/Query:** Tinh chỉnh lại tham số gửi sang Diffbot trong node `Get Diffbot Entities` để tập trung khai thác các dữ liệu cụ thể theo nhu cầu ngành nghề của doanh nghiệp (như tài chính, pháp lý, nhân sự...).

### 📌 Kết luận
Tự động hóa quy trình phân tích tài liệu với sự kết hợp giữa Google Drive, Foxit API, Diffbot và Gmail sẽ giúp các sếp giải phóng hoàn toàn sức lao động thủ công, nắm bắt thông tin cốt lõi từ tài liệu nhanh như chớp. Chúc các sếp cài đặt thành công và hẹn gặp lại ở các bài hướng dẫn automation tiếp theo!