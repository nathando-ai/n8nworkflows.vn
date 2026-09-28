---
title: "🚀 Tự động tạo ảnh AI mô phỏng cửa thông minh với Replicate và n8n"
description: "Hướng dẫn cấu hình workflow n8n tích hợp Replicate AI để tự động hóa quy trình tạo ảnh mockup cửa thông minh (Lemaar Door Mockedup) cực kỳ nhanh chóng và chuyên nghiệp."
slug: "tu-dong-tao-anh-ai-replicate-lemaar-door-n8n"
tags: [n8n, automation, no-code, replicate, ai-image-generation, content-creation]
keywords: [n8n workflow, tạo ảnh ai replicate, lemaar door mockedup, tự động hóa n8n, ai image generation]
---

# 🚀 Tự động tạo ảnh AI mô phỏng cửa thông minh với Replicate và n8n

Trong kỷ nguyên sáng tạo nội dung số, việc tạo ra các hình ảnh mockup trực quan, độc đáo cho sản phẩm (đặc biệt là nội thất, cửa thông minh) thường tốn rất nhiều thời gian và chi phí thiết kế thủ công. Nếu các sếp đang tìm giải pháp tự động hóa quy trình này bằng AI, workflow n8n tích hợp mô hình **Replicate's Lemaar Door Mockedup** chính là "vũ khí tối thượng".

Workflow này giúp các sếp kết nối trực tiếp với API của Replicate, gửi yêu cầu tạo ảnh (prompt), theo dõi tiến trình xử lý và nhận lại kết quả hoàn toàn tự động mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gửi yêu cầu và nhận kết quả ảnh AI từ Replicate trực tiếp trong n8n.
- **Tiết kiệm thời gian & chi phí:** Loại bỏ hoàn toàn các bước thao tác thủ công trên giao diện web của Replicate, tối ưu hóa quy trình làm việc cho đội ngũ Marketing/Design.
- **Quy trình thông minh:** Tự động kiểm tra trạng thái xử lý (Polling mechanism) cho đến khi ảnh được tạo thành công.
- **Dễ dàng mở rộng:** Dễ dàng tích hợp thêm các bước lưu trữ vào Google Drive, gửi về Slack/Telegram hoặc đăng trực tiếp lên mạng xã hội.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản trên **Replicate** và lấy **Replicate API Key**.
- Workflow mẫu từ tác giả Yaron Been (*Creativeathive Lemaar Door Mockedup AI Generator*).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n (ID: `6889`) hoặc copy trực tiếp mã nguồn JSON và paste vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes được tối ưu hóa cho tác vụ gọi API bất đồng bộ. Các sếp cần chú ý cấu hình các node sau:

- **Set API Key (`Set API Key` - Node loại `set`):**
  - Điền Replicate API Key của các sếp vào đây dưới dạng biến để các node HTTP Request có thể gọi dữ liệu xác thực.
- **Gửi yêu cầu tạo ảnh (`Create Prediction` - Node loại `httpRequest`):**
  - Cấu hình endpoint gọi tới model `creativeathive/lemaar-door-mockedup` trên Replicate.
  - Truyền tham số `prompt` (mô tả chi tiết loại cửa hoặc bối cảnh các sếp muốn AI vẽ).
- **Trích xuất ID (`Extract Prediction ID` - Node loại `code`):**
  - Node này dùng mã Javascript nhỏ để lấy `prediction_id` từ kết quả trả về của bước khởi tạo, phục vụ cho việc kiểm tra trạng thái.
- **Vòng lặp kiểm tra (`Wait` & `Check Prediction Status` & `Check If Complete`):**
  - Node `Wait` giúp tạo độ trễ hợp lý trước khi gọi lại API kiểm tra.
  - Node `Check If Complete` (If Node) sẽ kiểm tra xem ảnh đã render xong chưa (`succeeded`). Nếu chưa, vòng lặp sẽ tiếp tục; nếu rồi, chuyển sang bước xử lý kết quả.
- **Xử lý kết quả (`Process Result` - Node loại `code`):**
  - Lấy đường dẫn URL hình ảnh hoàn chỉnh cuối cùng từ kết quả của Replicate.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** trên node `On clicking 'execute'` để test thử với prompt mặc định.
- Kiểm tra kết quả trả về ở node cuối cùng để đảm bảo link ảnh hoạt động tốt.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** ngay sau node `Process Result` để nhận ngay hình ảnh vừa tạo về điện thoại hoặc nhóm chat làm việc.
- **Lưu trữ tự động:** Kết hợp với node **Google Drive** hoặc **Supabase** để tải file ảnh về lưu trữ lâu dài thay vì chỉ dùng link tạm thời của Replicate.
- **Nhận prompt từ Google Sheets:** Thay thế trigger thủ công bằng Google Sheets Trigger để tạo hàng loạt ảnh mockup tự động từ danh sách prompt có sẵn.

### 📌 Kết luận
Workflow tạo ảnh AI mô phỏng cửa thông minh với Replicate là một giải pháp mẫu cực kỳ xuất sắc để tự động hóa các tác vụ Multimodal AI trong n8n. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình sáng tạo nội dung hình ảnh cho doanh nghiệp của các sếp!