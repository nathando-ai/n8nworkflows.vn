---
title: "🚀 Tự động tạo và chỉnh sửa ảnh chuyên nghiệp với Simbrams Ri AI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Simbrams Ri AI trên Replicate để tự động hóa quy trình tạo ảnh và Inpainting (chỉnh sửa cục bộ) siêu thực."
slug: "tao-anh-realistic-inpainting-simbrams-ri-ai-n8n"
tags: [n8n, automation, ai-image-generation, replicate, inpainting]
keywords: [n8n workflow, simbrams ri ai, replicate api, inpainting ảnh, tự động hóa tạo ảnh ai]
---

# 🚀 Tự động tạo và chỉnh sửa ảnh chuyên nghiệp với Simbrams Ri AI trong n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải chỉnh sửa từng chi tiết nhỏ trên hình ảnh sản phẩm, thêm/bớt vật thể bằng các công cụ đồ họa thủ công vừa tốn thời gian, vừa đòi hỏi kỹ năng Photoshop phức tạp? Việc sản xuất hàng loạt hình ảnh quảng cáo cá nhân hóa theo cách truyền thống đang ngốn rất nhiều nguồn lực của doanh nghiệp.

Đừng lo, giải pháp ở đây rồi! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa hoàn toàn quy trình gọi API đến mô hình **Simbrams Ri AI** (thông qua Replicate) để thực hiện các tác vụ tạo ảnh và **Realistic Inpainting** (ghép/sửa ảnh thông minh) một cách mượt mà và không tốn một giọt mồ hôi thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến các yêu cầu đầu vào thành hình ảnh hoàn thiện thông qua API mà không cần thao tác tay.
- **Inpainting chuẩn xác:** Xử lý các yêu cầu chỉnh sửa cục bộ, ghép đối tượng vào ảnh gốc một cách siêu thực.
- **Tối ưu thời gian:** Rút ngắn thời gian sản xuất nội dung visual từ vài giờ xuống chỉ còn vài giây.
- **Linh hoạt mở rộng:** Dễ dàng tích hợp thêm vào các hệ thống CRM, Telegram, Google Sheets hoặc Web App sẵn có của công ty.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đã sẵn sàng (Self-hosted hoặc n8n Cloud).
- Tài khoản trên **Replicate** và lấy **Replicate API Key** (dùng để gọi mô hình `simbrams/ri`).
- Hình ảnh gốc (image) và vùng mặt nạ (mask) chuẩn bị sẵn để thực hiện inpainting.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, sau đó dán trực tiếp vào giao diện n8n Editor của mình (hoặc chọn Import từ file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 8 nodes được bố trí mạch lạc giúp xử lý vòng lặp gọi API bất đồng bộ:
- **On clicking 'execute' (`manualTrigger`):** Điểm khởi chạy thủ công để test workflow. Các sếp có thể thay thế bằng Webhook hoặc Schedule Trigger nếu muốn chạy tự động.
- **Set API Key (`set`):** Nơi các sếp cấu hình thông tin xác thực, bao gồm Replicate API Key và các thông số đầu vào (prompt, link ảnh gốc, link mask).
- **Create Prediction (`httpRequest`):** Node gửi request POST tới Replicate để khởi tạo tiến trình tạo/sửa ảnh với mô hình `simbrams/ri`.
- **Extract Prediction ID (`code`):** Node JavaScript nhỏ giúp bóc tách mã ID của tiến trình (`prediction_id`) từ kết quả trả về để chuẩn bị kiểm tra trạng thái.
- **Wait (`wait`):** Tạm dừng luồng trong giây lát (ví dụ: vài giây) để AI có thời gian xử lý bức ảnh ở phía server.
- **Check Prediction Status (`httpRequest`):** Gửi request GET kiểm tra xem AI đã render xong bức ảnh hay chưa.
- **Check If Complete (`if`):** Kiểm tra điều kiện xem trạng thái tiến trình đã là `succeeded` hay chưa. Nếu chưa, luồng có thể quay lại chờ tiếp; nếu rồi, chuyển sang bước xử lý kết quả.
- **Process Result (`code`):** Nhận kết quả cuối cùng, trích xuất đường dẫn URL hình ảnh hoàn chỉnh để các sếp tải về hoặc gửi đi các nền tảng khác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu và kiểm tra kết quả trả về ở node cuối cùng.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** sau node *Process Result* để hệ thống tự động bắn ảnh vừa tạo về nhóm chat ngay khi hoàn tất.
- **Lưu trữ tự động:** Kết hợp thêm node **Google Drive** hoặc **Supabase** để lưu trữ file ảnh gốc kết quả thay vì phụ thuộc vào link tạm thời của Replicate.
- **Mở rộng quy mô:** Chuyển đổi Trigger thành *Webhook* để nhận yêu cầu tạo ảnh từ các trang web bán hàng hoặc ứng dụng của khách hàng.

### 📌 Kết luận
Workflow sử dụng mô hình Simbrams Ri AI trên Replicate là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình sản xuất hình ảnh bằng AI trong n8n. Hãy áp dụng ngay vào hệ thống của các sếp để nâng tầm tự động hóa và tiết kiệm chi phí vận hành nhé!