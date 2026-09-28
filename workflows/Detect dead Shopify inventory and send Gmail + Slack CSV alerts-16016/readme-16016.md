---
title: "🚀 Tự động phát hiện hàng tồn kho ế ẩm trên Shopify và gửi báo cáo qua Gmail & Slack"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để quét dữ liệu Shopify hàng ngày, nhận diện sản phẩm chết (dead inventory) và tự động gửi file CSV báo cáo qua Gmail và Slack."
slug: "tu-dong-phat-hien-hang-ton-kho-shopify-va-gui-bao-cao-slack-gmail"
tags: [n8n, automation, shopify, ecommerce, inventory-management, slack, gmail]
keywords: [n8n workflow, shopify dead inventory, tự động hóa kho hàng, quản lý hàng tồn kho shopify, n8n shopify automation]
---

# 🚀 Tự động phát hiện hàng tồn kho ế ẩm trên Shopify và gửi báo cáo qua Gmail & Slack

Các chủ cửa hàng Shopify và quản lý kho chắc chắn hiểu rõ cảm giác "đau đầu" khi vốn bị chôn vùi trong những món hàng tồn kho ế ẩm (dead stock) mà không bán được. Việc kiểm tra thủ công từng sản phẩm, đối chiếu lịch sử đơn hàng hàng tuần hay hàng tháng vừa tốn thời gian, vừa dễ sai sót, lại khiến dòng tiền của doanh nghiệp bị đình trệ.

Workflow n8n này sẽ giải quyết triệt để bài toán đó: tự động hóa 100% quy trình quét dữ liệu đơn hàng và sản phẩm trên Shopify, lọc ra các mặt hàng không có giao dịch trong khoảng thời gian định sẵn, đóng gói thành file CSV và gửi thẳng đến email của quản lý cũng như kênh Slack của team.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu dòng tiền:** Phát hiện ngay các mặt hàng "đóng băng" để có chiến lược xả kho, giảm giá hoặc ngừng nhập hàng kịp thời.
- **Tiết kiệm 100% thời gian thủ công:** Lịch trình tự động chạy hàng ngày mà không cần con người can thiệp.
- **Báo cáo trực quan, chuyên nghiệp:** Tự động tổng hợp dữ liệu thành file CSV gọn gàng, gửi tức thì qua Gmail và Slack.
- **Giám sát thông minh:** Tự động cảnh báo về Slack ngay lập tức nếu có lỗi xảy ra trong quá trình quét dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Shopify:** Đã cấu hình và cấp quyền (API scopes) để đọc dữ liệu đơn hàng (`read_orders`) và sản phẩm (`read_products`).
- **Tài khoản Gmail:** Kết nối qua OAuth2 để gửi email báo cáo.
- **Workspace Slack:** Đã tạo sẵn kênh thông báo (channel) để nhận file CSV báo cáo và cảnh báo lỗi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo một workflow mới và copy/paste toàn bộ mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 13 nodes được sắp xếp logic từ quét dữ liệu, xử lý đến cảnh báo. Các sếp cần cấu hình các điểm quan trọng sau:

- **Set Detector Configuration:** 
  - Tại đây các sếp định nghĩa các thông số cốt lõi: `daysWithoutSales` (số ngày không có giao dịch tính là hàng chết), `orderFetchDays` (số ngày đơn hàng cần quét ngược về quá khứ), `recipientMail` (email nhận báo cáo) và `slackEscalationChannel` (kênh Slack nhận cảnh báo).
- **Fetch Shopify Orders & Fetch Shopify Products:** 
  - Chọn hoặc tạo mới **Credentials** kết nối Shopify (`shopifyOAuth2Api`) bằng thông tin cửa hàng Shopify của các sếp. Đảm bảo cấu hình đúng phân quyền đọc (read scope).
- **Email Dead Inventory Report:** 
  - Chọn **Credentials** Gmail (`gmailOAuth2`) để cho phép n8n gửi email từ tài khoản của các sếp.
- **Send CSV Report to Slack & Post Error to Slack:** 
  - Cấu hình **Credentials** Slack (`slackApi`) và chọn đúng kênh (Channel) mà team kho hoặc ban giám đốc đang sử dụng để nhận file báo cáo CSV cũng như tin nhắn khi có sự cố.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công (Test run) để kiểm tra xem dữ liệu trả về từ Shopify có chính xác không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang chế độ **Active** để hệ thống tự động chạy theo lịch trình hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình quản lý kho hơn nữa, các sếp có thể mở rộng workflow này bằng các cách:
- **Tích hợp Google Sheets:** Lưu thêm một bản sao danh sách hàng tồn kho ế ẩm vào Google Sheets để các bộ phận kinh doanh dễ dàng theo dõi và lên chiến dịch marketing xả hàng.
- **Nhắc nhở qua Telegram/Zalo:** Thay vì chỉ gửi Slack, có thể bổ sung node gửi tin nhắn tóm tắt qua Telegram Bot cho các cửa hàng trưởng.
- **Phân loại mức độ tồn kho:** Tùy chỉnh code node **Identify Dead Inventory** để chia thành nhiều mức độ (Ế nhẹ, ế nặng, sắp hủy...) để có phương án xử lý linh hoạt hơn.

### 📌 Kết luận
Việc kiểm soát hàng tồn kho chưa bao giờ dễ dàng đến thế khi đã có tự động hóa lo. Hãy triển khai ngay workflow này để tối ưu hóa nguồn vốn và gia tăng hiệu quả vận hành cho cửa hàng Shopify của các sếp ngay hôm nay!