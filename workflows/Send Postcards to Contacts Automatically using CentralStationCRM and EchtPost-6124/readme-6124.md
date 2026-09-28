---
title: "📬 Tự động gửi thiệp mừng đến khách hàng qua CentralStationCRM và EchtPost"
description: "Hướng dẫn tự động hóa gửi thiệp mừng đến khách hàng khi cập nhật thông tin trong CentralStationCRM bằng n8n và EchtPost"
slug: "tu-dong-gui-thiep-mung-khach-hang-centralstationcrm-echtpost"
tags: [n8n, automation, no-code, crm, postcard]
keywords: [n8n workflow, tự động hóa, crm, thiệp mừng, EchtPost]
---

# 📬 Tự động gửi thiệp mừng đến khách hàng qua CentralStationCRM và EchtPost

[![CSCRM Logo](https://s3.42he.com/cscrm-marketing-page-production/Logo_Central_Station_CRM_0dd02e23d2.jpeg)](https://centralstationcrm.de)

[CentralStationCRM](https://centralstationcrm.de) là CRM đơn giản và trực quan dành cho các đội nhỏ. Trên n8n, chúng tôi chia sẻ các ý tưởng workflow CRM để giúp các sếp làm việc hiệu quả hơn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi thiệp mừng đến khách hàng mới cập nhật trong CentralStationCRM
- Tiết kiệm thời gian và công sức thủ công
- Đảm bảo thông tin gửi đi chính xác và kịp thời
- Tăng cường tương tác với khách hàng thông qua thiệp mừng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản CentralStationCRM
- Tài khoản EchtPost
- API Key của EchtPost
- Template ID của EchtPost
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n](https://n8n.io/workflows/6124)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ nội dung JSON và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Person is updated in CentralStationCRM" (Webhook)**
   - Double-click vào node này
   - Đảm bảo HTTP Method là POST
   - Authentication: none
   - Lưu ý: Sau khi cấu hình xong, bạn sẽ cần cấu hình webhook trong CentralStationCRM (xem phần 2 bên dưới)

2. **Node "Set fields needed for EchtPost" (Set)**
   - Double-click vào node này
   - Kiểm tra các trường dữ liệu được thiết lập có phù hợp với yêu cầu của EchtPost hay không

3. **Node "Is 'EchtPost' included in 'taggings'?" (If)**
   - Double-click vào node này
   - Kiểm tra logic điều kiện có đúng là kiểm tra từ "EchtPost" trong trường taggings hay không

4. **Node "Send postcard with EchtPost" (HTTP Request)**
   - Double-click vào node này
   - METHOD: POST
   - URL: https://api.echtpost.de/v1/cards
   - Authentication: none
   - SEND BODY: True
   - Body Content Type: JSON
   - Specify Body: Using JSON
   - JSON Code (Chuyển sang "Expression"!):
     ```json
     {
       "apikey": "ENTER HERE-API-KEY",
       "card": {
         "template_id": "HERE-TEMPLATE-ID",
         "deliver_at": "3-days-from-now",
         "notification_type": "before_send",
         "notification_email": "YOUR EMAIL",
         "contacts_attributes": [
           {
             "company_name": "{{ $json.body.record.companies[0].name }}",
             "street": "{{ $json.body.record.addrs[0].street }}",
             "zip": "{{ $json.body.record.addrs[0].zip }}",
             "city": "{{ $json.body.record.addrs[0].city }}",
             "country_code": "{{ $json.body.record.addrs[0].country_code }}"
           }
         ]
       }
     }
     ```
   - Thay thế các giá trị API Key, Template ID và email của bạn vào các trường tương ứng

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, hãy test workflow với dữ liệu mẫu:
   - Thêm tag "EchtPost" cho một người trong CentralStationCRM
   - Click vào "Listen for Test Event" trên node webhook trước khi cập nhật thông tin người đó
   - Kiểm tra xem workflow có chạy đúng và gửi thiệp thành công hay không

2. Khi đã test thành công, chuyển từ "Test URL" sang "Production URL":
   - Double-click vào node webhook
   - Copy URL mới được tạo
   - Cập nhật URL mới này vào webhook trong CentralStationCRM (xem phần 2 bên dưới)

3. Cuối cùng, bật Active workflow để bắt đầu tự động hóa quá trình gửi thiệp mừng.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo qua Slack/Telegram khi thiệp được gửi thành công
- Lưu log các thiệp đã gửi vào Google Sheets để theo dõi
- Tạo báo cáo định kỳ về số lượng thiệp đã gửi và tỷ lệ mở
- Kết hợp với các workflow khác để tự động hóa thêm các tác vụ liên quan đến khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức khi gửi thiệp mừng đến khách hàng. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn và tăng cường tương tác với khách hàng một cách hiệu quả. Hãy thử áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!