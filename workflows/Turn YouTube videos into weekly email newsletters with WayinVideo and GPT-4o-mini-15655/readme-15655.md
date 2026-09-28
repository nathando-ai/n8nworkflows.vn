---
title: "🚀 Tự động hóa YouTube thành email tin tức hàng tuần với WayinVideo và GPT-4o-mini"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi video YouTube thành email tin tức hàng tuần với n8n, WayinVideo và GPT-4o-mini. Tiết kiệm thời gian và nâng cao hiệu quả nội dung."
slug: "tu-dong-hoa-youtube-thanh-email-tin-tuc-hang-tuan"
tags: [n8n, automation, no-code, content-creation, ai]
keywords: [n8n workflow, tự động hóa nội dung, AI tạo nội dung, email marketing, YouTube]
---

# 🚀 Tự động hóa YouTube thành email tin tức hàng tuần với WayinVideo và GPT-4o-mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà sáng tạo nội dung khi phải xem hàng chục video YouTube mỗi tuần và viết email tin tức từ đầu. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** so với làm thủ công
- Tạo ra **email tin tức chuyên nghiệp** mỗi tuần tự động
- **Tăng tương tác** nhờ nội dung cá nhân hóa và chất lượng cao
- **Hoạt động liên tục** 24/7 mà không cần can thiệp
- **Tiết kiệm chi phí** cho dịch vụ AI và nhân lực
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã tạo sẵn
- API Key từ [WayinVideo](https://wayin.video/)
- Tài khoản OpenAI với API Key
- Danh sách video YouTube cần xử lý (đã lưu trong Google Sheets)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15655](https://n8n.io/workflows/15655)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node 4 & 6 (WayinVideo - Submit Summarization & Get Summary Results)**
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thật của bạn
   - Đảm bảo tài khoản WayinVideo có đủ credit

2. **Node 11 (OpenAI - GPT-4o-mini Model)**
   - Kết nối với tài khoản OpenAI của bạn
   - Đảm bảo có đủ credit trong tài khoản OpenAI

3. **Node 2 & 14 (Google Sheets - Read Pending Videos & Mark Video Processed)**
   - Kết nối với tài khoản Google OAuth2
   - Thay thế `YOUR_VIDEO_QUEUE_SHEET_ID` bằng ID của Google Sheet chứa danh sách video

4. **Node 13 (Google Sheets - Save Newsletter Draft)**
   - Kết nối với tài khoản Google OAuth2
   - Thay thế `YOUR_NEWSLETTER_SHEET_ID` bằng ID của Google Sheet lưu bản nháp tin tức

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Thêm 1-2 video YouTube vào tab Video Queue
   - Chạy workflow thủ công để kiểm tra
2. Bật Active workflow:
   - Chọn "Activate" trong n8n Editor
   - Đảm bảo workflow sẽ chạy tự động mỗi thứ Hai lúc 7AM

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets để theo dõi lịch sử
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tuần/tháng về hiệu suất
4. **Tối ưu hóa nội dung**: Thêm node phân tích từ khóa SEO cho email tin tức

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các nhà sáng tạo nội dung, nhà báo, và đội ngũ marketing muốn tự động hóa quá trình chuyển đổi video YouTube thành email tin tức hàng tuần. Với sự kết hợp của n8n, WayinVideo và GPT-4o-mini, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao chất lượng nội dung một cách đáng kể. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!