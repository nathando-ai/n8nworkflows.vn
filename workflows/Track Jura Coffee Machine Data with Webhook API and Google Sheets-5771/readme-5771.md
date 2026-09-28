---
title: "🚀 Theo dõi dữ liệu máy pha cà phê Jura bằng Webhook API và Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi số lượng cà phê được pha từ máy Jura thông qua webhook và lưu trữ dữ liệu vào Google Sheets"
slug: "theo-doi-du-lieu-may-pha-ca-phe-jura"
tags: [n8n, automation, no-code, coffee, iot]
keywords: [n8n workflow, tự động hóa, máy pha cà phê, Jura, Google Sheets]
---

# 🚀 Theo dõi dữ liệu máy pha cà phê Jura bằng Webhook API và Google Sheets

[Các sếp! Bạn có biết rằng mỗi ngày có hàng trăm ly cà phê được pha ra từ máy Jura của công ty không? Nhưng liệu bạn có đang theo dõi số lượng này một cách tự động không? Với workflow này, các sếp có thể dễ dàng thu thập và lưu trữ dữ liệu từ máy pha cà phê Jura của mình vào Google Sheets mà không cần viết một dòng code nào!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi có dữ liệu mới từ máy pha cà phê.
- **Dữ liệu chính xác**: Thời gian và số lượng cà phê được ghi lại một cách tự động và chính xác.
- **Dễ theo dõi**: Dữ liệu được lưu trữ trong Google Sheets, giúp các sếp dễ dàng phân tích và tạo báo cáo.
- **Tích hợp dễ dàng**: Có thể kết nối với các hệ thống khác để tạo ra các báo cáo và biểu đồ trực quan.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Máy pha cà phê Jura đã được cấu hình để gửi dữ liệu qua BLE.
- Tài khoản Google và Google Sheets đã được tạo sẵn.
- Tài khoản n8n đã được cấu hình và có quyền truy cập vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import" ở góc trên bên phải.
3. Chọn file JSON chứa workflow này và nhấn "Import".

Hoặc, các sếp có thể copy/paste JSON của workflow vào n8n Editor bằng cách:

1. Mở n8n Editor.
2. Nhấn vào nút "Create new workflow".
3. Nhấn vào nút "Import from JSON".
4. Dán JSON của workflow vào ô nhập liệu và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm các node chính sau:

- **Receive Coffee Count (POST)**: Node này nhận dữ liệu từ máy pha cà phê Jura thông qua webhook POST. Các sếp cần cấu hình đường dẫn webhook `{{WEBHOOK_POST_PATH}}` để máy pha cà phê có thể gửi dữ liệu đến.

- **Generate Timestamp**: Node này tạo ra thời gian hiện tại để ghi lại thời điểm dữ liệu được nhận.

- **Prepare Row Data**: Node này chuẩn bị dữ liệu để ghi vào Google Sheets. Các sếp cần đảm bảo rằng dữ liệu được gửi từ máy pha cà phê Jura bao gồm trường `total_coffees`.

- **Fetch Sheet Rows**: Node này lấy dữ liệu từ Google Sheets. Các sếp cần cấu hình `{{SHEET_ID}}`, `{{SHEET_NAME}}` và credentials của Google Sheets.

- **Respond with Sheet Data**: Node này trả về dữ liệu từ Google Sheets thông qua webhook GET. Các sếp cần cấu hình đường dẫn webhook `{{WEBHOOK_GET_PATH}}`.

- **Append to Google Sheet**: Node này ghi dữ liệu vào Google Sheets. Các sếp cần đảm bảo rằng Google Sheets đã được cấu hình với các cột `date`, `time`, và `coffee counter`.

- **Limit to Last Row**: Node này giới hạn số lượng hàng được trả về từ Google Sheets để chỉ lấy hàng cuối cùng.

- **Webhook2**: Node này nhận yêu cầu GET để trả về dữ liệu từ Google Sheets. Các sếp cần cấu hình đường dẫn webhook `{{WEBHOOK_GET_PATH}}`.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node như trên, các sếp có thể kích hoạt workflow bằng cách:

1. Nhấn vào nút "Activate" ở góc trên bên phải của n8n Editor.
2. Kiểm tra dữ liệu mẫu bằng cách gửi một yêu cầu POST đến webhook `{{WEBHOOK_POST_PATH}}` với dữ liệu mẫu:
```json
{
  "total_coffees": 123
}
```
3. Kiểm tra dữ liệu trong Google Sheets để đảm bảo rằng dữ liệu đã được ghi lại đúng cách.
4. Kiểm tra webhook GET `{{WEBHOOK_GET_PATH}}` để đảm bảo rằng dữ liệu được trả về đúng cách.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối với Slack/Telegram**: Các sếp có thể cấu hình workflow để gửi thông báo qua Slack hoặc Telegram mỗi khi có dữ liệu mới từ máy pha cà phê.
- **Lưu log**: Các sếp có thể cấu hình workflow để lưu log các yêu cầu và phản hồi để dễ dàng theo dõi và gỡ lỗi.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về số lượng cà phê được pha trong một khoảng thời gian nhất định.
- **Tích hợp với các hệ thống khác**: Các sếp có thể kết nối workflow này với các hệ thống khác để tạo ra các báo cáo và biểu đồ trực quan.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi số lượng cà phê được pha từ máy Jura và lưu trữ dữ liệu vào Google Sheets. Với workflow này, các sếp có thể dễ dàng theo dõi và phân tích dữ liệu về số lượng cà phê được pha mỗi ngày, giúp tối ưu hóa quá trình pha cà phê và cải thiện trải nghiệm của khách hàng. Hãy áp dụng ngay workflow này để tự động hóa quy trình theo dõi dữ liệu từ máy pha cà phê Jura của bạn!