---
title: "🚀 Tự động tạo Video Demo Highlight Reels với WayinVideo AI và n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động trích xuất các khoảnh khắc nổi bật từ video demo sản phẩm bằng WayinVideo Find Moments API và gửi email báo cáo."
slug: "tu-dong-tao-video-demo-highlight-reels-wayinvideo-n8n"
tags: [n8n, automation, no-code, ai-video, content-creation, wayinvideo]
keywords: [n8n workflow, tạo highlight video, WayinVideo API, tự động hóa marketing, AI multimodal]
---

# 🚀 Tự động tạo Video Demo Highlight Reels với WayinVideo AI

Đối với các team product marketer, sales, và content creator, việc phải tua đi tua lại các bản ghi demo dài để tìm ra những phân đoạn đắt giá luôn tốn rất nhiều thời gian. Nỗi đau này giờ đây được giải quyết triệt để với workflow n8n tích hợp **WayinVideo Find Moments API**. 

Chỉ cần điền URL video demo và câu lệnh (query) bằng tiếng Anh mô tả nội dung cần tìm, AI sẽ tự động quét toàn bộ bản ghi, trích xuất các phân đoạn khớp nhất và gửi một email định dạng chuyên nghiệp chứa tiêu đề, mốc thời gian, điểm mức độ phù hợp, mô tả chi tiết cùng link tải về cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian thủ công:** Không cần phải xem lại video demo hàng giờ liền để cắt ghép.
- **Chính xác tuyệt đối:** AI tự động tìm kiếm đúng phân đoạn theo đúng yêu cầu bằng ngôn ngữ tự nhiên.
- **Báo cáo trực quan qua Email:** Nhận ngay email tổng hợp với đầy đủ mốc thời gian, mô tả và link tải clip tiện lợi.
- **Tự động hóa hoàn toàn:** Hoạt động 24/7 từ lúc nhận form yêu cầu đến khi gửi kết quả hoàn thiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản và **API Key** từ **WayinVideo** (để gọi Find Moments API).
- Tài khoản **Gmail** (để cấu hình node gửi email tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **1. Form — Demo URL + Query + Email**: Nơi người dùng nhập URL video demo, tên sản phẩm, câu lệnh tìm kiếm khoảnh khắc và email nhận kết quả.
- **2. WayinVideo — Submit Find Moments** & **4. WayinVideo — Get Moments Result**: Thay thế đoạn `YOUR_WAYINVIDEO_API_KEY` bằng API Key thật của các sếp trong phần header `Authorization`.
- **3. Wait — 90 Seconds** & **6. Wait — 30 Seconds Retry**: Các node tạm dừng và lặp lại để chờ WayinVideo xử lý xong video.
- **5. IF — Status SUCCEEDED?**: Kiểm tra trạng thái xử lý, nếu thành công sẽ chuyển tiếp sang bước gửi email, nếu chưa sẽ tiếp tục vòng lặp chờ.
- **7. Gmail — Send Review Email**: Kết nối tài khoản Gmail của các sếp thông qua Google OAuth2 để gửi email chứa danh sách các video clip đã trích xuất.

#### 3. Kích hoạt ⚡️
- Thực hiện một lượt chạy thử (Test run) với dữ liệu mẫu từ Form để kiểm tra toàn bộ luồng.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tránh vòng lặp vô hạn (Infinite Loop):** Nếu WayinVideo không trả về trạng thái `SUCCEEDED` (do URL lỗi, video riêng tư...), workflow có thể bị kẹt ở node 4 và 6. Các sếp nên bổ sung một biến đếm số lần thử (retry counter) và thêm một node IF để dừng lại sau 10 lần, sau đó gửi email báo lỗi.
- **Lưu trữ lâu dài:** Các liên kết tải về (`export_link`) trong email chỉ có hiệu lực trong **24 giờ**. Các sếp có thể chèn thêm node **Google Drive** hoặc **Cloudinary** trước node Gmail để lưu trữ file vĩnh viễn.
- **Mở rộng thông báo:** Kết hợp thêm node **Slack** hoặc **Telegram** để bắn thông báo ngay khi AI tìm xong các khoảnh khắc demo.

### 📌 Kết luận
Workflow tự động hóa tạo Demo Highlight Reels này là một "vũ khí" cực mạnh giúp tối ưu hóa quy trình làm content và sales demo của doanh nghiệp. Hãy triển khai ngay hôm nay để tận hưởng sức mạnh của AI trong tự động hóa công việc!