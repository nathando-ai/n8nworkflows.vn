---
title: "🚀 Tự động quét và tạo danh sách khách hàng tiềm năng (Leads) từ Google Maps với n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa tìm kiếm khách hàng tiềm năng từ Google Maps API, lưu trữ và quản lý qua Google Sheets một cách chuyên nghiệp."
slug: "tao-danh-sach-khach-hang-tu-google-maps-n8n"
tags: [n8n, automation, no-code, sales, marketing, google-maps, google-sheets]
keywords: [n8n workflow, tạo leads google maps, tự động hóa sales, google maps api n8n, khai thác khách hàng tiềm năng]
---

# 🚀 Tự động quét và tạo danh sách khách hàng tiềm năng (Leads) từ Google Maps

Việc tìm kiếm khách hàng tiềm năng (Leads) thủ công trên Google Maps tốn rất nhiều thời gian, công sức và dễ bị sót dữ liệu. Các sếp thường phải copy/paste từng tên quán ăn, công ty, số điện thoại, địa chỉ vào Excel — một quy trình cực kỳ "gây nản" cho đội ngũ Sales và Marketing.

Được thiết kế bởi chuyên gia **Alex Kim** (n8n Ambassador & Verified Partner), workflow này sẽ giúp các sếp tự động hóa 100% quy trình quét dữ liệu doanh nghiệp, quán xá, cửa hàng từ Google Maps theo danh mục và mã bưu chính (Zip Codes), sau đó tự động lưu trữ và đồng bộ hóa gọn gàng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Quét dữ liệu theo giờ hoặc chạy thủ công mà không cần thao tác tay.
- **Dữ liệu chuẩn xác & Sạch sẽ**: Tích hợp tính năng tự động lọc (`Filter`) và loại bỏ trùng lặp (`Remove Duplicates`) giúp danh sách leads luôn tinh gọn.
- **Xử lý thông minh (Exponential Backoff)**: Cơ chế chờ và thử lại tự động (`Wait`, `Check Max Retries`) giúp tránh việc bị Google Maps API chặn do gửi quá nhiều request cùng lúc.
- **Đồng bộ Google Sheets mượt mà**: Tự động thêm mới hoặc cập nhật trạng thái leads (`Update Status to Success`, `Add rows in Google Sheets`) trực tiếp vào file quản lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Cloud Account**: Đã bật Google Maps API (Places API) và cấu hình OAuth2 Credentials.
- **Google Sheets**: Một file Google Sheets chuẩn bị sẵn cấu trúc lưu trữ (bao gồm các sheet chứa danh mục/subcategories, mã bưu chính/zip codes và trạng thái).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chính thức của n8n (ID: 2605) hoặc copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Settings & Google Sheets Nodes (`GS - Get Subcategory`, `GS - Get Zip Codes`, `GS - Get Status`, `Add rows in Google Sheets`, `Update Status to Success`)**: 
  - Kết nối tài khoản Google Sheets thông qua `Google Sheets OAuth2 API`.
  - Trỏ đúng đường dẫn URL của file Google Sheets và tên các Sheet tương ứng (Subcategories, Zip Codes, Leads Data).
- **GMaps API (Node `httpRequest`)**:
  - Cấu hình Credentials sử dụng `Google OAuth2 API` kết nối với dự án Google Cloud đã bật Google Maps API.
  - Kiểm tra lại phần endpoint và query parameters để đảm bảo gửi đúng từ khóa tìm kiếm và khu vực.
- **Cơ chế xử lý lỗi (`Exponential Backoff`, `Wait`)**: 
  - Các node này đã được Alex Kim thiết lập sẵn để xử lý mã lỗi từ API. Các sếp có thể giữ nguyên thời gian chờ (delay) để đảm bảo giới hạn gọi API (Rate Limit) của Google.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** ở node `When clicking "Execute Workflow"` để chạy thử nghiệm với một lượng dữ liệu nhỏ nhằm kiểm tra kết nối Google Sheets và Google Maps API.
- Nếu dữ liệu đổ về bảng tính chính xác, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch trình (`Run workflow every hours`).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram / Slack Bot**: Thêm node thông báo để ngay khi workflow quét xong một mẻ leads hoặc gặp lỗi quá giới hạn, hệ thống sẽ gửi tin nhắn hú họa cho các sếp ngay lập tức.
- **Tích hợp AI (OpenAI / Claude)**: Sau khi lấy được thông tin website của doanh nghiệp từ Google Maps, các sếp có thể dùng node AI để tự động phân tích độ lớn doanh nghiệp hoặc soạn sẵn email giới thiệu dịch vụ cá nhân hóa.
- **Chia nhỏ Batch**: Tinh chỉnh thông số ở node `Loop Zips` và `Loop Subcats` để tối ưu hóa tốc độ quét mà không vi phạm chính sách của Google API.

### 📌 Kết luận
Workflow "Generate Leads with Google Maps" là một "vũ khí" cực kỳ lợi hại cho các đội ngũ Sales và Growth Hacker muốn xây dựng data khách hàng tự động, quy mô lớn. Hãy cài đặt ngay lên VPS của các sếp và bắt đầu thu thập khách hàng tiềm năng ngay hôm nay!