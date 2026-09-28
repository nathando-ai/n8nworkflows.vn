---
title: "🚀 Tự Động Hoàn Thành Báo Cáo Airbnb London: Scrape 1000+ Listing & Lưu Trữ Trên Google Sheets (Không Cần Code)"
description: "Workflow này tự động scrape tất cả các listing Airbnb ở London (hoặc bất kỳ địa điểm nào) với pagination, lấy chi tiết đầy đủ từ URL, và lưu trữ vào Google Sheets với định dạng chuyên nghiệp - tiết kiệm 10+ giờ công so với phương pháp thủ công."
slug: "tieu-dong-hoan-thanh-bao-cao-airbnb-london"
tags: [n8n, automation, market-research, airbnb-scraping, google-sheets, mcp, no-code]
keywords: [n8n workflow airbnb, scrape airbnb listing, tự động hóa nghiên cứu thị trường, lưu trữ dữ liệu airbnb, google sheets automation, mcp airbnb]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Airbnb London: Scrape 1000+ Listing & Lưu Trữ Trên Google Sheets**

### **Nỗi Đau Của Các Sếp Khi Nghiên Cứu Thị Trường Airbnb**
Các sếp thường phải:
- **Tốn thời gian vô cùng** để copy-paste thông tin từ hàng trăm trang listing Airbnb vào Excel/Google Sheets.
- **Mất nhiều công sức** để tìm kiếm và lấy chi tiết đầy đủ (giá, đánh giá, tiện ích, quy định nhà) từ từng URL.
- **Không có dữ liệu toàn diện** vì chỉ lấy được một số trang đầu tiên (do Airbnb giới hạn pagination).
- **Không thể tự động hóa** vì không biết cách scrape dữ liệu mà không vi phạm chính sách của Airbnb.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Scrape tự động** tất cả listing từ Airbnb (London hoặc bất kỳ địa điểm nào) với pagination.
✅ **Lấy chi tiết đầy đủ** từ URL của mỗi listing (giá, đánh giá, tiện ích, quy định nhà, mô tả).
✅ **Lưu trữ vào Google Sheets** với định dạng chuyên nghiệp, sẵn sàng phân tích.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công** so với phương pháp thủ công: Không cần copy-paste từ hàng trăm trang.
- **Dữ liệu toàn diện**: Scrape tất cả listing từ Airbnb (không giới hạn trang).
- **Chi tiết đầy đủ**: Lấy thông tin từ URL của mỗi listing (giá, đánh giá, tiện ích, quy định nhà).
- **Sẵn sàng phân tích**: Dữ liệu được lưu vào Google Sheets với định dạng chuyên nghiệp.
- **Hoạt động tự động**: Chỉ cần kích hoạt workflow một lần, nó sẽ chạy liên tục.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (cài trên VPS hoặc máy chủ riêng).
2. **Credentials MCP (Model Context Protocol)**:
   - **MCP Client API Key**: Đăng ký tại [MCP Airbnb](https://mcp.airbnb.com/) và thêm vào n8n dưới tên `mcpClientApi`.
   - **Google Sheets OAuth2 API Key**: Tạo tại [Google Cloud Console](https://console.cloud.google.com/) và thêm vào n8n dưới tên `googleSheetsOAuth2Api`.
3. **Google Sheet sẵn sàng**:
   - ID Sheet: `15IOJquaQ8CBtFilmFTuW8UFijux10NwSVzStyNJ1MsA` (hoặc tạo sheet mới và thay đổi trong node `Clear Google Sheet`).
   - Các cột bắt buộc:
     ```
     id, name, url, price_per_night, total_price, price_details, beds_rooms, rating, reviews, badge, location, houseRules, highlights, description, amenities
     ```
4. **Tham số search mặc định** (có thể điều chỉnh trong node `Airbnb Search`):
   - **Địa điểm**: "London" (thay đổi theo nhu cầu).
   - **Người lớn**: 7.
   - **Trẻ em**: 1.
   - **Ngày check-in**: "2025-08-14".
   - **Ngày check-out**: "2025-08-17".
   - **Số trang**: 2 (có thể tăng lên 5-10 trang nếu cần).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào n8n Editor:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5981) hoặc copy toàn bộ JSON dưới đây vào file `airbnb-scrape.json`.
2. **Mở n8n Editor** và nhấn `Import` → Chọn file JSON vừa tải.
3. **Hoặc copy/paste JSON** vào tab `JSON` của n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần điều chỉnh các node quan trọng sau:

##### **A. Cấu Hình MCP Client**
- **Node**: `Airbnb Search` và `Get Airbnb Listing Details`.
- **Lưu ý**:
  - Đảm bảo credentials `mcpClientApi` đã được thêm vào n8n và có quyền truy cập vào tools `airbnb_search` và `airbnb_listing_details`.
  - Nếu không có quyền, liên hệ với [MCP Airbnb](https://mcp.airbnb.com/) để cấp phép.

##### **B. Cấu Hình Google Sheets**
- **Node**: `Clear Google Sheet` và `Update Google Sheet`.
- **Lưu ý**:
  - Thay đổi `Sheet ID` trong node `Clear Google Sheet` nếu sử dụng sheet mới (ví dụ: `123456789abcdefghijklmnopqrstuvwxyz`).
  - Đảm bảo sheet đã được chia sẻ với tài khoản Google OAuth2 đã cấu hình trong n8n.

##### **C. Điều Chỉnh Tham Số Search**
- **Node**: `Airbnb Search`.
- **Lưu ý**:
  - Thay đổi `location`, `adults`, `children`, `check-in`, `check-out` theo nhu cầu.
  - Thay đổi `page_limit` trong node `If1` để điều chỉnh số trang scrape (mặc định là 2).

##### **D. Định Dạng Dữ Liệu**
- **Node**: `Format Data`, `Edit Fields`, `Final Results`.
- **Lưu ý**:
  - Các node này sử dụng JavaScript để định dạng dữ liệu. Nếu cần thay đổi cách xử lý dữ liệu, các sếp có thể mở tab `Code` và chỉnh sửa logic.

##### **E. Kích Hoạt Workflow**
1. **Test Run**:
   - Nhấn `Execute Workflow` để chạy thử với dữ liệu mẫu.
   - Kiểm tra Google Sheet xem dữ liệu đã được lưu chưa.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang trạng thái `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Scrape Địa Điểm Khác**:
   - Thay đổi `location` trong node `Airbnb Search` để scrape listing ở Paris, New York, hoặc bất kỳ địa điểm nào.
2. **Lưu Log Hoạt Động**:
   - Thêm node `Slack` hoặc `Email` để nhận báo cáo khi workflow hoàn thành.
   - Ví dụ: Sau node `Update Google Sheet`, thêm node `Slack` để gửi thông báo thành công.
3. **Tự Động Hoàn Thành Định Kỳ**:
   - Sử dụng node `Schedule` để chạy workflow hàng tuần/tháng.
4. **Phân Tích Dữ Liệu**:
   - Sau khi dữ liệu được lưu vào Google Sheets, các sếp có thể sử dụng **Google Data Studio** hoặc **Power BI** để tạo báo cáo thị trường chuyên nghiệp.

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình nghiên cứu thị trường Airbnb, tiết kiệm thời gian và công sức so với phương pháp thủ công. Bằng cách scrape tất cả listing từ Airbnb và lưu trữ vào Google Sheets, các sếp có thể **phân tích dữ liệu một cách chuyên nghiệp** và đưa ra quyết định kinh doanh chính xác hơn.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Chạy thử** và kiểm tra kết quả.
3. **Tích hợp vào quy trình** của doanh nghiệp để tối ưu hóa nghiên cứu thị trường.

👉 [Tải workflow JSON](https://n8n.io/workflows/5981) và bắt đầu tự động hóa ngay! 🚀