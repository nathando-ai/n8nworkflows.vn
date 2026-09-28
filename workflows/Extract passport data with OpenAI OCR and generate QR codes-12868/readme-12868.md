---
title: "🚀 Trích xuất thông tin hộ chiếu tự động bằng OpenAI OCR và tạo mã QR trong n8n"
description: "Xây dựng quy trình tự động hóa quét ảnh hộ chiếu, trích xuất dữ liệu chuẩn hóa bằng OpenAI Vision AI, tạo mã QR và gửi kết quả tức thì qua Form và Gmail."
slug: "trich-xuat-thong-tin-ho-chieu-openai-ocr-qr-code"
tags: [n8n, automation, open-ai, ocr, qr-code, gpt-4, document-extraction]
keywords: [n8n workflow, trích xuất hộ chiếu, openai ocr, tạo mã qr tự động, xử lý ảnh n8n, icts automation]
---

# 🚀 Trích xuất thông tin hộ chiếu tự động bằng OpenAI OCR và tạo mã QR

Các sếp có đang gặp khó khăn trong việc xử lý và nhập liệu thông tin từ hàng loạt ảnh hộ chiếu của khách hàng? Việc gõ tay thủ công vừa tốn thời gian, dễ sai sót chính tả (tên, số hộ chiếu, ngày sinh), lại vừa làm chậm trễ quy trình chăm sóc khách hàng hoặc làm thủ tục.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do **ICTS Automation** thiết kế. Quy trình này giúp tự động hóa 100% việc nhận ảnh hộ chiếu từ form, đọc dữ liệu thông minh bằng OpenAI OCR, chuẩn hóa dữ liệu, tạo mã QR tương ứng và gửi trả kết quả qua cả màn hình Form lẫn Gmail chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Khách hàng upload ảnh, hệ thống tự động xử lý từ A-Z mà không cần nhân sự can thiệp thủ công.
- **Độ chính xác cao:** Ứng dụng sức mạnh của OpenAI OCR (GPT-4 Vision) giúp đọc chính xác các trường thông tin khó trên hộ chiếu.
- **Trải nghiệm mượt mà:** Trả kết quả ngay lập tức trực tiếp trên trang hoàn tất của Form và gửi email xác nhận kèm mã QR chuyên nghiệp.
- **Bảo mật & Tối ưu:** Dữ liệu hình ảnh được kiểm tra định dạng, resize tối ưu trước khi gửi lên AI giúp tiết kiệm chi phí và tăng tốc độ xử lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (có hỗ trợ mô hình Vision như GPT-4o hoặc GPT-4o-mini).
- **Tài khoản Gmail** (để cấu hình node gửi email tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc file JSON được cung cấp, sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 13 nodes được chia thành 3 giai đoạn chính. Các sếp chú ý cấu hình các điểm sau:

- **Node `On form submission` (formTrigger):** Nơi người dùng tải lên ảnh hộ chiếu. Các sếp có thể tùy chỉnh lại giao diện form cho phù hợp với nhận diện thương hiệu của mình.
- **Node `Grab image` & `Resize Image` (editImage):** Kiểm tra định dạng file ảnh và tiến hành resize kích thước tối ưu để đảm bảo OCR đọc chính xác và tiết kiệm dung lượng token.
- **Node `OCR - openAI` (httpRequest):** 
  - Cần cấu hình **Credentials** cho OpenAI API.
  - Kiểm tra lại Prompt trong phần Body của HTTP Request để đảm bảo AI trả về đúng các trường dữ liệu cần thiết (Họ tên, Số hộ chiếu, Ngày sinh, Quốc tịch,...).
- **Node `Data standardization` & `Prepare QR url` (code):** Chạy các đoạn mã JavaScript tùy chỉnh để làm sạch dữ liệu trả về từ AI và tạo đường dẫn/định dạng cho mã QR.
- **Node `Send a message` (gmail):** 
  - Kết nối tài khoản **Gmail OAuth2** của các sếp.
  - Thay đổi địa chỉ email nhận mẫu (`YOUR_EMAIL`) thành email thực tế để test.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử nghiệm tải lên một hình ảnh hộ chiếu mẫu rõ nét để kiểm tra luồng dữ liệu.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Kết nối thêm node **Google Sheets** hoặc **Airtable** ngay sau bước chuẩn hóa dữ liệu để lưu lại lịch sử danh sách khách hàng đã quét hộ chiếu.
- **Cảnh báo qua kênh chat:** Tích hợp thêm node **Telegram** hoặc **Slack** để thông báo về ban quản trị mỗi khi có một hộ chiếu mới được quét thành công.
- **Mở rộng biểu mẫu:** Tùy chỉnh prompt của OpenAI để trích xuất thêm các loại giấy tờ tùy thân khác như Căn cước công dân (CCCD) hoặc Giấy phép lái xe.

### 📌 Kết luận
Việc tự động hóa trích xuất thông tin hộ chiếu và tạo mã QR chưa bao giờ dễ dàng đến thế với n8n và OpenAI. Giải pháp này từ **ICTS Automation** sẽ giúp các doanh nghiệp lữ hành, khách sạn hoặc dịch vụ visa tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!