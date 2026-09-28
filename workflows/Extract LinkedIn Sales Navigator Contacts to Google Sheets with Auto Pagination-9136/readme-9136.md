---
title: "🚀 Tự động trích xuất danh bạ LinkedIn Sales Navigator vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu khách hàng tiềm năng từ LinkedIn Sales Navigator, tự động phân trang và lưu thẳng vào Google Sheets mà không cần code."
slug: "trich-xuat-linkedin-sales-navigator-google-sheets-n8n"
tags: [n8n, automation, no-code, linkedin, google-sheets, scraping]
keywords: [n8n workflow, linkedin sales navigator, cào dữ liệu linkedin, google sheets automation, tự động hóa marketing]
---

# 🚀 Tự động trích xuất danh bạ LinkedIn Sales Navigator vào Google Sheets

Các sếp đang làm Sales, B2B Marketing hay Lead Generation chắc chắn đều ngán ngẩm cảnh phải copy-paste thủ công từng thông tin liên hệ từ LinkedIn Sales Navigator vào file Excel. Vừa tốn hàng giờ đồng hồ, vừa dễ sai sót lại cực kỳ nhàm chán. 

Bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Workflow này giúp các sếp cào dữ liệu contact (họ tên, chức danh, công ty, địa chỉ, link profile...) từ LinkedIn Sales Navigator, tự động chuyển trang (pagination) và đồng bộ thẳng vào Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý dữ liệu lớn mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì ngồi copy từng trang, hệ thống tự động cào hàng trăm contact chỉ trong vài phút.
- **Dữ liệu chuẩn xác, sạch sẽ:** Tự động phân tách tên, chức danh, công ty, địa chỉ và profile URL đưa vào đúng cột trên Google Sheets.
- **Thông minh & An toàn:** Tích hợp tính năng tự động phân trang (auto-pagination) và cơ chế giãn cách thời gian (rate limit) thông minh giúp bảo vệ tài khoản LinkedIn không bị khóa.
- **Vận hành hoàn toàn tự động:** Chạy mượt mà trên nền tảng n8n self-hosted, không cần can thiệp thủ công sau khi setup.
:::

### 🏆 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Self-hosted n8n (Workflow yêu cầu môi trường tự host để gọi API ổn định).
- **Tài khoản LinkedIn:** Có đăng ký tài khoản LinkedIn Sales Navigator.
- **API Access:** Key truy cập API trích xuất (có thể liên hệ tác giả để xin dùng thử miễn phí 1 tháng).
- **Tiện ích trình duyệt:** Cài đặt extension [EditThisCookie](https://chromewebstore.google.com/detail/editthiscookie-v3/ojfebgpkimhlhcblbalbfjblapadhbol) để lấy cookie phiên đăng nhập.
- **Google Sheets:** Tài khoản Google kết nối với n8n OAuth2 và một file Google Sheet chuẩn bị sẵn để lưu data.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste toàn bộ cấu trúc JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **Node `Scrape LinkedIn Contacts API` (HTTP Request):**
  - Cần cài đặt Header Auth credentials với `x-api-key` nhận được từ tác giả.
  - Cung cấp thông tin trong phần cấu hình (cookies phiên đăng nhập LinkedIn lấy từ EditThisCookie, đường dẫn tìm kiếm Sales Navigator URL, và số trang cần cào `total_pages`).
- **Node `Set Search Parameters` (Set):** 
  - Tùy chỉnh các tham số tìm kiếm và URL Sales Navigator phù hợp với chiến dịch của các sếp.
- **Node `Save Contacts to Google Sheets` (Google Sheets):**
  - Kết nối tài khoản Google Sheets của các sếp (chọn `googleSheetsOAuth2Api`).
  - Trỏ tới file Google Sheet và Sheet Name tương ứng, chọn thao tác `append` để thêm dòng mới liên tục.
- **Node `Rate Limit Delay Between Requests` (Wait):** 
  - ⚠️ **TUYỆT ĐỐI KHÔNG GIẢM THỜI GIAN NÀY.** Khoảng nghỉ ngẫu nhiên từ 30-60 giây giữa các request giúp đánh lừa thuật toán, mô phỏng hành vi lướt web của con người và bảo vệ tài khoản LinkedIn khỏi bị quét/khóa.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** trên node `Start Workflow` (Manual Trigger) để test thử nghiệm với 1-2 trang dữ liệu đầu tiên.
- Kiểm tra lại Google Sheets xem dữ liệu đã đổ về chuẩn xác chưa.
- Sau khi mọi thứ mượt mà, bật công tắc **Active** góc trên cùng bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng để nhận tin nhắn thông báo mỗi khi workflow quét xong một chiến dịch Lead Generation.
- **Tự động làm sạch dữ liệu:** Kết hợp thêm các node Code (JavaScript) để chuẩn hóa số điện thoại, viết hoa chữ cái đầu của tên hoặc loại bỏ các ký tự đặc biệt trước khi lưu vào Google Sheets.
- **Lưu log lỗi:** Thiết lập đường nhánh Error Trigger để gửi email cảnh báo cho các sếp nếu phiên đăng nhập LinkedIn hết hạn (cookie expired).

### 📌 Kết luận
Việc cào dữ liệu khách hàng tiềm năng chưa bao giờ dễ dàng và an toàn đến thế với sự kết hợp giữa n8n và LinkedIn Sales Navigator. Hãy triển khai ngay hôm nay để tối ưu hóa phễu bán hàng B2B của các sếp!