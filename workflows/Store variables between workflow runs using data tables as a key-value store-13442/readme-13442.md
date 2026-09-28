---
title: "🔄 Lưu trữ biến toàn cục giữa các lần chạy workflow n8n - Giải pháp lưu trữ dữ liệu tạm thời"
description: "Hướng dẫn chi tiết cách lưu trữ và truy xuất biến toàn cục giữa các lần chạy workflow n8n bằng cách sử dụng data table như kho lưu trữ key-value"
slug: "luu-tru-bien-toan-cuc-giua-cac-lan-chay-workflow-n8n"
tags: [n8n, automation, no-code, data-table, key-value-store]
keywords: [n8n workflow, lưu trữ biến, tự động hóa, data table, key-value store]
---

# 🔄 Lưu trữ biến toàn cục giữa các lần chạy workflow n8n - Giải pháp lưu trữ dữ liệu tạm thời

[Các sếp đang gặp khó khăn khi cần lưu trữ và truy xuất dữ liệu tạm thời giữa các lần chạy workflow n8n. Workflow này cung cấp giải pháp hoàn hảo bằng cách sử dụng data table như kho lưu trữ key-value, giúp lưu trữ và truy xuất dữ liệu một cách hiệu quả và đáng tin cậy.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Lưu trữ và truy xuất dữ liệu tạm thời giữa các lần chạy workflow một cách hiệu quả
- Tiết kiệm thời gian và công sức khi không cần phải cấu hình lại các biến mỗi lần chạy workflow
- Tăng tính linh hoạt và khả năng tùy chỉnh của workflow
- Đảm bảo tính nhất quán và đáng tin cậy của dữ liệu trong quá trình tự động hóa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã được cài đặt và cấu hình
- Quyền truy cập vào data table trong n8n
- Biến cần lưu trữ và giá trị mặc định (nếu có)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/13442](https://n8n.io/workflows/13442)
2. Nhấp vào nút "Download" để tải xuống file JSON của workflow
3. Trong giao diện n8n, nhấp vào nút "Import" và chọn file JSON đã tải xuống
4. Hoàn tất quá trình import và mở workflow trong n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Create Globals table"**:
   - Đảm bảo rằng bạn đã tạo một data table mới với tên "Globals" trong n8n
   - Cấu hình các cột "key" và "value" trong data table

2. **Node "Get Global 'your_variable_name'"**:
   - Thay thế placeholder **your_variable_name** bằng tên biến thực tế mà bạn muốn lưu trữ
   - Cấu hình các tham số cần thiết để truy xuất dữ liệu từ data table

3. **Node "Set default value"**:
   - Thiết lập giá trị mặc định cho biến nếu biến chưa tồn tại trong data table
   - Cấu hình các tham số cần thiết để thiết lập giá trị mặc định

4. **Node "Format value"**:
   - Định dạng giá trị của biến trước khi sử dụng trong workflow
   - Cấu hình các tham số cần thiết để định dạng giá trị

5. **Node "Upsert Global 'your_variable_name'"**:
   - Thay thế placeholder **your_variable_name** bằng tên biến thực tế mà bạn muốn lưu trữ
   - Cấu hình các tham số cần thiết để cập nhật hoặc chèn dữ liệu vào data table

#### 3. Kích hoạt ⚡️
1. Kiểm tra và cấu hình lại các node theo hướng dẫn trên
2. Nhấp vào nút "Execute workflow" để chạy workflow và kiểm tra kết quả
3. Bật Active workflow để workflow tự động chạy theo lịch trình hoặc sự kiện

### ✍️ Mẹo & gợi ý nâng cao
- Sử dụng workflow này để lưu trữ và truy xuất dữ liệu tạm thời giữa các lần chạy workflow khác nhau
- Kết hợp với các node khác để tạo ra các workflow phức tạp và linh hoạt hơn
- Tùy chỉnh giá trị mặc định và định dạng giá trị để phù hợp với nhu cầu cụ thể của bạn
- Sử dụng data table để lưu trữ nhiều biến cùng một lúc và quản lý chúng một cách hiệu quả

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn hảo để lưu trữ và truy xuất dữ liệu tạm thời giữa các lần chạy workflow n8n. Với việc sử dụng data table như kho lưu trữ key-value, các sếp có thể tiết kiệm thời gian và công sức khi không cần phải cấu hình lại các biến mỗi lần chạy workflow. Hãy áp dụng ngay workflow này để nâng cao hiệu suất và tính linh hoạt của các workflow tự động hóa của bạn!