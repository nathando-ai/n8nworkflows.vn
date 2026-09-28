---
title: "🚀 Tự động hóa quản lý kho WooCommerce với AI Gemini và BrowserAct"
description: "Hướng dẫn chi tiết cách tự động đồng bộ kho hàng WooCommerce với dữ liệu từ các nhà cung cấp, cập nhật sản phẩm hiện có và tạo mới sản phẩm với mô tả do AI tạo."
slug: "tu-dong-hoa-quan-ly-kho-woocommerce-voi-ai-gemini-va-browseract"
tags: [n8n, automation, no-code, woocommerce, google-gemini, browseract]
keywords: [n8n workflow, tự động hóa, woocommerce, google gemini, browseract, quản lý kho]
---

# 🚀 Tự động hóa quản lý kho WooCommerce với AI Gemini và BrowserAct

[Các sếp đang gặp khó khăn khi phải quản lý kho hàng WooCommerce thủ công, phải cập nhật giá cả và tồn kho từ nhiều nhà cung cấp khác nhau. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này với công nghệ AI và web scraping.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động cập nhật kho hàng hàng ngày mà không cần can thiệp thủ công.
- Chính xác: Đồng bộ dữ liệu từ nhiều nguồn khác nhau một cách đáng tin cậy.
- Cá nhân hóa: Tạo mô tả sản phẩm chuyên nghiệp với công nghệ AI Gemini.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản API BrowserAct để thực hiện web scraping.
- Cài đặt node cộng đồng BrowserAct cho n8n: [n8n Nodes BrowserAct](https://www.npmjs.com/package/n8n-nodes-browseract-workflows)
- Tài khoản Google Sheets chứa danh sách nhà cung cấp và URL trang kho hàng.
- Tài khoản WooCommerce để quản lý sản phẩm.
- Tài khoản Google Gemini để sử dụng AI Agent.
- Tài khoản Slack để nhận thông báo lỗi.
- Các template BrowserAct có tên "WooCommerce Inventory & Stock Synchronization" và "WooCommerce Product Data Reconciliation".
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/10089)
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cấu hình Credentials**:
   - Thêm credentials cho BrowserAct, Google Sheets, WooCommerce, Google Gemini và Slack.
   - Hướng dẫn chi tiết: [How to Connect n8n to Browseract](https://www.youtube.com/watch?v=RoYMdJaRdcQ)

2. **Cấu hình BrowserAct Templates**:
   - Đảm bảo có các template "Get Product Stock Data" và "Add Missing Product" trong tài khoản BrowserAct của bạn.
   - Hướng dẫn sử dụng template: [How to Use & Customize BrowserAct Templates](https://www.youtube.com/watch?v=CPZHFUASncY)

3. **Cấu hình Google Sheets**:
   - Trong node "Get Suppliers & Links", chỉ định spreadsheet chứa danh sách nhà cung cấp.
   - Spreadsheet phải có các cột: `Inventory page` (URL trang kho), `Name` (tên nhà cung cấp), và có thể có `Product Type` nếu sử dụng bộ lọc theo danh mục.

4. **Cấu hình Slack**:
   - Cập nhật Channel ID trong các node Slack để nhận thông báo lỗi.

5. **Cấu hình bộ lọc danh mục (Tùy chọn)**:
   - Điều chỉnh logic trong node `Check the Category` nếu muốn lọc sản phẩm theo danh mục.

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật chế độ Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa định kỳ**: Thay thế node Manual Trigger bằng Schedule Trigger để chạy workflow theo lịch.
2. **Kết hợp với Slack**: Thêm các thông báo Slack cho các sự kiện quan trọng như hoàn thành cập nhật kho.
3. **Báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng ngày qua email hoặc Slack.
4. **Xử lý lỗi nâng cao**: Tùy chỉnh các thông báo lỗi để bao gồm thông tin chi tiết hơn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình quản lý kho WooCommerce một cách hiệu quả và chính xác. Với sự kết hợp của công nghệ AI Gemini và BrowserAct, các sếp có thể tiết kiệm thời gian và giảm thiểu lỗi trong quá trình quản lý kho hàng. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh của bạn!