---
title: "🚀 Tự động quét danh sách doanh nghiệp từ Google Maps vào Google Sheets hoặc Excel với Serper"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa tìm kiếm và trích xuất dữ liệu doanh nghiệp từ Google Maps sử dụng Serper API, lưu trực tiếp vào Google Sheets hoặc file Excel."
slug: "tao-danh-sach-doanh-nghiep-google-maps-serper-n8n"
tags: [n8n, automation, lead-generation, google-maps, serper, google-sheets, excel]
keywords: [n8n workflow, tự động hóa tìm kiếm, quét data google maps, serper api, lead generation n8n, google sheets automation]
---

# 🚀 Tự động quét danh sách doanh nghiệp từ Google Maps vào Google Sheets hoặc Excel với Serper

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) bằng cách thủ công trên Google Maps tốn rất nhiều thời gian: phải gõ từng từ khóa, copy từng tên công ty, địa chỉ, số điện thoại rồi paste vào file Excel. Quy trình này vừa nhàm chán, vừa dễ sai sót. 

Giải pháp? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình trích xuất dữ liệu doanh nghiệp từ Google Maps thông qua **Serper API**, sau đó tự động phân tích, sắp xếp và lưu trữ gọn gàng vào **Google Sheets** hoặc xuất file **Excel (XLSX)** chỉ trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy-paste thủ công hàng trăm kết quả tìm kiếm trên Google Maps.
- **Dữ liệu chuẩn xác, sạch sẽ:** Tự động lọc và cấu trúc hóa các thông tin quan trọng như tên, địa chỉ, website, đánh giá, tọa độ...
- **Linh hoạt lưu trữ:** Tùy chọn lưu thẳng lên Google Sheets để team sales cùng truy cập hoặc tải về dưới dạng file Excel.
- **Giao diện Chat thông minh:** Kích hoạt quá trình tìm kiếm nhanh chóng thông qua Chat Trigger trực quan.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã kích hoạt (Self-hosted hoặc n8n Cloud).
- **Serper API Key:** Tài khoản tại [Serper.dev](https://serper.dev) để gọi API tìm kiếm Google Maps.
- **Google Sheets Credentials:** Tài khoản Google Cloud/Service Account để n8n có thể ghi dữ liệu vào Google Sheets (nếu dùng phương án lưu Google Sheets).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau đây để workflow hoạt động mượt mà:

- **Node `When chat message received` (chatTrigger):** Nơi bắt đầu yêu cầu tìm kiếm của các sếp (ví dụ: *"Tìm các quán cà phê tại Quận 1, TP.HCM"*).
- **Node `Initialization` & `Variables Chat` (set):** Thiết lập các biến mặc định cho từ khóa tìm kiếm, vị trí hoặc giới hạn số lượng kết quả trả về.
- **Node `Extract Serper Map` (httpRequest):** Node cốt lõi gọi đến Serper API. Các sếp cần cấu hình Header chứa **API Key** của Serper.dev và truyền tham số từ khóa từ node chat vào.
- **Node `Split Out Serper` (splitOut):** Tách mảng kết quả thô từ API thành các dòng dữ liệu độc lập để xử lý từng doanh nghiệp một.
- **Node `Prepare Data` & `Extract Data   ` (set):** Làm sạch, chuẩn hóa các trường dữ liệu (Tên, Địa chỉ, Số điện thoại, Rating, Link Website...).
- **Node `Upsert Data in Sheets` (googleSheets) hoặc `Get Data in XLSX` (convertToFile):** 
  - Chọn tài khoản Google Credentials và trỏ tới file Google Sheets, Sheet Name cụ thể nếu muốn lưu online.
  - Hoặc sử dụng node chuyển đổi định dạng sang Excel nếu muốn tải file trực tiếp về máy.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** và nhập thử một từ khóa qua khung chat để kiểm tra xem dữ liệu có đổ về Google Sheets/Excel đúng ý không.
- Sau khi test thành công, gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm node gửi thông báo qua Telegram hoặc Slack ngay khi workflow quét xong danh sách doanh nghiệp kèm theo link file Excel.
- **Lên lịch định kỳ (Schedule Trigger):** Thay vì dùng Chat Trigger, các sếp có thể đổi thành Schedule Trigger để hệ thống tự động quét lead mới hàng tuần theo các từ khóa cố định.
- **Lọc trùng lặp:** Kết hợp thêm logic kiểm tra dữ liệu cũ trong Google Sheets trước khi Upsert để tránh bị trùng lặp các doanh nghiệp đã quét trước đó.

### 📌 Kết luận
Workflow tích hợp Serper API và Google Maps này là "vũ khí" cực mạnh cho các đội ngũ Marketing và Sales trong việc chủ động khai thác data khách hàng địa phương. Hãy thiết lập ngay hôm nay để tự động hóa toàn bộ quy trình tìm kiếm khách hàng tiềm năng cho doanh nghiệp của các sếp!