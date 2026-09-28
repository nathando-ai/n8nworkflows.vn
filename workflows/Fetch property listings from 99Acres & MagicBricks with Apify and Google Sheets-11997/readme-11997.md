---
title: "🚀 Tự động cào dữ liệu bất động sản từ 99Acres & MagicBricks vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động thu thập, làm sạch và lưu trữ danh sách bất động sản từ 99Acres và MagicBricks thông qua Apify và Google Sheets."
slug: "tu-dong-cao-du-lieu-bat-dong-san-99acres-magicbricks-n8n"
tags: [n8n, automation, real-estate, apify, google-sheets, web-scraping]
keywords: [n8n workflow, 99Acres scraping, MagicBricks automation, cào dữ liệu bất động sản, google sheets automation]
---

# 🚀 Tự động cào dữ liệu bất động sản từ 99Acres & MagicBricks vào Google Sheets

Các sếp làm trong ngành môi giới hoặc nghiên cứu thị trường bất động sản chắc chắn hiểu cảm giác mệt mỏi khi phải copy/paste thủ công từng tin đăng từ các cổng thông tin lớn như **99Acres** hay **MagicBricks**. Việc này không chỉ tốn hàng giờ đồng hồ mà dữ liệu thu về còn dễ bị lệch lạc, thiếu sót và khó tổng hợp.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do tác giả **Parth Pansuriya** thiết kế. Workflow này giúp tự động hóa 100% quy trình: nhận URL tìm kiếm từ Form, gọi Apify để cào dữ liệu, làm sạch và phân loại, sau đó tự động khởi tạo và đồng bộ toàn bộ vào Google Sheets một cách ngăn nắp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Chỉ cần nhập URL tìm kiếm qua form, mọi việc còn lại hệ thống tự lo.
- **Dữ liệu chuẩn hóa & sạch sẽ**: Tự động lọc bỏ các tin trùng lặp, chuẩn hóa cấu trúc dữ liệu (Mã BĐS, Tiêu đề, Giá, Đơn giá/Sqft, Đường dẫn).
- **Phân tách khoa học**: Tự động tạo Google Spreadsheet mới với các Sheet riêng biệt cho từng cổng 99Acres và MagicBricks.
- **Tiết kiệm 95% thời gian**: Thay vì mất cả ngày tổng hợp thủ công, toàn bộ dữ liệu trả về chỉ trong vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google**: Để kết nối Google Sheets (OAuth2).
- **Tài khoản Apify**: Lấy API Token và cấu hình Actor để cào dữ liệu từ 99Acres và MagicBricks (được gọi thông qua HTTP Request node).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua menu giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Property Search URLs (Form Trigger)**: Nơi người dùng gửi URL tìm kiếm. Các sếp có thể mở node này để tùy chỉnh giao diện form nhận đầu vào cho 99Acres và MagicBricks.
- **Fetch 99Acres Listings & Fetch MagicBricks Listings (HTTP Request)**: Cấu hình kết nối tới Apify API bằng cách điền API Token và Actor ID tương ứng để cào dữ liệu từ URL đã truyền vào.
- **Filter & Format 99Acres Listings & Filter & Format MagicBricks Listings (Code)**: Các node JavaScript này làm nhiệm vụ bóc tách, chuẩn hóa dữ liệu thô (Property ID, Title, Price, Price per Sqft, URL) và loại bỏ các tin đăng bị trùng lặp.
- **Create Master Spreadsheet & Append Rows (Google Sheets)**: 
  - Kết nối tài khoản Google Sheets của các sếp qua **Google Sheets OAuth2 API**.
  - Node `Create Master Spreadsheet` sẽ tự động sinh ra một file Google Sheet mới cho mỗi lần chạy.
  - Các node `Append Rows` sẽ đẩy dữ liệu đã làm sạch vào đúng Sheet tương ứng (99Acres sheet và MagicBricks sheet) mà không cần cấu hình thủ công tên file trước.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử bằng cách gửi form với các URL hợp lệ.
- Kiểm tra kết quả trả về trên Google Drive/Google Sheets xem file đã được tạo và điền dữ liệu chuẩn chỉnh chưa.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi quá trình cào dữ liệu hoàn tất kèm theo link Google Sheets.
- **Lên lịch chạy định kỳ (Cron/Schedule)**: Thay vì dùng Form Trigger, các sếp có thể đổi thành Schedule Trigger để hệ thống tự động quét thị trường bất động sản mỗi tuần/mỗi tháng một lần cho các khu vực mục tiêu.
- **Lưu trữ lịch sử**: Kết hợp thêm cơ chế ghi log vào một Master Sheet tổng hợp để theo dõi biến động giá bất động sản theo thời gian.

### 📌 Kết luận
Việc nghiên cứu thị trường bất động sản chưa bao giờ dễ dàng đến thế khi có sự trợ giúp của tự động hóa n8n kết hợp với AI/Scraper. Hãy áp dụng ngay workflow này để tối ưu hóa năng suất cho đội ngũ của các sếp nhé!