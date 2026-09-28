---
title: "🚀 Tự động hóa tạo TikTok Shorts từ Podcast Video với WayinVideo & PostPulse"
description: "Hướng dẫn tự động hóa chuyển đổi podcast video thành TikTok shorts và lên lịch đăng bằng n8n, tiết kiệm thời gian và tối ưu nội dung cho nền tảng TikTok"
slug: "tu-dong-hoa-tao-tiktok-shorts-tu-podcast-video"
tags: [n8n, automation, no-code, content creation, multimodal AI]
keywords: [n8n workflow, tự động hóa nội dung, tạo TikTok shorts, podcast video, PostPulse]
---

# 🚀 Tự động hóa tạo TikTok Shorts từ Podcast Video với WayinVideo & PostPulse

[Các sếp] có biết không? Việc chuyển đổi podcast video thành TikTok shorts và lên lịch đăng thủ công tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ 5 phút trở lên
- **Chính xác**: Giảm thiểu lỗi do thao tác thủ công
- **Tối ưu nội dung**: Tạo ra các đoạn clip ngắn phù hợp với TikTok
- **Lên lịch tự động**: Đăng bài định kỳ mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản PostPulse và API key (để upload và lên lịch bài viết)
- Tài khoản WayinVideo (để tạo và lấy các đoạn clip)
- URL của podcast video cần chuyển đổi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15181](https://n8n.io/workflows/15181)
2. Click vào nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "On form submission"**: Cấu hình form để nhận URL của podcast video
- **Node "Clip Videos"**: Cần cấu hình credentials cho WayinVideo
- **Node "Upload media" và "Schedule a light post"**: Cần cấu hình credentials cho PostPulse
- **Node "Wait"**: Đặt thời gian chờ phù hợp (mặc định 5 phút)

#### 3. Kích hoạt ⚡️
1. Test run workflow với URL mẫu của podcast video
2. Kiểm tra kết quả trên PostPulse để đảm bảo các đoạn clip đã được upload và lên lịch đúng
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo khi workflow hoàn thành (Slack, Telegram, Email)
- Tự động hóa quá trình chọn clip hay nhất dựa trên lượt xem
- Tạo nhiều phiên bản TikTok shorts từ một podcast video duy nhất
- Kết hợp với các công cụ phân tích để tối ưu nội dung cho TikTok

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tạo và quản lý nội dung TikTok từ podcast video. Với sự tự động hóa toàn diện, các sếp có thể tập trung vào việc sáng tạo nội dung hơn là quản lý quy trình kỹ thuật. Hãy thử ngay và trải nghiệm sự khác biệt!