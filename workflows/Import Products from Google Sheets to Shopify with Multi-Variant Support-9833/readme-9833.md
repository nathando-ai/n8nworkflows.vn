---
title: "🚀 Tự động đồng bộ sản phẩm từ Google Sheets lên Shopify có hỗ trợ nhiều biến thể (Multi-Variant)"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để nhập hàng loạt sản phẩm đơn và sản phẩm có nhiều biến thể từ Google Sheets lên cửa hàng Shopify một cách tự động."
slug: "dong-bo-san-pham-google-sheets-shopify-n8n"
tags: [n8n, automation, shopify, google-sheets, e-commerce, no-code]
keywords: [n8n workflow, tự động hóa shopify, import sản phẩm google sheets shopify, quản lý biến thể shopify n8n]
---

# 🚀 Tự động đồng bộ sản phẩm từ Google Sheets lên Shopify (Hỗ trợ Multi-Variant)

Các sếp đang kinh doanh trên Shopify chắc chắn đã từng "đau đầu" khi phải nhập thủ công hàng trăm, hàng nghìn sản phẩm lên hệ thống, đặc biệt là các mặt hàng có nhiều biến thể (size, màu sắc, chất liệu...) kèm theo giá bán và tồn kho khác nhau. Việc làm thủ công này vừa tốn thời gian, dễ sai sót lại cực kỳ mệt mỏi mỗi khi cập nhật kho hàng.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán trên. Chỉ với một file Google Sheets chứa danh sách sản phẩm, hệ thống sẽ tự động phân loại sản phẩm đơn hay sản phẩm đa biến thể, kết nối với Shopify GraphQL API để tạo sản phẩm, cấu hình biến thể và cập nhật tồn kho chính xác theo từng kho hàng (Location).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải copy/paste thủ công từng sản phẩm hay biến thể lên trang quản trị Shopify.
- **Xử lý thông minh Multi-Variant:** Tự động phân tách và gán đúng biến thể, SKU, giá cả, hình ảnh cho từng sản phẩm nhờ node `single and multivariant products` và `is variant?`.
- **Đồng bộ kho hàng chuẩn xác:** Tự động lấy ID kho (`Shopify, GetLocations`) và cập nhật số lượng tồn kho (`SetInventory`, `Create SetInventory`) tức thì.
- **Hoạt động linh hoạt:** Dễ dàng kích hoạt thủ công qua `When clicking ‘Execute workflow’` bất cứ lúc nào các sếp cập nhật xong bảng dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n đang hoạt động.
- File Google Sheets chứa dữ liệu sản phẩm (tiêu đề, SKU, URL hình ảnh, giá, tồn kho, vendor, type...).
- Tài khoản Shopify Admin với quyền truy cập API (Shopify Admin API Access Token).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON tải từ trang gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow kết nối trơn tru với cửa hàng Shopify và Google Sheets của các sếp, hãy cấu hình kỹ các điểm sau:

- **Cấu hình Shopify Credentials:** 
  Tạo một Header Auth credential mới trong n8n với thông số:
  - `Name`: `X-Shopify-Access-Token`
  - `Value`: [Mã Shopify Admin API Access Token của các sếp]
- **Node `set shop url`:** 
  Cập nhật subdomain cửa hàng của các sếp vào biến URL theo định dạng: `https://[yourshop].myshopify.com/`
- **Node `Shopify, GetLocations`:** 
  Cập nhật endpoint với URL cửa hàng của các sếp và chọn đúng credentials Shopify vừa tạo.
- **Node `Get row(s) in sheet`:** 
  Kết nối tài khoản Google Sheets cá nhân, chọn file Google Sheets chứa dữ liệu sản phẩm và tên Sheet tương ứng.
- **Node `Shopify, CreateProduct` & `CreateProduct2`:** 
  Kiểm tra và tùy chỉnh thông tin mặc định như `vendor` và `productType` trong code JSON nếu muốn thay đổi thương hiệu hoặc phân loại sản phẩm cho phù hợp với cửa hàng.
- **Các node xử lý biến thể (`Split Out1`, `SetVariant`, `Update Variants`, `SetInventory`, `adjust variants`):** 
  Các node này sẽ tự động phân chia các biến thể thành các mục riêng lẻ để tạo và cập nhật ở các bước tiếp theo, đảm bảo không sót bất kỳ thuộc tính nào của sản phẩm.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Test run`) bằng cách bấm vào node `When clicking ‘Execute workflow’` để kiểm tra log dữ liệu xem đã đẩy lên Shopify thành công chưa.
- Sau khi chắc chắn mọi thứ hoạt động mượt mà, hãy gạt công tắc sang chế độ **Active** để chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Bot:** Thêm node thông báo qua Telegram hoặc Slack vào cuối luồng để nhận tin nhắn báo cáo ngay khi quá trình đồng bộ hoàn tất hoặc gặp lỗi.
- **Lưu log vào Google Sheets:** Thêm một bước cập nhật ngược lại Google Sheets (đánh dấu "Đã đồng bộ") để tránh việc import trùng lặp sản phẩm ở các lần chạy sau.
- **Tự động hóa theo lịch:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để tự động quét file Google Sheets đồng bộ sản phẩm vào khung giờ thấp điểm mỗi ngày.

### 📌 Kết luận
Workflow này là "vũ khí" cực kỳ lợi hại cho các nhà bán hàng Shopify muốn tối ưu hóa quy trình vận hành kho vận và sản phẩm. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho các công việc kinh doanh cốt lõi!