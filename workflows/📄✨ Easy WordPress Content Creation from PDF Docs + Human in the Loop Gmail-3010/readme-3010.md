---
title: "🚀 Tự động hóa tạo bài viết WordPress từ PDF + Xác nhận người dùng qua Gmail"
description: "Hướng dẫn chi tiết workflow n8n tự động chuyển đổi PDF thành bài viết WordPress chuyên nghiệp, bao gồm tạo hình ảnh AI, xác nhận nội dung và thông báo kết quả."
slug: "tu-dong-hoa-tao-bai-viet-wordpress-tu-pdf"
tags: [n8n, automation, no-code, wordpress, ai]
keywords: [n8n workflow, tự động hóa, tạo nội dung, pdf to wordpress, ai content generation]
---

# 🚀 Tự động hóa tạo bài viết WordPress từ PDF + Xác nhận người dùng qua Gmail

[Các sếp đang gặp khó khăn khi phải chuyển đổi tài liệu PDF thành bài viết WordPress chuyên nghiệp một cách thủ công. Quá trình này tốn thời gian, dễ sai sót và không đảm bảo tính nhất quán về chất lượng nội dung. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ trích xuất nội dung đến xuất bản bài viết, đồng thời tích hợp xác nhận nội dung qua email để đảm bảo chất lượng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động chuyển đổi PDF thành bài viết WordPress trong vòng vài phút.
- Chất lượng nội dung: Sử dụng AI tạo tiêu đề và nội dung chuyên nghiệp, đồng thời có xác nhận người dùng.
- Tính nhất quán: Đảm bảo định dạng và chất lượng nội dung thống nhất.
- Tích hợp đa kênh: Thông báo kết quả qua email và Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để tạo nội dung bằng AI).
- Tài khoản WordPress với quyền quản trị (để tạo bài viết và tải ảnh).
- Tài khoản Gmail (để gửi email xác nhận nội dung).
- Tài khoản Telegram (để nhận thông báo kết quả).
- Tài khoản imgbb (để lưu trữ ảnh tạo bởi AI).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/3010](https://n8n.io/workflows/3010).
2. Nhấn nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Upload PDF"**:
   - Đảm bảo đường dẫn "path" là "pdf" để trùng khớp với form trigger.

2. **Node "gpt-4o-mini"**:
   - Thêm credentials OpenAI API.
   - Điều chỉnh prompt trong node để phù hợp với phong cách nội dung của các sếp.

3. **Node "Create Wordpress Post"**:
   - Thêm credentials WordPress API.
   - Kiểm tra các tham số như "status" (draft/publish) và "categories".

4. **Node "Human In The Loop Approve Blog Post"**:
   - Thêm credentials Gmail OAuth2.
   - Cập nhật địa chỉ email người nhận xác nhận nội dung.

5. **Node "Send Error Message"**:
   - Thêm credentials Telegram API.
   - Cập nhật ID chat hoặc tên người dùng Telegram để nhận thông báo lỗi.

6. **Node "Save Image to imgbb.com"**:
   - Thêm API key của imgbb vào URL request.
   - Kiểm tra định dạng ảnh (JPEG/PNG) và kích thước tối đa.

#### 3. Kích hoạt ⚡️
1. Kiểm tra workflow bằng cách gửi một file PDF mẫu vào form trigger.
2. Đảm bảo tất cả các node hoạt động đúng và không có lỗi.
3. Bật chế độ Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung AI**: Điều chỉnh prompt trong node "gpt-4o-mini" để phù hợp với phong cách viết và chủ đề của các sếp.
2. **Tích hợp Slack**: Thay thế node Telegram bằng node Slack để nhận thông báo trên Slack.
3. **Lưu log hoạt động**: Thêm node lưu log hoạt động vào workflow để theo dõi lịch sử tạo bài viết.
4. **Tự động hóa định kỳ**: Sử dụng node Schedule Trigger để tự động xử lý các file PDF mới theo lịch trình.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình tạo bài viết WordPress từ PDF, từ trích xuất nội dung đến xuất bản bài viết, đồng thời tích hợp xác nhận nội dung qua email để đảm bảo chất lượng. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả làm việc! 🎉