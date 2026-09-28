---
title: "🚀 Tự động đồng bộ dữ liệu khách hàng từ Adobe Commerce sang KlickTipp với phân loại theo giá trị đơn hàng"
description: "Hướng dẫn tự động hóa đồng bộ dữ liệu khách hàng từ Adobe Commerce sang KlickTipp, phân loại khách hàng theo giá trị đơn hàng và gắn thẻ tự động để tối ưu hóa chiến dịch marketing"
slug: "tu-dong-dong-bo-du-lieu-khach-hang-adobe-commerce-sang-klicktipp"
tags: [n8n, automation, no-code, e-commerce, marketing]
keywords: [n8n workflow, tự động hóa, Adobe Commerce, KlickTipp, phân loại khách hàng, marketing tự động]
---

# 🚀 Tự động đồng bộ dữ liệu khách hàng từ Adobe Commerce sang KlickTipp với phân loại theo giá trị đơn hàng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải thủ công đồng bộ dữ liệu khách hàng giữa các hệ thống, đặc biệt là từ Adobe Commerce sang KlickTipp. Quá trình này tốn thời gian, dễ xảy ra lỗi và không thể tự động phân loại khách hàng theo giá trị đơn hàng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này, đồng thời phân loại khách hàng và gắn thẻ tự động dựa trên giá trị đơn hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ dữ liệu khách hàng từ Adobe Commerce sang KlickTipp mà không cần can thiệp thủ công.
- Chính xác: Giảm thiểu lỗi do nhập liệu thủ công.
- Cá nhân hóa: Phân loại khách hàng theo giá trị đơn hàng và gắn thẻ tự động.
- Hoạt động liên tục: Workflow chạy tự động theo lịch trình đã đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Adobe Commerce với quyền truy cập API.
- Tài khoản KlickTipp với quyền truy cập API.
- Các trường tùy chỉnh sau trong KlickTipp:
  - `Payment ID`
  - `Total`
  - `Receipt URL`
  - `Products`
- Các thẻ sau trong KlickTipp:
  - `Premium customer`
  - `Clothing buyer`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấp vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/9469](https://n8n.io/workflows/9469).
3. Hoặc, tải xuống file JSON từ liên kết trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Cấu hình thời gian chạy workflow theo nhu cầu của các sếp.

2. **Node "Get Adobe Commerce customers"**:
   - Cấu hình credentials cho kết nối với Adobe Commerce.
   - Đảm bảo rằng các trường dữ liệu cần thiết đã được ánh xạ đúng.

3. **Node "Transfer customers to KlickTipp"**:
   - Cấu hình credentials cho kết nối với KlickTipp.
   - Kiểm tra các trường dữ liệu cần thiết đã được ánh xạ đúng.

4. **Node "Get Adobe Commerce orders"**:
   - Cấu hình credentials cho kết nối với Adobe Commerce.
   - Đảm bảo rằng các trường dữ liệu cần thiết đã được ánh xạ đúng.

5. **Node "Transfer order data to KlickTipp"**:
   - Cấu hình credentials cho kết nối với KlickTipp.
   - Kiểm tra các trường dữ liệu cần thiết đã được ánh xạ đúng.

6. **Node "Tag contact for high-value order"**:
   - Cấu hình credentials cho kết nối với KlickTipp.
   - Đảm bảo rằng các trường dữ liệu cần thiết đã được ánh xạ đúng.

7. **Node "Tag contact for clothing purchase"**:
   - Cấu hình credentials cho kết nối với KlickTipp.
   - Đảm bảo rằng các trường dữ liệu cần thiết đã được ánh xạ đúng.

8. **Node "Route by SKU and total amount"**:
   - Cấu hình các điều kiện để phân loại khách hàng theo giá trị đơn hàng và gắn thẻ tự động.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy thành công hoặc gặp lỗi.
- Lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.
- Gửi báo cáo định kỳ về hoạt động của workflow để tối ưu hóa và cải thiện.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ dữ liệu khách hàng từ Adobe Commerce sang KlickTipp, phân loại khách hàng theo giá trị đơn hàng và gắn thẻ tự động. Với việc tự động hóa toàn bộ quá trình này, các sếp có thể tiết kiệm thời gian, giảm thiểu lỗi và tối ưu hóa chiến dịch marketing. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh!