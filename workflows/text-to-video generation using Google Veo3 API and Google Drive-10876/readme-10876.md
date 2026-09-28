---
title: "🎬 Tự động hóa tạo video CGI với Google Veo3 API & Google Drive"
description: "Hướng dẫn tự động hóa quy trình tạo video CGI từ văn bản bằng Google Veo3 API, tải lên Google Drive và gửi thông báo qua email - hoàn toàn không cần code"
slug: "tu-dong-hoa-tao-video-cgi-voi-google-veo3-api-va-google-drive"
tags: [n8n, automation, no-code, google-drive, google-veo3, content-creation, ai-video]
keywords: [n8n workflow, tự động hóa video, google veo3 api, tạo video từ văn bản, google drive automation]
---

# 🎬 Tự động hóa tạo video CGI với Google Veo3 API & Google Drive

[Các sếp] có biết rằng việc tạo video CGI từ văn bản thường tốn nhiều thời gian và công sức? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ tạo video đến chia sẻ kết quả - chỉ với vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo video CGI trong vài phút thay vì vài giờ
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi khởi động
- **Chia sẻ dễ dàng**: Video được tự động tải lên Google Drive và chia sẻ
- **Theo dõi tiến trình**: Nhận thông báo email khi video hoàn thành hoặc gặp lỗi
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ
- API Key của Google Veo3
- Thiết lập SMTP cho gửi email (Gmail, Outlook, v.v.)
- Form để nhận prompt từ người dùng (có thể sử dụng Google Forms hoặc Form trong n8n)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/10876)
2. Chọn "Copy JSON" và lưu file JSON vào máy
3. Trong n8n Editor, nhấn "Import from file" và chọn file JSON đã lưu

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Đảm bảo form có trường "prompt" để nhận văn bản đầu vào
   - Cấu hình form để nhận dữ liệu từ người dùng

2. **Node "Veo 3 API Processor"**:
   - Thêm API Key của Google Veo3 vào credentials
   - Kiểm tra endpoint API có chính xác không

3. **Node "Upload File to Google Drive"**:
   - Thiết lập credentials Google Drive OAuth2
   - Chỉ định thư mục đích trong Google Drive

4. **Node "Set Google Drive Permissions"**:
   - Cấu hình quyền chia sẻ phù hợp (viewer, editor, owner)
   - Thêm email người nhận nếu cần

5. **Các node gửi email**:
   - Cấu hình SMTP credentials cho từng node email
   - Điền địa chỉ email người nhận
   - Tùy chỉnh nội dung email theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu:
   - Submit form với prompt mẫu
   - Kiểm tra từng bước xử lý trong workflow
2. Sau khi test thành công, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo đến kênh chat khi video hoàn thành
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets để theo dõi lịch sử tạo video
3. **Tự động hóa báo cáo**: Thêm node gửi báo cáo hàng tuần về số lượng video đã tạo
4. **Xử lý lỗi nâng cao**: Thêm node gửi thông báo đến số điện thoại khi gặp lỗi nghiêm trọng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình tạo video CGI từ văn bản, từ tạo video đến chia sẻ kết quả. Với việc tích hợp Google Veo3 API và Google Drive, các sếp có thể tiết kiệm thời gian đáng kể và đảm bảo quy trình làm việc được thực hiện một cách chuyên nghiệp. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!