---
title: "💰 Tự động cập nhật HubSpot khi có hóa đơn mới từ Stripe"
description: "Tự động hóa quy trình cập nhật trạng thái giao dịch trong HubSpot ngay khi nhận được thanh toán từ Stripe, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-cap-nhat-hubspot-khi-co-hoa-don-moi-tu-stripe"
tags: [n8n, automation, no-code, stripe, hubspot]
keywords: [n8n workflow, tự động hóa, stripe, hubspot, quản lý giao dịch]
---

# 💰 Tự động cập nhật HubSpot khi có hóa đơn mới từ Stripe

[Các sếp bán hàng và marketing thường phải làm việc với nhiều công cụ như Stripe và HubSpot. Tuy nhiên, việc đồng bộ dữ liệu giữa hai nền tảng này thường tốn thời gian và dễ gây lỗi khi làm thủ công. Workflow này sẽ tự động cập nhật trạng thái giao dịch trong HubSpot ngay khi nhận được thanh toán từ Stripe, giúp các sếp tiết kiệm thời gian và giảm thiểu sai sót.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cập nhật trạng thái giao dịch trong HubSpot ngay khi nhận thanh toán từ Stripe
- Giảm thiểu sai sót thủ công trong quá trình đồng bộ dữ liệu
- Tiết kiệm thời gian cho các sếp bán hàng và marketing
- Nhận thông báo ngay trên Slack khi có sự cố trong quá trình xử lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Stripe với quyền truy cập API
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản Slack để nhận thông báo (tùy chọn)
- PO Number (Purchase Order Number) trong hóa đơn Stripe để tìm kiếm deal tương ứng trong HubSpot
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [workflow gốc](https://n8n.io/workflows/1468)
2. Nhấn nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When Invoice Paid" (stripeTrigger)**
   - Cấu hình credentials: Chọn "stripeApi" đã được thiết lập trước đó
   - Tham số quan trọng: Không cần cấu hình thêm, node này sẽ kích hoạt khi có hóa đơn mới được thanh toán

2. **Node "Find Deal based on PO Number" (hubspot)**
   - Cấu hình credentials: Chọn "hubspotApi" đã được thiết lập trước đó
   - Tham số quan trọng:
     - Operation: Đã được thiết lập là "search"
     - Query: Sử dụng biểu thức `={{ $node["When Invoice Paid"].json["data"]["object"]["metadata"]["po_number"] }}` để tìm kiếm deal dựa trên PO Number trong hóa đơn Stripe

3. **Node "Update Deal to Paid" (hubspot)**
   - Cấu hình credentials: Chọn "hubspotOAuth2Api" đã được thiết lập trước đó
   - Tham số quan trọng:
     - Operation: Đã được thiết lập là "update"
     - Deal ID: Sử dụng biểu thức `={{ $node["Find Deal based on PO Number"].json.results[0].id }}` để lấy ID của deal cần cập nhật
     - Properties: Cập nhật các thuộc tính cần thiết (ví dụ: "dealstage" để chuyển trạng thái deal sang "Closed Won")

4. **Node "Send invoice paid message" (slack)**
   - Cấu hình credentials: Chọn "slackApi" đã được thiết lập trước đó
   - Tham số quan trọng:
     - Channel: Chọn kênh Slack để gửi thông báo
     - Text: Tùy chỉnh nội dung thông báo (ví dụ: "Hóa đơn mới đã được thanh toán: {{ $node["When Invoice Paid"].json["data"]["object"]["id"] }}")

5. **Node "Send no PO Message" (slack)**
   - Cấu hình credentials: Chọn "slackApi" đã được thiết lập trước đó
   - Tham số quan trọng:
     - Channel: Chọn kênh Slack để gửi thông báo
     - Text: Tùy chỉnh nội dung thông báo (ví dụ: "Không tìm thấy PO Number trong hóa đơn: {{ $node["When Invoice Paid"].json["data"]["object"]["id"] }}")

6. **Node "Send Deal not found message" (slack)**
   - Cấu hình credentials: Chọn "slackApi" đã được thiết lập trước đó
   - Tham số quan trọng:
     - Channel: Chọn kênh Slack để gửi thông báo
     - Text: Tùy chỉnh nội dung thông báo (ví dụ: "Không tìm thấy deal tương ứng với PO Number: {{ $node["When Invoice Paid"].json["data"]["object"]["id"] }}")

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra hoạt động của workflow với dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn nút "Activate Workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Google Sheets" để lưu trữ log các giao dịch đã được xử lý
- Kết hợp với node "Email" để gửi báo cáo hàng tuần về các giao dịch mới
- Tạo một workflow phụ để xử lý các hóa đơn không có PO Number một cách thủ công
- Thiết lập thông báo Slack cho các sếp quản lý để theo dõi tình trạng giao dịch

### 📌 Kết luận
Workflow này giúp các sếp bán hàng và marketing tự động cập nhật trạng thái giao dịch trong HubSpot ngay khi nhận thanh toán từ Stripe, tiết kiệm thời gian và giảm thiểu sai sót thủ công. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!