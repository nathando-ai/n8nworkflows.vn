---
title: "🚀 Tự động lưu đơn hàng E-commerce vào Google Sheets theo từng tháng với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt webhook từ Shopify, phân loại và ghi nhận đơn hàng vào Google Sheets theo từng tab tháng riêng biệt kèm theo dõi trạng thái."
slug: "tu-dong-luu-don-hang-ecommerce-vao-google-sheets"
tags: [n8n, automation, no-code, ecommerce, shopify, google-sheets, webhook]
keywords: [n8n workflow, tự động hóa đơn hàng, shopify google sheets, lưu đơn hàng tự động, quản lý đơn hàng n8n]
---

# 🚀 Tự động lưu đơn hàng E-commerce vào Google Sheets theo từng tháng với n8n

Các sếp có đang đau đầu vì mỗi ngày phải copy-paste thủ công hàng chục, hàng trăm đơn hàng từ sàn thương mại điện tử (như Shopify) vào Google Sheets để báo cáo? Việc này không chỉ tốn thời gian, dễ nhầm lẫn mà còn khiến việc theo dõi trạng thái giao hàng trở nên cực kỳ rối rắm khi doanh số tăng cao.

Với workflow n8n này, các sếp sẽ tự động hóa 100% quy trình: khi có đơn hàng mới từ cửa hàng, hệ thống sẽ tự động bắt sự kiện qua Webhook, kiểm tra xem tab tháng hiện tại đã tồn tại trên Google Sheets chưa (nếu chưa sẽ tự tạo mới), ghi tiêu đề, và đẩy dữ liệu đơn hàng vào đúng tab tháng kèm theo cột trạng thái rõ ràng (*Not Shipped, Shipped, Delivered...*).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần động tay, đơn hàng từ Shopify đổ về Google Sheets ngay lập tức.
- **Quản lý khoa học theo tháng**: Tự động tạo tab (sub-sheet) riêng cho từng tháng (ví dụ: *Tháng 10, Tháng 11...*), giúp file báo cáo gọn gàng, dễ nhìn.
- **Theo dõi trạng thái chuẩn xác**: Đồng bộ trạng thái đơn hàng (Not Shipped, Pickup Scheduled, Shipped, InTransit, Delivered, Cancelled).
- **Hoạt động 24/7**: Đảm bảo không bỏ sót bất kỳ đơn hàng nào dù là nửa đêm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Cửa hàng Shopify** (hoặc nền tảng e-commerce hỗ trợ Webhook).
- **Google Account** đã kết nối Credentials (Google Sheets OAuth2 API) với n8n.
- Một file Google Sheets trống để làm kho chứa dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON được chia sẻ từ cộng đồng n8n) vào giao diện Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các điểm cốt lõi sau:

- **Node `Config (set spreadsheetId)`**: 
  - Mở file Google Sheet của các sếp lên, copy đoạn ID trên thanh URL (nằm giữa `/d/` và `/edit`).
  - Dán ID này vào node `Config (set spreadsheetId)` để n8n biết cần ghi dữ liệu vào file nào.
- **Node `Order created` (Webhook)**: 
  - Lấy Production/Test Webhook URL từ node này.
  - Mang sang cấu hình trong cửa hàng Shopify: Vào **Settings** → **Notifications** → **Webhooks** → Thêm Webhook cho các sự kiện: *Order creation, Order update, Order fulfillment*.
- **Các Node gọi API Google Sheets (`Create Month Sheet`, `Write Headers`, `Get Order Sheets metadata`, v.v.)**:
  - Đảm bảo các sếp đã chọn đúng tài khoản **Google Sheets OAuth2 API** đã cấp quyền truy cập vào Google Drive/Sheets của sếp.
- **Node `Append to Existing Orders Sheet` & `Append to Orders Sheet`**:
  - Chọn lại Google Spreadsheet ID và cấu hình ánh xạ các trường dữ liệu (Row values) khớp với cấu trúc cột (A đến I) mà sếp mong muốn.

#### 3. Kích hoạt ⚡️
- Nhấp **Execute Node** ở node Webhook và thử tạo một đơn hàng nháp (hoặc gửi test webhook từ Shopify) để kiểm tra dữ liệu chảy qua các node `If`, `Generate Sheet Name`, `Set Sheet Starting row col` có đúng ý không.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node Telegram hoặc Slack sau bước ghi đơn hàng thành công để đội ngũ vận hành (fulfillment) nhận chuông thông báo ngay khi có khách chốt đơn.
- **Báo cáo doanh thu định kỳ**: Dùng thêm node Cron (Schedule Trigger) chạy vào cuối ngày để tổng hợp số lượng đơn và doanh thu trong ngày gửi về email hoặc nhóm chat.
- **Mở rộng trạng thái**: Tùy biến lại danh sách trạng thái trong Google Sheet phù hợp với đơn vị vận chuyển (GHN, GHTK, ViettelPost...) mà cửa hàng đang sử dụng.

### 📌 Kết luận
Việc tự động hóa quy trình quản lý đơn hàng e-commerce chưa bao giờ dễ dàng đến thế với n8n. Chỉ với vài bước thiết lập đơn giản, các sếp đã tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng và loại bỏ hoàn toàn sai sót. Lên đồ và áp dụng ngay thôi các sếp ơi!