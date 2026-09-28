---
title: "🚀 Tự động đồng bộ hóa ghi chú cuộc họp Fathom với liên hệ GoHighLevel"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ hóa ghi chú cuộc họp từ Fathom với liên hệ trong GoHighLevel, tiết kiệm thời gian và nâng cao hiệu quả quản lý khách hàng."
slug: "tu-dong-dong-bo-ghi-chu-cuoc-hop-fathom-voi-gohighlevel"
tags: [n8n, automation, no-code, crm, ai-summarization]
keywords: [n8n workflow, tự động hóa, crm, ghi chú cuộc họp, gohighlevel]
---

# 🚀 Tự động đồng bộ hóa ghi chú cuộc họp Fathom với liên hệ GoHighLevel

[Các sếp] có biết không? Mỗi tuần, các bạn mất tới 10+ giờ để thủ công đồng bộ hóa ghi chú cuộc họp từ Fathom với hệ thống CRM GoHighLevel. Việc này không chỉ tốn thời gian mà còn dễ gây lỗi và làm mất đi tính cá nhân hóa trong quản lý khách hàng.

Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình này chỉ trong vài bước đơn giản. Hệ thống sẽ tự động:
- Nhận dữ liệu từ Fathom khi cuộc họp kết thúc
- Tìm kiếm và khớp thông tin khách hàng trong GoHighLevel
- Tạo ghi chú chi tiết và chuyển đổi các hành động cần làm thành công việc trong hệ thống

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm tới 10+ giờ mỗi tuần nhờ tự động hóa
- **Chính xác cao**: Dữ liệu được đồng bộ hóa chính xác và liên tục
- **Cá nhân hóa**: Ghi chú chi tiết giúp hiểu rõ hơn về nhu cầu khách hàng
- **Hiệu quả cao**: Các hành động cần làm được chuyển đổi thành công việc trong hệ thống
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Fathom với quyền truy cập API/webhook
- Tài khoản GoHighLevel với Private Integration Token hoặc OAuth app
- Các quyền truy cập cần thiết trong GoHighLevel: `contacts.readonly`, `contacts.write`, `conversations.readonly`, `conversations.write`, `conversations/message.write`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, làm theo các bước sau:

1. Truy cập vào n8n Editor của các sếp
2. Nhấp vào biểu tượng "+" ở góc trái màn hình
3. Chọn "Import from URL"
4. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/13136`
5. Nhấp vào "Import" để hoàn tất quá trình

Hoặc các sếp cũng có thể:
1. Truy cập link workflow: [Sync Fathom meeting summaries and action items with GoHighLevel contacts](https://n8n.io/workflows/13136)
2. Nhấp vào nút "Copy JSON" ở góc trên bên phải
3. Trong n8n Editor, nhấp vào biểu tượng "+" và chọn "Import from JSON"
4. Dán nội dung đã copy vào ô nhập liệu và nhấp "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 19 nodes chính, các sếp cần chú ý cấu hình các node quan trọng sau:

1. **Fathom Webhook** (node đầu tiên):
   - Đảm bảo đã cấu hình đúng path và phương thức HTTP
   - Tham số cần cấu hình:
     - Path: `fathom-webhook`
     - HTTP Method: `POST`

2. **Config** (node thứ hai):
   - Cấu hình tham số `ghl_location_id` với ID vị trí của các sếp trong GoHighLevel

3. **Các node HTTP Request**:
   - Tất cả các node HTTP Request đều cần được kết nối với GoHighLevel OAuth2 credentials
   - Đảm bảo các node này được cấu hình đúng endpoint và phương thức HTTP

4. **Các node Code**:
   - Các node Code được sử dụng để xử lý và chuyển đổi dữ liệu
   - Các sếp cần kiểm tra và đảm bảo các hàm xử lý dữ liệu hoạt động đúng

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình đầy đủ các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. **Test run dữ liệu mẫu**:
   - Các sếp có thể tạo một cuộc họp thử nghiệm trong Fathom
   - Sau khi cuộc họp kết thúc, hệ thống sẽ gửi webhook đến workflow
   - Kiểm tra xem dữ liệu được xử lý và đồng bộ hóa đúng như mong đợi

2. **Bật Active workflow**:
   - Sau khi đã kiểm tra và đảm bảo workflow hoạt động đúng
   - Các sếp có thể bật chế độ Active cho workflow để nó hoạt động liên tục

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**:
   - Các sếp có thể thêm node gửi thông báo đến Slack hoặc Telegram khi có cuộc họp mới được xử lý
   - Điều này giúp các sếp theo dõi quá trình đồng bộ hóa một cách dễ dàng

2. **Lưu log hoạt động**:
   - Thêm node lưu log hoạt động của workflow
   - Giúp các sếp theo dõi và kiểm tra lại các cuộc họp đã được xử lý

3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow phụ để gửi báo cáo hàng tuần về các cuộc họp đã được xử lý
   - Bao gồm số lượng cuộc họp, số lượng liên hệ được cập nhật, số lượng công việc mới được tạo

4. **Tích hợp với các hệ thống khác**:
   - Các sếp có thể mở rộng workflow để tích hợp với các hệ thống khác như Google Calendar, Outlook, hoặc các hệ thống CRM khác

### 📌 Kết luận
Workflow "Sync Fathom meeting summaries and action items with GoHighLevel contacts" là giải pháp hoàn hảo cho các sếp muốn tự động hóa việc đồng bộ hóa ghi chú cuộc họp từ Fathom với hệ thống CRM GoHighLevel. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian, nâng cao hiệu quả quản lý khách hàng và tập trung vào những việc quan trọng hơn trong công việc hàng ngày.