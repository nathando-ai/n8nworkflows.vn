---
title: "🚀 Tự động hóa tạo video AI cực đỉnh từ văn bản và hình ảnh với Seedance 1 Lite trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng và vận hành workflow n8n tích hợp AI Bytedance Seedance 1 Lite qua Replicate để tạo video tự động từ text hoặc image."
slug: "tao-video-ai-tu-dong-seedance-1-lite-n8n"
tags: [n8n, automation, ai-video, replicate, bytedance, content-creation]
keywords: [n8n workflow, seedance 1 lite, ai video generator, replicate api, tu dong hoa tao video, bytedance seedance]
---

# 🚀 Tự động hóa tạo video AI cực đỉnh từ văn bản và hình ảnh với Seedance 1 Lite

Các sếp có đang cảm thấy mệt mỏi và tốn quá nhiều thời gian khi phải tạo từng đoạn video ngắn thủ công cho các chiến dịch marketing, TikTok hay Reels không? Việc thuê Editor hoặc tự mày mò trên các công cụ trả phí vừa tốn kém lại khó scale số lượng lớn.

Đừng lo, trong bài viết này, tôi sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ mạnh mẽ do chuyên gia Yaron Been thiết kế. Workflow này sẽ kết nối trực tiếp với mô hình **Bytedance Seedance 1 Lite** thông qua Replicate API, giúp các sếp tự động hóa 100% quy trình biến văn bản (Text-to-Video) hoặc hình ảnh (Image-to-Video) thành những thước phim AI sống động mà không cần tốn một giọt mồ hôi code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập câu lệnh (prompt) hoặc hình ảnh gốc, AI sẽ tự động lo phần việc nặng nhọc còn lại.
- **Tiết kiệm chi phí khủng:** Tận dụng Replicate API với mô hình Seedance 1 Lite giá rẻ nhưng chất lượng cực cao từ Bytedance.
- **Quy trình chuẩn hóa:** Workflow tích hợp sẵn cơ chế chờ (Wait) và kiểm tra trạng thái (Status Check) thông minh, đảm bảo không bị lỗi timeout khi render video.
- **Dễ dàng mở rộng:** Có thể kết hợp thêm Google Sheets để đọc danh sách prompt hàng loạt hoặc bắn kết quả trực tiếp về Telegram/Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản trên **Replicate** và lấy sẵn **Replicate API Token**.
- Prompt mô tả nội dung video hoặc link hình ảnh đầu vào (nếu dùng tính năng Image-to-Video).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n chính thức (Template ID: `7098`) hoặc copy đoạn JSON tương ứng để paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 8 nodes được sắp xếp cực kỳ khoa học. Các sếp cần chú ý cấu hình các node sau:

- **Node `Set API Key`**: 
  - Đây là nơi lưu trữ thông tin xác thực. Các sếp cần thay thế giá trị khóa API mẫu bằng **Replicate API Key** chính chủ của mình.
- **Node `Create Prediction` (HTTP Request)**: 
  - Kiểm tra lại endpoint gọi API tới Replicate cho mô hình `bytedance/seedance-1-lite`. 
  - Tại phần Body, tùy chỉnh tham số `prompt` (và `image` nếu muốn làm dạng Image-to-Video) theo nhu cầu thực tế của chiến dịch.
- **Node `Extract Prediction ID` (Code)** và **Node `Wait`**: 
  - Node Code sẽ bóc tách mã định danh (ID) của tiến trình render video từ phản hồi của Replicate. 
  - Node Wait đóng vai trò tạm dừng một khoảng thời gian ngắn (ví dụ: 5-10 giây) trước khi chuyển sang bước kiểm tra tiếp theo để tránh làm quá tải hệ thống.
- **Node `Check Prediction Status` (HTTP Request)** & **Node `Check If Complete` (If)**: 
  - Hệ thống sẽ liên tục hỏi trạng thái render video của Replicate. Nếu hoàn tất (`succeeded`), luồng sẽ đi tiếp; nếu chưa, vòng lặp sẽ tiếp tục chờ cho đến khi xong.
- **Node `Process Result` (Code)**: 
  - Xử lý kết quả trả về, lấy đường dẫn (URL) video hoàn chỉnh để các sếp có thể dễ dàng tải xuống hoặc chuyển tiếp sang các ứng dụng khác.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`On clicking 'execute'` (Manual Trigger)** để chạy thử nghiệm (Test Run) với một prompt mẫu xem video render ra có mượt mà hay không.
- Sau khi test thành công, hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Google Sheets:** Thay vì nhập prompt thủ công bằng tay, các sếp có thể tạo một bảng Google Sheets chứa danh sách hàng trăm ý tưởng video và cho n8n quét qua từng dòng một.
- **Nhận thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để khi video render xong, hệ thống sẽ tự động gửi link video trực tiếp về điện thoại cho các sếp kiểm duyệt ngay lập tức.
- **Lưu trữ tự động:** Tự động đẩy file video hoàn thành lên Google Drive hoặc OneDrive để làm kho tư liệu truyền thông dài hạn.

### 📌 Kết luận
Việc ứng dụng AI vào sản xuất nội dung video chưa bao giờ dễ dàng và tối ưu chi phí đến thế. Với workflow n8n tích hợp Seedance 1 Lite này, các sếp hoàn toàn có thể xây dựng một "xưởng sản xuất video tự động" cho riêng mình chỉ trong vòng vài nốt nhạc. Hãy bắt tay vào cài đặt ngay hôm nay để tối ưu hóa sức mạnh của tự động hóa và AI nhé!