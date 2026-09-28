---
title: "🚀 Tự động trích xuất dữ liệu hóa đơn từ Google Drive vào Google Sheets với Mistral OCR và Gemini AI"
description: "Hướng dẫn chi tiết workflow n8n tự động nhận diện hóa đơn PDF/hình ảnh từ Google Drive, bóc tách thông tin bằng Mistral OCR kết hợp Gemini AI và lưu trữ có cấu trúc vào Google Sheets."
slug: "tu-dong-trich-xuat-hoa-don-google-drive-mistral-ocr-gemini-sheets"
tags: [n8n, automation, ai, google-drive, google-sheets, mistral-ocr, gemini]
keywords: [n8n workflow, trích xuất hóa đơn tự động, mistral ai ocr, google gemini agent, google sheets automation]
---

# 🚀 Tự động trích xuất dữ liệu hóa đơn từ Google Drive vào Google Sheets với Mistral OCR và Gemini AI

Các sếp có đang đau đầu vì mỗi tháng phải ngồi gõ thủ công hàng trăm tờ hóa đơn, biên lai vào file Excel? Việc này không chỉ tốn hàng tá thời gian, dễ gây nhầm lẫn con số mà còn làm gián đoạn các công việc ưu tiên khác của đội ngũ kế toán, vận hành. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một **Workflow n8n tự động hóa 100%**, kết hợp sức mạnh của **Mistral OCR** (đọc hiểu văn bản/hình ảnh cực đỉnh) và **Google Gemini AI** (bóc tách cấu trúc dữ liệu thông minh) để xử lý mọi hóa đơn đổ về Google Drive và đồng bộ thẳng vào Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Ngay khi có file hóa đơn mới (PDF hoặc hình ảnh) bỏ vào thư mục Google Drive, workflow sẽ tự kích hoạt.
- **Không trùng lặp**: Hệ thống tự động kiểm tra Google Sheets để bỏ qua các file đã xử lý nhờ cơ chế tracking `Id`.
- **Độ chính xác cao**: Kết hợp Mistral OCR trích xuất văn bản thô và Gemini AI định hình đúng các trường dữ liệu (Tổng tiền, Ngày, Mã số thuế, Nhà cung cấp...).
- **Tiết kiệm 95% thời gian**: Giải phóng đội ngũ kế toán khỏi các tác vụ nhập liệu tay nhàm chán.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- Tài khoản **Google Drive & Google Sheets** (để cấu hình credentials OAuth2).
- **Mistral AI API Key** (Đăng ký tại [Mistral La Plateforme](https://mistral.ai/products/la-plateforme)).
- **Google Gemini API Key** (Google Palm/Gemini API credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (từ nguồn n8n template #4868) và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 20 nodes với sự kết hợp của Trigger, AI Agent, HTTP Request và Google nodes. Các sếp lưu ý cấu hình kỹ các điểm sau:

- **On new file in Google Drive & Load files from Google Drive folder**: 
  - Chọn đúng Credentials Google Drive.
  - Trỏ đến **thư mục nguồn** trên Google Drive nơi các sếp sẽ upload hóa đơn lên.
- **Get already processed rows from Sheets & Get Fields Schema & Save data to Google Sheets**:
  - Chọn Credentials Google Sheets.
  - Chọn file Google Sheets quản lý hóa đơn của các sếp.
  - **LƯU Ý CỰC KỲ QUAN TRỌNG**: Cột đầu tiên (ô **A1**) trong file Google Sheets **BẮT BUỘC phải đặt tên là "Id"**. Cột này dùng để lưu Google Drive File ID nhằm ngăn chặn việc xử lý lại các file cũ.
  - Các cột tiếp theo ở dòng 1 chính là các trường dữ liệu mà các sếp muốn AI bóc tách (Ví dụ: `Supplier`, `Date`, `Total Amount`, `Tax Code`...).
- **Các node Mistral (Mistral Upload, Mistral Signed URL, Mistral OCR, Mistral IMAGE OCR...)**:
  - Thêm Mistral Cloud API Credentials. Các node này sẽ tự động phân loại nếu là file tài liệu (PDF) hay hình ảnh (IMAGE) để gọi đúng API OCR của Mistral.
- **Google Gemini Chat Model & Field Extractor (AI Agent)**:
  - Cấu hình Google Palm/Gemini API Key. Node Agent sẽ sử dụng schema lấy từ Google Sheets để định hướng Gemini trích xuất thông tin hóa đơn chuẩn xác nhất.

#### 3. Kích hoạt ⚡️
- Bấm nút **"Test workflow"** (`When clicking ‘Test workflow’`) hoặc tải một file hóa đơn mẫu lên Google Drive để kiểm tra luồng chạy qua các node `If`, `Filter processed files` và lưu vào Google Sheets.
- Nếu dữ liệu đổ về bảng tính chính xác, hãy gạt công tắc **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối luồng để gửi thông báo real-time ("Đã xử lý xong hóa đơn từ [Tên Nhà Cung Cấp] - Tổng tiền: [X] VNĐ") cho quản lý duyệt.
- **Phân loại thư mục**: Sau khi xử lý xong, có thể bổ sung node Google Drive di chuyển file hóa đơn sang thư mục "Processed" để giữ cho thư mục gốc luôn gọn gàng.
- **Xử lý lỗi (Error Handling)**: Thêm Error Trigger để bắt các trường hợp hóa đơn quá mờ, AI không đọc được và gửi cảnh báo về email hoặc chatwork.

### 📌 Kết luận
Việc tự động hóa quy trình nhập liệu hóa đơn chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n và các mô hình AI tiên tiến như Mistral và Gemini. Hãy áp dụng ngay vào doanh nghiệp của mình để tối ưu hóa năng suất vận hành ngay hôm nay!