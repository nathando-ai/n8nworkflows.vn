---
title: "🚀 Tự động hóa chuyển đổi ảnh selfie thành ảnh chuyên nghiệp cho LinkedIn với Nano Banana Pro & Telegram"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi ảnh selfie thành ảnh chuyên nghiệp cho LinkedIn bằng công nghệ AI Nano Banana Pro và Telegram, tiết kiệm thời gian và nâng cao hình ảnh cá nhân"
slug: "tu-dong-hoa-chuyen-doi-anh-selfie-thanh-anh-chuyen-nghiep-linkedin"
tags: [n8n, automation, no-code, AI, content creation]
keywords: [n8n workflow, tự động hóa, Nano Banana Pro, LinkedIn, ảnh chuyên nghiệp]
---

# 🚀 Tự động hóa chuyển đổi ảnh selfie thành ảnh chuyên nghiệp cho LinkedIn với Nano Banana Pro & Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải tự tay chỉnh sửa ảnh selfie thành ảnh chuyên nghiệp cho LinkedIn. Quá trình này tốn thời gian, yêu cầu kỹ năng chỉnh sửa ảnh và đôi khi không đạt được kết quả như mong muốn. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần code, chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình từ 30 phút xuống còn vài giây
- Chất lượng ảnh chuyên nghiệp: Sử dụng công nghệ AI Nano Banana Pro để nâng cao hình ảnh
- Tích hợp Telegram: Cho phép người dùng gửi ảnh trực tiếp qua Telegram
- Lưu trữ đa dạng: Ảnh kết quả được lưu tự động lên Google Drive và FTP
- Hoạt động liên tục: Workflow chạy 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và ID người dùng
- API Key từ Fal.ai (Nano Banana Pro)
- Tài khoản Google Drive với quyền truy cập đầy đủ
- Thông tin FTP (Server Path, Base URL)
- Ảnh selfie cần chuyển đổi (có thể gửi qua Telegram hoặc nhập URL trực tiếp)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/11458)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

Hoặc có thể copy/paste JSON trực tiếp vào n8n Editor:

```json
{
  "nodes": [
    // Danh sách các nodes từ workflow gốc
  ],
  "connections": [
    // Danh sách các kết nối giữa nodes
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Sanitaze"**:
   - Thay thế XXXX trong code bằng Telegram User ID của bạn
   - Ví dụ: `if (message.text.includes('XXXX')) {`

2. **Node "Create Image"**:
   - Cấu hình "Header Auth" với:
     - Name: "Authorization"
     - Value: "Key YOURAPIKEY" (thay YOURAPIKEY bằng API Key từ Fal.ai)

3. **Node "Set FTP params"**:
   - Cấu hình các tham số FTP:
     - ftp_path: Đường dẫn đến thư mục lưu trữ trên server FTP
     - base_url: URL cơ sở của website (ví dụ: https://website.com/images/)

4. **Node "Upload Image" (Google Drive)**:
   - Cấu hình Google Drive OAuth2 và chọn thư mục lưu trữ

5. **Node "Telegram Trigger"**:
   - Cấu hình Telegram API và chọn bot để nhận ảnh

6. **Node "Get Image"**:
   - Đảm bảo đã cấu hình đúng Telegram API credentials

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Execute workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Drive và FTP để đảm bảo ảnh đã được chuyển đổi và lưu thành công
3. Nếu mọi thứ hoạt động tốt, click vào nút "Active workflow" để kích hoạt workflow chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack**: Thêm node Slack để nhận thông báo khi quá trình chuyển đổi hoàn thành
2. **Lưu log**: Thêm node để ghi log quá trình xử lý cho việc theo dõi và debug
3. **Gửi báo cáo định kỳ**: Tự động gửi báo cáo hàng ngày về số lượng ảnh đã xử lý
4. **Tối ưu hóa chất lượng**: Thử nghiệm với các prompt khác nhau trong node "Create Image" để đạt được kết quả tốt nhất

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quá trình chuyển đổi ảnh selfie thành ảnh chuyên nghiệp cho LinkedIn. Với sự tích hợp của Nano Banana Pro AI và Telegram, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao hình ảnh cá nhân một cách chuyên nghiệp. Hãy áp dụng ngay để nâng cao hình ảnh cá nhân và tạo ấn tượng tốt với đối tác và khách hàng!