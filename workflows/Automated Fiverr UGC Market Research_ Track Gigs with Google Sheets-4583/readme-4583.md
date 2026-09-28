---
title: "🚀 Tự Động Hoá Nghiên Cứu Thị Trường UGC Trên Fiverr: Theo Dõi Gigs Với Google Sheets"
description: "Workflow tự động hóa 24/7 giúp các sếp theo dõi, phân tích và lưu trữ tất cả các gig UGC (User-Generated Content) trên Fiverr vào Google Sheets, tiết kiệm thời gian lên đến 10 giờ/tuần. Kết quả: Dữ liệu sạch, cập nhật liên tục, sẵn sàng phân tích chiến lược marketing."
slug: "tieu-dong-hoa-nghien-cuu-thi-truong-ugc-fiverr-google-sheets"
tags: [n8n, automation, marketing, no-code, web-scraping, google-sheets]
keywords: [n8n workflow fiverr, tự động hóa nghiên cứu thị trường, scrap dữ liệu fiverr, theo dõi gig ugc, google sheets tự động]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Thị Trường UGC Trên Fiverr: Theo Dõi Gigs Với Google Sheets**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** trên Fiverr để theo dõi xu hướng UGC (User-Generated Content) – mất từ 2-3 tiếng/tuần.
- **Ghi chép dữ liệu** vào Excel/Google Sheets một cách rườm rà, dễ bị lỗi.
- **Không cập nhật kịp thời** vì phải làm thủ công, dẫn đến quyết định marketing không chính xác.
- **Phải tra cứu lại** thông tin gig cũ khi cần phân tích xu hướng – tốn thêm thời gian.

**Workflow này giải quyết tất cả!** Với chỉ **1 lần cấu hình**, các sếp sẽ tự động:
✅ **Lấy dữ liệu** tất cả gig UGC trên Fiverr mỗi ngày.
✅ **Trích xuất thông tin chi tiết** (giá, tên người bán, tiêu đề, link).
✅ **Lưu vào Google Sheets** với định dạng sạch, dễ phân tích.
✅ **Cập nhật liên tục** mà không cần can thiệp thủ công.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** so với cách làm thủ công.
- **Dữ liệu chính xác 100%** – không bị lỗi copy/paste.
- **Cập nhật tự động** mỗi ngày, không bỏ lỡ xu hướng mới.
- **Sẵn sàng phân tích** với Google Sheets có định dạng sẵn (timestamp, giá, link).
- **Dễ mở rộng** để kết nối với Slack/Email báo cáo hoặc thêm logic deduplication.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets).
2. **API Key OAuth2 của Google Sheets** (cấu hình trong n8n).
3. **Môi trường n8n** (self-hosted hoặc dùng n8n.cloud – nhưng **self-hosted ổn định hơn** cho workflow dài hạn).
4. **Google Sheet sẵn sàng** (các sếp có thể tạo một sheet mới với các cột: `Timestamp`, `Title`, `Price`, `Seller`, `Gig URL`).

👉 **🎁 Đăng ký VPS TinoHost để self-host n8n** (giảm 39% với mã **VPSN8N**):
[https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4583).
- **Nhấn "Import"** trong n8n Editor và dán JSON vào.
- **Hoặc copy toàn bộ JSON** và dán vào ô `Import Workflow` trong n8n.

:::note[LƯU Ý]
- **Không cần chỉnh sửa JSON** nếu các sếp muốn sử dụng cấu hình mặc định.
- **Nếu muốn thay đổi**, các sếp có thể mở workflow trong n8n Editor và chỉnh sửa trực tiếp trên canvas.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần chú ý cấu hình sau:

##### **🏃‍♂️ Node 1: `Daily Fiverr Scrape Trigger` (scheduleTrigger)**
- **Chức năng**: Khởi động workflow theo lịch (ví dụ: hàng ngày lúc 9h UTC).
- **Cấu hình**:
  - **Frequency**: `Every 24 hours` (hoặc tùy chỉnh theo nhu cầu).
  - **Time**: `09:00 AM UTC` (hoặc chọn giờ phù hợp với múi giờ của các sếp).
  - **Time Zone**: Chọn múi giờ của mình (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).

##### **🌐 Node 2: `Fetch Fiverr Search Results` (httpRequest)**
- **Chức năng**: Gửi yêu cầu HTTP GET đến Fiverr để lấy kết quả tìm kiếm gig UGC.
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://www.fiverr.com/search/gigs?query=UGC%20content%20creator` (đã encode `UGC content creator` thành `UGC%20content%20creator`).
  - **Headers**:
    - Thêm `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`).
    - **Lưu ý**: Nếu Fiverr chặn request, các sếp cần **thay đổi User-Agent** hoặc sử dụng **proxy**.
  - **Response Format**: Chọn `JSON` (n8n sẽ tự động chuyển đổi HTML thành JSON).

