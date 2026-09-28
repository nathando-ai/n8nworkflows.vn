---
title: "🚀 Tự động viết tin tức công nghệ hàng ngày với OpenAI và WordPress"
description: "Hướng dẫn tự động hóa viết tin tức công nghệ hàng ngày từ RSS feeds đến WordPress bằng n8n và OpenAI, tiết kiệm thời gian và nâng cao hiệu suất nội dung"
slug: "tu-dong-viet-tin-tuc-cong-nghe-hang-ngay-voi-openai-wordpress"
tags: [n8n, automation, no-code, content creation, AI]
keywords: [n8n workflow, tự động hóa nội dung, AI viết tin tức, WordPress, OpenAI]
---

# 🚀 Tự động viết tin tức công nghệ hàng ngày với OpenAI và WordPress

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải viết tin tức công nghệ hàng ngày? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ thu thập tin tức đến xuất bản bài viết WordPress hoàn toàn không cần can thiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và xử lý tin tức từ 4 nguồn uy tín hàng ngày
- **Nội dung chuyên nghiệp**: Sử dụng AI để viết bài với chất lượng tương đương chuyên gia
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, bài viết được xuất bản tự động
- **Nâng cao hiệu suất**: Tạo ra nội dung liên tục mà không phải lo lắng về thời gian
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI và API key
- WordPress site với application password đã kích hoạt
- Tài khoản n8n đã cài đặt các node cần thiết (LangChain, WordPress)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập URL: `https://n8n.io/workflows/13924`
3. Hoặc copy JSON từ [link gốc](https://n8n.io/workflows/13924) và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Daily 8AM Trigger"**:
   - Đảm bảo múi giờ của server n8n đã được đặt chính xác
   - Có thể điều chỉnh thời gian kích hoạt nếu cần

2. **Node "OpenAI Chat Model"**:
   - Thêm OpenAI API key vào Credentials
   - Đảm bảo tài khoản OpenAI có đủ credit để chạy workflow
   - Có thể thay đổi model (gpt-4, gpt-3.5-turbo) trong node này

3. **Node "Create WordPress Draft"**:
   - Thêm WordPress API credentials (site URL + application password)
   - Có thể thay đổi trạng thái bài viết (draft, publish) trong node này

4. **Các node RSS Feed**:
   - Có thể thay thế các nguồn RSS hiện tại bằng nguồn khác
   - Đảm bảo các nguồn RSS mới có cấu trúc tương tự để tránh lỗi

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả ở các node quan trọng (Merge All Feeds, AI Write News Article)
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi bài viết được xuất bản
2. **Lưu log hoạt động**: Thêm node lưu log các bài viết đã xuất bản
3. **Tùy chỉnh nội dung**: Điều chỉnh prompt trong node "AI Write News Article" để phù hợp với phong cách viết của các sếp
4. **Gửi báo cáo định kỳ**: Thêm node gửi báo cáo hàng tuần về số lượng bài viết đã xuất bản

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình viết tin tức công nghệ hàng ngày, tiết kiệm thời gian và nâng cao hiệu suất nội dung. Với sự kết hợp của n8n và OpenAI, các sếp có thể tạo ra nội dung chất lượng cao mà không cần phải tốn nhiều thời gian và công sức. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!