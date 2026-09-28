---
title: "🚀 Tự Động Kiểm Tra Kho Shopify & Gửi Cảnh Báo Hàng Sắp Hết Lên Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động quét kho hàng Shopify mỗi ngày, lọc sản phẩm sắp hết và gửi thông báo tức thì lên Slack giúp chống đứt gãy nguồn hàng."
slug: "tu-dong-kiem-tra-kho-shopify-va-gui-canh-bao-slack"
tags: [n8n, automation, shopify, slack, ecommerce, inventory-management]
keywords: [n8n workflow, shopify inventory alert, tu dong hoa kho hang, canh bao hang sap het, quan ly ton kho shopify]
keywords: [n8n workflow, shopify inventory alert, tu dong hoa kho hang, canh bao hang sap het, quan ly ton kho shopify]
---

# 🚀 Tự Động Kiểm Tra Kho Shopify & Gửi Cảnh Báo Hàng Sắp Hết Lên Slack

Các sếp kinh doanh trên Shopify chắc chắn đã từng trải qua cảm giác "dở khóc dở cười" khi khách chốt đơn rần rần nhưng kiểm lại kho thì... hết hàng từ lúc nào, dẫn đến việc phải hủy đơn hoặc chậm trễ giao hàng, làm giảm uy tín cửa hàng. Việc ngồi kiểm tra hàng nghìn sản phẩm thủ công mỗi ngày là bất khả thi.

Đừng lo, workflow n8n này do chuyên gia **David Olusola** thiết kế sẽ thay các sếp "gác cổng" kho hàng 24/7. Hệ thống sẽ tự động quét toàn bộ sản phẩm trên Shopify, phát hiện các mặt hàng sắp chạm ngưỡng tối thiểu và bắn tin nhắn báo động trực tiếp vào kênh Slack của đội ngũ vận hành.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chống đứt gãy nguồn hàng:** Phát hiện sớm sản phẩm sắp hết để kịp thời lên kế hoạch nhập hàng, tránh mất doanh thu oan uổng.
- **Tự động hóa 100%:** Loại bỏ hoàn toàn thao tác kiểm kê thủ công mỗi sáng, tiết kiệm hàng chục giờ làm việc mỗi tháng.
- **Báo cáo chi tiết tức thì:** Thông báo rõ ràng tên sản phẩm, biến thể và số lượng tồn kho ngay trên Slack (kênh `#inventory`).
- **Tùy chỉnh linh hoạt:** Dễ dàng thay đổi ngưỡng cảnh báo (threshold) tùy theo tốc độ bán hàng của từng dòng sản phẩm.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Cửa hàng Shopify đã bật tính năng theo dõi tồn kho (Inventory Tracking).
- Tài khoản Slack có quyền tạo hoặc tích hợp bot vào kênh thông báo (ví dụ: `#inventory`).
- Đã cài đặt n8n (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện (n8n hỗ trợ phím tắt `Ctrl + V` / `Cmd + V` để paste node).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Daily Inventory Check (`scheduleTrigger`):** 
  - Mặc định lịch chạy là 9 giờ sáng mỗi ngày. Các sếp có thể đổi sang khung giờ khác nếu muốn (ví dụ: chạy 2 lần/ngày vào sáng và chiều).
- **Get All Products (`shopify`):** 
  - Chọn tài khoản kết nối (Credentials) với cửa hàng Shopify của các sếp (yêu cầu quyền đọc sản phẩm và kho hàng).
  - Giữ nguyên thông số `Resource: Product` và `Operation: Get All`.
- **Filter Low Stock Items (`code`):** 
  - Node này dùng đoạn mã Javascript để lọc sản phẩm. Các sếp cần chú ý biến `lowStockThreshold` (mặc định để `10`). 
  - *Mẹo:* Đổi số `10` thành `5` cho hàng bán chạy (fast-moving), `20` cho hàng đi chậm, hoặc `50` cho các mặt hàng bán số lượng lớn.
- **Check if Alerts Needed (`if`):** 
  - Node này kiểm tra xem mảng dữ liệu trả về từ bước lọc có sản phẩm nào không. Nếu có (tồn tại sản phẩm thấp hơn ngưỡng), workflow mới tiếp tục chạy.
- **Format Alert Message (`set`):** 
  - Tùy chỉnh cấu trúc nội dung tin nhắn sẽ hiển thị trên Slack (bao gồm tên sản phẩm, SKU, số lượng tồn kho hiện tại để tiện đặt hàng lại).
- **Send Inventory Alert (`slack`):** 
  - Kết nối tài khoản Slack của doanh nghiệp và chọn đúng kênh nhận thông báo (ví dụ: `#inventory`).

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** để chạy thử nghiệm xem dữ liệu có đổ về Slack mượt mà hay không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản node cuối và đổi thành node **Telegram** hoặc **Email (Gmail/SMTP)** để gửi cảnh báo song song cho bộ phận mua hàng (Purchasing).
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ngay sau bước lọc để ghi lại lịch sử các mặt hàng chạm mốc tồn kho thấp mỗi ngày, phục vụ việc phân tích xu hướng nhập hàng.
- **Tích hợp tự động tạo Purchase Order:** Nâng cấp workflow bằng cách gọi API đến các hệ thống ERP hoặc phần mềm quản lý kho khác để tự động tạo phiếu đề xuất mua hàng.

### 📌 Kết luận
Quản lý kho hàng chưa bao giờ là việc dễ dàng nếu làm thủ công. Với workflow n8n tích hợp Shopify và Slack này, các sếp hoàn toàn có thể yên tâm ngủ ngon vì hệ thống đã tự động "canh kho" thay bạn mỗi ngày. "Lên đồ" ngay và tối ưu hóa vận hành doanh nghiệp của mình thôi nào!