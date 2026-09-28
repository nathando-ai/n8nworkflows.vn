---
title: "📊 Theo dõi tương tác bài viết Facebook tự động với Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi tương tác (like, comment, share) trên Facebook và lưu kết quả vào Google Sheets để báo cáo hiệu suất"
slug: "theo-doi-tuong-tac-facebook-google-sheets"
tags: [n8n, automation, social media, google sheets, facebook]
keywords: [n8n workflow, tự động hóa, facebook analytics, google sheets, social media tracking]
---

# 📊 Theo dõi tương tác bài viết Facebook tự động với Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải theo dõi tương tác trên Facebook một cách thủ công? Với workflow này, các sếp có thể tự động hóa việc thu thập dữ liệu tương tác (like, comment, share) từ trang Facebook và lưu trữ vào Google Sheets một cách tự động, giúp tiết kiệm thời gian và tăng hiệu suất làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động thu thập dữ liệu tương tác từ Facebook mà không cần can thiệp thủ công.
- Dữ liệu chính xác: Dữ liệu được lưu trữ và cập nhật tự động vào Google Sheets, đảm bảo tính chính xác và cập nhật liên tục.
- Dễ dàng báo cáo: Dữ liệu được tổ chức rõ ràng trong Google Sheets, giúp các sếp dễ dàng tạo báo cáo và phân tích hiệu suất.
- Hoạt động liên tục: Workflow có thể được lập lịch để chạy định kỳ, đảm bảo dữ liệu luôn được cập nhật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook và quyền truy cập vào trang Facebook cần theo dõi.
- Tài khoản Google và quyền truy cập vào Google Sheets.
- API Key từ Facebook Graph API và Google Sheets API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/13462](https://n8n.io/workflows/13462).
2. Nhấp vào nút "Import" để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấp vào nút "Import" và chọn file JSON đã tải xuống.

Hoặc, các sếp có thể copy/paste JSON vào n8n Editor bằng cách:

1. Copy nội dung JSON từ trang [n8n.io/workflows/13462](https://n8n.io/workflows/13462).
2. Trong n8n Editor, nhấp vào nút "Import" và chọn "Paste JSON".
3. Dán nội dung JSON vào ô nhập liệu và nhấp vào "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When clicking ‘Execute workflow’ (manualTrigger)**: Node này kích hoạt workflow khi các sếp nhấp vào nút "Execute workflow" trong n8n Editor.
- **Set Max Posts (set)**: Node này đặt số lượng bài viết tối đa cần phân tích. Các sếp cần điều chỉnh giá trị này theo nhu cầu.
- **Get Page Info (facebookGraphApi)**: Node này lấy thông tin trang Facebook. Các sếp cần cấu hình credentials cho Facebook Graph API.
- **Get Page Feed (facebookGraphApi)**: Node này lấy danh sách bài viết từ trang Facebook. Các sếp cần cấu hình credentials cho Facebook Graph API.
- **Get comments (facebookGraphApi)**: Node này lấy danh sách bình luận cho từng bài viết. Các sếp cần cấu hình credentials cho Facebook Graph API.
- **Get Likes (facebookGraphApi)**: Node này lấy danh sách lượt thích cho từng bài viết. Các sếp cần cấu hình credentials cho Facebook Graph API.
- **Get Shares (facebookGraphApi)**: Node này lấy danh sách lượt chia sẻ cho từng bài viết. Các sếp cần cấu hình credentials cho Facebook Graph API.
- **Add n. likes (googleSheets)**: Node này thêm số lượng lượt thích vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets API và điền thông tin về Spreadsheet ID và Sheet Name.
- **Add n. comments (googleSheets)**: Node này thêm số lượng bình luận vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets API và điền thông tin về Spreadsheet ID và Sheet Name.
- **Add n. shares (googleSheets)**: Node này thêm số lượng lượt chia sẻ vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets API và điền thông tin về Spreadsheet ID và Sheet Name.

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**: Các sếp nên chạy workflow với dữ liệu mẫu để kiểm tra tính chính xác và hiệu suất.
- **Bật Active workflow**: Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, các sếp có thể bật chế độ Active để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lập lịch chạy định kỳ**: Các sếp có thể thay thế node "manualTrigger" bằng node "Schedule Trigger" để workflow chạy tự động theo lịch trình.
- **Thêm thông báo**: Các sếp có thể thêm node "Slack" hoặc "Email" để nhận thông báo khi workflow hoàn thành.
- **Tích hợp với các công cụ khác**: Các sếp có thể tích hợp workflow với các công cụ khác như Google Analytics, Google Data Studio để tạo báo cáo chi tiết hơn.
- **Tối ưu hiệu suất**: Các sếp có thể điều chỉnh số lượng bài viết tối đa và thời gian chờ giữa các node để tránh bị giới hạn API.

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hiệu quả để theo dõi tương tác trên Facebook và lưu trữ dữ liệu vào Google Sheets. Với các bước cấu hình đơn giản và hiệu suất cao, các sếp có thể tiết kiệm thời gian và tăng hiệu suất làm việc. Hãy áp dụng ngay để bắt đầu theo dõi tương tác trên Facebook một cách tự động và hiệu quả!