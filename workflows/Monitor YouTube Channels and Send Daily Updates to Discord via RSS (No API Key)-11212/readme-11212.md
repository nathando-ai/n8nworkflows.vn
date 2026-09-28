---
title: "🚀 Tự động theo dõi kênh YouTube và gửi cập nhật hàng ngày lên Discord qua RSS (Không cần API Key)"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động quét video mới trong 24 giờ qua từ các kênh YouTube yêu thích và gửi thông báo trực tiếp vào Discord hoàn toàn miễn phí."
slug: "tu-dong-theo-doi-youtube-va-gui-discord-qua-rss"
tags: [n8n, automation, youtube, discord, rss, social-media]
keywords: [n8n workflow, youtube to discord, rss feed n8n, tu dong hoa youtube, discord webhook]
---

# 🚀 Tự động theo dõi kênh YouTube và gửi cập nhật hàng ngày lên Discord qua RSS

Các sếp có đang tốn hàng giờ mỗi ngày để lướt YouTube, kiểm tra xem các content creator, đối thủ hay kênh tin tức công nghệ yêu thích đã ra video mới chưa? Việc này vừa thủ công, tốn thời gian lại rất dễ bỏ lỡ thông tin quan trọng. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh do tác giả **Vasyl Pavlyuchok** xây dựng. Workflow này sẽ tự động hóa 100% quy trình: quét danh sách kênh YouTube yêu thích, lọc các video mới xuất bản trong 24 giờ qua và bắn tin báo cáo gọn gàng vào kênh Discord của các sếp. Điểm ăn tiền nhất là **không cần xin Google YouTube API Key**, tận dụng trực tiếp RSS Feed cực kỳ mượt mà và miễn phí!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần mở app hay truy cập web thủ công, mọi video mới đều được tổng hợp gọn gàng.
- **Không bỏ lỡ tin tức:** Cập nhật đều đặn mỗi ngày vào khung giờ cố định (mặc định 8:30 sáng).
- **Không tốn phí API:** Tận dụng RSS Feed chuẩn của YouTube, không cần xin cấp quyền hay lo lắng về giới hạn quota của Google API.
- **Tùy biến linh hoạt:** Dễ dàng thêm bớt kênh YouTube và chọn kênh Discord nhận tin phù hợp với đội nhóm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Một **Discord Webhook URL** từ kênh Discord mà các sếp muốn nhận thông báo.
- Danh sách các **YouTube Channel ID** của các kênh mà các sếp muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này từ n8n, sau đó dán trực tiếp vào n8n Editor của mình hoặc import file JSON thông qua giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được cấu hình sẵn mạch lạc. Các sếp cần chú ý các điểm sau để chạy trơn tru:

- **Node `Define Channel IDs` (Set):** Nơi các sếp định nghĩa danh sách ID các kênh YouTube muốn theo dõi. Template mẫu đang để sẵn các kênh AI tiếng Tây Ban Nha. Các sếp hãy thay thế bằng Channel ID của các kênh mình thích.
  - *Mẹo tìm Channel ID:* Vì YouTube hiện dùng handle (ví dụ `@n8n`), ID thực tế bị ẩn. Các sếp có thể dùng trang web "YouTube Channel ID Finder" hoặc vào trang kênh -> Chuột phải -> *View Page Source* -> Tìm từ khóa `channel_id`.
- **Node `Split Channel IDs` & `Fetch Youtube RSS`:** Node này sẽ tách danh sách và tự động gọi RSS Feed tương ứng với từng kênh (`https://www.youtube.com/feeds/videos.xml?channel_id=ID_CUA_BAN`). Các sếp không cần chỉnh sửa gì ở đây.
- **Node `Daily Trigger` (Schedule Trigger):** Mặc định workflow được cấu hình chạy tự động mỗi ngày lúc 8:30 sáng. Các sếp có thể bấm vào để đổi khung giờ tùy ý.
- **Node `Filter Last 24h` (Filter):** Bộ lọc thông minh chỉ giữ lại những video được đăng tải trong vòng 24 giờ qua.
- **Node `Wait 2 sec` (Wait):** Tránh việc gửi tin nhắn quá nhanh gây nghẽn hoặc bị Discord giới hạn tần suất (Rate limit).
- **Node `Discord Notification` (Discord):** Đây là nơi các sếp cần cấu hình **Credentials** cho Discord Webhook. Hãy dán Webhook URL của kênh Discord nhà các sếp vào đây để bắt đầu nhận tin.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử xem dữ liệu từ RSS có đổ về và đẩy qua Discord thành công hay không.
- Nếu mọi thứ hiển thị ngon lành, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Thay vì chỉ gửi Discord, các sếp có thể nối thêm node Telegram, Slack hoặc Email để nhận tin ở nhiều nơi khác nhau.
- **Lưu trữ lịch sử:** Kết nối thêm node Google Sheets hoặc Notion ở cuối luồng để lưu lại danh sách video đã gửi, tạo thư viện kiến thức cá nhân hoặc team.
- **Tích hợp AI tóm tắt:** Thêm một node AI (OpenAI/Anthropic) trước bước gửi Discord để nhờ AI tóm tắt ngắn gọn nội dung video trước khi gửi, giúp tiết kiệm thời gian xem.

### 📌 Kết luận
Một workflow siêu gọn nhẹ nhưng giải quyết cực kỳ gọn gàng bài toán theo dõi tin tức, nội dung video từ YouTube. Hãy áp dụng ngay để tối ưu hóa thời gian cập nhật thông tin mỗi ngày cho bản thân và đội ngũ nhé các sếp!