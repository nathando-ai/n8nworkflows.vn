---
title: "🚀 Tự Động Quét & Lọc Khách Hàng Tiềm Năng Bằng Google Maps & Places API"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm, lọc leads theo ngành nghề và khu vực từ Google Maps, sau đó lưu trực tiếp vào Google Sheets hoàn toàn tự động."
slug: "tao-business-leads-google-maps-google-sheets-n8n"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, no-code]
keywords: [n8n workflow, quét leads google maps, google places api, tự động hóa sales, lead generation n8n]
---

# 🚀 Tự Động Quét & Lọc Khách Hàng Tiềm Năng Bằng Google Maps & Places API

Các sếp có đang đau đầu vì tốn hàng giờ đồng hồ mỗi ngày để tìm kiếm thông tin khách hàng tiềm năng (leads) trên Google Maps, copy-paste thủ công tên, số điện thoại, địa chỉ vào Excel? Việc này không chỉ mất thời gian, dễ sai sót mà còn làm gián đoạn các chiến dịch sales quan trọng của đội ngũ.

Hãy để workflow n8n này giúp các sếp giải quyết triệt để bài toán trên! Hệ thống sẽ tự động nhận thông tin yêu cầu từ Form, gọi trực tiếp vào **Google Maps & Places API**, lọc các kết quả chất lượng và tự động đồng bộ danh sách khách hàng sạch sẽ vào **Google Sheets** chỉ trong vài giây. 100% tự động, không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần điền form yêu cầu (loại hình kinh doanh, khu vực), hệ thống tự động làm phần còn lại.
- **Dữ liệu chuẩn xác:** Khai thác trực tiếp từ kho dữ liệu khổng lồ của Google Maps & Places API.
- **Lọc leads thông minh:** Tự động kiểm tra và loại bỏ các kết quả không hợp lệ, giữ lại thông tin liên hệ chất lượng.
- **Đồng bộ thời gian thực:** Toàn bộ khách hàng tiềm năng được đẩy thẳng vào Google Sheets, sẵn sàng cho team Sales gọi chốt đơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Maps Platform API Key** (Đã kích hoạt Places API và Geocoding API).
- **Tài khoản Google** để kết nối với Google Sheets (OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này (hoặc copy toàn bộ mã JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Extraction Configs (`formTrigger`):** Đây là điểm khởi đầu, tạo một giao diện form để các sếp nhập các thông tin: Loại hình kinh doanh (ví dụ: Coffee shop, Spa...), khu vực mục tiêu (ví dụ: Quận 1, TP.HCM), số lượng leads tối đa cần quét và Google Maps API Key của các sếp.
- **Get Location Coordinates (`httpRequest`):** Node này dùng Geocoding API của Google để đổi tên khu vực các sếp nhập thành tọa độ (Latitude & Longitude) chính xác.
- **Search Google Places (`httpRequest`):** Sử dụng Places API để tìm kiếm các địa điểm dựa trên tọa độ và từ khóa ngành nghề. Các sếp cần đảm bảo API Key truyền vào đúng định dạng của Google.
- **If Lead is Valid (`if`):** Bộ lọc thông minh giúp kiểm tra xem kết quả trả về có đầy đủ thông tin cơ bản (tên, địa chỉ, thông tin liên hệ) hay không trước khi lưu.
- **Append row in sheet (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets thông qua **Credentials** (`googleSheetsOAuth2Api`).
  - Chọn file Google Sheets và đúng Sheet Name mà các sếp muốn lưu trữ danh sách leads.
  - Map các trường dữ liệu từ các node trước vào đúng cột trong Google Sheet (Tên doanh nghiệp, Địa chỉ, Số điện thoại, Website...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau node thêm vào Google Sheets để bắn thông báo real-time về máy mỗi khi có danh sách leads mới được quét xong.
- **Làm sạch dữ liệu nâng cao:** Kết hợp thêm các AI Node (như OpenAI / Anthropic) để phân loại mức độ tiềm năng hoặc viết email chào hàng (cold email) cá nhân hóa cho từng lead.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy theo lịch (Cron/Schedule) để tổng hợp số lượng leads quét được mỗi tuần gửi vào email của sếp lớn.

### 📌 Kết luận
Việc tìm kiếm khách hàng tiềm năng thủ công đã lỗi thời và tốn kém nhân lực. Với workflow n8n tích hợp Google Maps API này, các sếp có thể xây dựng một cỗ máy khai thác dữ liệu tự động 24/7, giúp đội ngũ sales luôn có nguồn leads dồi dào để tiếp cận. Triển khai ngay hôm nay để bứt phá doanh thu thôi nào các sếp!