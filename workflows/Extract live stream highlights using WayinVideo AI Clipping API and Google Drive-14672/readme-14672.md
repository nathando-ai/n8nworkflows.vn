---
title: "🚀 Tự động cắt video Highlight Live Stream bằng WayinVideo AI và Google Drive trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình cắt video highlight từ live stream sử dụng WayinVideo AI Clipping API và lưu trữ trực tiếp lên Google Drive."
slug: "tu-dong-cat-video-highlight-live-stream-wayinvideo-ai-google-drive"
tags: [n8n, automation, no-code, ai, content-creation, google-drive, video-processing]
keywords: [n8n workflow, WayinVideo AI, cắt video highlight, tự động hóa live stream, Google Drive integration]
---

# 🚀 Tự động cắt video Highlight Live Stream bằng WayinVideo AI và Google Drive

Các sếp làm sáng tạo nội dung, streamer hay marketer chắc chắn đều hiểu cảm giác "nản" cỡ nào khi phải ngồi hàng giờ xem lại các buổi live stream dài 2-3 tiếng chỉ để cắt ra vài đoạn ngắn làm TikTok, Reels hay Shorts. Việc này vừa tốn thời gian, vừa đòi hỏi nhân sự phải có gu dựng video.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Người dùng chỉ cần điền link live stream vào một Form, AI của WayinVideo sẽ lo phần "đãi cát tìm vàng" để xuất ra các đoạn highlight đắt giá nhất, sau đó tự động tải về và lưu ngay vào Google Drive của các sếp! Không cần biết code, không cần tốn hàng giờ liền thủ công nữa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Bỏ qua hoàn toàn khâu xem lại video và cắt thủ công.
- **Tự động hóa hoàn toàn:** Nhận link từ form -> AI xử lý -> Lưu thẳng vào Google Drive sẵn sàng để đăng tải.
- **Thông minh & Chính xác:** Tự động tạo tiêu đề, chấm điểm, gắn thẻ (tags) và lấy đúng mốc thời gian (timestamps) cho từng đoạn clip.
- **Hoạt động liên tục 24/7:** Sẵn sàng nhận yêu cầu bất cứ lúc nào thông qua giao diện Web Form thân thiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WayinVideo API Key:** Tài khoản và API key từ dịch vụ WayinVideo AI Clipping.
- **Google Drive Account:** Tài khoản Google để cấu hình OAuth2 và lấy Folder ID lưu trữ video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này và import trực tiếp vào n8n Editor của mình, hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp nhớ cấu hình kỹ các node sau:

- **Node `2. WayinVideo — Submit Clipping Task1` & `4. WayinVideo — Get Clips Result1` (HTTP Request):** 
  - Thay thế chuỗi `YOUR_WAYIN_API_KEY_HERE` bằng API Key thật của các sếp trong phần Header xác thực của API.
- **Node `7. Google Drive — Upload Clip`:** 
  - Kết nối tài khoản Google Drive của các sếp bằng **Google Drive OAuth2 credentials**.
  - Thay thế `YOUR_GOOGLE_DRIVE_FOLDER_ID_HERE` bằng ID của thư mục trên Google Drive nơi các sếp muốn lưu các đoạn clip highlight.
- **Node `3. Wait — 90 Seconds1`:** 
  - Mặc định đặt thời gian chờ là 90 giây. *Lưu ý quan trọng:* Nếu live stream của các sếp dài hơn 90 phút, hãy tăng thời gian chờ lên `180` hoặc `300` giây để đảm bảo WayinVideo kịp xử lý xong trước khi lấy kết quả.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách gửi dữ liệu qua Web Form.
- Sau khi kiểm tra mọi thứ chạy ổn định, gạt công tắc sang **Active** để chính thức đưa vào vận hành thực tế và gửi link Form cho đội ngũ hoặc streamer sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh thông số AI:** Các sếp có thể đổi `target_duration` thành `DURATION_15_30` nếu muốn cắt các đoạn ngắn làm Reels/Shorts, hoặc đổi `ratio` thành `RATIO_16_9` nếu muốn làm video ngang cho YouTube.
- **Tích hợp Google Sheets:** Thêm một node Google Sheets ngay sau node 7 để tự động ghi log tên clip, điểm số AI, và link Google Drive vào bảng tính theo dõi nội dung.
- **Nhận thông báo qua Telegram/Slack:** Thêm node gửi thông báo về nhóm chat khi video đã được cắt xong và lưu thành công trên Drive để team dựng phim biết và lấy dựng ngay.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung muốn tối ưu hóa quy trình sản xuất video ngắn từ các buổi phát trực tiếp. Hãy cài đặt ngay hôm nay để giải phóng sức lao động và tăng tốc độ "xuất bản" nội dung của các sếp nhé!