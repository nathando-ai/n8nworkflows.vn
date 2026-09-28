---
title: "🚀 Tự động chèn watermark cho hàng loạt ảnh giữa 2 thư mục Google Drive"
description: "Hướng dẫn tự động hóa chèn watermark cho hàng loạt ảnh giữa 2 thư mục Google Drive bằng n8n, tiết kiệm thời gian và đảm bảo thương hiệu"
slug: "tu-dong-chen-watermark-anh-google-drive"
tags: [n8n, automation, no-code, google-drive, watermark]
keywords: [n8n workflow, tự động hóa, watermark ảnh, google drive, xử lý hàng loạt ảnh]
---

# 🚀 Tự động chèn watermark cho hàng loạt ảnh giữa 2 thư mục Google Drive

[Các sếp đang gặp khó khăn khi phải chèn watermark thủ công cho hàng loạt ảnh trong Google Drive. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi xử lý hàng loạt ảnh
- Đảm bảo thương hiệu bằng cách chèn watermark tự động
- Tự động hóa toàn bộ quy trình xử lý ảnh
- Tăng tính chuyên nghiệp cho các dự án ảnh
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập vào 2 thư mục (nguồn và đích)
- Thiết lập OAuth2 cho Google Drive trong n8n
- ID của 2 thư mục Google Drive (nguồn và đích)
- Quyền truy cập vào n8n Editor để import và cấu hình workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/15249](https://n8n.io/workflows/15249)
3. Hoặc tải file JSON về máy và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Manual Trigger**:
   - Node này dùng để kích hoạt workflow thủ công
   - Không cần cấu hình gì đặc biệt

2. **Google Drive: List Files in Folder A**:
   - Kết nối với tài khoản Google Drive của bạn
   - Thay thế `YOUR_FOLDER_A_ID` bằng ID thực của thư mục nguồn
   - Đảm bảo tài khoản có quyền truy cập vào thư mục này

3. **Filter: Images Only**:
   - Node này tự động lọc chỉ giữ lại các file ảnh
   - Không cần cấu hình gì thêm

4. **Loop: One Image at a Time**:
   - Node này xử lý từng ảnh một để tránh quá tải bộ nhớ
   - Không cần cấu hình gì thêm

5. **Google Drive: Download Image**:
   - Kết nối với tài khoản Google Drive của bạn
   - Đảm bảo đã thiết lập credentials Google Drive OAuth2
   - Không cần cấu hình gì thêm

6. **Edit Image: Apply Watermark**:
   - Cấu hình watermark theo yêu cầu:
     - Text: Nhập văn bản watermark của bạn
     - Font size: Chọn kích thước phù hợp
     - Colour: Chọn màu sắc cho watermark
     - Opacity: Điều chỉnh độ mờ của watermark
     - Position: Chọn vị trí đặt watermark (góc trên trái, giữa, dưới, v.v.)

7. **Google Drive: Upload to Folder B**:
   - Kết nối với tài khoản Google Drive của bạn
   - Thay thế `YOUR_FOLDER_B_ID` bằng ID thực của thư mục đích
   - Đảm bảo tài khoản có quyền ghi vào thư mục này

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trong thư mục đích để đảm bảo watermark được chèn đúng
3. Nếu mọi thứ ổn, nhấn "Activate Workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Để lấy ID thư mục Google Drive, mở thư mục trong Google Drive và sao chép phần cuối của URL: "https://drive.google.com/drive/folders/YOUR_FOLDER_ID"
- Có thể kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Để xử lý nhiều ảnh cùng lúc, có thể tăng số lượng batch trong node "Loop: One Image at a Time"
- Có thể lưu log xử lý vào Google Sheets để theo dõi tiến độ
- Có thể thêm bước gửi email báo cáo khi hoàn thành xử lý

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình chèn watermark cho hàng loạt ảnh giữa 2 thư mục Google Drive. Với chỉ vài bước cấu hình đơn giản, các sếp có thể tiết kiệm thời gian đáng kể và đảm bảo thương hiệu cho các dự án ảnh của mình. Hãy áp dụng ngay để nâng cao hiệu quả làm việc!