---
title: "🚀 Đồng bộ sản phẩm giữa Airtable và Shopify với quản lý tồn kho"
description: "Hướng dẫn tự động hóa đồng bộ sản phẩm từ Airtable sang Shopify với quản lý tồn kho, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "dong-bo-san-pham-airtable-shopify-quan-ly-ton-kho"
tags: [n8n, automation, no-code, airtable, shopify]
keywords: [n8n workflow, tự động hóa, airtable, shopify, quản lý tồn kho]
---

# 🚀 Đồng bộ sản phẩm giữa Airtable và Shopify với quản lý tồn kho

[Các sếp đang gặp khó khăn khi phải đồng bộ thủ công sản phẩm giữa Airtable và Shopify, dẫn đến mất thời gian và dễ xảy ra lỗi. Workflow này giúp tự động hóa toàn bộ quá trình đồng bộ, đảm bảo dữ liệu luôn đồng bộ và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ sản phẩm từ Airtable sang Shopify
- Quản lý tồn kho tự động theo từng vị trí kho
- Giảm thiểu lỗi thủ công
- Tiết kiệm thời gian đáng kể trong quá trình quản lý sản phẩm
- Dữ liệu luôn đồng bộ và chính xác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtable với bảng sản phẩm đã cấu hình
- Tài khoản Shopify với quyền truy cập API
- API Key của Airtable
- URL của cửa hàng Shopify
- Các credentials cho các node GraphQL và Airtable
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/7468
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Airtable, FetchRecords"**:
   - Cấu hình credentials cho Airtable
   - Điền thông tin bảng và view cần đồng bộ
   - Đảm bảo cột "sync" được đặt thành true cho các bản ghi cần đồng bộ

2. **Tất cả các node GraphQL**:
   - Thay đổi URL của Shopify store trong tất cả các node GraphQL
   - Đảm bảo sử dụng API version 2025-04

3. **Node "If product exists"**:
   - Cấu hình điều kiện kiểm tra sản phẩm đã tồn tại trong Shopify

4. **Node "Loop"**:
   - Cấu hình số lượng bản ghi xử lý trong mỗi batch

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu
2. Kiểm tra kết quả đồng bộ trên cả Airtable và Shopify
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập báo cáo định kỳ về trạng thái đồng bộ
- Kết hợp với Slack/Telegram để nhận thông báo khi đồng bộ hoàn thành
- Thêm chức năng kiểm tra tồn kho định kỳ
- Tự động cập nhật giá sản phẩm khi có thay đổi trong Airtable

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý sản phẩm giữa hai nền tảng Airtable và Shopify. Bằng cách tự động hóa toàn bộ quá trình đồng bộ, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong kinh doanh. Hãy áp dụng ngay để nâng cao hiệu quả quản lý sản phẩm của bạn!