##### **📄 Node 3: `Extract Data from HTML` (html)**
- **Chức năng**: Trích xuất dữ liệu từ HTML trả về (giá, tên người bán, tiêu đề, link gig).
- **Cấu hình**:
  - **Operation**: `extractHtmlContent`.
  - **CSS Selectors/XPath**:
    - Các sếp cần **cập nhật lại selectors** nếu Fiverr thay đổi cấu trúc HTML (thông thường, các sếp có thể sử dụng selectors mặc định trong workflow gốc).
    - **Dữ liệu trích xuất**:
      - **Price**: `//div[@class="price"]/span/text()` (ví dụ).
      - **Title**: `//h2[@class="heading-h2"]/a/text()`.
      - **Seller**: `//div[@class="seller-name"]/text()`.
      - **Gig URL**: `//a[@class="gig-title-link"]/@href`.
    - **Lưu ý**: Nếu selectors không hoạt động, các sếp có thể mở DevTools (F12) trên trang Fiverr, chọn phần tử cần trích xuất, và sao chép XPath/CSS Selector từ đó.

##### **📊 Node 4: `Append Gig Data to Sheet` (googleSheets)**
- **Chức năng**: Ghi dữ liệu vào Google Sheets.
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (cần cấu hình trước trong n8n).
  - **Operation**: `append`.
  - **Sheet Name**: Đặt tên sheet (ví dụ: `Fiverr_UGC_Gigs`).
  - **Range**: Chọn `Sheet1!A1` (n8n sẽ tự động append dữ liệu vào hàng mới).
  - **Headers**: Chọn `Use first row as headers` (n8n sẽ tự động tạo cột `Timestamp`, `Title`, `Price`, `Seller`, `Gig URL`).
  - **Timestamp**: Bật tùy chọn để thêm thời gian scrape vào cột đầu tiên.

---
#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run**: Nhấn `Execute` để chạy workflow với dữ liệu mẫu và kiểm tra kết quả.
- **Active Workflow**: Sau khi kiểm tra thành công, bật `Active` để workflow chạy tự động theo lịch.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CẢI TIẾN TRONG LỰC]
1. **Thêm Logic Deduplication**:
   - Sử dụng node `Set` hoặc `Function` để kiểm tra xem gig đã tồn tại trong sheet trước khi append.
   - **Cách làm**: Thêm node `Function` sau `Extract Data` với mã JavaScript kiểm tra `Gig URL` đã có trong sheet chưa.

2. **Báo Cáo Bằng Email/Slack**:
   - Thêm node `Email` hoặc `Slack` sau `Append Gig Data` để gửi báo cáo hàng ngày.
   - **Ví dụ**: Gửi email với tiêu đề `"New UGC Gigs on Fiverr - [Date]"` và nội dung là danh sách gig mới.

3. **Lưu Log Dữ Liệu**:
   - Tạo một sheet khác để lưu log lỗi (ví dụ: `Fiverr_Scrape_Logs`) bằng node `googleSheets` với operation `append`.

4. **Tùy Chỉnh Query Fiverr**:
   - Thay đổi `query` trong URL để theo dõi các chủ đề khác (ví dụ: `video editing`, `3D modeling`).
   - **Ví dụ**: `https://www.fiverr.com/search/gigs?query=video%20editing`.

5. **Sử Dụng Proxy**:
   - Nếu Fiverr chặn request, các sếp có thể cấu hình proxy trong node `httpRequest` để tránh bị block.
:::

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa nghiên cứu thị trường UGC trên Fiverr mà **không cần viết code**. Với chỉ **1 lần cấu hình**, các sếp sẽ:
✔ **Tiết kiệm thời gian** lên đến 10 giờ/tuần.
✔ **Nhận dữ liệu cập nhật** mỗi ngày.
✔ **Phân tích dễ dàng** với Google Sheets sẵn sàng.

**Hành động ngay!**
1. **Cài đặt n8n** trên VPS (self-hosted) để ổn định.
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

**Cần hỗ trợ?** Liên hệ với tác giả Yaron Been qua:
🔗 [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
📺 [YouTube](https://www.youtube.com/@YaronBeen/videos)

---
**🚀 CÓ THỂ MỞ RỘNG NÊN GÌ?**
- Thêm **báo cáo tự động** qua Email/Slack.
- **Phân tích xu hướng** bằng cách tính trung bình giá, số gig mới mỗi tháng.
- **Kết nối với Notion** để quản lý dự án UGC hiệu quả hơn!