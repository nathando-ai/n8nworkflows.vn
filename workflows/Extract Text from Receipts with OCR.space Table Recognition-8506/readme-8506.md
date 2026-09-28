---
title: "🚀 Tự động trích xuất văn bản từ hóa đơn, biên nhận bằng OCR.space trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động upload hóa đơn, nhận diện văn bản và bảng biểu với OCR.space API cực kỳ nhanh chóng và chính xác."
slug: "trich-xuat-van-ban-hoa-don-ocr-space-n8n"
tags: [n8n, automation, no-code, ocr, ai-processing, invoice-processing]
keywords: [n8n workflow, ocr space api, trich xuat hoa don, tu dong hoa ocr, n8n form trigger]
---

# 🚀 Tự động trích xuất văn bản từ hóa đơn, biên nhận với OCR.space trên n8n

Việc nhập liệu thủ công từ các hóa đơn, biên nhận giấy hoặc ảnh chụp thường tốn rất nhiều thời gian và dễ xảy ra sai sót. Đối với các doanh nghiệp vừa và nhỏ, việc đầu tư các giải pháp AI đắt tiền đôi khi chưa thực sự cần thiết. 

Giải pháp? Workflow n8n này sẽ giúp các sếp xây dựng một hệ thống OCR mini ngay lập tức: Khách hàng hoặc nhân viên chỉ cần upload ảnh hóa đơn qua một giao diện Form trực tuyến, hệ thống sẽ tự động gọi API OCR.space để bóc tách toàn bộ văn bản (hỗ trợ cả nhận diện dạng bảng biểu) và hiển thị kết quả ngay lập tức để copy-sử dụng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần gõ lại thủ công nội dung từ hóa đơn, biên nhận.
- **Giao diện thân thiện:** Tích hợp Form upload trực quan, dễ dàng sử dụng cho cả người không rành kỹ thuật.
- **Linh hoạt xử lý:** Tùy chọn chế độ nhận diện bảng biểu (Table Recognition) giúp bóc tách dữ liệu có cấu trúc tốt hơn.
- **Hoạt động 24/7:** Vận hành tự động hoàn toàn trên nền tảng n8n không giới hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản miễn phí tại [OCR.space](https://ocr.space/) để lấy **API Key** (dùng xác thực qua Header Auth).
- Ảnh hóa đơn/biên nhận (dung lượng $\le 1$ MB).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/8506](https://n8n.io/workflows/8506)) và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Trigger • Upload image for OCR (`formTrigger`):**
  - Node này tạo một Web Form công cộng cho phép người dùng tải lên hình ảnh (kích thước tối đa 1 MB) và câu hỏi tùy chọn liệu nội dung có phải là bảng hay không (`isTable`). Các sếp có thể tùy chỉnh giao diện form theo ý muốn.

- **Prepare • Normalize inputs (`set`):**
  - Node này nhận dữ liệu từ Form, chuyển đổi trường radio thành định dạng cờ Boolean `isTable` (true/false) để gửi chuẩn xác sang API và giữ nguyên file đính kèm.

- **OCR.space • Parse image (`httpRequest`):**
  - Đây là "trái tim" của workflow. Sếp cần cấu hình **Credentials** loại `Header Auth` với API Key lấy từ OCR.space.
  - Các tham số mặc định được thiết lập sẵn: Ngôn ngữ (`pol` - tiếng Ba Lan, sếp có thể đổi thành `eng` cho tiếng Anh hoặc `vie` nếu tài khoản hỗ trợ), Engine (`2`), và truyền biến `isTable`.

- **Display • Show OCR text (`form` - Completion):**
  - Hiển thị kết quả văn bản đã bóc tách từ trường `ParsedResults[0].ParsedText` bên trong một khung định dạng monospace giúp dễ dàng copy-paste.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách upload một hình ảnh hóa đơn mẫu lên form.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp, các sếp có thể mở rộng thêm:
1. **Lưu trữ tự động:** Thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử text bóc tách được cùng thời gian và tên file.
2. **Gửi thông báo:** Tích hợp node **Telegram** hoặc **Slack** để bắn thông báo kèm nội dung hóa đơn về nhóm làm việc ngay khi có người upload.
3. **Xử lý hậu kỳ bằng AI:** Kết hợp thêm node **OpenAI / Claude** để phân tích text thô thành các trường dữ liệu gọn gàng (Tổng tiền, Ngày tháng, Tên nhà cung cấp...).

### 📌 Kết luận
Với workflow OCR.space kết hợp n8n này, việc số hóa hóa đơn và chứng từ trở nên dễ dàng và tiết kiệm chi phí hơn bao giờ hết. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình làm việc của đội ngũ nhé!