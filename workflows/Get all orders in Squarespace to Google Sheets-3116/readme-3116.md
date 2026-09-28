---
title: "🚀 Đồng bộ toàn bộ đơn hàng từ Squarespace lên Google Sheets tự động với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình đồng bộ đơn hàng từ nền tảng Squarespace vào Google Sheets bằng n8n, giúp quản lý doanh thu và kho hàng chính xác."
slug: "dong-bo-don-hang-squarespace-google-sheets-n8n"
tags: [n8n, automation, no-code, squarespace, google-sheets, ecommerce, sales]
keywords: [n8n workflow, tự động hóa squarespace, đồng bộ đơn hàng google sheets, quản lý đơn hàng squarespace, n8n ecommerce automation]
---

# 🚀 Đồng bộ toàn bộ đơn hàng từ Squarespace lên Google Sheets tự động

Các sếp đang kinh doanh online trên nền tảng Squarespace chắc chắn đã từng đau đầu với việc phải kiểm tra và copy-paste thủ công từng đơn hàng vào Google Sheets để báo cáo doanh thu, xử lý vận chuyển hoặc phân tích dữ liệu. Việc này không chỉ tốn hàng giờ đồng hồ mỗi ngày mà còn rất dễ xảy ra sai sót, nhầm lẫn số liệu.

Giải pháp ở đây là gì? Hãy để chiếc workflow n8n này "gánh" hết! Hệ thống sẽ tự động lấy toàn bộ đơn hàng từ cửa hàng Squarespace của các sếp và đổ thẳng vào Google Sheets theo lịch trình định sẵn hoặc chạy thủ công tùy ý. 100% tự động, không tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh canh trang quản trị Squarespace rồi nhập liệu vào Excel/Sheets bằng tay.
- **Dữ liệu thời gian thực (Real-time):** Đơn hàng vừa "nổ" là được ghi nhận ngay vào bảng tính nhờ tính năng lịch trình tự động.
- **Chống trùng lặp thông minh:** Sử dụng cơ chế cập nhật tự động (appendOrUpdate), đảm bảo dữ liệu luôn sạch sẽ và chính xác.
- **Vận hành 24/7:** Hoạt động trơn tru không nghỉ lễ, giúp đội ngũ bán hàng và kho vận luôn có sẵn số liệu mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Cửa hàng **Squarespace** và quyền truy cập Squarespace Commerce API (API Key / Header Auth).
- Tài khoản **Google Sheets** đã tạo sẵn một file tính dùng để lưu danh sách đơn hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy sao chép mã nguồn JSON của workflow này, sau đó mở n8n Editor, tạo một workflow mới và chọn **Import from JSON** để dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Node `Globals` (Set):** 
  Đây là nơi các sếp định cấu hình các tham số lọc đơn hàng từ Squarespace. Hãy mở node này và cập nhật các giá trị:
  - `api-version`: Phiên bản API hiện tại của Squarespace (xem trong tài liệu Squarespace Orders API).
  - `modifiedAfter` / `modifiedBefore`: Lọc đơn hàng theo khoảng thời gian (định dạng ISO 8601) nếu cần.
  - `fulfillmentStatus`: Trạng thái đơn hàng muốn lấy (ví dụ: `PENDING`, `FULFILLED`, hoặc `CANCELED`).
  - `maxPage`: Đặt là `-1` để kích hoạt tính năng phân trang vô tận, giúp lấy toàn bộ đơn hàng có sẵn.

- **Node `Query Orders` (HTTP Request):**
  - Cần cấu hình **Credentials** loại `httpHeaderAuth` để kết nối thành công với API của Squarespace (dùng mã API Key được cấp từ trang quản trị cửa hàng).

- **Node `Split Out Order` (Split Out):**
  - Node này có nhiệm vụ tách mảng dữ liệu các đơn hàng trả về từ API thành từng dòng đơn hàng riêng lẻ để xử lý tuần tự.

- **Node `Squarespace Orders Spreadsheet` (Google Sheets):**
  - Chọn **Credentials** kết nối tài khoản Google Sheets của các sếp (`googleSheetsOAuth2Api`).
  - Chọn file Spreadsheet và Sheet Name tương ứng.
  - Đảm bảo thiết lập `Operation` là **Append or Update** để n8n tự động thêm mới hoặc cập nhật đơn hàng cũ nếu có thay đổi.

#### 3. Kích hoạt ⚡️
- Nhấn **On clicking 'execute'` để test thử một lần xem dữ liệu từ Squarespace có đổ về Google Sheets chuẩn chỉnh chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm theo lịch trình từ **Schedule Trigger**.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau node Google Sheets để gửi thông báo real-time về nhóm chat mỗi khi có đơn hàng mới.
- **Lưu Log lỗi:** Thêm nhánh Error Trigger để gửi email cảnh báo cho quản lý nếu kết nối API với Squarespace gặp sự cố.
- **Tích hợp CRM/Email Marketing:** Kết nối tiếp dữ liệu khách hàng từ đơn hàng vào các chiến dịch chăm sóc khách hàng tự động (như Mailchimp, Brevo).

### 📌 Kết luận
Việc tự động hóa quy trình đồng bộ đơn hàng từ Squarespace lên Google Sheets không chỉ giúp tiết kiệm thời gian mà còn nâng tầm chuyên nghiệp cho cửa hàng của các sếp. Hãy cài đặt ngay hôm nay để tối ưu hóa vận hành kinh doanh!