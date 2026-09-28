---
title: "🚀 Tự động hóa xử lý hóa đơn qua LINE: Đọc OCR, phân tích bằng Gemini AI và lưu vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động nhận ảnh hóa đơn từ LINE, trích xuất text bằng OCR.space, phân tích dữ liệu thông minh với Google Gemini AI và lưu trữ tự động vào Google Sheets."
slug: "tu-dong-hoa-xu-ly-hoa-don-line-ocr-gemini-google-sheets"
tags: [n8n, automation, line-bot, google-sheets, ocr-space, google-gemini, ai-agent]
keywords: [n8n workflow, line bot hoa don, ocr space n8n, google gemini ai hoa don, tu dong hoa don google sheets]
---

# 🚀 Tự động hóa xử lý hóa đơn qua LINE: Đọc OCR, phân tích bằng Gemini AI và lưu vào Google Sheets

Các sếp có đang đau đầu mỗi khi phải thu thập, nhập liệu thủ công hàng đống hóa đơn giấy, hóa đơn chụp ảnh gửi qua chat vào Excel hay Google Sheets? Việc này vừa tốn thời gian, dễ gây sai sót con số, lại cực kỳ nhàm chán cho đội ngũ kế toán hoặc quản lý.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ xịn sò giúp tự động hóa 100% quy trình này: chỉ cần chụp ảnh hóa đơn gửi vào **LINE Bot**, hệ thống sẽ tự động bóc tách thông tin, gọi **Gemini AI** đọc hiểu, ghi nhận vào **Google Sheets** và nhắn lại kết quả ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần gõ tay, chỉ cần chụp ảnh gửi qua LINE là xong.
- **AI thông minh:** Google Gemini tự động nhận diện số hóa đơn, ngày tháng, tên nhà cung cấp, tổng tiền, tiền thuế... cực kỳ chính xác.
- **Đồng bộ thời gian thực:** Dữ liệu tự động nhảy đẹp đẽ vào Google Sheets ngay sau vài giây.
- **Phản hồi tức thì:** Bot LINE sẽ gửi tin nhắn xác nhận thành công hoặc báo lỗi nếu ảnh gửi lên không phải là hóa đơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản LINE Developers:** Tạo Messaging API channel để lấy Channel Access Token.
- **Tài khoản OCR.space:** Lấy API key miễn phí tại `ocr.space/ocrapi/freekey` (25,000 request/tháng hoàn toàn miễn phí).
- **Google AI Studio:** Lấy API key Google Gemini miễn phí tại `aistudio.google.com`.
- **Google Account:** Kết nối Google Sheets Credentials trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy đoạn mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm 15 nodes được sắp xếp logic rõ ràng từ khâu nhận Webhook cho đến xử lý AI và lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Node `Variables (API Key Management)` (`set`):** Đây là nơi tập trung các biến cấu hình quan trọng nhất. Các sếp cần điền chính xác:
  - Token LINE Messaging API.
  - OCR.space API Key.
  - Google Spreadsheet ID (ID của file Google Sheets dùng để lưu hóa đơn).
  - Tên Sheet (`SHEET_NAME`).
- **Node `Receive LINE Webhook` (`webhook`):** Cấu hình path là `line-invoice` và method là `POST`. Sau khi kích hoạt workflow, nhớ cập nhật Webhook URL này vào phần cấu hình của LINE Developers channel.
- **Node `Google Gemini Chat Model` & `AI Agent - Parse Invoice with Gemini` (`agent`):** Kết nối thông tin xác thực Google Gemini và kiểm tra câu lệnh (prompt) của AI để đảm bảo nó trích xuất đúng các trường dữ liệu mong muốn (số hóa đơn, ngày phát hành, tên nhà cung cấp, tổng tiền...).
- **Node `Append to Google Sheets` (`googleSheets`):** Chọn đúng tài khoản Google Credentials đã kết nối và trỏ tới đúng bảng tính, các cột dữ liệu tương ứng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một bức ảnh hóa đơn thử nghiệm vào LINE Bot của các sếp để kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật nút **Active** để workflow chính thức chạy 24/7 tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Kết nối thêm node Telegram hoặc Slack ở nhánh **LINE Reply - Success** để gửi thông báo chi phí mới về group chat nội bộ của công ty.
- **Phân loại theo tháng:** Tùy biến `SHEET_NAME` trong node Variables để tự động tạo hoặc ghi dữ liệu vào các sheet riêng theo từng tháng hoặc từng dự án.
- **Nâng cấp OCR:** Nếu hóa đơn có layout phức tạp hoặc chữ viết tay, các sếp có thể thay thế OCR.space bằng Google Cloud Vision API để đạt độ chính xác cao hơn nữa.

### 📌 Kết luận
Việc tự động hóa hóa đơn chưa bao giờ dễ dàng đến thế với sự kết hợp giữa LINE Bot, OCR và Gemini AI trên nền tảng n8n. Hãy áp dụng ngay hôm nay để giải phóng thời gian cho đội ngũ kế toán và tối ưu hóa vận hành doanh nghiệp các sếp nhé!