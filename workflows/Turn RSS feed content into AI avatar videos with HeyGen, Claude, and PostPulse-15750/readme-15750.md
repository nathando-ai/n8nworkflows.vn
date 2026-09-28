---
title: "🎥 Tự động hóa nội dung: Chuyển đổi RSS thành video AI avatar với HeyGen, Claude và PostPulse"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi nội dung RSS thành video AI avatar, lên lịch đăng lên mạng xã hội với n8n, HeyGen và PostPulse"
slug: "tu-dong-hoa-rss-thanh-video-ai-avatar"
tags: [n8n, automation, no-code, content creation, ai avatar]
keywords: [n8n workflow, tự động hóa nội dung, video AI avatar, HeyGen, PostPulse, Claude]
---

# 🎥 Tự động hóa nội dung: Chuyển đổi RSS thành video AI avatar với HeyGen, Claude và PostPulse

[Các sếp] có biết không? Với workflow này, các sếp có thể tự động hóa quy trình tạo nội dung hấp dẫn từ RSS feed, chuyển đổi thành video AI avatar chuyên nghiệp và lên lịch đăng lên mạng xã hội - tất cả chỉ với vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình từ 30-60 phút thành vài giây
- **Nội dung chuyên nghiệp**: Video AI avatar chất lượng cao từ HeyGen
- **Lên lịch tự động**: Đăng video lên mạng xã hội theo lịch trình đã thiết lập
- **Tăng tương tác**: Nội dung hấp dẫn hơn so với bài viết truyền thống
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản PostPulse và API key
- Tài khoản HeyGen và API key
- Tài khoản Anthropic (cho Claude) và API key
- RSS feed URL muốn chuyển đổi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15750](https://n8n.io/workflows/15750)
2. Nhấn nút "Import" trên trang workflow
3. Hoặc copy JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **RSS Feed Trigger** (Node đầu tiên):
   - Cấu hình URL của RSS feed muốn theo dõi
   - Thiết lập tần suất kiểm tra (ví dụ: mỗi giờ)

2. **Create Video Script** (Node Anthropic):
   - Chọn credentials cho Anthropic
   - Tùy chỉnh prompt để tạo script từ nội dung RSS (ví dụ: "Tạo script video ngắn gọn từ nội dung này: {{ $node["RSS Feed Trigger"].json["description"] }}")

3. **Create Avatar Video** (Node HTTP Request):
   - Thiết lập URL endpoint của HeyGen
   - Cấu hình headers với API key của HeyGen
   - Đảm bảo body request chứa script từ node trước đó

4. **Upload media** và **Schedule a light post** (Node PostPulse):
   - Cấu hình credentials cho PostPulse
   - Thiết lập thời gian đăng bài (ví dụ: mỗi ngày lúc 9:00 AM)

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra video được tạo trên HeyGen
3. Xác nhận video được đăng lên PostPulse đúng thời gian
4. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log các video đã tạo vào Google Sheets để theo dõi hiệu suất
- Tạo nhiều phiên bản video với các avatar khác nhau cho các kênh khác nhau
- Thêm bước xử lý lỗi tự động khi có vấn đề xảy ra trong quá trình tạo video

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình tạo nội dung từ RSS đến đăng lên mạng xã hội, tiết kiệm thời gian quý giá và tạo ra nội dung chuyên nghiệp hơn. Hãy thử ngay và nâng cấp chiến lược nội dung của các sếp!