---
title: "🚀 Tự động tạo ảnh AI tiết kiệm chi phí với BananaAPI và Nano Banana Engine trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp BananaAPI để tự động tạo và chỉnh sửa ảnh AI bằng Nano Banana Engine thông qua biểu mẫu trực tuyến với chi phí siêu rẻ chỉ $0.025/ảnh."
slug: "tu-dong-tao-anh-ai-banana-api-nano-banana-n8n"
tags: [n8n, automation, ai-image-generation, banana-api, no-code]
keywords: [n8n workflow, tạo ảnh ai tự động, banana api, nano banana engine, ai image generator n8n]
---

# 🚀 Tự động tạo ảnh AI tiết kiệm chi phí với BananaAPI và Nano Banana Engine

Các nhà sáng tạo nội dung, marketer và lập trình viên thường đối mặt với bài toán chi phí đắt đỏ từ các dịch vụ tạo ảnh AI truyền thống (như phí thuê bao hàng tháng dù dùng ít hay nhiều). Việc tạo ảnh thủ công qua web cũng làm gián đoạn quy trình làm việc tự động.

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp xây dựng một workflow n8n hoàn chỉnh, cho phép người dùng nhập prompt qua **Form**, hệ thống tự động gọi **BananaAPI** sử dụng **Google Nano Banana Engine** để xử lý, kiểm tra trạng thái lặp lại thông minh và trả về link ảnh hoàn chỉnh chỉ với chi phí cực rẻ **$0.025/ảnh** mà không lo hết hạn credit.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu chi phí tuyệt đối:** Chỉ $0.025/ảnh, hình thức trả phí theo lượt dùng (pay-as-you-go), credit không bao giờ hết hạn.
- **Tự động hóa 100%:** Người dùng chỉ cần điền form, hệ thống tự động xử lý từ khâu gửi yêu cầu, chờ đợi đến khi hoàn thành và trả kết quả.
- **Hỗ trợ đa dạng:** Cho phép tùy chỉnh kích thước ảnh (16:9, 1:1, 9:16...), định dạng file (PNG, JPEG) và đính kèm ảnh gốc để AI biến đổi/chỉnh sửa.
- **Cơ chế lặp thông minh:** Node **If** kết hợp **Wait** giúp kiểm tra liên tục trạng thái xử lý của AI mà không làm nghẽn hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **BananaAPI.com** và lấy **API key (Bearer token)** tại [bananaapi.com/api](https://bananaapi.com/api).
- Kiến thức cơ bản về câu lệnh Prompt AI để tạo ra những bức ảnh chất lượng cao.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ kho lưu trữ n8n (Link gốc: [n8n Workflow #8375](https://n8n.io/workflows/8375)), sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON dán vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính được liên kết chặt chẽ. Các sếp cần chú ý các điểm sau:

- **Form — Get Prompt (`formTrigger`):** 
  - Biểu mẫu này cấu hình sẵn các trường thu thập thông tin từ người dùng: `api_token` (để xác thực), `prompt` (mô tả ảnh), `Output Format` (PNG/JPEG), `Image Size` (tỷ lệ khung hình) và các trường `image_url` tùy chọn nếu muốn dùng ảnh gốc để edit.
- **Submit — Banana API (`httpRequest`):**
  - **Method:** `POST`
  - **URL:** `https://bananaapi.com/api/n8n/generate/`
  - **Headers:** Cấu hình `Content-Type: application/json` và `Authorization: Bearer {{ $json.api_token }}`.
  - **Body:** Đảm bảo truyền đúng các thông số từ form sang (prompt, image_size, output_format, image_urls). Node này sẽ trả về một `taskId` dùng để theo dõi tiến trình.
- **Wait 5s & Check Status (`wait` & `httpRequest`):**
  - Node **Wait 5s** tạo khoảng trễ trước khi gọi API kiểm tra trạng thái.
  - Node **Check Status** gửi request `GET` tới `https://bananaapi.com/api/n8n/image-status/{{ $json.taskId }}`.
- **If (`if`):**
  - Kiểm tra trạng thái trả về (`status`). Nếu chưa hoàn thành (`completed`), workflow sẽ đi qua vòng lặp **Wait 5s (loop)** và quay lại kiểm tra tiếp. Nếu đã hoàn thành, chuyển sang bước trả kết quả.
- **Return Links (`set`):**
  - Trích xuất và định dạng kết quả cuối cùng gồm: `image_url` (link ảnh hoàn thiện), `task_id` và `status`.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với dữ liệu mẫu bằng cách submit form thử nghiệm để đảm bảo hệ thống nhận prompt và trả về link ảnh chính xác.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook Response:** Thay vì chỉ trả về qua node Set mặc định, các sếp có thể gắn thêm node Webhook Response để trả dữ liệu JSON trực tiếp về giao diện Frontend/App của riêng mình.
- **Gửi thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn link ảnh vừa tạo trực tiếp về nhóm chat của team.
- **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử prompt và link ảnh tạo ra phục vụ việc tra cứu sau này.
- **Điều chỉnh thời gian chờ:** Nếu các bức ảnh phức tạp mất nhiều thời gian hơn, hãy tăng thời gian ở các node **Wait** lên 8-10 giây để giảm tải số lượng request kiểm tra trạng thái.

### 📌 Kết luận
Với sự kết hợp mượt mà giữa n8n, BananaAPI và Nano Banana Engine, các sếp đã có ngay một xưởng sản xuất ảnh AI tự động với chi phí cực kỳ tối ưu. Hãy triển khai ngay hôm nay để tự động hóa quy trình sáng tạo nội dung hình ảnh cho doanh nghiệp của mình!