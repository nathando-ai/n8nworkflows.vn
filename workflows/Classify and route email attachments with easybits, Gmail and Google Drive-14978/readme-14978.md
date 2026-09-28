---
title: "📂 Tự Động Phân Loại & Lưu File Gmail Vào Google Drive Với AI (Easybits)"
description: "Workflow n8n thông minh giúp tự động trích xuất dữ liệu từ file đính kèm, phân loại bằng AI và lưu trữ có hệ thống vào Google Drive, đồng thời báo cáo qua Slack."
slug: "tu-dong-phan-loai-luu-file-gmail-google-drive"
tags: [n8n, automation, no-code, gmail, google-drive, ai-extraction]
keywords: [n8n workflow, tự động hóa email, trích xuất dữ liệu file, google drive automation, easybits]
---

# 📂 Tự Động Phân Loại & Lưu File Gmail Vào Google Drive Với AI (Easybits)

Trong môi trường làm việc hiện đại, email không chỉ là kênh giao tiếp mà còn là "kho dữ liệu" khổng lồ. Các sếp thường xuyên nhận được hàng chục, thậm chí hàng trăm file đính kèm (hóa đơn, hợp đồng, báo cáo, hình ảnh...) mỗi ngày. Việc phải mở từng file, đọc nội dung, quyết định lưu vào thư mục nào trên Google Drive và sau đó thông báo cho team là một quy trình thủ công, tốn thời gian và dễ gây sai sót.

Workflow này chính là giải pháp "chốt hạ" cho bài toán đó. Sử dụng sức mạnh của **Easybits** (công cụ trích xuất dữ liệu từ file) kết hợp với **Gmail**, **Google Drive** và **Google Sheets**, quy trình này sẽ tự động nhận file, "đọc" nội dung bên trong, phân loại chúng một cách thông minh và lưu trữ đúng chỗ. Các sếp chỉ cần ngồi yên và xem kết quả được báo cáo qua Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý file lớn hoặc tần suất email cao, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian xử lý file đính kèm:** Không cần mở file, không cần copy-paste, không cần tạo thư mục thủ công.
- **Lưu trữ có hệ thống:** File được tự động phân loại và lưu vào các thư mục con cụ thể trên Google Drive dựa trên nội dung (ví dụ: Hóa đơn, Hợp đồng, Ảnh...).
- **Dữ liệu hóa thông tin:** Trích xuất các trường dữ liệu quan trọng (ngày, số tiền, tên khách hàng...) từ file và lưu vào Google Sheets để dễ dàng phân tích.
- **Thông báo tức thì:** Team nhận được thông báo qua Slack khi có file quan trọng được xử lý, kèm link truy cập nhanh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail:** Đã kết nối với n8n (OAuth2).
2. **Tài khoản Google Drive:** Đã kết nối với n8n (OAuth2).
3. **Tài khoản Google Sheets:** Đã kết nối với n8n (OAuth2).
4. **Tài khoản Slack:** Đã kết nối với n8n (OAuth2 hoặc Webhook).
5. **Tài khoản Easybits:** API Key để sử dụng node `easybitsExtractor` (dùng để trích xuất dữ liệu từ PDF, Word, Excel, Image...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/14978) hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from Clipboard**.
3. Dán JSON vào và nhấn **Import**. Workflow sẽ hiện ra với đầy đủ các node.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng cần cấu hình lại cho phù hợp với hệ thống của các sếp:

*   **Node: Gmail Trigger**
    *   Chọn **Credentials** Gmail của các sếp.
    *   Trong phần **Options**, chọn **Trigger on**: `New Message` (hoặc `New Message with Attachment` nếu muốn lọc chỉ file đính kèm).
    *   Cấu hình **Filter**: Có thể đặt điều kiện để chỉ xử lý email từ các địa chỉ cụ thể hoặc có subject chứa từ khóa nhất định.

*   **Node: Easybits Extractor**
    *   Đây là "trái tim" của workflow. Chọn **Credentials** Easybits.
    *   **Input Data**: Đảm bảo node này nhận được binary data (file đính kèm) từ node Gmail trước đó.
    *   **Extraction Schema**: Đây là phần quan trọng nhất. Các sếp cần định nghĩa các trường dữ liệu muốn trích xuất (ví dụ: `invoice_number`, `total_amount`, `date`, `customer_name`).
    *   **Prompt (nếu dùng AI mode)**: Nếu dùng chế độ AI, hãy viết prompt rõ ràng để AI hiểu cần lấy thông tin gì từ file.

