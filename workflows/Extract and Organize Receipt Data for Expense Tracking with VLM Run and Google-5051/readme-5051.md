---
title: "🚀 Tự Động Trích Xuất Hóa Đơn và Quản Lý Chi Phí với n8n, VLM Run và Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi Google Drive, trích xuất thông tin hóa đơn bằng AI VLM Run và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-trich-xuat-hoa-don-quan-ly-chi-phi-n8n"
tags: [n8n, automation, no-code, finance, google-drive, google-sheets, ai]
keywords: [n8n workflow, tự động hóa chi phí, trích xuất hóa đơn AI, VLM Run, Google Sheets automation]
---

# 🚀 Tự Động Trích Xuất Hóa Đơn và Quản Lý Chi Phí với n8n, VLM Run và Google Drive

Việc nhập liệu hóa đơn, chứng từ thủ công để làm báo cáo tài chính hay quản lý chi phí cá nhân luôn là "cơn ác mộng" tốn nhiều thời gian và dễ xảy ra sai sót. Các sếp có từng nghĩ đến việc chỉ cần chụp ảnh hóa đơn, vứt vào một thư mục trên Google Drive là toàn bộ thông tin quan trọng (tên cửa hàng, tổng tiền, loại tiền tệ, ngày giao dịch) tự động nhảy gọn gàng vào bảng tính Google Sheets chưa?

Workflow này do kỹ sư phần mềm **Shahrear** xây dựng sẽ giải quyết triệt để bài toán trên bằng cách kết hợp sức mạnh của tự động hóa n8n và AI thị giác máy tính (**VLM Run**). Hoàn toàn tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải gõ tay từng con số từ hóa đơn vào Excel.
- **Chính xác cao:** AI VLM Run tự động đọc hiểu cả hóa đơn chụp bằng điện thoại di động lẫn file PDF scan mờ.
- **Đồng bộ thời gian thực:** Dữ liệu chi phí được ghi nhận ngay lập tức vào Google Sheets ngay khi vừa tải ảnh lên Drive.
- **Hoạt động 24/7:** Quản lý toàn bộ chi phí kinh doanh, đi lại hoặc tài chính cá nhân một cách tự động và chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
2. **Google Drive & Google Sheets:** Tài khoản Google để cấu hình OAuth2 Credentials.
3. **VLM Run API:** Tài khoản và API Key từ VLM Run (hỗ trợ package `@vlm-run/n8n-nodes-vlmrun`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã JSON của workflow từ link gốc hoặc tạo mới bằng cách sắp xếp 5 nodes theo đúng cấu trúc dưới đây:
- `Monitor Receipt Uploads` (Google Drive Trigger)
- `Download Receipt File` (Google Drive)
- `VLM Run Receipt Parser` (VLM Run Custom Node)
- `Format Receipt Data` (Set)
- `Save to Expense Database` (Google Sheets)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **Monitor Receipt Uploads (`googleDriveTrigger`):**
  - Kết nối `googleDriveOAuth2Api`.
  - Chọn thư mục trên Google Drive mà các sếp muốn dùng làm nơi nhận ảnh/PDF hóa đơn (ví dụ: thư mục "Receipts").
- **Download Receipt File (`googleDrive`):**
  - Operation chọn `download`. Node này sẽ lấy file từ sự kiện trigger ở trên để chuyển sang bước AI xử lý.
- **VLM Run Receipt Parser (`@vlm-run/n8n-nodes-vlmrun.vlmRun`):**
  - Cấu hình `vlmRunApi` bằng API Key của các sếp.
  - Node này sẽ tự động trích xuất các trường dữ liệu như: Tên cửa hàng (Merchant), Thông tin khách hàng, Tổng tiền (Amount), Loại tiền tệ (Currency), và Ngày giao dịch (Transaction date).
- **Format Receipt Data (`set`):**
  - Chuẩn hóa lại các trường dữ liệu nhận được từ AI trước khi đẩy vào Google Sheets, giúp bảng tính sạch sẽ, đúng định dạng.
- **Save to Expense Database (`googleSheets`):**
  - Kết nối `googleSheetsOAuth2Api`.
  - Chọn file Spreadsheet quản lý chi phí và chọn Sheet Name tương ứng.
  - Mapping các cột dữ liệu đã format vào đúng các cột trong bảng tính (Tên khách hàng, Tên cửa hàng, Số tiền, Ngày giao dịch...).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử tải lên một vài tấm ảnh hóa đơn mẫu vào thư mục Google Drive để test.
- Kiểm tra xem dữ liệu đã được bóc tách và đổ về Google Sheets chuẩn xác chưa.
- Gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Telegram** hoặc **Slack** ở cuối workflow để gửi thông báo chi phí mới vừa được ghi nhận kèm số tiền và tên cửa hàng về điện thoại ngay lập tức.
- **Quản lý danh mục chi phí:** Có thể bổ sung thêm một bước AI phân loại (như: Ăn uống, Di chuyển, Thiết bị văn phòng...) để báo cáo chi phí trực quan hơn.
- **Tạo bảng Dashboard:** Kết hợp Google Sheets với Looker Studio để vẽ biểu đồ chi phí tự động theo tháng/quý.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn không chỉ giúp tiết kiệm thời gian mà còn giúp doanh nghiệp kiểm soát tài chính minh bạch, nhanh chóng. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa năng suất làm việc!