---
title: "🚀 Tự động gộp nhiều file PDF chuyên nghiệp trong n8n với CustomJS API"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tải, gộp và lưu trữ nhiều file PDF thành một file hoàn chỉnh bằng n8n workflow và CustomJS API."
slug: "gop-nhieu-file-pdf-tu-dong-voi-customjs-api-trong-n8n"
tags: [n8n, automation, pdf-toolkit, customjs, file-management]
keywords: [n8n workflow, gộp file pdf, merge pdf n8n, customjs api, tự động hóa file]
keywords: [n8n workflow, gộp file pdf, merge pdf n8n, customjs api, tự động hóa file]
---

# 🚀 Tự động gộp nhiều file PDF chuyên nghiệp trong n8n với CustomJS API

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công tải về hàng loạt báo cáo, hóa đơn hay tài liệu dạng PDF từ các nguồn khác nhau, rồi lại dùng các công cụ online không bảo mật để gộp chúng lại thành một file duy nhất? Quy trình thủ công này vừa tốn thời gian, dễ nhầm lẫn, lại vừa tiềm ẩn rủi ro lộ lọt dữ liệu nhạy cảm của doanh nghiệp.

Giải pháp ở đây là gì? Hãy để n8n thay bạn làm tất cả! Với workflow **Merge Multiple PDF Files with CustomJS API**, các sếp có thể tự động tải các file PDF từ các nguồn, gộp chúng lại một cách mượt mà và lưu trữ ngay lập tức mà không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn cảnh kéo thả thủ công từng file PDF qua các trang web bên thứ ba.
- **Bảo mật tuyệt đối:** Toàn bộ dữ liệu file được xử lý trực tiếp trên hệ thống n8n tự host của doanh nghiệp.
- **Linh hoạt mở rộng:** Dễ dàng kết nối nguồn file đầu vào từ HTTP, Google Drive, Email hoặc bất kỳ API nào.
- **Hoạt động tự động 24/7:** Chạy ngầm mượt mà theo lịch trình hoặc kích hoạt theo sự kiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (khuyên dùng bản Self-hosted).
- Tài khoản và thông tin xác thực **CustomJS API credentials** (cho node `Merge PDF1`).
- Các đường dẫn URL chứa file PDF nguồn (hoặc cấu hình các node HTTP Request tương ứng).
- Quyền truy cập đọc/ghi file trên hệ thống ổ đĩa của n8n (cho các node `Read/Write Files from Disk`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ JSON workflow từ n8n.io/workflows/3873).
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **HTTP Request & HTTP Request2:** Cấu hình đường dẫn URL chính xác của các file PDF cần tải xuống từ internet hoặc hệ thống khác.
- **Merge:** Dùng để gom dữ liệu nhị phân (binary data) của các file PDF lại với nhau trước khi tiến hành gộp.
- **Merge PDF1 (`@custom-js/n8n-nodes-pdf-toolkit.mergePdfs`):** Node quan trọng nhất thực hiện việc gộp file. Các sếp bắt buộc phải điền **CustomJS API Credentials** hợp lệ để node này có thể hoạt động.
- **Read/Write Files from Disk & Read/Write Files from Disk4:** Cấu hình thư mục lưu trữ (`File Path`) trên ổ đĩa của server n8n để đọc file đầu vào và ghi file PDF sau khi đã gộp thành công.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** (bắt đầu từ node `When clicking ‘Test workflow’`) để kiểm tra toàn bộ luồng chạy xem có lỗi phát sinh không.
- Kiểm tra thư mục đích trên ổ đĩa xem file PDF gộp đã xuất hiện chưa.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để nhận thông báo kèm file PDF vừa gộp hoặc link tải ngay khi hoàn tất.
- **Tự động hóa theo lịch:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để tự động gộp báo cáo hàng ngày/hàng tuần.
- **Lưu trữ đám mây:** Thay vì lưu trên ổ đĩa VPS, có thể dùng node Google Drive hoặc OneDrive để tự động upload file PDF đã gộp lên đám mây cho team cùng xem.

### 📌 Kết luận
Workflow **Merge Multiple PDF Files with CustomJS API** là một mảnh ghép tuyệt vời giúp tối ưu hóa các tác vụ xử lý tài liệu file cứng/file mềm trong doanh nghiệp. Hãy cài đặt ngay hôm nay để giải phóng sức lao động khỏi những công việc lặp đi lặp lại nhé các sếp!