---
title: "🚀 Tự động trích xuất video cảm nhận khách hàng bằng AI và lưu Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc nhận link video gốc, dùng AI của WayinVideo cắt thành các đoạn ngắn ấn tượng và lưu trữ trực tiếp vào Google Drive."
slug: "tu-dong-trich-xuat-video-testimonial-wayinvideo-google-drive"
tags: [n8n, automation, no-code, ai-video, google-drive, content-creation]
keywords: [n8n workflow, WayinVideo AI, trích xuất video tự động, Google Drive automation, testimonial video clipping]
---

# 🚀 Tự động trích xuất video cảm nhận khách hàng (Testimonial) bằng WayinVideo AI và Google Drive

Việc xử lý các video phỏng vấn hoặc cảm nhận khách hàng (testimonial) dài dằng dặc để cắt ra những phân đoạn đắt giá (shorts, reels, TikTok) thường ngốn rất nhiều thời gian của đội ngũ Marketing. Thủ công từng công đoạn từ xem lại video, chọn khoảnh khắc, cắt dựng cho đến lưu trữ khiến anh em mệt mỏi.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa **100%** quy trình: Nhận yêu cầu qua Form 👉 Gửi sang AI của WayinVideo để phân tích và cắt video 👉 Tải về 👉 Lưu tự động vào Google Drive sẵn sàng để đăng tải.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải ngồi tua video hàng giờ để tìm khoảnh khắc hay.
- **AI thông minh:** Tự động phát hiện những phân đoạn ấn tượng nhất và tạo ra các video dọc (vertical clips) chuẩn xu hướng mạng xã hội.
- **Tổ chức khoa học:** Video sau khi cắt được tải xuống và đẩy thẳng vào đúng thư mục Google Drive định sẵn với tên gọi rõ ràng.
- **Vận hành trơn tru:** Hoạt động tự động từ khâu thu thập thông tin qua Form cho đến khi hoàn tất lưu trữ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WayinVideo API Key:** Tài khoản và API key từ nền tảng WayinVideo AI.
- **Google Drive Account:** Tài khoản Google để cấu hình OAuth2 kết nối với n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node sau để workflow chạy mượt mà:

- **Node `2. WayinVideo — Submit Clipping Task` & `4. WayinVideo — Get Clip Results` (HTTP Request):** Thay thế đoạn `YOUR_WAYIN_API_KEY` bằng Bearer Token thực tế từ tài khoản WayinVideo của các sếp.
- **Node `7. Google Drive — Upload Clip`:** Tạo kết nối Google Drive OAuth2 trong n8n, sau đó thay thế `YOUR_GOOGLE_DRIVE_FOLDER_ID` bằng ID thư mục Google Drive đích mà các sếp muốn lưu video.
- **Node `3. Wait — 90 Seconds` (Lưu ý quan trọng ⚠️):** Workflow mặc định chờ 90 giây trước khi lấy kết quả. Nếu các sếp xử lý video quá dài (trên 30 phút), thời gian này có thể chưa đủ khiến kết quả trả về trống. Hãy tăng thời gian chờ hoặc tối ưu hóa bằng vòng lặp kiểm tra trạng thái nếu cần.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) bằng một video mẫu để kiểm tra toàn bộ luồng dữ liệu.
- Bật công tắc **Active** để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh tỷ lệ video:** Thay đổi tham số `RATIO_9_16` thành `RATIO_16_9` trong payload gửi đi nếu các sếp muốn xuất video khổ ngang cho YouTube/Facebook thay vì video dọc.
- **Điều chỉnh số lượng clip:** Thay đổi giá trị `limit` trong node gửi request để kiểm soát số lượng clip tối đa được trích xuất.
- **Thêm thông báo:** Gắn thêm một node **Slack** hoặc **Gmail** ngay sau node Google Drive để bắn thông báo cho team Marketing ngay khi video đã được cắt và lưu xong.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ sản xuất nội dung, agency hay các nhà sáng tạo nội dung muốn tối ưu hóa thời gian xử lý video hậu kỳ bằng sức mạnh của AI. Hãy áp dụng ngay vào hệ thống của các sếp để bứt phá hiệu suất công việc!