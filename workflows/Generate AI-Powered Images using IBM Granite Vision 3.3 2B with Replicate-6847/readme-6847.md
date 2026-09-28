---
title: "🚀 Tạo nội dung trực quan thông minh với IBM Granite Vision 3.3 2B và Replicate trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình xử lý hình ảnh và văn bản đa phương thức bằng mô hình IBM Granite Vision qua Replicate API."
slug: "tao-anh-ai-ibm-granite-vision-replicate-n8n"
tags: [n8n, automation, replicate, ai-agents, content-creation]
keywords: [n8n workflow, ibm granite vision, replicate api, ai image generation, tu dong hoa n8n]
---

# 🚀 Tự động hóa xử lý ảnh & nội dung đa phương thức với IBM Granite Vision 3.3 2B & Replicate

Chào các sếp! Việc phân tích tài liệu trực quan, biểu đồ, bảng biểu hoặc tạo nội dung từ hình ảnh thủ công thường tốn rất nhiều thời gian và dễ xảy ra sai sót. Hiểu được nỗi đau đó, workflow n8n này sẽ giúp các sếp tự động hóa hoàn toàn quy trình kết nối với mô hình **IBM Granite Vision 3.3 2B** thông qua **Replicate API**, giúp xử lý các tác vụ AI đa phương thức (Multimodal AI) một cách mượt mà, chuyên nghiệp và không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gửi yêu cầu, theo dõi trạng thái và nhận kết quả tự động mà không cần can thiệp thủ công.
- **Xử lý thông minh:** Tận dụng sức mạnh của mô hình IBM Granite Vision để hiểu tài liệu, bảng biểu, biểu đồ và hình ảnh.
- **Cơ chế retry thông minh:** Hệ thống tự động chờ và kiểm tra trạng thái dự đoán (prediction) cho đến khi hoàn thành hoặc báo lỗi.
- **Sẵn sàng triển khai:** Tích hợp sẵn các node log yêu cầu, xử lý lỗi chi tiết giúp dễ dàng debug và phát triển mở rộng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Replicate Account:** Tài khoản tại [Replicate](https://replicate.com) kèm theo **API Token** cá nhân.
- **Workflow Template:** File JSON của workflow do chuyên gia Yaron Been thiết kế.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` / `Cmd+V` để dán trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes được cấu hình sẵn, các sếp cần chú ý cấu hình các node quan trọng sau:
- **Set API Token**: 
  - Mở node này và thay thế chuỗi `'YOUR_REPLICATE_API_TOKEN'` bằng mã API Token thực tế lấy từ tài khoản Replicate của các sếp.
- **Set Image Parameters**:
  - Tùy chỉnh các tham số đầu vào cho mô hình như `prompt`, `images` (đường dẫn hình ảnh cần phân tích), `max_tokens`, `temperature`,... theo nhu cầu thực tế của dự án.
- **Vòng lặp kiểm tra (Create Image Prediction -> Wait 5s -> Check Status -> Is Complete?)**:
  - Node `Create Image Prediction` sẽ gửi request lên Replicate API và trả về một `prediction ID`.
  - Các node `Wait` và `Check Status` (HTTP Request) sẽ thực hiệnpolling liên tục để cập nhật tiến độ xử lý của AI cho đến khi hoàn tất.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Manual Trigger** để chạy thử nghiệm (Test run) với dữ liệu mẫu.
- Kiểm tra kết quả trả về ở node `Display Result` hoặc kiểm tra log tại node `Log Request`.
- Sau khi test chạy mượt mà, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp, các sếp có thể mở rộng thêm:
- **Tích hợp Thông báo:** Kết nối thêm node **Telegram** hoặc **Slack** để gửi kết quả phân tích hình ảnh ngay lập tức về nhóm chat khi hoàn tất.
- **Lưu trữ dữ liệu:** Đẩy kết quả trả về (Response URL/Text) trực tiếp vào **Google Sheets** hoặc **Airtable** để làm báo cáo định kỳ.
- **Nhận diện tự động:** Kết hợp thêm Webhook Trigger để nhận ảnh từ người dùng gửi lên qua Form hoặc Zalo/Messenger, biến workflow này thành một trợ lý AI thực thụ.

### 📌 Kết luận
Với workflow tích hợp **IBM Granite Vision 3.3 2B và Replicate**, các sếp đã sở hữu ngay một hệ thống xử lý ảnh và thị giác máy tính tự động cực kỳ mạnh mẽ. Chúc các sếp ứng dụng thành công và hẹn gặp lại ở các bài hướng dẫn tự động hóa tiếp theo!