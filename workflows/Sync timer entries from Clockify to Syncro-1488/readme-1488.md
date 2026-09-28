```yaml
---
title: "🚀 Tự động đồng bộ dữ liệu thời gian từ Clockify sang Syncro với n8n"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu thời gian từ Clockify sang Syncro bằng workflow n8n, tiết kiệm thời gian và giảm sai sót thủ công"
slug: "tu-dong-dong-bo-du-lieu-thoi-gian-tu-clockify-sang-syncro"
tags: [n8n, automation, no-code, clockify, syncro]
keywords: [n8n workflow, tự động hóa, clockify, syncro, thời gian làm việc]
---
```

# 🚀 Tự động đồng bộ dữ liệu thời gian từ Clockify sang Syncro với n8n

[Các sếp] có biết không? Mỗi khi phải chuyển đổi dữ liệu thời gian làm việc từ Clockify sang Syncro thủ công, không chỉ tốn thời gian mà còn dễ xảy ra sai sót. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc đồng bộ dữ liệu
- Giảm thiểu sai sót do nhập liệu thủ công
- Tự động hóa toàn bộ quá trình từ Clockify đến Syncro
- Dữ liệu luôn được cập nhật mới nhất
- Tích hợp dễ dàng với các hệ thống khác trong công ty
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Clockify với quyền truy cập API
- Tài khoản Syncro với quyền truy cập API
- Tài khoản Google với quyền truy cập Google Sheets API
- API keys cho cả hai dịch vụ trên
- Biết cách tạo và cấu hình credentials trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [workflow gốc](https://n8n.io/workflows/1488)
2. Click vào nút "Download" để tải file JSON về máy
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về
4. Hoặc các sếp có thể copy toàn bộ JSON từ trang web và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm nhiều node quan trọng cần được cấu hình:

1. **Webhook Node**:
   - Path: `82b654d7-aeb2-4cc1-97a8-0ebd1a729202`
   - HTTP Method: POST
   - Các sếp có thể thay đổi path này thành bất kỳ giá trị nào phù hợp với hệ thống của mình

2. **Google Sheets Nodes**:
   - Tất cả các node Google Sheets đều sử dụng credentials "googleApi"
   - Các sếp cần cấu hình credentials này trước khi sử dụng
   - Các node này thực hiện các thao tác:
     - `append`: Thêm dữ liệu mới vào Google Sheets
     - `lookup`: Tìm kiếm dữ liệu trong Google Sheets

3. **HTTP Request Nodes**:
   - `NewSyncroTimer`: Tạo timer mới trong Syncro
   - `UpdateSyncroTimer`: Cập nhật timer trong Syncro
   - Cả hai node này đều sử dụng credentials "httpHeaderAuth"
   - Các sếp cần cấu hình credentials này với API key của Syncro

4. **Function Node**:
   - `MatchTechnician`: Hàm này ánh xạ kỹ thuật viên từ Clockify sang Syncro
   - Các sếp có thể chỉnh sửa hàm này để phù hợp với cấu trúc dữ liệu của công ty

5. **Set Nodes**:
   - `ForGoogle`: Cấu hình các biến cho Google Sheets
   - `ForSyncro`: Cấu hình các biến cho Syncro
   - `EnvVariables`: Cấu hình các biến môi trường
   - `SetTechnicians`: Cấu hình danh sách kỹ thuật viên

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình xong tất cả các node quan trọng:

1. Các sếp nên test workflow với dữ liệu mẫu trước khi chạy thực tế
2. Sau khi test thành công, các sếp có thể kích hoạt workflow bằng cách bật nút "Active"
3. Workflow sẽ tự động chạy theo lịch trình được cấu hình trong node Webhook

### ✍️ Mẹo & gợi ý nâng cao
1. Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận thông báo khi đồng bộ hoàn tất
2. Để lưu log các hoạt động, các sếp có thể thêm node Google Sheets để ghi lại lịch sử đồng bộ
3. Nếu công ty có nhiều dự án, các sếp có thể tạo nhiều bản sao của workflow này và cấu hình riêng cho từng dự án
4. Các sếp có thể lập lịch chạy workflow theo định kỳ bằng cách sử dụng node Schedule trong n8n

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ dữ liệu thời gian từ Clockify sang Syncro, tiết kiệm thời gian và giảm thiểu sai sót. Với việc tự động hóa này, các sếp có thể tập trung vào công việc quan trọng hơn thay vì phải tốn thời gian cho các công việc lặp lại. Hãy thử ngay và trải nghiệm sự tiện lợi mà n8n mang lại!