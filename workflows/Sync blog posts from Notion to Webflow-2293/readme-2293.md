---
title: "🚀 Tự động đồng bộ bài viết từ Notion sang Webflow - Giải pháp tiết kiệm thời gian cho các sếp"
description: "Hướng dẫn chi tiết cách tự động đồng bộ nội dung bài viết từ Notion sang Webflow bằng n8n, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-bai-viet-notion-sang-webflow"
tags: [n8n, automation, no-code, notion, webflow]
keywords: [n8n workflow, tự động hóa, đồng bộ nội dung, notion, webflow]
---

# 🚀 Tự động đồng bộ bài viết từ Notion sang Webflow - Giải pháp tiết kiệm thời gian cho các sếp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải chuyển đổi nội dung từ Notion sang Webflow thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian chuyển đổi nội dung thủ công
- Đảm bảo đồng bộ dữ liệu 100% chính xác giữa Notion và Webflow
- Tự động xử lý cả bài viết mới và cập nhật bài viết hiện có
- Hoạt động liên tục theo lịch trình đã đặt
- Nhận thông báo thành công qua Slack khi quá trình hoàn tất
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với cơ sở dữ liệu bài viết
- Tài khoản Webflow với collection bài viết
- Tài khoản Slack (tùy chọn, để nhận thông báo)
- API keys cho Notion và Webflow
- Tạo 2 trường trong cơ sở dữ liệu Notion:
  - Trường "slug" (text) để đồng bộ với Webflow
  - Trường "Sync to Webflow?" (checkbox) để chọn bài viết cần đồng bộ
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2293](https://n8n.io/workflows/2293)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get simple page data" và "Get all page data"**:
   - Chọn credentials "notionApi"
   - Điền ID cơ sở dữ liệu Notion vào trường "databaseId"

2. **Node "Get all blog posts1"**:
   - Chọn credentials "notionApi"
   - Điền ID cơ sở dữ liệu Notion vào trường "databaseId"

3. **Node "Create post1" và "Get all collection posts1"**:
   - Chọn credentials "webflowOAuth2Api"
   - Điền Site ID và Collection ID của Webflow vào các trường tương ứng

4. **Node "Success message1" (tùy chọn)**:
   - Chọn credentials "slackOAuth2Api"
   - Điền Channel ID của Slack để nhận thông báo

5. **Node "Schedule Trigger"**:
   - Thiết lập lịch chạy workflow theo nhu cầu (ví dụ: hàng ngày lúc 9h sáng)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để test từng node từ đầu đến cuối
2. Kiểm tra kết quả ở mỗi node để đảm bảo dữ liệu được xử lý đúng
3. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động xử lý hình ảnh**: Thêm node để tự động tải hình ảnh từ Notion lên Webflow và cập nhật URL trong nội dung
2. **Xử lý các trường tùy chỉnh**: Mở rộng workflow để đồng bộ các trường tùy chỉnh từ Notion sang Webflow
3. **Lưu log hoạt động**: Thêm node để lưu log các bài viết đã được đồng bộ để theo dõi lịch sử
4. **Xử lý lỗi tự động**: Thêm node để gửi thông báo lỗi qua Slack khi workflow gặp sự cố

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý nội dung. Bằng cách tự động đồng bộ bài viết từ Notion sang Webflow, các sếp có thể tập trung vào việc tạo nội dung chất lượng hơn thay vì phải chuyển đổi thủ công. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!