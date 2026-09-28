---
title: "🚀 Tự Động Tạo Mô Hình 3D Từ Hình Ảnh Bằng AI Hunyuan3D và Replicate trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình biến hình ảnh 2D thành mô hình 3D chất lượng cao sử dụng AI Hunyuan3D qua Replicate API."
slug: "tao-mo-hinh-3d-tu-hinh-anh-hunyuan3d-replicate-n8n"
tags: [n8n, automation, ai, 3d-modeling, replicate, hunyuan3d, content-creation]
keywords: [n8n workflow, tao mo hinh 3d ai, hunyuan3d replicate, tu dong hoa 3d, n8n viet nam]
---

# 🚀 Tự Động Tạo Mô Hình 3D Từ Hình Ảnh Bằng AI Hunyuan3D và Replicate

Các sếp có bao giờ gặp khó khăn khi phải thuê designer dựng hình 3D thủ công từ các bản vẽ 2D hoặc ảnh sản phẩm, vừa tốn kém chi phí lại mất rất nhiều thời gian? Việc chuyển đổi hình ảnh thành tài sản 3D (3D assets) giờ đây đã trở nên đơn giản và tự động hóa hoàn toàn với sức mạnh của AI.

Bài viết này sẽ hướng dẫn các sếp cách triển khai một workflow n8n cực kỳ mạnh mẽ, tận dụng mô hình **Hunyuan3D** thông qua **Replicate API** để tự động "biến" ảnh 2D thành mô hình 3D chỉ trong nháy mắt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ AI nặng và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chuyển đổi file ảnh sản phẩm hoặc bản vẽ thành mô hình 3D mà không cần can thiệp thủ công.
- **Tiết kiệm chi phí:** Cắt giảm đáng kể ngân sách thuê thiết kế 3D cho cácự án thương mại điện tử, game hoặc AR/VR.
- **Quy trình thông minh:** Workflow tự động gửi yêu cầu, kiểm tra trạng thái xử lý (polling) và trả về kết quả khi hoàn thành.
- **Tích hợp linh hoạt:** Dễ dàng mở rộng kết nối với Google Drive, Telegram hoặc hệ thống CRM để lưu trữ và gửi file 3D cho khách hàng/đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Replicate** và **Replicate API Token** để gọi mô hình AI `ndreca/hunyuan3d-2-test`.
- Hình ảnh đầu vào (định dạng JPG/PNG) sắc nét, rõ chủ thể để AI nhận diện tốt nhất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy đoạn mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm 8 nodes được tối ưu sẵn từ khâu kích hoạt, gọi API, chờ xử lý cho đến trích xuất kết quả.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **On clicking 'execute' (`manualTrigger`):** Node kích hoạt thủ công để kiểm tra (có thể thay thế bằng Webhook hoặc Schedule Trigger nếu muốn tự động hóa hàng loạt).
- **Set API Key (`set`):** Nơi các sếp cấu hình Replicate API Key của mình. Hãy tạo một biến chứa API Key để các node gọi HTTP phía sau dễ dàng xác thực.
- **Create Prediction (`httpRequest`):** Node gửi request đến Replicate API sử dụng mô hình `ndreca/hunyuan3d-2-test`. Tại đây, các sếp cần truyền link hình ảnh đầu vào (`image`) vào phần body của request.
- **Extract Prediction ID (`code`):** Node JavaScript xử lý phản hồi từ Replicate, bóc tách lấy `Prediction ID` để phục vụ cho việc theo dõi tiến trình.
- **Wait (`wait`):** Do việc tạo mô hình 3D mất một khoảng thời gian nhất định (vài giây đến vài phút tùy AI), node này đóng vai trò tạm dừng workflow trong giây lát trước khi kiểm tra lại trạng thái.
- **Check Prediction Status (`httpRequest`):** Node gọi lại API của Replicate dựa trên `Prediction ID` để cập nhật trạng thái render 3D (đang xử lý hay đã hoàn thành).
- **Check If Complete (`if`):** Kiểm tra xem mô hình 3D đã render xong chưa. Nếu chưa, vòng lặp sẽ quay lại trạng thái chờ; nếu rồi, chuyển sang bước lấy kết quả.
- **Process Result (`code`):** Node trích xuất đường dẫn tải xuống (download URL) của file mô hình 3D hoàn chỉnh để các sếp sử dụng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một hình ảnh mẫu để test thử quá trình gọi API và nhận kết quả.
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động gửi file về Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối workflow để bot tự động gửi file mô hình 3D trực tiếp cho các sếp ngay khi xử lý xong.
- **Lưu trữ đám mây:** Kết nối thêm node Google Drive hoặc AWS S3 để tự động tải file 3D về kho lưu trữ riêng của doanh nghiệp.
- **Xử lý hàng loạt (Batch Processing):** Thay thế Manual Trigger bằng Google Sheets Trigger để tự động quét danh sách link ảnh và dựng hình 3D hàng loạt.

### 📌 Kết luận
Workflow tích hợp Hunyuan3D qua Replicate này là một "vũ khí" cực kỳ lợi hại giúp các sếp tối ưu hóa quy trình sản xuất nội dung 3D, ứng dụng mạnh mẽ trong thương mại điện tử và thiết kế. Hãy cài đặt ngay lên hệ thống n8n của các sếp và trải nghiệm sức mạnh của AI ngay hôm nay!