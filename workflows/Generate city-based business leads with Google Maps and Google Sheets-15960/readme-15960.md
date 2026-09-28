---
title: "🚀 Tự động quét và tạo danh sách khách hàng tiềm năng từ Google Maps với n8n"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu doanh nghiệp theo thành phố từ Google Maps, vượt qua giới hạn API và đồng bộ trực tiếp vào Google Sheets."
slug: "tu-dong-quet-leads-tu-google-maps-google-sheets"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, no-code]
keywords: [n8n workflow, tạo lead tự động, google maps scraper, cào dữ liệu doanh nghiệp, google sheets automation]
---

# 🚀 Tự động quét và tạo danh sách khách hàng tiềm năng từ Google Maps với n8n

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) thủ công trên Google Maps tốn rất nhiều thời gian của đội ngũ sales: phải gõ từng từ khóa, lướt từng trang, copy thủ công tên, số điện thoại, website rồi dán vào Excel. Chưa kể, các API thông thường thường bị giới hạn số lượng kết quả trả về, khiến các sếp bỏ lỡ vô số khách hàng tiềm năng quý giá.

Workflow n8n này do chuyên gia **Abdullah Al Shishani** phát triển sẽ giải quyết triệt để bài toán trên. Hệ thống hoạt động hoàn toàn tự động 100% không cần code: chỉ cần điền form yêu cầu, workflow sẽ tự động chia nhỏ bản đồ thành lưới tọa độ, quét sâu 3 trang kết quả, lọc bỏ trùng lặp và lưu trữ gọn gàng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải copy-paste thủ công, hàng trăm lead chất lượng được tổng hợp chỉ sau vài phút.
- **Vượt giới hạn API:** Sử dụng hệ thống lưới tọa độ động (Dynamic Grid) giúp quét triệt để mọi doanh nghiệp trong thành phố mà không bị giới hạn kết quả.
- **Dữ liệu sạch & chuẩn hóa:** Tự động loại bỏ các bản ghi trùng lặp (dựa trên Place ID) và trích xuất chi tiết: số điện thoại, website, địa chỉ, đánh giá (ratings).
- **Đồng bộ thời gian thực:** Dữ liệu tự động đẩy thẳng vào Google Sheets sẵn sàng cho đội telesales gọi điện ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets Account** (để lưu trữ danh sách lead).
- **Google Cloud Console Project** đã bật các dịch vụ:
  - Geocoding API
  - Places API (New hoặc Legacy)
- **Google Maps API Key** để sử dụng trong form đầu vào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp hoặc sao chép toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Dấu ba chấm (...) -> **Import from File / Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình các node quan trọng sau:

- **On form submission (`formTrigger`):** Node này tạo ra một giao diện web form nhỏ. Khi chạy test hoặc Active, n8n sẽ cung cấp một URL form để các sếp nhập loại hình doanh nghiệp, thành phố và Google Maps API Key.
- **Geocode Target City & Search Page (1, 2, 3) (`httpRequest`):** Các node này gọi trực tiếp đến Google Maps API. Hãy đảm bảo API Key của các sếp đã được cấp quyền gọi Geocoding và Places API.
- **Wait for Page (2, 3) (`wait`):** Các node tạm dừng giữa các trang nhằm tuân thủ giới hạn tốc độ (rate limit) của Google, tránh việc bị block API.
- **Append row in sheet (`googleSheets`):** 
  - Chọn **Credentials** kết nối với tài khoản Google của các sếp (sử dụng *Google Sheets OAuth2 API*).
  - Chọn file Google Sheet đích (Master Spreadsheet) và Tab/Sheet cụ thể nơi lưu dữ liệu.
  - Kiểm tra lại phần mapping các trường thông tin (tên, số điện thoại, địa chỉ, website...) khớp với các cột trong Sheet.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và truy cập vào URL của form (`On form submission`) để điền thử dữ liệu mẫu (Ví dụ: Thành phố "Hanoi", Ngành nghề "Coffee shop").
- Kiểm tra kết quả trả về trong n8n và Google Sheets.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau node `Append row in sheet` để nhận thông báo ngay lập tức về điện thoại mỗi khi quét xong một thành phố mới.
- **Tùy chỉnh vùng quét:** Chỉnh sửa hệ thống tính toán tọa độ trong node `Generate Dynamic Grid` để mở rộng hoặc thu hẹp bán kính quét theo nhu cầu thực tế của chiến dịch.
- **Lọc tự động:** Thêm một node `If` trước khi ghi vào Google Sheet để lọc bỏ các doanh nghiệp không có số điện thoại hoặc có điểm đánh giá thấp hơn mức mong muốn.

### 📌 Kết luận
Workflow "Generate city-based business leads with Google Maps and Google Sheets" là một vũ khí cực kỳ mạnh mẽ cho các đội ngũ Sales và Marketing hiện đại. Thay vì tốn hàng giờ cào dữ liệu thủ công, giờ đây các sếp chỉ cần vài cú click để sở hữu một phễu lọc khách hàng tự động, chính xác và chuyên nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất kinh doanh!