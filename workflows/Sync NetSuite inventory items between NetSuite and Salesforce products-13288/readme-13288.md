---
title: "🔄 Đồng bộ sản phẩm NetSuite với Salesforce - Giải pháp tự động hóa CRM hoàn hảo"
description: "Hướng dẫn chi tiết cách tự động đồng bộ sản phẩm giữa NetSuite và Salesforce bằng n8n. Tiết kiệm thời gian, giảm lỗi và duy trì dữ liệu đồng bộ 24/7."
slug: "dong-bo-san-pham-netsuite-salesforce-n8n"
tags: [n8n, automation, no-code, crm, salesforce, netsuite]
keywords: [n8n workflow, tự động hóa crm, đồng bộ sản phẩm, netsuite salesforce, tự động hóa doanh nghiệp]
---

# 🔄 Đồng bộ sản phẩm NetSuite với Salesforce - Giải pháp tự động hóa CRM hoàn hảo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải đồng bộ thủ công giữa hai hệ thống CRM lớn như NetSuite và Salesforce. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ sản phẩm giữa NetSuite và Salesforce mỗi ngày
- Giảm thiểu lỗi nhập liệu thủ công
- Duy trì dữ liệu đồng bộ liên tục 24/7
- Tiết kiệm thời gian và nguồn lực cho đội ngũ bán hàng
- Dữ liệu luôn cập nhật mới nhất giữa hai hệ thống
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản NetSuite với quyền truy cập API
- Tài khoản Salesforce với quyền truy cập API
- Credentials cho cả hai hệ thống (NetSuite OAuth 2.0 và Salesforce OAuth 2.0)
- Trường External ID trong Salesforce để ánh xạ với NetSuite Internal ID
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13288](https://n8n.io/workflows/13288)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoàn tất import và mở workflow trong Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **NetSuite Credentials**:
   - Node: "NS: Inventory Item - Get record", "NS: Inventory Item - Get Delta records", "NS: Inventory Item - Get list of All records"
   - Cấu hình: Thêm NetSuite OAuth 2.0 credentials với các quyền truy cập cần thiết

2. **Salesforce Credentials**:
   - Node: "Salesforce: Add Products", "Salesforce: Get Pricebook values"
   - Cấu hình: Thêm Salesforce OAuth 2.0 credentials với các quyền truy cập cần thiết

3. **Cấu hình phân trang**:
   - Node: "Retrieve Paging Offset and LastExportDate", "Update Paging Offset and LastExportDate"
   - Cấu hình: Đảm bảo biến offset và lastExportDate được khởi tạo đúng

4. **Lọc dữ liệu**:
   - Node: "NS: Inventory Item - Get Delta records" (nếu sử dụng chế độ delta)
   - Cấu hình: Thêm tham số Q để lọc dữ liệu theo nhu cầu (xem tài liệu NetSuite)

5. **Xử lý dữ liệu**:
   - Node: "Prepare Salesforce Payload"
   - Cấu hình: Kiểm tra và điều chỉnh mapping giữa các trường NetSuite và Salesforce

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Chạy workflow với 1-2 sản phẩm mẫu để kiểm tra kết quả
   - Kiểm tra dữ liệu trong cả hai hệ thống để đảm bảo đồng bộ

2. Bật Active workflow:
   - Sau khi kiểm tra thành công, bật chế độ Active
   - Đối với chế độ tự động hóa hàng ngày, đảm bảo node "Execute Workflow Daily" được cấu hình đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**:
   - Thêm node gửi thông báo khi workflow hoàn thành hoặc gặp lỗi
   - Cài đặt cảnh báo cho các trường hợp dữ liệu không đồng bộ

2. **Lưu log hoạt động**:
   - Thêm node ghi log chi tiết các hoạt động đồng bộ
   - Lưu trữ log trong Google Sheets hoặc cơ sở dữ liệu

3. **Tự động báo cáo**:
   - Thêm node tạo báo cáo hàng ngày về số lượng sản phẩm đã đồng bộ
   - Gửi báo cáo qua email hoặc lưu vào hệ thống quản lý

4. **Xử lý lỗi nâng cao**:
   - Thêm node xử lý các trường hợp lỗi cụ thể
   - Tự động retry khi gặp lỗi tạm thời

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc đồng bộ sản phẩm giữa NetSuite và Salesforce. Với việc tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong khi dữ liệu luôn được cập nhật và đồng bộ chính xác. Đừng để công việc thủ công làm chậm lại quá trình kinh doanh - áp dụng ngay workflow này để tối ưu hóa quy trình CRM của doanh nghiệp!