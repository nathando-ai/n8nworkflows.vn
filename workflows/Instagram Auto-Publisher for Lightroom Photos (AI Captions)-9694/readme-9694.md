---
title: "🚀 Tự động hóa đăng ảnh Instagram từ Lightroom kèm Caption AI bằng n8n"
description: "Hướng dẫn chi tiết thiết lập workflow n8n tự động lấy ảnh chưa đăng từ Lightroom, sử dụng AI (Anthropic) viết caption thông minh và xuất bản lên Instagram qua Graph API."
slug: "tu-dong-hoa-dang-anh-instagram-tu-lightroom-kem-caption-ai"
tags: [n8n, automation, instagram, adobe-lightroom, ai-captions, anthropic]
keywords: [n8n workflow, tự động đăng ảnh instagram, lightroom automation, ai caption generator, instagram graph api, n8n viet nam]
---

# 🚀 Tự động hóa đăng ảnh Instagram từ Lightroom kèm Caption AI

Các sếp là nhiếp ảnh gia, nhà sáng tạo nội dung và đang đau đầu vì mất quá nhiều thời gian để chọn ảnh từ Lightroom, nghĩ caption, hashtag rồi thủ công bấm đăng lên Instagram? Việc duy trì lịch đăng bài đều đặn trở thành gánh nặng lớn khi bạn muốn tập trung vào chuyên môn chụp ảnh.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: quét ảnh chưa đăng trong cơ sở dữ liệu, phân tích thông tin ALT và EXIF, nhờ AI (Anthropic) viết một chiếc caption cực nghệ, sau đó tự động xuất bản lên Instagram và cập nhật trạng thái "đã đăng". Không cần code, hoạt động mượt mà 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh copy/paste hình ảnh hay loay hoay nghĩ câu chữ, hashtag mỗi ngày.
- **Caption thông minh chuẩn AI:** AI (Anthropic) đọc hiểu thông tin ALT và thông số EXIF của ảnh để viết caption tự nhiên, thu hút người xem.
- **Đồng bộ mượt mà:** Tự động đánh dấu ảnh nào đã đăng để tránh việc đăng trùng lặp.
- **Vận hành tự động 24/7:** Lên lịch chạy định kỳ bằng Schedule Trigger, tài khoản Instagram luôn giữ được độ phủ sóng đều đặn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã chạy ổn định và có domain public (để Instagram gọi lấy hình ảnh từ Lightroom).
- **Tài khoản Instagram Business/Creator:** Liên kết với một Facebook Page.
- **Meta App & Graph API Token:** Long-lived access token để gọi Instagram Graph API (phiên bản v23.0 trở lên).
- **Anthropic API Key:** Tài khoản Claude API để sinh nội dung caption.
- **n8n Data Table:** Bảng dữ liệu chứa danh sách thông tin ảnh từ Lightroom.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow do tác giả Camille Roux cung cấp và paste trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 11 nodes được chia thành 5 bước rõ ràng. Các sếp cần cấu hình kỹ các điểm sau:

- **Schedule Trigger:** Cài đặt lịch chạy (cron expression hoặc khung giờ cố định) tùy theo tần suất muốn đăng bài lên Instagram của các sếp.
- **Get row(s) & Update row(s) (Data Table):** Trỏ tới bảng dữ liệu (`Photos`) chứa các cột bắt buộc: `lr_asset_id`, `alt`, `lr_asset`, `ig_posted_at`, `ig_id`, `ig_caption`. Đảm bảo node lọc các dòng có `ig_posted_at` đang để trống (chưa đăng).
- **Limit:** Thiết lập số lượng ảnh tối đa được xử lý trong mỗi lần chạy (ví dụ: 1 bài/lần chạy).
- **Message a model (Anthropic):** Kết nối thông tin `Anthropic API` credentials và cấu hình prompt để AI viết caption dựa trên ALT và thông số EXIF truyền vào.
- **Instagram Auth & HTTP Request nodes (`get access_token`, `Get instagram id`, `Create container`, `Publish image`):** 
  - Điền `httpBearerAuth` với Long-lived Token từ Facebook/Instagram Graph API.
  - Cấu hình endpoint API chính xác cho tài khoản Instagram Business của các sếp.
  - Đảm bảo URL ảnh (`lr_asset`) từ Lightroom là đường dẫn công khai (Public URL) để Instagram server có thể tải về tạo container.
- **Params (Set Node):** Khai báo các tham số cấu hình chung dùng xuyên suốt trong workflow.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Execute Workflow**) với một dòng dữ liệu mẫu để kiểm tra từ bước AI viết caption đến lúc tạo container và publish lên Instagram thành công.
- Kiểm tra lại Data Table xem trạng thái `ig_posted_at` và `ig_id` đã được cập nhật chưa.
- Bật công tắc **Active** để workflow tự động chạy theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo kèm hình ảnh và caption vừa đăng về máy cho các sếp tiện theo dõi.
- **Lưu log lỗi:** Sử dụng Error Trigger để bắt sự cố (nếu token hết hạn hoặc lỗi ảnh) và gửi cảnh báo ngay lập tức.
- **Đa dạng hóa mạng xã hội:** Từ node sinh caption của AI, có thể nhánh thêm các HTTP Request để đẩy bài viết đồng thời lên Facebook Page, LinkedIn hoặc Twitter.

### 📌 Kết luận
Workflow tự động hóa Instagram từ Lightroom kết hợp AI Caption là một trợ thủ đắc lực giúp tối ưu hóa quy trình làm việc của các nhiếp ảnh gia và marketer. Hãy cài đặt ngay hôm nay để giải phóng thời gian sáng tạo của các sếp!