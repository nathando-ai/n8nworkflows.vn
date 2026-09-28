---
title: "🚀 Tự động chấm điểm phiếu trả lời trắc nghiệm OMR bằng AI Vision và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động chấm phiếu OMR, nhận diện đáp án bằng AI Vision, so sánh đáp án đúng và lưu kết quả vào Google Sheets qua n8n."
slug: "tu-dong-cham-diem-phieu-omr-ai-vision-google-sheets"
tags: [n8n, automation, ai-vision, google-sheets, education-tech, ohlama]
keywords: [cham diem omr tu dong, ai vision cham bai, n8n webhook google sheets, tu dong hoa giao duc]
---

# 🚀 Tự động chấm điểm phiếu trả lời trắc nghiệm OMR bằng AI Vision và Google Sheets

Các thầy cô, trung tâm luyện thi hay trường học có đang mất hàng giờ đồng hồ chỉ để chấm từng xấp bài thi trắc nghiệm thủ công? Việc này không chỉ tốn thời gian, dễ gây nhầm lẫn mà còn khiến học sinh phải chờ đợi kết quả quá lâu.

Được phát triển bởi **InfyOm Technologies**, workflow n8n này sẽ giải quyết hoàn toàn bài toán trên bằng cách tự động hóa 100% quy trình chấm điểm phiếu OMR (Optical Mark Recognition). Hệ thống sẽ tiếp nhận ảnh chụp phiếu làm bài qua Webhook, sử dụng AI Vision để đọc các ô trắc nghiệm đã tô, so sánh với đáp án chuẩn, tính điểm và lưu trữ trực tiếp vào Google Sheets mà không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần tải ảnh phiếu trả lời lên, AI sẽ tự động đọc tên học sinh, số báo danh và các đáp án đã chọn.
- **Chính xác & Khách quan:** Giảm thiểu tuyệt đối sai sót do con người khi chấm bài thủ công hàng loạt.
- **Tốc độ chớp nhoáng:** Trả kết quả điểm số chi tiết ngay lập tức qua Webhook và đồng bộ dữ liệu về Google Sheets theo thời gian thực.
- **Tiết kiệm nguồn lực:** Thay vì tốn hàng giờ chấm bài, hệ thống tự động xử lý mọi thứ một cách mượt mà.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **AI Model (Ollama / Gemini Vision):** Node AI Vision trong workflow sử dụng Ollama để xử lý hình ảnh. Đảm bảo các sếp đã cấu hình kết nối Ollama với mô hình hỗ trợ thị giác máy tính (như Gemini hoặc Llama 3 Vision / llava).
- **Google Sheets:** Tài khoản Google để kết nối OAuth2 và lưu trữ kết quả. (Tham khảo mẫu Google Sheet gốc tại [đây](https://docs.google.com/spreadsheets/d/15nvRI8zcJ2n-QBXNk9xyd1GM8Vj7_1lJ3K7vO7Qfq3w/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 8 nodes chính được chia thành các luồng xử lý sau:

- **Send Student Ans Img (`webhook`):** 
  - Đường dẫn endpoint mặc định: `omr-sheet-checker` (phương thức `POST`).
  - Khi test hoặc gửi request, truyền dữ liệu dạng `Form-Data` với:
    - `key`: `file`
    - `value`: Upload hình ảnh phiếu OMR của học sinh.

- **Analyze image (`ollama`):** 
  - Node này chịu trách nhiệm phân tích hình ảnh phiếu trả lời bằng AI Vision. 
  - Cần cấu hình thông tin kết nối Ollama credentials và chọn đúng model AI có khả năng đọc hiểu hình ảnh (Vision Model).

- **Set Your Correct Answer (`set`):** 
  - Các sếp cần cấu hình đáp án đúng của bài kiểm tra tại node này để hệ thống có cơ sở so sánh với bài làm của học sinh.

- **Convert User Ans in Formate & Calculate Result (`code`):** 
  - Các node Javascript chạy ngầm giúp chuẩn hóa định dạng câu trả lời của học sinh và tính toán điểm số chi tiết (đúng/sai, tổng điểm).

- **Append Result in Sheet (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets của các sếp (OAuth2).
  - Trỏ tới file Google Sheet lưu kết quả (có thể sử dụng cấu trúc mẫu được cung cấp sẵn) để tự động ghi nhận thông tin học sinh và điểm số.

- **Send Result Respond (`respondToWebhook`):** 
  - Trả về kết quả JSON chi tiết cho phía gọi API (gồm thông tin học sinh, đáp án, điểm số) ngay sau khi xử lý xong.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request test bằng Postman hoặc curl với hình ảnh phiếu OMR mẫu.
- Kiểm tra kết quả trả về ở webhook response và xem dữ liệu đã được đẩy lên Google Sheets thành công chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để đưa vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Kết nối thêm node Telegram để ngay khi chấm xong bài, hệ thống tự động bắn tin nhắn báo điểm về nhóm chat của giáo viên hoặc phụ huynh.
- **Lưu trữ file ảnh:** Kết hợp lưu file ảnh phiếu OMR gốc lên Google Drive hoặc AWS S3 kèm theo đường dẫn trong Google Sheets để tiện việc tra cứu, đối chiếu về sau.
- **Mở rộng hàng loạt:** Xây dựng thêm giao diện Frontend đơn giản (hoặc Mini App Telegram) để học sinh/giáo viên tự chụp ảnh và chấm điểm tự động trên điện thoại.

### 📌 Kết luận
Việc tự động hóa chấm điểm trắc nghiệm OMR chưa bao giờ dễ dàng đến thế với sức mạnh của AI Vision và n8n. Hãy "lên đồ" ngay hôm nay để tiết kiệm thời gian, tối ưu hóa quy trình quản lý học tập và nâng cao trải nghiệm cho nhà trường!