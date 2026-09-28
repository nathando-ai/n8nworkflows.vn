---
title: "🚀 Tự động hóa xử lý hồ sơ y tế với Mistral OCR và Google Sheets trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin từ tài liệu y tế bằng Mistral OCR và lưu trữ cấu trúc vào Google Sheets."
slug: "tu-dong-hoa-ho-so-y-te-mistral-ocr-google-sheets"
tags: [n8n, automation, no-code, ai, ocr, google-sheets]
keywords: [n8n workflow, mistral ocr, tự động hóa y tế, google sheets automation, trích xuất văn bản ai]
---

# 🚀 Tự động hóa xử lý hồ sơ y tế với Mistral OCR và Google Sheets

Các phòng khám, bệnh viện và cơ sở y tế thường xuyên đối mặt với núi hồ sơ giấy tờ, kết quả xét nghiệm và bệnh án dạng PDF hoặc hình ảnh. Việc nhập liệu thủ công không chỉ tốn hàng giờ đồng hồ mỗi ngày mà còn tiềm ẩn rủi ro sai sót thông tin bệnh nhân.

Giải pháp? Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa 100% không cần code, tận dụng sức mạnh của **Mistral OCR** để đọc tài liệu, xử lý bằng **Code Node**, và tự động đồng bộ dữ liệu chuẩn chỉnh vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file tài liệu lớn mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Người dùng tải tài liệu lên qua form, hệ thống tự động xử lý từ A-Z mà không cần can thiệp thủ công.
- **Trích xuất thông tin chính xác bằng AI**: Tận dụng công nghệ OCR tiên tiến của Mistral AI để bóc tách dữ liệu phức tạp.
- **Cấu trúc hóa dữ liệu thông minh**: Node code tự động phân loại tên bệnh nhân, chẩn đoán, thuốc men, kết quả xét nghiệm,...
- **Lưu trữ tập trung**: Dữ liệu được ghi nhận ngay lập tức vào Google Sheets, sẵn sàng cho việc tra cứu và báo cáo.
:::

### 🔐 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Mistral AI** và **API Key** để gọi các endpoint OCR.
- **Tài khoản Google** để kết nối với Google Sheets.
- **Mẫu Google Sheet** chuẩn bị sẵn để lưu trữ dữ liệu (có thể dùng template mẫu từ tác giả gốc).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ n8n.io và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính được cấu hình tuần tự như sau:

- **On form submission (`formTrigger`)**: 
  - Tạo giao diện form đơn giản để người dùng upload tài liệu y tế (đặt tên trường file là `Document`).
- **Upload to Mistral (`httpRequest`)**:
  - Gửi file được upload lên endpoint `https://api.mistral.ai/v1/files`.
  - Cấu hình Authentication dạng **HTTP Header Auth** với Mistral API Key.
- **Get Signed URL (`httpRequest`)**:
  - Gọi yêu cầu lấy URL tạm thời được bảo mật từ Mistral để truy cập file vừa upload.
- **Get OCR Results (`httpRequest`)**:
  - Gửi Signed URL đến API OCR của Mistral để trích xuất toàn bộ nội dung văn bản có trong tài liệu.
- **Data cleaning (`code`)**:
  - Sử dụng đoạn mã JavaScript để phân tích văn bản thô từ kết quả OCR.
  - Bóc tách các trường dữ liệu quan trọng: Tên bệnh nhân (Name), Ngày sinh (DOB), Mã bệnh nhân (Patient ID), Chẩn đoán (Diagnosis), Thuốc (Medications), Kết quả xét nghiệm (Lab Results), Ghi chú (Notes)...
- **Google Sheets (`googleSheets`)**:
  - Kết nối tài khoản Google qua OAuth2.
  - Chọn file Google Sheets và sheet tương ứng (ví dụ: tab "Patients" trong file Medical Records).
  - Cấu hình operation là **Append** để thêm dòng dữ liệu mới sau mỗi lần có form submit thành công.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** bằng cách upload thử một tài liệu y tế mẫu lên form để kiểm tra dữ liệu chảy qua từng node có đúng cấu trúc hay không.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node Telegram hoặc Slack để gửi thông báo ngay lập tức cho đội ngũ y tế khi có hồ sơ bệnh án mới được xử lý xong.
- **Lưu trữ file gốc**: Tự động lưu bản sao file PDF/Ảnh của bệnh nhân lên Google Drive hoặc AWS S3 dựa trên ID bệnh nhân để dễ dàng tra cứu về sau.
- **Xử lý ngoại lệ (Error Handling)**: Thêm Error Trigger để cảnh báo nếu tài liệu quá mờ hoặc định dạng không được hỗ trợ bởi OCR.

### 📌 Kết luận
Ứng dụng AI OCR vào quy trình xử lý hồ sơ y tế không chỉ giúp tiết kiệm hàng đống thời gian nhập liệu thủ công mà còn hạn chế tối đa sai sót y khoa do nhầm lẫn thông số. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!