*   **Node: Switch (Phân loại)**
    *   Node này dùng để quyết định lưu file vào thư mục nào dựa trên kết quả trích xuất hoặc loại file.
    *   Các sếp cần chỉnh các **Rules** (Điều kiện). Ví dụ:
        *   Nếu `file_type` là `pdf` và `category` là `invoice` -> Đi đến nhánh "Lưu Hóa đơn".
        *   Nếu `file_type` là `image` -> Đi đến nhánh "Lưu Ảnh".
    *   Hãy thêm các nhánh (Output) tương ứng với các loại thư mục mà các sếp muốn tạo trên Google Drive.

*   **Node: Google Drive (Upload)**
    *   Chọn **Credentials** Google Drive.
    *   **Folder ID**: Các sếp cần tạo sẵn các thư mục trên Google Drive (ví dụ: `Invoices`, `Contracts`, `Reports`) và copy **Folder ID** của từng thư mục.
    *   Gán Folder ID tương ứng vào từng nhánh của node Switch.
    *   **File Name**: Có thể dùng biểu thức để đặt tên file tự động, ví dụ: `={{ $json.invoice_number }}_{{ $json.date }}.pdf`.

*   **Node: Google Sheets (Append)**
    *   Chọn **Credentials** Google Sheets.
    *   **Document ID**: ID của Sheet mà các sếp muốn lưu dữ liệu trích xuất.
    *   **Sheet Name**: Tên tab trong Sheet.
    *   **Mapping**: Ánh xạ các trường dữ liệu từ Easybits Extractor vào các cột trong Sheet.

*   **Node: Slack (Send Message)**
    *   Chọn **Credentials** Slack.
    *   **Channel**: Chọn kênh Slack muốn nhận thông báo.
    *   **Message**: Tùy chỉnh nội dung thông báo. Có thể chèn link Google Drive vừa tạo để team click vào xem file ngay.

*   **Node: Merge**
    *   Node này hợp nhất dữ liệu từ các nhánh khác nhau (nếu có) trước khi gửi Slack hoặc lưu Sheets. Đảm bảo các input của Merge node được kết nối đúng từ các nhánh xử lý trước đó.

#### 3. Kích hoạt ⚡️
1. **Test Run**: Gửi một email mẫu có file đính kèm (ví dụ: một hóa đơn PDF) đến địa chỉ Gmail đã cấu hình.
2. Chạy workflow bằng nút **Execute Workflow**.
3. Kiểm tra:
    *   File có được lưu vào đúng thư mục trên Google Drive không?
    *   Dữ liệu có được trích xuất và ghi vào Google Sheets không?
    *   Có nhận được thông báo trên Slack không?
4. Nếu mọi thứ ổn, bật **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm AI Summarization**: Thay vì chỉ trích xuất dữ liệu, các sếp có thể thêm một node LLM (như OpenAI) để tóm tắt nội dung file và gửi kèm trong tin nhắn Slack.
- **Tạo báo cáo định kỳ**: Thêm một workflow khác chạy hàng tuần để đọc dữ liệu từ Google Sheets và gửi báo cáo tổng hợp (tổng số hóa đơn, tổng doanh thu...) qua Email hoặc Slack.
- **Xử lý lỗi**: Thêm một nhánh "Error" trong workflow để gửi thông báo cảnh báo khi file không thể trích xuất hoặc lưu trữ thất bại.
- **Đa dạng định dạng file**: Easybits hỗ trợ nhiều định dạng. Các sếp có thể mở rộng workflow để xử lý cả Excel, Word, hoặc ảnh chụp hóa đơn.

### 📌 Kết luận
Workflow này là một ví dụ điển hình cho sức mạnh của tự động hóa kết hợp AI. Thay vì để các file đính kèm nằm rải rác trong hộp thư, các sếp sẽ có một hệ thống lưu trữ có cấu trúc, dữ liệu được số hóa và dễ dàng truy cập. Hãy áp dụng ngay để giải phóng thời gian và nâng cao hiệu suất làm việc của team!