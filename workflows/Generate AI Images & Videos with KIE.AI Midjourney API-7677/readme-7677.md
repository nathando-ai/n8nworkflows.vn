---
title: "🚀 Tự Động Tạo Ảnh & Video AI Bằng KIE.AI Midjourney API Trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp KIE.AI Midjourney API giúp tạo ảnh và video tự động qua giao diện Form với 3 chế độ text-to-image, image-to-image và image-to-video."
slug: "tao-anh-video-ai-kie-ai-midjourney-api-n8n"
tags: [n8n, automation, ai-generation, midjourney, kie-ai, text-to-image, image-to-video]
keywords: [n8n workflow, KIE.AI API, tạo ảnh AI, tạo video AI, text-to-image, image-to-video, tự động hóa n8n]
---

# 🚀 Tự Động Tạo Ảnh & Video AI Bằng KIE.AI Midjourney API Trên n8n

Việc tạo nội dung hình ảnh và video thủ công bằng các công cụ AI thường tốn rất nhiều thời gian chuyển đổi giữa các nền tảng, quản lý prompt và theo dõi tiến trình xử lý. Đối với các nhà sáng tạo nội dung, marketer hay designer, việc lặp đi lặp lại các thao tác này làm giảm hiệu suất đáng kể.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách cung cấp một giao diện Form trực quan. Các sếp chỉ cần nhập yêu cầu, hệ thống sẽ tự động gọi **KIE.AI Midjourney API**, theo dõi trạng thái xử lý theo thời gian thực và trả về kết quả hoàn chỉnh mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Loại bỏ hoàn toàn các thao tác thủ công, tập trung vào sáng tạo nội dung.
- **Đa dạng chế độ**: Hỗ trợ 3 tính năng mạnh mẽ gồm Text-to-Image (`mj_txt2img`), Image-to-Image (`mj_img2img`) và Image-to-Video (`mj_video` / `mj_video_hd`).
- **Giám sát thời gian thực**: Hệ thống tự động kiểm tra trạng thái xử lý mỗi 10 giây và hiển thị kết quả ngay khi hoàn tất.
- **Giao diện thân thiện**: Người dùng cuối chỉ cần thao tác qua một form web đơn giản, không đòi hỏi kỹ năng kỹ thuật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Một môi trường n8n đang hoạt động (Cloud hoặc Self-hosted).
- **KIE.AI Account**: Đăng ký tài khoản tại [KIE.AI](https://kie.ai/) để lấy API Key sử dụng cho việc xác thực.
- **Reference Images** (Tùy chọn): Link ảnh công khai nếu sử dụng tính năng Image-to-Image hoặc Image-to-Video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở giao diện n8n Editor, chọn **Import from File** hoặc dán (Paste) trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các phần sau:

- **Submit Text Prompt for Video Generation (`formTrigger`)**: 
  - Node này tạo giao diện form cho người dùng nhập liệu. Các sếp cần đảm bảo các trường dữ liệu thu thập bao gồm:
    - `tasktype`: Chọn chế độ tạo (`mj_txt2img`, `mj_img2img`, `mj_video`, `mj_video_hd`).
    - `prompt`: Đoạn mô tả chi tiết nội dung cần tạo.
    - `imgurl`: Đường dẫn ảnh gốc (Bắt buộc với Image-to-Image/Video, để trống nếu dùng Text-to-Image).
    - `api_key`: Khóa API cá nhân lấy từ KIE.AI.

- **Send Video Generation Request to KIE.AI API (`httpRequest`)**:
  - Cấu hình phương thức gọi API đến endpoint của KIE.AI.
  - Sử dụng thông tin từ `formTrigger` (bao gồm `api_key` và các tham số prompt/tasktype) vào phần Header hoặc Body của request.

- **Wait for Video Processing Completion (`wait`)**:
  - Cấu hình thời gian chờ giữa các lần kiểm tra (mặc định thiết lập kiểm tra định kỳ để tránh quá tải API).

- **Obtain the generated status (`httpRequest`)**:
  - Node này gọi API kiểm tra tiến độ xử lý của tác vụ AI dựa trên ID trả về từ bước khởi tạo.

- **Check if Video Generation is Complete (`if`)**:
  - Thiết lập điều kiện kiểm tra xem trạng thái trả về từ KIE.AI đã ở trạng thái "Success" hay chưa. Nếu chưa, vòng lặp sẽ tiếp tục chờ; nếu rồi, chuyển sang bước hiển thị kết quả.

- **Format and Display Video Results (`set`)**:
  - Chuẩn hóa cấu trúc dữ liệu đầu ra để hiển thị link hình ảnh hoặc video thành phẩm trực quan cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu từ Form.
- Kiểm tra xem API KIE.AI có phản hồi chính xác không.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo**: Kết hợp thêm node Telegram hoặc Slack để gửi thông báo trực tiếp về máy cá nhân ngay khi video/ảnh được render xong.
- **Tối ưu Prompt**: Hướng dẫn đội ngũ viết prompt chi tiết, kết hợp mô tả về ánh sáng (dramatic, neon), góc máy (close-up, wide shot) và phong cách nghệ thuật (cinematic, anime) để đạt chất lượng AI tốt nhất.
- **Lưu trữ tự động**: Thêm node Google Drive hoặc S3 để tự động tải các file media được tạo ra và lưu trữ lâu dài.

### 📌 Kết luận
Workflow tích hợp KIE.AI Midjourney API trên n8n là giải pháp tự động hóa toàn diện giúp tiết kiệm hàng giờ đồng hồ thao tác thủ công. Hãy áp dụng ngay để tối ưu hóa quy trình sáng tạo nội dung hình ảnh và video cho doanh nghiệp của các sếp!