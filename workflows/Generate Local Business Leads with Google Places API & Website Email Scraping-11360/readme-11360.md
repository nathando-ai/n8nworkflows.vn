---
title: "🚀 Tự động quét khách hàng tiềm năng địa phương với Google Places API và Website Email Scraping"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm doanh nghiệp địa phương, cào dữ liệu website và lấy email khách hàng tiềm năng hoàn toàn tự động bằng n8n."
slug: "tao-lead-doanh-nghiep-dia-phuong-google-places-n8n"
tags: [n8n, automation, lead-generation, google-places, web-scraping, no-code]
keywords: [n8n workflow, quét lead địa phương, google places api, lấy email website, cào dữ liệu tự động, lead generation automation]
---

# 🚀 Tự động quét khách hàng tiềm năng địa phương với Google Places API & Website Email Scraping

Việc tìm kiếm khách hàng tiềm năng (Local Leads) theo cách thủ công như lướt Google Maps, copy từng tên công ty, số điện thoại, rồi cố gắng tìm email trên website của họ ngốn rất nhiều thời gian và công sức của đội ngũ Sales. 

Chính vì vậy, workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động hóa từ A-Z quy trình: nhận yêu cầu từ biểu mẫu, gọi Google Places API tìm kiếm doanh nghiệp, cào dữ liệu website để lấy email liên hệ, và gom lại thành một tệp CSV hoàn chỉnh. Các sếp chỉ việc bấm nút và nhận danh sách "nóng hổi"!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh copy-paste thủ công từ Google Maps vào Excel.
- **Dữ liệu phong phú & chính xác:** Lấy được thông tin chi tiết (Tên, địa chỉ, số điện thoại, đánh giá, website và đặc biệt là email liên hệ trực tiếp từ trang web).
- **Quy trình khép kín tự động:** Nhập từ khóa qua Form -> Xử lý ngầm -> Xuất file CSV sẵn sàng cho các chiến dịch Email Marketing hay Cold Calling.
- **Tối ưu chi phí API:** Tích hợp sẵn các node chờ (Wait) và chia lô (Batch) giúp tránh việc bị Google Places API chặn do vượt quá giới hạn tốc độ (Rate Limit).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Google Cloud Console:** Cần tạo một API Key cho dịch vụ **Google Places API** (hoặc Places API New).
- **Form đầu vào:** Sẵn sàng sử dụng `Form Trigger` tích hợp sẵn trong workflow để nhập từ khóa tìm kiếm (Ví dụ: Ngành nghề, khu vực).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow (hoặc tải file JSON từ nguồn) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Form Trigger & Parse Form Data:** Đây là điểm khởi đầu. Các sếp có thể tùy chỉnh các trường (fields) trên form để người dùng nhập từ khóa ngành nghề (ví dụ: "Nhà hàng", "Spa") và khu vực (ví dụ: "Quận 1, TP.HCM").
- **Google Places Search1 & Get Business Details:** Đây là 2 node HTTP Request chịu trách nhiệm gọi API của Google. Các sếp bắt buộc phải điền **Google Places API Key** của mình vào phần Header hoặc Query Parameters của các node này.
- **Wait (Rate Limit) & Wait:** Node chờ rất quan trọng để tuân thủ quy định về tốc độ gọi API của Google, tránh việc bị trả về lỗi `OVER_QUERY_LIMIT`.
- **Extract Emails & Clean:** Node Code này chứa đoạn script dùng Regex để quét và làm sạch các địa chỉ email tìm thấy trên website của doanh nghiệp.
- **Convert to CSV:** Node này chuyển đổi toàn bộ dữ liệu đã được tổng hợp thành định dạng file CSV để các sếp dễ dàng tải về hoặc đẩy tiếp lên Google Drive/Email.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử điền thông tin vào `Form Trigger` để test với một từ khóa nhỏ trước.
- Sau khi kiểm tra dữ liệu trả về ở bảng điều khiển bên phải thấy chính xác, các sếp gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets / Airtable:** Thay vì chỉ xuất file CSV, các sếp có thể thay thế hoặc nối thêm node Google Sheets để tự động lưu mọi lead quét được vào một bảng tính chung của đội ngũ Sales.
- **Gửi thông báo qua Telegram/Slack:** Thêm một node Telegram để bot hú lên ngay khi workflow quét xong một danh sách lead mới.
- **Gửi Email tự động:** Kết hợp thêm node Gmail hoặc Resend để tự động gửi chuỗi email chăm sóc (Cold Email) ngay sau khi có danh sách lead.

### 📌 Kết luận
Workflow quét lead địa phương bằng Google Places kết hợp Website Scraping này là một "vũ khí bí mật" giúp các Agency, đội ngũ Sales và Marketer tiết kiệm hàng đống thời gian tìm kiếm khách hàng. Hãy triển khai ngay trên hệ thống n8n của các sếp để tối ưu hóa hiệu suất kinh doanh!