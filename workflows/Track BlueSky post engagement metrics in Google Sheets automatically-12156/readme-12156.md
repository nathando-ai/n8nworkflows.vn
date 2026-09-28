---
title: "📈 Tự động theo dõi lượt tương tác bài viết BlueSky trong Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi lượt thích, chia sẻ và bình luận bài viết BlueSky trong Google Sheets mà không cần viết code"
slug: "tu-dong-theo-doi-tuong-tac-blueskysheet"
tags: [n8n, automation, no-code, bluesky, google-sheets]
keywords: [n8n workflow, tự động hóa, bluesky, google sheets, phân tích nội dung]
---

# 📈 Tự động theo dõi lượt tương tác bài viết BlueSky trong Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công lượt tương tác bài viết trên BlueSky. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động cập nhật lượt thích, chia sẻ, bình luận hàng ngày
- Chính xác: Dữ liệu được cập nhật liên tục mà không bị lỗi
- Cá nhân hóa: Theo dõi chỉ những bài viết trong vòng 14 ngày gần nhất
- Hoạt động liên tục: Không bị gián đoạn ngay cả khi một bài viết bị xóa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BlueSky với App Password
- Google Sheet đã chuẩn bị với các cột: Posted At, Post Link, Status, Likes, Reposts, Replies
- Thời gian (timezone) của bạn (ví dụ: America/Los_Angeles)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12156)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Configuration**:
   - Mở node "Configuration" và điền:
     - BlueSky Handle (ví dụ: steve.bsky.social)
     - App Password của bạn
     - Timezone của bạn (ví dụ: America/Los_Angeles)

2. **Node Get row(s) in sheet**:
   - Đảm bảo Google Sheet của bạn có cột "Status" với giá trị "Posted" cho các bài viết đã đăng

3. **Node BlueSky Auth**:
   - Không cần cấu hình gì thêm, node này tự động xác thực với BlueSky

4. **Node Get Post Stats**:
   - Không cần cấu hình gì thêm, node này tự động lấy dữ liệu từ BlueSky

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi có bài viết đạt ngưỡng tương tác nhất định
- Lưu log hoạt động vào Google Sheet riêng để theo dõi lịch sử cập nhật
- Gửi báo cáo hàng tuần tự động qua email với các bài viết có lượt tương tác cao nhất

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi tương tác bài viết trên BlueSky. Với việc tự động hóa hoàn toàn, dữ liệu luôn được cập nhật chính xác và liên tục, giúp các sếp đưa ra quyết định nhanh chóng và hiệu quả hơn. Hãy thử ngay để nâng cao hiệu quả quản lý nội dung của bạn!