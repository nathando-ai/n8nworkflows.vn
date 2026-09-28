---
title: "🚀 Tự động hóa tạo ảnh AI với Replicate Lemaar Door Mockedup trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng và triển khai workflow n8n tích hợp Replicate API để tự động tạo và xử lý hình ảnh AI mô phỏng cửa thông minh một cách chuyên nghiệp."
slug: "tu-dong-hoa-tao-anh-ai-replicate-lemaar-door-mockedup-n8n"
tags: [n8n, automation, replicate, ai-image-generation, no-code, multimodal-ai]
keywords: [n8n workflow, tạo ảnh AI, Replicate API, Lemaar Door Mockedup, tự động hóa n8n]
---

# 🚀 Tự động hóa tạo ảnh AI với Replicate Lemaar Door Mockedup trên n8n

Các sếp có đang gặp khó khăn trong việc phải thủ công tạo, kiểm tra và chờ đợi các mô hình AI xử lý hình ảnh phức tạp? Quy trình thủ công này không chỉ ngốn rất nhiều thời gian mà còn dễ phát sinh lỗi khi gọi API. 

Giải pháp được đưa ra ở đây là một **n8n Workflow hoàn chỉnh** giúp tự động hóa toàn bộ quá trình gửi yêu cầu, theo dõi trạng thái xử lý (polling loop) và nhận kết quả từ mô hình AI **Replicate Lemaar Door Mockedup** mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Loại bỏ hoàn toàn thao tác thủ công khi gọi API tạo ảnh từ Replicate.
- **Cơ chế thông minh (Polling Loop)**: Tự động chờ và kiểm tra trạng thái tiến trình (prediction status) cho đến khi hoàn thành hoặc báo lỗi.
- **Xử lý lỗi mạnh mẽ**: Có sẵn các nhánh phân tách thành công/thất bại và ghi log (logging) chi tiết giúp dễ dàng debug.
- **Sẵn sàng mở rộng**: Dễ dàng tích hợp thêm các bước gửi kết quả về Telegram, Slack, Google Drive hay Email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản [Replicate](https://replicate.com) và **Replicate API Token** hợp lệ (đã nạp credit để chạy model).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) -> **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 13 nodes chính để thực hiện quy trình vòng lặp gọi API. Các sếp cần chú ý cấu hình các node quan trọng sau:

- **Set API Token**: 
  - Chọn node này và thay thế chuỗi `'YOUR_REPLICATE_API_TOKEN'` bằng **API Token thực tế** lấy từ tài khoản Replicate của các sếp.
- **Set Other Parameters**: 
  - Nơi thiết lập các tham số đầu vào cho mô hình `creativeathive/lemaar-door-mockedup`. 
  - Các sếp có thể tùy chỉnh tham số `prompt`, kích thước (`width`, `height`), hoặc truyền thêm `image`/`mask` nếu muốn chạy chế độ Image-to-Image / Inpainting.
- **Create Other Prediction** & **Check Status** (HTTP Request nodes):
  - Kiểm tra lại endpoint gọi tới Replicate API (`https://api.replicate.com/v1/predictions`) đảm bảo đã truyền đúng Header xác thực chứa API Token ở trên.
- **Wait 5s** & **Wait 10s**: 
  - Các node chờ nhịp nhàng giúp tránh việc gọi liên tục quá nhiều lần (rate limit) trong lúc chờ AI render ảnh.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** thông qua **Manual Trigger** để test chạy thử với các tham số mặc định.
- Theo dõi kết quả trả về ở node **Display Result** hoặc **Success Response**.
- Khi mọi thứ chạy trơn tru, hãy chuyển trạng thái workflow sang **Active** để sẵn sàng sử dụng lâu dài.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Nối thêm node Telegram hoặc Slack sau node **Success Response** để nhận ngay hình ảnh AI vừa tạo về thẳng điện thoại hoặc nhóm chat làm việc.
- **Lưu trữ tự động**: Kết nối kết quả URL hình ảnh vào Google Drive hoặc Notion để lưu trữ kho tài nguyên thiết kế của doanh nghiệp.
- **Tạo Webhook Trigger**: Thay thế **Manual Trigger** bằng **Webhook Trigger** để có thể gọi quy trình tạo ảnh này từ một ứng dụng bên ngoài hoặc website của các sếp.

### 📌 Kết luận
Workflow tích hợp Replicate AI với n8n này là một cỗ máy tự động tuyệt vời giúp tiết kiệm thời gian xử lý đồ họa và tối ưu hóa quy trình làm việc với AI. Hãy cài đặt ngay hôm nay để trải nghiệm sức mạnh tự động hóa không giới hạn!