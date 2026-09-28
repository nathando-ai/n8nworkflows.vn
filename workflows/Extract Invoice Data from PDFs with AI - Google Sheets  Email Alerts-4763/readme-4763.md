---
title: "🚀 Tự động trích xuất hóa đơn PDF bằng AI, lưu Google Sheets và gửi Email thông báo"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt file hóa đơn PDF mới từ Google Drive, dùng AI trích xuất thông tin, lưu vào Google Sheets và gửi email cảnh báo."
slug: "trich-xuat-hoa-don-pdf-ai-google-sheets-email"
tags: [n8n, automation, ai, google-sheets, gmail, finance]
keywords: [n8n workflow, tự động hóa hóa đơn, AI extract invoice, google drive trigger, trích xuất pdf bằng ai]
---

# 🚀 Tự động trích xuất hóa đơn PDF bằng AI, lưu Google Sheets và gửi Email thông báo

Các sếp có đang cảm thấy mệt mỏi mỗi cuối tháng khi phải ngồi "vọc" từng file PDF hóa đơn, thủ công copy tên công ty, mã số thuế, tổng tiền rồi nhập vào Google Sheets? Chỉ cần vài chục hóa đơn là đã hoa mắt chóng mặt, chưa kể nguy cơ gõ nhầm số liệu dẫn đến lệch sổ sách tài chính.

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ xịn sò do tác giả Aashit Sharma thiết kế. Workflow này sẽ tự động hóa toàn bộ quy trình: từ lúc hóa đơn vừa xuất hiện trên Google Drive, AI sẽ đọc hiểu, trích xuất thông tin chuẩn xác, lưu thẳng vào Google Sheets và tự động gửi email thông báo. Hoàn toàn tự động 100%, không tốn một giọt mồ hôi thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh gõ tay nhập liệu thủ công, giải phóng nhân sự kế toán làm việc có giá trị hơn.
- **Độ chính xác tuyệt đối:** Sử dụng sức mạnh của AI LangChain và các mô hình ngôn ngữ lớn để đọc hiểu cấu trúc hóa đơn đa dạng.
- **Lưu trữ đồng bộ:** Tự động ghi nhận thông tin vào Google Sheets gọn gàng, sẵn sàng cho việc báo cáo tài chính.
- **Cảnh báo tức thì:** Gửi email thông báo ngay khi hóa đơn mới được xử lý thành công qua Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản Google Drive & Google Sheets** (để cấu hình Trigger và lưu dữ liệu).
- **Tài khoản Gmail** (để gửi email thông báo).
- **OpenAI API Key** hoặc **Ollama** (để chạy các Model AI phân tích văn bản).
- **Postgres Database** (tùy chọn, dùng cho PGVector Store nếu cần lưu trữ vector nâng cao).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ trang n8n chính thức (link gốc ở template số 4763) hoặc tải file JSON về, sau đó chọn **Import from File** hoặc dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình lại các node trọng điểm sau:
- **Google Drive Trigger - file creation**: Kết nối tài khoản Google Drive của sếp và chọn thư mục (Folder) chuyên để nhận các file hóa đơn PDF đầu vào.
- **Download Binary - file**: Đảm bảo node này lấy đúng ID của file vừa được trigger từ Google Drive.
- **Extract from PDF**: Trích xuất toàn bộ văn bản thô từ file PDF đầu vào chuẩn bị cung cấp cho AI.
- **Information Extractor & Create Email Agent / Ollama Model**: Cấu hình credentials cho OpenAI hoặc Ollama. Tại đây, các sếp viết prompt hướng dẫn AI trích xuất các trường thông tin cụ thể từ hóa đơn (như: Tên nhà cung cấp, Ngày hóa đơn, Tổng tiền, Mã số thuế...).
- **Update DB - spreadsheet**: Kết nối tài khoản Google Sheets, chọn đúng file Google Sheet và bảng tính (Sheet Name) để map các trường dữ liệu AI vừa trích xuất vào các cột tương ứng.
- **Send Email**: Kết nối tài khoản Gmail của sếp, thiết lập người nhận và nội dung template email thông báo khi hóa đơn mới được xử lý xong.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử tải lên một file hóa đơn PDF mẫu lên thư mục Google Drive đã chọn để kiểm tra luồng chạy.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot Telegram/Slack:** Thay vì chỉ gửi email, các sếp có thể thêm một node Telegram hoặc Slack để bắn thông báo ngay lập tức lên nhóm chat kế toán của công ty.
- **Phân loại tự động:** Sử dụng AI để phân loại hóa đơn theo danh mục (Chi phí marketing, Văn phòng phẩm, Thuê server...) trước khi ghi vào Google Sheets.
- **Lưu trữ file backup:** Thêm bước di chuyển file PDF gốc sang một thư mục "Đã xử lý" trên Google Drive để tránh bị trùng lặp file.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn PDF chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n và AI. Hãy áp dụng ngay workflow này để giải phóng sức lao động cho đội ngũ kế toán và tối ưu hóa vận hành doanh nghiệp của các sếp ngay hôm nay!