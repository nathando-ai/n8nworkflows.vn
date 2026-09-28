---
title: "🚀 Tự động trích xuất văn bản từ PDF và hình ảnh bằng AI và lưu vào Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn việc đọc file PDF, hình ảnh qua Google Gemini & Vertex AI rồi chuyển đổi thành file CSV lưu trữ trên Google Drive."
slug: "trich-xuat-van-ban-pdf-image-ai-google-drive"
tags: [n8n, automation, google-drive, google-gemini, vertex-ai, ai-agent]
keywords: [n8n workflow, trích xuất pdf bằng ai, google gemini n8n, vertex ai n8n, tự động hóa google drive, convert pdf to csv ai]
---

# 🚀 Tự động trích xuất văn bản từ PDF và hình ảnh bằng AI và lưu vào Google Drive

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi copy, nhập liệu thủ công hàng đống hóa đơn, tài liệu PDF hay hình ảnh chụp màn hình chưa? Việc này vừa tốn thời gian, dễ sai sót lại chẳng mang lại giá trị gia tăng nào cho doanh nghiệp.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ mạnh mẽ do tác giả **Keith Rumjahn** chia sẻ. Workflow này sẽ tự động "bắt sóng" khi có file mới xuất hiện trên Google Drive, phân loại PDF hay ảnh, dùng AI (Google Gemini / Vertex AI) để thông minh hóa việc đọc hiểu nội dung, và cuối cùng tự động xuất ra file CSV gọn gàng! 100% tự động, không cần đụng tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần ném file PDF hoặc ảnh vào thư mục Google Drive, hệ thống tự lo phần còn lại.
- **Xử lý đa định dạng thông minh:** Tự động nhận diện và phân luồng xử lý riêng cho file PDF hoặc hình ảnh (sử dụng Gemini Chat Model và Vertex AI).
- **Chuyển đổi dữ liệu sạch:** Tự động cấu trúc hóa dữ liệu trích xuất được thành file CSV chuẩn chỉnh.
- **Lưu trữ ngăn nắp:** Tự động đẩy file CSV kết quả về lại Google Drive để dễ dàng tra cứu, báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã chạy ổn định (Self-hosted hoặc Cloud).
- **Google Drive Account:** Dùng để làm trigger nhận file và lưu file CSV kết quả. Cần cấu hình Google API Credentials.
- **Google Gemini / Vertex AI API:** Tài khoản Google Cloud đã bật Vertex AI API và Google Palm/Gemini API key.
- **OpenRouter Account (Tùy chọn bổ trợ):** Nếu các sếp muốn route dữ liệu qua các mô hình AI khác (thông qua node `Send data to A.I.`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> Nhấp vào menu 3 chấm ở góc trên bên phải -> **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **Node `Get PDF or Images` (Google Drive Trigger):** 
  - Tạo một thư mục riêng biệt trên Google Drive của các sếp để thả file tài liệu/ảnh vào.
  - Nhớ chia sẻ (Share) thư mục này cho tài khoản Google Cloud Service Account của các sếp (Ví dụ dạng: `n8n-server@n8n-server-xxxxxx.iam.gserviceaccount.com`).
  - Chọn đúng ID thư mục trong node này để nó bắt sự kiện `File Created`.

- **Node `Route based on PDF or Image` (Switch):**
  - Node này sẽ phân loại xem file đầu vào là PDF hay hình ảnh để đi theo 2 nhánh xử lý riêng biệt. Các sếp kiểm tra lại điều kiện phân loại dựa trên định dạng file (`mimeType`).

- **Nhóm xử lý PDF (`Download PDF`, `Extract data from PDF`, `Send data to A.I.` / `Convert to CSV`):**
  - Node `Download PDF` và `Extract data from PDF` sẽ đọc nội dung văn bản bên trong file PDF.
  - Node `Send data to A.I.` sử dụng kết nối Header Auth (OpenRouter hoặc API tương đương). Các sếp cần điền `Authorization` với giá trị `Bearer {API token}` của mình.

- **Nhóm xử lý Ảnh (`Download Image`, `Vertex A.I. extract text`, `Google Gemini Chat Model`):**
  - Bật Vertex API trên Google Cloud Console và phân quyền đầy đủ cho tài khoản Service Account.
  - Node `Vertex A.I. extract text` (`chainLlm`) kết hợp với `Google Gemini Chat Model` sẽ làm nhiệm vụ OCR và phân tích nội dung hình ảnh cực kỳ chính xác.

- **Nhóm lưu trữ (`Convert to CSV`, `Upload to Google Drive` & các bản sao):**
  - Cấu hình lại thư mục đích trên Google Drive nơi file CSV thành phẩm sẽ được tự động tải lên lưu trữ.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và thử upload một file PDF hoặc 1 tấm ảnh chứa text lên thư mục Google Drive đã định nghĩa để test run.
- Sau khi test thành công và nhìn thấy file CSV xuất hiện trên Drive, các sếp bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để mỗi khi trích xuất xong, bot sẽ nhắn tin thông báo kèm link file CSV trên Google Drive cho các sếp.
- **Lưu vào Database:** Thay vì chỉ lưu ra file CSV trên Google Drive, các sếp có thể đổi node `Convert to CSV` thành `Google Sheets` hoặc `Supabase` để lưu thẳng vào bảng dữ liệu trực tuyến, tiện cho việc làm dashboard.
- **Xử lý hàng loạt:** Kết hợp thêm các bước đổi tên file, di chuyển file gốc vào thư mục "Đã xử lý" (Processed) trên Google Drive để tránh việc 1 file bị quét xử lý nhiều lần.

### 📌 Kết luận
Đây là một giải pháp tự động hóa tuyệt vời giúp tiết kiệm hàng giờ đồng hồ nhập liệu thủ công mỗi tuần nhờ sức mạnh của AI hiện đại (Gemini & Vertex AI). Hãy cài đặt ngay vào hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc nhé! Chúc các sếp thao tác thành công!