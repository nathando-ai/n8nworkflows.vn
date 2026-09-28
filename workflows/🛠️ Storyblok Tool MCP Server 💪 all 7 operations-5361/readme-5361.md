---
title: "🚀 Tự động hóa Storyblok với n8n: Quản lý 7 thao tác nội dung một cách hiệu quả"
description: "Hướng dẫn tự động hóa 7 thao tác chính của Storyblok (Delete, Get, Publish, Unpublish) bằng n8n để tiết kiệm thời gian và nâng cao hiệu suất quản lý nội dung."
slug: "tu-dong-hoa-storyblok-voi-n8n"
tags: [n8n, automation, no-code, storyblok, content-management]
keywords: [n8n workflow, tự động hóa nội dung, storyblok api, quản lý nội dung]
---

# 🚀 Tự động hóa Storyblok với n8n: Quản lý 7 thao tác nội dung một cách hiệu quả

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý nội dung Storyblok thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn 7 thao tác chính của Storyblok (Delete, Get, Publish, Unpublish)
- Tiết kiệm thời gian quản lý nội dung lên tới 80%
- Giảm lỗi do thao tác thủ công
- Tích hợp dễ dàng với các hệ thống khác
- Hoạt động liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Storyblok với quyền truy cập API
- API Key từ Storyblok
- n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5361)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Storyblok Tool MCP Server** (Node đầu tiên):
   - Chọn "Credentials" đã được cấu hình với API Key của Storyblok
   - Điền các tham số cần thiết cho thao tác MCP

2. **Delete a story**:
   - Cấu hình ID của story cần xóa
   - Thiết lập các tùy chọn xóa (nếu có)

3. **Get a story**:
   - Cấu hình ID của story cần lấy
   - Chọn các trường dữ liệu cần lấy

4. **Get many stories**:
   - Thiết lập các bộ lọc để lấy nhiều story cùng lúc
   - Cấu hình số lượng story trả về

5. **Publish a story**:
   - Cấu hình ID của story cần publish
   - Thiết lập các tùy chọn publish (nếu có)

6. **Unpublish a story**:
   - Cấu hình ID của story cần unpublish
   - Thiết lập các tùy chọn unpublish (nếu có)

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu với mỗi node để đảm bảo hoạt động đúng
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi các thao tác hoàn thành
- Lưu log các thao tác vào Google Sheets để theo dõi lịch sử
- Tự động gửi báo cáo hàng ngày về các thay đổi nội dung
- Kết hợp với các công cụ khác như Zapier để mở rộng khả năng tích hợp

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn 7 thao tác chính của Storyblok, tiết kiệm thời gian và giảm lỗi. Với khả năng tích hợp dễ dàng, các sếp có thể mở rộng và tối ưu hóa quy trình quản lý nội dung của mình một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!