---
title: "🔄 Tự động đồng bộ liên hệ giữa KlickTipp và Pipedrive - Giải pháp CRM toàn diện"
description: "Hướng dẫn chi tiết cách tự động đồng bộ liên hệ, trạng thái marketing và phân khúc giữa KlickTipp và Pipedrive - tiết kiệm thời gian và đảm bảo dữ liệu luôn đồng bộ 100%"
slug: "tu-dong-dong-bo-klicktipp-pipedrive"
tags: [n8n, automation, no-code, CRM, email-marketing]
keywords: [n8n workflow, tự động hóa CRM, đồng bộ dữ liệu, KlickTipp, Pipedrive]
---

# 🔄 Tự động đồng bộ liên hệ giữa KlickTipp và Pipedrive - Giải pháp CRM toàn diện

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Đồng bộ tự động 2 chiều giữa KlickTipp và Pipedrive trong thời gian gần thực
- Tiết kiệm 80% thời gian thủ công cập nhật dữ liệu
- Đảm bảo dữ liệu luôn đồng bộ giữa hai hệ thống CRM
- Tự động xử lý trạng thái marketing và phân khúc khách hàng
- Giảm thiểu lỗi do nhập liệu thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản KlickTipp và Pipedrive đã kích hoạt
- API keys cho cả hai hệ thống
- Quyền truy cập để tạo webhook và custom fields
- Các sếp cần chuẩn bị:
  - Tạo custom field trong KlickTipp để lưu ID Pipedrive
  - Tạo custom field trong Pipedrive để lưu ID KlickTipp
  - Cấu hình webhook cho cả hai hệ thống
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13233](https://n8n.io/workflows/13233)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Contact tagged in KlickTipp"**:
   - Cấu hình credentials cho KlickTipp API
   - Điền path của webhook KlickTipp (ví dụ: "0b382f31-c74b-4418-bb89-caaa09915282")

2. **Node "Changes in Pipedrive1"**:
   - Cấu hình credentials cho Pipedrive API
   - Đảm bảo webhook Pipedrive đã được kích hoạt

3. **Node "Create a person" và "Update a person"**:
   - Cấu hình credentials cho Pipedrive API
   - Kiểm tra và điều chỉnh các trường dữ liệu cần đồng bộ

4. **Node "Create contact with DOI" và "Create contact with SOI"**:
   - Cấu hình credentials cho KlickTipp API
   - Đảm bảo các trường dữ liệu được ánh xạ đúng

5. **Node "Assign Label Customer" và "Assign Label ABC"**:
   - Cấu hình credentials cho Pipedrive API
   - Điền đúng ID của các label trong Pipedrive

6. **Node "Tag contact in KlickTipp2" và "Tag contact in KlickTipp3"**:
   - Cấu hình credentials cho KlickTipp API
   - Điền đúng ID của các tag trong KlickTipp

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kích hoạt workflow bằng cách nhấn nút "Active" ở góc trên bên phải
3. Theo dõi quá trình đồng bộ dữ liệu trong phần "Executions"

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa báo cáo**: Kết nối với Slack/Telegram để nhận thông báo khi đồng bộ hoàn thành
2. **Lưu log hoạt động**: Thêm node lưu log các thay đổi quan trọng vào Google Sheets
3. **Xử lý lỗi tự động**: Cấu hình email thông báo khi có lỗi xảy ra trong quá trình đồng bộ
4. **Mở rộng phân khúc**: Thêm các phân khúc khách hàng mới bằng cách thêm các node switch và tagging tương ứng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc đồng bộ dữ liệu giữa KlickTipp và Pipedrive, giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi nhập liệu. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các hoạt động quan trọng hơn trong quản lý khách hàng.