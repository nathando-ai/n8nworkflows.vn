---
title: "📧 Tự động chuyển đổi RSS feed thành email - Workflow n8n đơn giản"
description: "Hướng dẫn chi tiết cách tự động hóa việc theo dõi RSS feed và nhận email thông báo mới nhất mỗi giờ với workflow n8n"
slug: "tu-dong-chuyen-doi-rss-feed-thanh-email"
tags: [n8n, automation, no-code, rss, email]
keywords: [n8n workflow, tự động hóa, rss feed, email thông báo]
---

# 📧 Tự động chuyển đổi RSS feed thành email - Workflow n8n đơn giản

[Các sếp đang gặp khó khăn khi phải theo dõi nhiều nguồn tin tức, blog, hoặc kênh thông tin quan trọng qua RSS feed. Với workflow này, các sếp có thể tự động hóa việc theo dõi và nhận email thông báo mới nhất mỗi giờ, giúp tiết kiệm thời gian và không bỏ lỡ bất kỳ thông tin quan trọng nào.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải truy cập từng trang web để kiểm tra cập nhật mới.
- Thông tin chính xác: Nhận được thông báo ngay khi có bài viết mới từ các nguồn tin quan trọng.
- Cá nhân hóa: Chỉ nhận thông báo từ các nguồn tin mà các sếp quan tâm.
- Hoạt động liên tục: Workflow chạy tự động mỗi giờ, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail và quyền truy cập API (cho node Gmail).
- Danh sách URL của các RSS feed mà các sếp muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập link: [https://n8n.io/workflows/2144](https://n8n.io/workflows/2144).
3. Hoặc tải file JSON về và chọn "Import from File".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "List of RSS feeds" (Set)**:
   - Thêm danh sách URL của các RSS feed mà các sếp muốn theo dõi vào trường "RSS Feed URLs".
   - Ví dụ:
     ```
     [
       "https://example.com/feed1.xml",
       "https://example.com/feed2.xml"
     ]
     ```

2. **Node "Send email with each post" (Gmail)**:
   - Chọn credentials cho tài khoản Gmail.
   - Cấu hình các trường:
     - **From**: Địa chỉ email gửi.
     - **To**: Địa chỉ email nhận thông báo.
     - **Subject**: Tiêu đề email (có thể sử dụng biểu thức để lấy tiêu đề từ bài viết).
     - **Body**: Nội dung email (có thể sử dụng biểu thức để lấy nội dung từ bài viết).

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test workflow với dữ liệu mẫu.
2. Sau khi test thành công, nhấn nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận thông báo thay vì email.
- **Lưu log**: Thêm node Google Sheets để lưu trữ lịch sử các bài viết đã gửi.
- **Gửi báo cáo định kỳ**: Thêm node Schedule để gửi báo cáo tổng hợp hàng ngày.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc theo dõi RSS feed và nhận thông báo mới nhất mỗi giờ. Điều này giúp tiết kiệm thời gian và không bỏ lỡ bất kỳ thông tin quan trọng nào. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!