---
title: "🚀 Tự động quét Lead doanh nghiệp từ Google Maps và đồng bộ Google Sheets với n8n"
description: "Xây dựng hệ thống quét thông tin khách hàng tiềm năng tự động từ Google Maps qua RapidAPI, chống trùng lặp thông minh và lưu trữ trực tiếp vào Google Sheets."
slug: "quet-lead-google-maps-n8n-rapidapi-google-sheets"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, rapidapi]
keywords: [n8n workflow, quét lead google maps, tự động hóa lead generation, rapidapi google maps, n8n google sheets]
---

# 🚀 Tự động quét Lead doanh nghiệp từ Google Maps và đồng bộ Google Sheets với n8n

Các sếp có đang tốn hàng giờ để tìm kiếm thông tin khách hàng tiềm năng (tên, số điện thoại, website, mạng xã hội) thủ công trên Google Maps không? Công việc này vừa nhàm chán, vừa tốn thời gian mà lại dễ bỏ sót dữ liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ do **Javier Hita** phát triển, giúp tự động hóa 100% quá trình trích xuất lead từ Google Maps thông qua RapidAPI, tích hợp cơ chế chống trùng lặp thông minh và lưu trữ gọn gàng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không còn phải copy/paste thủ công từng doanh nghiệp.
- **Dữ liệu sạch & chuẩn hóa**: Tự động lọc bỏ các lead trùng lặp ở cả cấp độ tìm kiếm và cấp độ doanh nghiệp (dựa vào `business_id`).
- **Tối ưu chi phí API**: Chế độ lọc thông minh giúp tiết kiệm 50-80% chi phí gọi API nhờ bỏ qua các từ khóa đã quét.
- **Kho dữ liệu sẵn sàng**: Thông tin chi tiết từ tên, địa chỉ, số điện thoại, website cho đến các trang mạng xã hội (Facebook, Instagram, LinkedIn) được lưu thẳng vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản RapidAPI** đã đăng ký gói Local Business Data API.
- **Google Sheets** chứa 2 sheet: `keyword_searches` (chứa từ khóa tìm kiếm) và `stores_data` (lưu kết quả).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 10 nodes phối hợp nhịp nhàng, các sếp cần lưu ý cấu hình các điểm sau:

- **Node `Load Search Criteria` & `Load Existing Leads` (`googleSheets`)**: 
  - Chọn tài khoản kết nối Google Sheets (`googleSheetsOAuth2Api`).
  - Trỏ đúng vào file Google Sheet chuẩn bị sẵn và chọn đúng tên 2 tab `keyword_searches` và `stores_data`.
- **Node `Google Maps API Request` (`httpRequest`)**: 
  - Cấu hình thông tin xác thực RapidAPI của các sếp bằng `httpHeaderAuth`.
  - Đảm bảo endpoint API gọi tới Local Business Data hoạt động chính xác.
- **Node `Rate Limit Delay` (`wait`)**: 
  - Mặc định đặt thời gian chờ là 10 giây giữa các request để tránh việc RapidAPI chặn IP hoặc giới hạn tốc độ (rate limit). Các sếp có thể điều chỉnh tùy theo gói API của mình.
- **Node `Save New Leads` (`googleSheets`)**: 
  - Thiết lập chế độ `Append` để tự động thêm các dòng lead mới vào tab `stores_data` mà không làm mất dữ liệu cũ.

#### 3. Cấu trúc dữ liệu Google Sheets mẫu
Tại tab **`keyword_searches`**, các sếp cấu hình các cột như sau:
```
| select | query | lat | lon | country_iso_code |
|--------|-------|-----|-----|------------------|
| X | Restaurants Madrid | 40.4168 | -3.7038 | ES |
| X | Hair Salons NYC | 40.7589 | -73.9851 | US |
```
*(Đánh dấu `X` vào cột `select` để chọn từ khóa cần quét).*

#### 4. Kích hoạt ⚡️
- Nhấn **`Start Lead Generation`** (`manualTrigger`) để chạy thử nghiệm với một vài dòng dữ liệu mẫu.
- Kiểm tra xem dữ liệu có được đẩy về Google Sheets chuẩn xác không.
- Bật **Active** workflow để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Slack hoặc Telegram ở cuối vòng lặp để nhận tin nhắn báo cáo mỗi khi quét xong một từ khóa hoặc hoàn thành danh sách lead.
- **Tự động hóa lịch trình**: Thay thế node `manualTrigger` bằng `Schedule Trigger` để chạy quét tự động hàng tuần hoặc hàng tháng mà không cần can thiệp thủ công.
- **Làm sạch dữ liệu**: Sử dụng thêm node Code bằng Python/JavaScript để chuẩn hóa lại số điện thoại hoặc định dạng email trước khi lưu vào Google Sheets.

### 📌 Kết luận
Với workflow n8n này, việc thu thập data khách hàng tiềm năng từ Google Maps đã trở nên dễ dàng và chuyên nghiệp hơn bao giờ hết. Hãy setup ngay hôm nay để tối ưu hóa đội ngũ sales và marketing của các sếp!