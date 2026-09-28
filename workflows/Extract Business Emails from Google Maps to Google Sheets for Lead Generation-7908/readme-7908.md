---
title: "🚀 Tự Động Quét Email Doanh Nghiệp Từ Google Maps Vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm, cào dữ liệu Google Maps, lọc website và trích xuất email doanh nghiệp để làm lead generation không cần code."
slug: "tu-dong-quet-email-google-maps-vao-google-sheets-n8n"
tags: [n8n, automation, no-code, lead-generation, google-maps, google-sheets, web-scraping]
keywords: [n8n workflow, quét email google maps, lead generation tự động, trích xuất email doanh nghiệp, n8n google sheets]
---

# 🚀 Tự Động Quét Email Doanh Nghiệp Từ Google Maps Vào Google Sheets

Các sếp có đang tốn hàng giờ đồng hồ mỗi ngày để tìm kiếm khách hàng tiềm năng thủ công trên Google Maps, click vào từng website, mò mẫm tìm email liên hệ rồi copy-paste vào file Excel? Công việc nhàm chán này không chỉ ngốn thời gian mà còn dễ gây mệt mỏi, sai sót và bỏ lỡ những cơ hội vàng trong kinh doanh.

Đừng lo, bài toán tìm kiếm khách hàng (Lead Generation) của các sếp sẽ được giải quyết triệt để với **Workflow n8n tự động quét email doanh nghiệp từ Google Maps**. Chỉ với vài thao tác thiết lập, hệ thống sẽ tự động hóa từ A-Z: tìm kiếm địa điểm, cào dữ liệu, lọc URL, truy cập website, bóc tách email sạch và lưu thẳng vào Google Sheets!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Deskt/VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất cả ngày lướt Google Maps, hệ thống gom hàng trăm leads chỉ trong vài phút.
- **Dữ liệu sạch và chuẩn xác:** Tự động loại bỏ các kết quả trùng lặp (`Remove Duplicates`) và lọc các dòng trống (`Filter Out Empties`).
- **Cá nhân hóa chiến dịch outreach:** Sở hữu danh sách email doanh nghiệp thực tế để chạy chiến dịch Email Marketing hoặc Cold Email hiệu quả.
- **Hoạt động tự động 24/7:** Kích hoạt dễ dàng thông qua giao diện chat (`When chat message received`) hoặc chạy theo lịch trình tùy chỉnh.
:::

### 📦 Các thành phần chính trong Workflow (14 Nodes)
Workflow này được chia thành 4 bước chính vô cùng bài bản:
1. **Google Maps Data Scraper (`When chat message received`, `Scrape Google Maps`):** Nhận từ khóa tìm kiếm và thu thập dữ liệu doanh nghiệp từ Google Maps.
2. **URL Filtering & Processing (`Filter Google URLs`, `Extract URLs`):** Lọc và xử lý danh sách website của doanh nghiệp.
3. **Smart Website Scraper (`Scrape Site`, `Loop Over Items`, `Wait`, `Wait1`):** Lần lượt truy cập từng website với độ trễ thông minh để tránh bị chặn IP.
4. **Email Extraction & Data Export (`Extract Emails`, `Filter Out Empties`, `Remove Duplicates`, `Add to Sheet`):** Trích xuất email từ mã nguồn trang web, lọc dữ liệu sạch, chống trùng lặp và đẩy thẳng vào Google Sheets.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Google (để kết nối với **Google Sheets** lưu danh sách leads).
- API Key hoặc dịch vụ tích hợp cho việc cào dữ liệu (tùy thuộc vào cấu hình node `Scrape Google Maps` và `Scrape Site`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này.
- Mở n8n Editor, chọn **Workflows** -> **Import from Clipboard** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:
- **When chat message received:** Điểm khởi đầu để nhập từ khóa cần tìm kiếm (ví dụ: *"Digital marketing agency in New York"*).
- **Scrape Google Maps & Scrape Site (`httpRequest`):** Kiểm tra lại API endpoint hoặc cấu hình request để đảm bảo quá trình cào dữ liệu từ Google Maps và website mục tiêu trả về kết quả chính xác.
- **Add to Sheet (Google Sheets):** 
  - Chọn tài khoản kết nối (`googleSheetsOAuth2Api`).
  - Chọn file Google Sheets và Sheet Name cụ thể để hệ thống ghi dữ liệu vào đúng bảng tính.
  - Đảm bảo các cột trong Google Sheets khớp với các trường dữ liệu trả về từ node `Extract Emails` (như Tên doanh nghiệp, Website, Email, Địa chỉ...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với một từ khóa mẫu và kiểm tra dữ liệu trả về ở các node trung gian.
- Sau khi kiểm tra dữ liệu đã vào Google Sheets thành công, gạt công tắc sang chế độ **Active** để chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Kết nối thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay lập tức mỗi khi hệ thống quét xong một chiến dịch leads mới.
- **Tự động hóa gửi Email:** Nối tiếp node Google Sheets bằng một công cụ gửi email (như Gmail hoặc Resend) để tự động gửi email giới thiệu dịch vụ tới danh sách vừa thu thập được.
- **Lưu trữ Log:** Thêm bước ghi lại lịch sử chạy workflow vào cơ sở dữ liệu hoặc một sheet riêng để dễ dàng theo dõi hiệu suất.

### 📌 Kết luận
Việc tự động hóa quy trình tìm kiếm khách hàng tiềm năng không chỉ giúp giải phóng sức lao động mà còn tăng tốc độ tiếp cận thị trường của doanh nghiệp. Hãy áp dụng ngay workflow này để tối ưu hóa đội ngũ sales và marketing của các sếp ngay hôm nay!