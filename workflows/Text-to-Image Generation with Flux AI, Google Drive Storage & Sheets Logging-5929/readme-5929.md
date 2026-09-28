---
title: "🎨 Tự động hóa tạo ảnh từ văn bản với Flux AI + Google Drive + Sheets"
description: "Hướng dẫn chi tiết cách tự động tạo ảnh từ văn bản bằng Flux AI, lưu vào Google Drive và ghi log vào Google Sheets - giải pháp hoàn toàn không cần code"
slug: "tu-dong-hoa-tao-anh-tu-van-ban-flux-ai-google-drive-sheets"
tags: [n8n, automation, no-code, ai, google-drive, google-sheets]
keywords: [n8n workflow, tự động hóa, tạo ảnh từ văn bản, flux ai, google drive, google sheets]
---

# 🎨 Tự động hóa tạo ảnh từ văn bản với Flux AI + Google Drive + Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải tạo nhiều ảnh từ văn bản thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tạo hàng trăm ảnh từ văn bản chỉ trong vài phút
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công
- Lưu trữ an toàn: Ảnh được lưu tự động vào Google Drive
- Theo dõi dễ dàng: Ghi log chi tiết vào Google Sheets
- Phát hiện lỗi tự động: Nếu có lỗi trong quá trình tạo ảnh, hệ thống sẽ ghi log lỗi ngay lập tức
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Drive và Google Sheets
- API Key từ RapidAPI cho Flux AI Text-to-Image Generator
- Thư mục Google Drive để lưu ảnh
- Google Sheet để ghi log (có thể tạo mới)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5929](https://n8n.io/workflows/5929)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Không cần cấu hình gì thêm, chỉ cần đảm bảo form hoạt động

2. **Node "HTTP Request"**:
   - Cần cấu hình credentials cho RapidAPI
   - Thêm header "X-RapidAPI-Key" với giá trị là API Key của bạn
   - Thêm header "X-RapidAPI-Host" với giá trị "text-to-image-generator-flux.p.rapidapi.com"

3. **Node "Google Drive"**:
   - Cấu hình credentials cho Google API
   - Chọn "Upload File" operation
   - Chỉ định folder ID trong Google Drive để lưu ảnh

4. **Node "Google Sheets" (Success Log)**:
   - Cấu hình credentials cho Google API
   - Chọn "Append" operation
   - Chỉ định Spreadsheet ID và Sheet Name
   - Đảm bảo các cột trong sheet phù hợp với dữ liệu đầu ra (prompt, filename, date)

5. **Node "Google Sheets5" (Error Log)**:
   - Cấu hình credentials cho Google API
   - Chọn "Append or Update" operation
   - Chỉ định Spreadsheet ID và Sheet Name khác với node Success Log
   - Đảm bảo các cột trong sheet phù hợp với dữ liệu lỗi (prompt, error message, date)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" ở góc trên bên phải
2. Test workflow bằng cách submit một prompt mẫu qua form
3. Kiểm tra kết quả trong Google Drive và Google Sheets

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi tạo ảnh thành công hoặc thất bại
2. **Lịch sử tạo ảnh**: Thêm node lưu log chi tiết hơn bao gồm thời gian tạo, kích thước ảnh, v.v.
3. **Tự động hóa báo cáo**: Tạo workflow định kỳ gửi báo cáo tổng hợp các ảnh đã tạo trong ngày
4. **Xử lý batch**: Sửa đổi form để chấp nhận nhiều prompt cùng lúc và xử lý song song

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong quá trình tạo ảnh từ văn bản. Với khả năng tự động hóa hoàn toàn và lưu trữ an toàn, đây là giải pháp lý tưởng cho các doanh nghiệp cần tạo nhiều ảnh từ văn bản một cách nhanh chóng và hiệu quả. Hãy thử ngay và trải nghiệm sự tiện lợi mà công nghệ tự động hóa mang lại!