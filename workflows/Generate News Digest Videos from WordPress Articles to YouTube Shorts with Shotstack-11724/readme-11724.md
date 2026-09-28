---
title: "🚀 Tự động tạo video YouTube Shorts tổng hợp tin tức từ WordPress với Shotstack và n8n"
description: "Biến các bài viết WordPress trong ngày thành video YouTube Shorts tự động hoàn toàn bằng n8n và Shotstack API, tiết kiệm 100% thời gian dựng video thủ công."
slug: "tao-video-youtube-shorts-tu-dong-tu-wordpress-voi-shotstack-n8n"
tags: [n8n, automation, wordpress, youtube, shotstack, ai-video]
keywords: [n8n workflow, tạo video tự động, wordpress to youtube shorts, shotstack api, automation n8n tieng viet]
---

# 🚀 Tự động hóa sản xuất YouTube Shorts từ bài viết WordPress với Shotstack

Các sếp làm nội dung hay quản lý trang tin tức chắc chắn hiểu rõ cảm giác "vắt chân lên cổ" mỗi ngày để chọn lọc bài viết, dựng video ngắn rồi đăng lên YouTube Shorts, TikTok. Việc này ngốn rất nhiều thời gian và công sức thủ công. 

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: quét các bài viết mới nhất trên website WordPress vào mỗi buổi chiều, xử lý hình ảnh/video đi kèm, gọi API dựng video chuyên nghiệp qua **Shotstack** và tự động xuất bản lên kênh **YouTube** dưới dạng Shorts mà không cần chạm tay vào một, thao tác dựng hình nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tệp video nặng mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%**: Chạy định kỳ mỗi tối, gom tất cả bài viết trong ngày thành một bản tin video hoàn chỉnh.
- **Tối ưu hóa đa nền tảng**: Tận dụng triệt để nội dung WordPress sẵn có để phủ sóng kênh YouTube Shorts, kéo traffic cực mạnh về website.
- **Tiết kiệm chi phí nhân sự**: Thay vì thuê editor dựng video hàng ngày, hệ thống tự động render qua Shotstack với chi phí siêu rẻ.
- **Chuyên nghiệp và nhất quán**: Tùy chỉnh linh hoạt logo, màu sắc thương hiệu, hình nền và nhạc nền thông qua bảng cấu hình tập trung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **WordPress Site**: Website tin tức/blog chạy mã nguồn WordPress (cần bật REST API).
- **Tài khoản Shotstack**: Đăng ký tài khoản tại Shotstack.io để lấy API Key dựng video.
- **Tài khoản YouTube / Google Cloud Console**: Tạo OAuth2 Credentials để n8n có quyền upload video lên kênh YouTube của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này.
- Mở n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thành phần sau để hệ thống chạy mượt mà:

- **Trice once a day - evenings (`scheduleTrigger`)**: Cài đặt thời gian chạy tự động mỗi tối (ví dụ: 18:00 hàng ngày).
- **Get articles from today (`wordpressApi`)**: Kết nối với tài khoản WordPress của các sếp. Node này sẽ lọc tất cả các bài viết được xuất bản trong ngày hôm đó (`getAll` operation).
- **Config Variables (`set`)**: Đây là nơi các sếp "trang trí" cho video của mình. Hãy chỉnh sửa các biến cấu hình như: Logo chính, Logo góc, Màu sắc nút bấm (Button color), Tiêu đề video, URL hình nền mặc định và URL âm thanh nền (sound URL).
- **Shotstack - Submit Request & Check Status (`httpRequest`)**: Nhập Shotstack API Key vào phần Header Auth để hệ thống gửi yêu cầu render video và liên tục kiểm tra trạng thái (polling mỗi 30 giây cho đến khi video sẵn sàng).
- **Upload video to youtube as (`youTube`)**: Kết nối tài khoản YouTube qua `youTubeOAuth2Api` để tự động đẩy video hoàn thiện lên kênh dưới dạng Shorts.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thủ công với dữ liệu ngày hiện tại.
- Kiểm tra kết quả trên Shotstack và kênh YouTube.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh phát hành**: Thêm các node upload để gửi đồng thời video hoàn thiện lên **TikTok** hoặc **Facebook Reels**.
- **Tích hợp thông báo**: Kết nối thêm node **Telegram** hoặc **Slack** để nhận thông báo kèm link video YouTube ngay khi render xong.
- **AI hóa nội dung**: Có thể tích hợp thêm các node AI (như OpenAI / Claude) trước bước tạo JSON để tóm tắt ngắn gọn tiêu đề bài báo cho phù hợp với thời lượng video Shorts.

### 📌 Kết luận
Việc tự động hóa sản xuất video từ bài viết cũ chưa bao giờ dễ dàng đến thế với combo **WordPress + n8n + Shotstack**. Hãy thiết lập ngay hôm nay để tối ưu hóa nguồn lực content marketing và bùng nổ lượt xem trên YouTube Shorts các sếp nhé!