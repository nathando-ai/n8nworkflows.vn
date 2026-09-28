---
title: "🚀 Tự động tạo YouTube RSS Feed cá nhân với Redis Caching và Trình phát video tích hợp"
description: "Xây dựng feed RSS tùy chỉnh cho các kênh YouTube yêu thích của bạn, tích hợp sẵn trình phát video trực tiếp trong app đọc tin và tối ưu tốc độ với Redis Cache."
slug: "tao-youtube-rss-feed-redis-cache-n8n"
tags: [n8n, automation, youtube, redis, rss, no-code]
keywords: [n8n workflow, youtube rss feed, redis caching, tự động hóa youtube, n8n webhook]
---

# 🚀 Tự động tạo YouTube RSS Feed cá nhân với Redis Caching và Trình phát video tích hợp

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở YouTube, bị lôi cuốn vào dòng video đề xuất (Shorts, video giải trí câu view) và mất hàng giờ liền thay vì chỉ xem nội dung từ các kênh mình thực sự quan tâm? Hay sếp muốn theo dõi các nhà sáng tạo nội dung yêu thích qua ứng dụng đọc RSS (RSS Reader) quen thuộc nhưng YouTube lại không cung cấp đầy đủ thông tin video và trình phát trực tiếp?

Workflow n8n tuyệt vời này từ tác giả **Quinten Alexander** chính là giải pháp tự động hóa 100% giúp các sếp gom tất cả video mới nhất từ các kênh YouTube yêu thích vào một file RSS cá nhân. Đặc biệt, workflow tích hợp sẵn **trình phát video nhúng (iframe)** ngay trong RSS reader và sử dụng **Redis Caching** để tăng tốc độ tải, tiết kiệm giới hạn gọi YouTube API!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với Redis, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Trải nghiệm không xao lãng:** Đọc và xem video trực tiếp ngay trong ứng dụng RSS oblige mà không cần truy cập vào trang chủ YouTube đầy cám dỗ.
- **Tối ưu hiệu suất:** Sử dụng Redis Cache giúp lưu trữ thông tin video đã tải, tránh việc gọi liên tục vào YouTube API mỗi lần làm mới feed.
- **Lọc thông minh:** Tự động loại bỏ các video YouTube Shorts và các video cũ đăng quá 1 tuần.
- **Hoạt động liên tục 24/7:** Biến n8n thành một RSS server cá nhân của riêng các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (ưu tiên bản Self-hosted qua Docker để dễ chạy kèm Redis).
- **Redis Database:** Dùng để cache dữ liệu RSS item (có thể chạy nhanh 1 container Redis qua Docker).
- **Google / YouTube API Credentials:** Tài khoản Google Cloud đã bật YouTube Data API v3 để lấy chi tiết video.
- **Ứng dụng đọc RSS:** Bất kỳ app đọc RSS nào hỗ trợ custom feed (NetNewsWire, Reeder, Feedly...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy toàn bộ JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp chỉ cần tập trung cấu hình 4 điểm mấu chốt sau đây:

- **Node `Set Channels` (Bước 1):** 
  Sửa đoạn JSON trong node này để thêm ID các kênh YouTube các sếp muốn theo dõi. 
  *Cách lấy Channel ID:* Vào trang kênh YouTube (VD: `youtube.com/@NetworkChuck`) -> Bấm "more" ở mô tả -> Cuộn xuống bấm "Share Channel" -> Chọn "Copy Channel-ID" và dán vào node này.
- **Node `Get Video Info From Cache` & `Cache Video Info` (Bước 2):** 
  Kết nối đến Redis Database của các sếp. Nếu chạy n8n và Redis trên cùng Docker network, cấu hình đơn giản: Host là `redis`, Port `6379`, để trống username/password.
- **Node `Get Video Details` (Bước 3):** 
  Cấu hình Google/YouTube API Credentials bằng tài khoản Google của các sếp để cấp quyền gọi YouTube Data API v3.
- **Node `RSS Webhook` (Bước 4):** 
  Copy đường dẫn **Production URL** từ node này và dán vào ứng dụng đọc RSS yêu thích của các sếp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách gọi Webhook URL trên trình duyệt hoặc app RSS.
- Sau khi kiểm tra mọi thứ trả về đúng cấu trúc XML của RSS, hãy gạt công tắc sang **Active** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn tin:** Kết hợp thêm các node RSS Feed Read từ các trang báo công nghệ, Medium hoặc Substack vào chung một feed tổng hợp.
- **Lọc nội dung nâng cao:** Chỉnh sửa code trong node `Build RSS Feed` hoặc `Extract Short Description` để tự động xóa các từ khóa quảng cáo, sponsor trong mô tả video.
- **Thông báo qua Telegram/Slack:** Thêm node Telegram để nhận thông báo mỗi khi kênh yêu thích ra video mới toanh.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho những ai muốn quản lý thông tin thông minh, tập trung và nói không với thuật toán câu view của YouTube. Hãy triển khai ngay lên hệ thống n8n của các sếp và tận hưởng trải nghiệm đọc tin tức, xem video hoàn toàn mới!