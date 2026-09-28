---
title: "🚀 Tự động trích xuất Google Ads Creatives theo Domain với SerpAPI và xuất ra CSV"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu quảng cáo từ Google Ads Transparency Center bằng SerpAPI, phân loại định dạng và xuất file CSV."
slug: "trich-xuat-google-ads-creatives-bang-serpapi-n8n"
tags: [n8n, automation, marketing, serpapi, google-ads, csv]
keywords: [n8n workflow, serpapi google ads, cào dữ liệu quảng cáo, google ads transparency center, tu dong hoa marketing]
---

# 🚀 Tự động trích xuất Google Ads Creatives theo Domain với SerpAPI và xuất ra CSV

Các nhà quảng cáo, marketer và agency thường tốn rất nhiều thời gian để "soi" chiến dịch quảng cáo của đối thủ cạnh tranh trên Google Ads Transparency Center. Việc thủ công tìm kiếm, lọc domain và copy từng hình ảnh, tiêu đề hay video tốn hàng giờ đồng hồ. 

Đừng làm việc đó bằng tay nữa! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n hoàn toàn tự động sử dụng **SerpAPI** để bóc tách toàn bộ mẫu quảng cáo (Text, Image, Video) của bất kỳ domain nào và lưu trực tiếp thành các file CSV gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Chỉ cần nhập Domain và Region, phần còn lại n8n lo.
- **Lọc chuẩn xác**: Tránh lấy nhầm quảng cáo của bên thứ ba bằng bộ lọc domain thông minh.
- **Phân loại rõ ràng**: Tự động chia quảng cáo thành 3 định dạng: Text, Image, Video và xuất ra 3 file CSV riêng biệt (`text_[domain]_ads.csv`, `image_[domain]_ads.csv`, `video_[domain]_ads.csv`).
- **Tiết kiệm thời gian nghiên cứu**: Giúp team Marketing phân tích chiến lược của đối thủ chỉ trong vòng vài nốt nhạc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản SerpAPI**: Cần có API Key để gọi dữ liệu từ `google_ads_transparency_center` engine. (Đăng ký tại [SerpAPI](https://serpapi.com/)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của workflow (hoặc import file JSON gốc) dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes chính. Các sếp cần chú ý cấu hình các điểm sau:

- **Set Domain & Region (Node `Set`)**: 
  - Đặt domain cần phân tích (ví dụ: `example.com`).
  - Điền mã vùng khu vực (Region Code) dạng số theo chuẩn của SerpAPI (Tra cứu mã vùng tại [SerpApi Regions](https://serpapi.com/google-ads-transparency-center-regions)).
- **Get Ads Page 1 (Node `HTTP Request`)**: 
  - Thêm Credentials xác thực cho SerpAPI (API Key).
  - Kết nối tới endpoint `google_ads_transparency_center` của SerpAPI sử dụng biến từ node `Set Domain & Region`.
- **Extract Ad Creatives (Node `Function`)**: 
  - Đoạn code JavaScript trong node này sẽ tự động lọc các quảng cáo có `target_domain` khớp chính xác với domain đầu vào, loại bỏ các kết quả nhiễu.
- **Split by Format (Node `Switch`)**: 
  - Phân loại dữ liệu dựa trên trường `format` của quảng cáo thành 3 nhánh riêng biệt: Text, Image và Video.
- **Convert Text/Image/Video Ads to CSV (Các node `Spreadsheet File`)**: 
  - Cấu hình thao tác `toFile` để lưu kết quả vào thư mục `/files/` trên hệ thống n8n với định dạng tên file tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm với domain mẫu.
- Kiểm tra kết quả trả về ở các nhánh CSV xem file đã được tạo chuẩn chỉnh chưa.
- Gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node Telegram hoặc Slack để nhận thông báo kèm file CSV ngay khi workflow chạy xong.
- **Tự động hóa định kỳ**: Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Schedule Trigger` để cào dữ liệu đối thủ hàng tuần/hàng tháng tự động.
- **Lưu trữ đám mây**: Thay vì lưu local trên VPS, có thể dùng node Google Drive để tự động upload các file CSV lên folder chung của team.

### 📌 Kết luận
Workflow "Extract Google Ads Creatives by Domain" là một vũ khí cực mạnh cho các Performance Marketer và Agency trong việc nghiên cứu thị trường và đối thủ. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình làm việc ngay hôm nay!