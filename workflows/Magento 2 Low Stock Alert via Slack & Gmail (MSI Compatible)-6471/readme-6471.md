---
title: "📦 Tự động cảnh báo tồn kho thấp Magento 2 qua Slack & Gmail (Hỗ trợ MSI)"
description: "Hướng dẫn thiết lập workflow n8n tự động kiểm tra kho hàng Magento 2 hàng ngày, lọc sản phẩm sắp hết và gửi thông báo qua Slack và Gmail."
slug: "magento-2-low-stock-alert-slack-gmail-n8n"
tags: [n8n, automation, magento2, ecommerce, slack, gmail]
keywords: [n8n workflow, magento 2 inventory alert, tu dong hoa kho hang, slack gmail notification, msi stock check]
---

# 📦 Tự động cảnh báo tồn kho thấp Magento 2 qua Slack & Gmail (Hỗ trợ MSI)

Trong vận hành thương mại điện tử, việc để sản phẩm "cháy hàng" (out-of-stock) mà không hay biết chính là cách nhanh nhất để đốt tiền quảng cáo và đẩy khách hàng vào tay đối thủ. Tuy nhiên, việc phải kiểm tra thủ công hàng ngàn SKU trên hệ thống Magento 2 mỗi ngày là một nỗi ác mộng đối với đội ngũ vận hành.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình quét kho, phát hiện sản phẩm sắp hết hàng (tương thích cả hệ thống MSI - Multi Source Inventory của Magento 2) và ngay lập tức gửi cảnh báo chi tiết qua **Slack** và **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Ngăn chặn thất thoát doanh thu:** Phát hiện ngay các mặt hàng sắp chạm ngưỡng tối thiểu để kịp thời nhập hàng, không bỏ lỡ đơn của khách.
- **Tự động hóa hoàn toàn:** Hệ thống tự quét kho định kỳ mỗi ngày mà không cần con người can thiệp.
- **Đa kênh thông báo:** Gửi đồng thời tin nhắn tức thời qua Slack cho đội ngũ kho và email qua Gmail cho quản lý.
- **Hỗ trợ chuẩn MSI:** Hoạt động mượt mà với các phiên bản Magento 2 hiện đại có quản lý đa kho.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Cửa hàng Magento 2 (Adobe Commerce) đang hoạt động và có quyền tạo API Token (Integration Token).
- Tài khoản Slack (đã tạo sẵn kênh thông báo, ví dụ: `#magento-notifications`).
- Tài khoản Gmail (để gửi email báo cáo).
- Xác định trước ngưỡng tồn kho tối thiểu cần cảnh báo (mặc định trong code là **5 đơn vị**).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n templates (link gốc: `https://n8n.io/workflows/6471`), sau đó copy và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Daily Inventory Check (`scheduleTrigger`):** Mặc định đang đặt lịch chạy lúc 8:50 sáng mỗi ngày. Các sếp có thể chỉnh lại giờ giấc cho phù hợp với khung giờ làm việc của công ty.
- **Get All Product Skus & Fetch MSI Stock Status (`httpRequest`):** 
  - Cần cấu hình Magento REST API Credentials (Bearer Token).
  - Đảm bảo endpoint trỏ đúng domain của trang Magento 2 của các sếp.
- **Process Stock Data and Identify Low Stock (`code`):** 
  - Mở node này và kiểm tra biến `lowStockThreshold` (ngưỡng cảnh báo hết hàng). Mặc định để là `5`, các sếp có thể đổi thành số lượng tùy ý theo mô hình kinh doanh.
- **Send Inventory Alert (`slack`) & Send a message (`gmail`):**
  - Kết nối tài khoản Slack và chọn đúng kênh nhận tin (Channel).
  - Cấu hình tài khoản Gmail gửi đi.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử xem dữ liệu từ Magento có kéo về thành công không.
- Nếu không có lỗi xuất hiện, gạt nút **Active** trên góc phải màn hình để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack và Gmail, các sếp có thể nối thêm node Telegram hoặc Zalo OA để bắn tin nhắn trực tiếp vào điện thoại cá nhân của quản lý kho.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để lưu lại lịch sử các lần cảnh báo tồn kho, giúp dễ dàng tra cứu xu hướng tiêu thụ sản phẩm.
- **Phân loại mức độ:** Tùy biến code trong node `Process Stock Data` để chia thành nhiều mức độ cảnh báo khác nhau (Ví dụ: Dưới 2 cái: Đỏ - Khẩn cấp; Dưới 5 cái: Vàng - Cần lưu ý).

### 📌 Kết luận
Việc tự động hóa cảnh báo tồn kho Magento 2 không chỉ giúp tiết kiệm hàng giờ kiểm tra thủ công mỗi ngày mà còn bảo vệ doanh thu khỏi việc bỏ lỡ khách hàng vì hết sản phẩm. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp thôi nào!