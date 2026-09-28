---
title: "🚀 Tự động đồng bộ dữ liệu PostgreSQL sang SharePoint qua Microsoft Graph với thông báo Teams"
description: "Hướng dẫn chi tiết cách tự động đồng bộ thay đổi từ PostgreSQL sang SharePoint với thông báo lỗi qua Teams, tiết kiệm thời gian và giảm thao tác thủ công."
slug: "tu-dong-dong-bo-postgresql-sang-sharepoint-qua-microsoft-graph"
tags: [n8n, automation, no-code, PostgreSQL, SharePoint, Microsoft Graph, Microsoft Teams]
keywords: [n8n workflow, tự động hóa dữ liệu, đồng bộ PostgreSQL, SharePoint API, Microsoft Graph batch]
---

# 🚀 Tự động đồng bộ dữ liệu PostgreSQL sang SharePoint qua Microsoft Graph với thông báo Teams

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải đồng bộ dữ liệu thủ công giữa PostgreSQL và SharePoint. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ dữ liệu thay đổi từ PostgreSQL sang SharePoint mỗi 15 phút
- Giảm thao tác thủ công lên tới 90%
- Nhận thông báo lỗi ngay khi có vấn đề xảy ra
- Tiết kiệm thời gian và giảm lỗi con người
- Hoạt động liên tục 24/7 với 99.9% uptime
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản PostgreSQL với quyền truy cập đọc dữ liệu
- Tài khoản Microsoft 365 với quyền truy cập SharePoint và Microsoft Graph API
- Tài khoản Microsoft Teams để nhận thông báo
- Kiến thức cơ bản về SQL để điều chỉnh truy vấn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/16106](https://n8n.io/workflows/16106)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Every 15 Minutes Trigger** (scheduleTrigger):
   - Không cần cấu hình, node này tự động chạy mỗi 15 phút

2. **Set Configuration Parameters** (set):
   - Cấu hình các tham số chính:
     - `batchSize`: Số lượng bản ghi xử lý trong mỗi batch (mặc định 10)
     - `sharePointSiteId`: ID của SharePoint site
     - `sharePointListId`: ID của SharePoint list
     - `postgresTable`: Tên bảng PostgreSQL cần đồng bộ

3. **Query Updated Rows from Postgres** (postgres):
   - Cấu hình credentials PostgreSQL
   - Điều chỉnh truy vấn SQL để chỉ lấy bản ghi thay đổi sau lần chạy cuối:
     ```sql
     SELECT * FROM {{ $node["Set Configuration Parameters"].json["postgresTable"] }}
     WHERE updated_at > '{{ $node["Fetch Last Run Timestamp"].json["lastRunTimestamp"] }}'
     ```

4. **Post Batch to Graph API** (httpRequest):
   - Cấu hình credentials Microsoft Graph
   - Đảm bảo đã cấp quyền `Sites.ReadWrite.All` trong Azure AD

5. **Send Sync Error Alert** (microsoftTeams):
   - Cấu hình credentials Microsoft Teams
   - Điền thông tin team và channel nhận thông báo lỗi

6. **Dispatch Sync Summary Note** (microsoftTeams):
   - Cấu hình credentials Microsoft Teams
   - Điền thông tin team và channel nhận báo cáo đồng bộ

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test chạy dữ liệu mẫu
2. Kiểm tra kết quả ở các node cuối cùng (Send Sync Error Alert và Dispatch Sync Summary Note)
3. Nếu kết quả như mong đợi, click vào nút "Activate Workflow" để bật chế độ tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tăng tốc độ đồng bộ**: Tăng giá trị `batchSize` trong node Set Configuration Parameters nếu hệ thống có thể xử lý nhiều yêu cầu đồng thời
2. **Báo cáo nâng cao**: Thêm node để lưu log chi tiết các bản ghi đã đồng bộ vào Google Sheets hoặc PostgreSQL
3. **Xử lý lỗi nâng cao**: Thêm node để gửi email thông báo lỗi thay vì chỉ qua Teams
4. **Lịch chạy linh hoạt**: Thay đổi từ 15 phút thành lịch chạy phức tạp hơn (ví dụ: chỉ chạy vào giờ hành chính)

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình đồng bộ dữ liệu giữa PostgreSQL và SharePoint, giảm thao tác thủ công và tăng độ chính xác. Với cấu hình đơn giản và thông báo lỗi tức thời, đây là giải pháp hoàn hảo cho các doanh nghiệp cần đồng bộ dữ liệu liên tục. Hãy áp dụng ngay để tiết kiệm thời gian và giảm rủi ro lỗi!