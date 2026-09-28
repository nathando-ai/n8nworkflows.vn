---
title: "🌍 Tự động hóa Dịch tài liệu đa ngôn ngữ với Google Drive và DeepL"
description: "Hướng dẫn chi tiết cách tự động dịch tài liệu PDF, DOCX, TXT, Markdown sang nhiều ngôn ngữ chỉ với Google Drive và DeepL"
slug: "tu-dong-hoa-dich-tai-lieu-da-ngon-ngu-google-drive-deepl"
tags: [n8n, automation, no-code, google-drive, deepl, document-translation]
keywords: [n8n workflow, tự động hóa, dịch tài liệu, google drive, deepl, pdf, docx, txt, markdown]
---

# 🌍 Tự động hóa Dịch tài liệu đa ngôn ngữ với Google Drive và DeepL

[Các sếp] có bao giờ phải dịch thủ công tài liệu sang nhiều ngôn ngữ không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình dịch tài liệu từ Google Drive sang nhiều ngôn ngữ chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc dịch tài liệu thủ công
- Đảm bảo độ chính xác cao nhờ công nghệ dịch thuật DeepL
- Tự động lưu trữ các bản dịch trong Google Drive với tên file rõ ràng (kèm mã ngôn ngữ)
- Nhận thông báo email khi quá trình dịch hoàn thành
- Tích hợp tùy chọn với Notion để theo dõi lịch sử dịch
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập vào thư mục nguồn và đích
- API Key của DeepL (có thể dùng phiên bản miễn phí với hạn mức 500,000 ký tự/tháng)
- Tài khoản Gmail để nhận thông báo
- (Tùy chọn) Tài khoản Notion để lưu lịch sử dịch
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10264](https://n8n.io/workflows/10264)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của các sếp

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Configuration (Edit Here)"** (nút màu vàng):
   - Thay đổi `sourceFolderId` thành ID thư mục Google Drive nơi các sếp muốn theo dõi
   - Thay đổi `destinationFolderId` thành ID thư mục đích để lưu các bản dịch
   - Điều chỉnh `targetLanguages` theo nhu cầu (mặc định: EN, ZH, KO, ES, FR, DE)
   - Cập nhật `notificationEmail` với địa chỉ email nhận thông báo

2. **Credentials**:
   - Thêm credentials cho Google Drive (OAuth2)
   - Thêm credentials cho DeepL API
   - Thêm credentials cho Gmail (OAuth2)
   - (Tùy chọn) Thêm credentials cho Notion API

3. **Node "Google Drive Trigger"**:
   - Đảm bảo đã chọn đúng credentials Google Drive
   - Kiểm tra lại `sourceFolderId` đã được cấu hình đúng

#### 3. Kích hoạt ⚡️
1. Chạy test với một file mẫu để kiểm tra toàn bộ quy trình
2. Bật Active workflow sau khi đã kiểm tra kỹ
3. Upload một file vào thư mục nguồn để bắt đầu quá trình dịch

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh ngôn ngữ**:
   - Thêm hoặc bớt ngôn ngữ trong mảng `targetLanguages` trong node "Configuration"
   - Đảm bảo DeepL API có hỗ trợ các ngôn ngữ này

2. **Tích hợp Slack**:
   - Thay thế node "Send Gmail Notification" bằng node Slack
   - Cấu hình webhook Slack để nhận thông báo

3. **Lưu log dịch**:
   - Thêm node "Write to File" sau node "Aggregate Translations" để lưu log chi tiết

4. **Xử lý lỗi nâng cao**:
   - Tùy chỉnh node "Error Handler" để xử lý các trường hợp lỗi cụ thể

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình dịch tài liệu đa ngôn ngữ, từ việc theo dõi file mới trong Google Drive đến việc lưu trữ các bản dịch hoàn chỉnh. Với việc tích hợp DeepL và Google Drive, các sếp có thể tiết kiệm thời gian đáng kể trong khi vẫn đảm bảo chất lượng dịch thuật cao. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!