---
title: "🚀 Tự động hóa Google Business Profile với n8n - Quản lý bài đăng & đánh giá 9 chức năng"
description: "Workflow n8n hoàn chỉnh giúp tự động hóa 9 thao tác trên Google Business Profile: tạo, xóa, cập nhật bài đăng, quản lý đánh giá và trả lời. Tiết kiệm thời gian và tối ưu hóa quản lý doanh nghiệp."
slug: "tu-dong-hoa-google-business-profile-voi-n8n"
tags: [n8n, automation, no-code, google-business-profile, marketing]
keywords: [n8n workflow, tự động hóa, google business profile, quản lý đánh giá, marketing]
---

# 🚀 Tự động hóa Google Business Profile với n8n - Quản lý bài đăng & đánh giá 9 chức năng

[Các sếp đang gặp khó khăn khi phải quản lý thủ công các bài đăng và đánh giá trên Google Business Profile. Với workflow này, các sếp có thể tự động hóa hoàn toàn 9 thao tác quan trọng nhất: tạo, xóa, cập nhật bài đăng, quản lý đánh giá và trả lời đánh giá.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý bài đăng và đánh giá lên đến 90%
- Tự động hóa 9 thao tác quan trọng trên Google Business Profile
- Tăng cường tương tác với khách hàng thông qua đánh giá và trả lời tự động
- Giảm thiểu sai sót trong quản lý thông tin doanh nghiệp
- Tích hợp dễ dàng với các hệ thống khác thông qua n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Business Profile với quyền quản trị
- API Key từ Google Cloud Console (với quyền Google Business Profile API)
- Tài khoản n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn "From File" và tải lên file JSON của workflow
4. Hoặc chọn "From URL" và nhập link: https://n8n.io/workflows/5250

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Business Profile Tool MCP Server**:
   - Cấu hình credentials với API Key từ Google Cloud Console
   - Điền thông tin xác thực Google Business Profile

2. **Các node Google Business Profile Tool**:
   - **Create post**: Cấu hình thông tin bài đăng cần tạo
   - **Delete post**: Cấu hình ID bài đăng cần xóa
   - **Get post**: Cấu hình ID bài đăng cần lấy thông tin
   - **Get many posts**: Cấu hình bộ lọc để lấy nhiều bài đăng
   - **Update a post**: Cấu hình ID bài đăng và thông tin cập nhật
   - **Delete a reply to a review**: Cấu hình ID đánh giá và ID trả lời cần xóa
   - **Get review**: Cấu hình ID đánh giá cần lấy thông tin
   - **Get many reviews**: Cấu hình bộ lọc để lấy nhiều đánh giá
   - **Reply to review**: Cấu hình ID đánh giá và nội dung trả lời

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn vào nút "Activate" để kích hoạt workflow
2. Thử chạy workflow với dữ liệu mẫu để kiểm tra hoạt động
3. Sau khi xác nhận hoạt động ổn định, lưu workflow và đặt lịch chạy định kỳ nếu cần

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi có đánh giá mới
2. Tạo workflow phụ để tự động trả lời đánh giá tích cực/tiêu cực khác nhau
3. Lưu log các thao tác quan trọng vào Google Sheets hoặc cơ sở dữ liệu
4. Tích hợp với hệ thống CRM để quản lý khách hàng tiềm năng từ đánh giá

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc quản lý Google Business Profile thông qua n8n. Với 9 thao tác tự động hóa, các sếp có thể tiết kiệm thời gian và tối ưu hóa quản lý doanh nghiệp một cách hiệu quả. Hãy thử ngay và nâng cao trải nghiệm quản lý của bạn!