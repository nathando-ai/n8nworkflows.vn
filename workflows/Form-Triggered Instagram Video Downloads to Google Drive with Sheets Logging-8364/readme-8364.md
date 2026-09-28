---
title: "🚀 Tự động tải video Instagram lưu Google Drive và ghi log Google Sheets với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa tải video từ Instagram thông qua Form, lưu trữ trực tiếp lên Google Drive, phân quyền chia sẻ và ghi log trạng thái thành công/thất bại vào Google Sheets."
slug: "tu-dong-tai-video-instagram-google-drive-n8n"
tags: [n8n, automation, no-code, instagram-downloader, google-drive, google-sheets]
keywords: [n8n workflow, tải video instagram tự động, google drive automation, google sheets logging, no-code automation]
---

# 🚀 Tự động hóa tải video Instagram lên Google Drive và quản lý lịch sử qua Google Sheets

Các sếp có đang gặp khó khăn khi phải thủ công copy link Instagram, tìm kiếm công cụ tải video bên ngoài, rồi lại lùi cui tải về máy và upload lên Google Drive cho team marketing hoặc lưu trữ? Việc này không chỉ tốn hàng tá thời gian mà còn cực kỳ nhàm chán khi phải xử lý số lượng lớn.

Đừng lo, bài toán này sẽ được giải quyết triệt để với **Workflow n8n** tự động 100% không cần code. Chỉ với một form nhập link đơn giản, hệ thống sẽ tự động tải video, đẩy thẳng lên Google Drive, tạo link chia sẻ công khai và tự động ghi log chi tiết vào Google Sheets (phân biệt rõ ràng cả thành công lẫn thất bại).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn thao tác thủ công copy - paste - tải về - upload.
- **Lưu trữ khoa học:** Video được gom gọn gàng vào thư mục Google Drive định sẵn với link chia sẻ công khai tự động.
- **Kiểm soát tuyệt đối:** Google Sheets tự động ghi nhận toàn bộ lịch sử chạy, phân loại rõ ràng trạng thái Thành công (`Drive_URL`) hoặc Thất bại (`N/A`).
- **Hoạt động 24/7:** Giao diện Form trực quan, sẵn sàng nhận link bất cứ lúc nào từ bất kỳ thiết bị nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt phiên bản n8n (Self-hosted hoặc Cloud).
- **Tài khoản Google:** 
  - Kết nối **Google Drive OAuth2 API** (để upload video và set quyền chia sẻ).
  - Kết nối **Google Sheets / Google API** (để ghi log dòng dữ liệu).
- **API bên thứ ba:** Endpoint của Instagram Video Downloader API (được tích hợp sẵn trong node HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy mã JSON của workflow này từ nguồn gốc hoặc kho lưu trữ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes chính hoạt động mượt mà theo 2 nhánh (Thành công và Thất bại). Các sếp cần cấu hình kỹ các điểm sau:

- **On form submission (`formTrigger`):** Node khởi đầu tạo giao diện Web Form đơn giản với trường `URL`. Các sếp có thể tuỳ chỉnh giao diện form cho đẹp mắt hơn nếu muốn.
- **Instagram Downloader API Request (`httpRequest`):** Node gửi request `POST` chứa link Instagram của người dùng lên API trung gian để lấy về đường dẫn file MP4 gốc. Cần kiểm tra kỹ Endpoint URL và Header xác thực (nếu API yêu cầu).
- **If (`if`):** Kiểm tra xem phản hồi từ API có chứa trường `error` hay không. 
  - ✅ **True Path:** Chuyển sang tải video MP4.
  - ❌ **False Path:** Chuyển sang nhánh xử lý lỗi (Wait + Sheets logging).
- **Upload To Google Drive (`googleDrive`):** Chọn Credentials Google Drive OAuth2 của các sếp và trỏ đến **Folder ID** cụ thể nơi lưu trữ video trên Drive.
- **Google Drive Set Permission (`googleDrive`):** Cấu hình thao tác (`operation: share`, `resource: file`) để tự động set quyền `Anyone with the link can view` nhằm lấy ra link xem trực tiếp (`webViewLink`).
- **Google Sheets & Google Sheets Append Row (`googleSheets`):** Kết nối tài khoản Google API, chọn đúng file Google Sheet và Sheet Name để ghi nhận dữ liệu:
  - Nhánh thành công: Lưu `URL` gốc và `Drive_URL` (link chia sẻ).
  - Nhánh thất bại: Lưu `URL` gốc kèm giá trị `N/A` cho `Drive_URL`.
- **Wait (`timer`):** Tạo độ trễ hợp lý trước khi ghi log lỗi vào Sheet, giúp tránh tình trạng spam request hoặc nghẽn API.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử bằng cách điền một link Instagram bất kỳ vào form để kiểm tra dữ liệu trả về trên Google Drive và Google Sheet.
- Nếu mọi thứ chạy mượt mà, các sếp gạt công tắc sang chế độ **Active** để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Gắn thêm node Telegram hoặc Slack ở nhánh Thành công/Thất bại để nhận thông báo ngay lập tức về điện thoại mỗi khi có video được tải xong hoặc xảy ra lỗi.
- **Tự động hóa nâng cao:** Kết hợp thêm node AI (như OpenAI / Anthropic) để tự động tạo caption hoặc tóm tắt nội dung video dựa trên metadata trước khi lưu vào Google Sheets.
- **Quản lý dung lượng Drive:** Định kỳ thiết lập workflow dọn dẹp hoặc phân loại video theo thư mục con dựa trên tên tài khoản Instagram.

### 📌 Kết luận
Tự động hóa tải video Instagram chưa bao giờ dễ dàng và mượt mà đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa thời gian, giải phóng sức lao động thủ công và tập trung vào các chiến lược sáng tạo nội dung đỉnh cao hơn cho doanh nghiệp của các sếp!