---
title: "🚀 Tự động thu thập dữ liệu kênh YouTube toàn diện vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động cào và cập nhật toàn bộ thông tin chi tiết của kênh YouTube (lượt xem, sub, video, quốc gia...) vào Google Sheets."
slug: "tu-dong-thu-thap-du-lieu-kenh-youtube-google-sheets-n8n"
tags: [n8n, automation, youtube, google-sheets, market-research, no-code]
keywords: [n8n workflow, crawl youtube data, youtube to google sheets, tự động hóa n8n, agent circle]
---

# 🚀 Tự động thu thập dữ liệu kênh YouTube toàn diện vào Google Sheets

Các sếp làm trong ngành Marketing Agency, MCN (Multi-Channel Network), nghiên cứu thị trường (Market Research) hay tư vấn kênh YouTube chắc chắn hiểu rõ nỗi khổ khi phải thủ công đi "soi" từng kênh đối thủ: từ số lượng subscriber, tổng lượt xem, ngày tạo kênh cho đến các thẻ tags. Việc này ngốn hàng giờ đồng hồ và rất dễ sai sót.

Giải pháp ở đây là gì? Một con bot tự động hóa 100% bằng **n8n** sẽ thay các sếp làm việc đó! Workflow này sẽ đọc danh sách link kênh YouTube từ Google Sheets, gọi YouTube API để lấy toàn bộ thông số chi tiết và tự động ghi ngược lại bảng tính một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Thay vì copy/paste thủ công, hàng trăm kênh YouTube được phân tích chỉ trong vài phút.
- **Dữ liệu chuẩn xác & thời gian thực:** Lấy trực tiếp từ YouTube API (tiêu đề, mô tả, sub, views, video count, ngày tạo, quốc gia, avatar...).
- **Quản lý trạng thái thông minh:** Tự động đánh dấu `Finished` khi thành công hoặc `Error` nếu lỗi, tránh việc xử lý trùng lặp.
- **Xây dựng dashboard dễ dàng:** Dữ liệu nằm sẵn trong Google Sheets giúp các sếp tạo báo cáo trực quan ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Account & Google Cloud Console:** Để tạo API Credentials kết nối Google Sheets và YouTube Data API v3.
- **Template Google Sheets:** Bản sao từ [YouTube - Get Channel Information Template](https://docs.google.com/spreadsheets/d/1easnNMrm8ovxhlZQwPUge6UbPnUVFKBeaQY5EmmG1gM/edit?gid=426418282#gid=426418282).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này.
- Mở giao diện n8n, chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON vào workspace).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Google Sheets Nodes (`Google Sheets - Get Channel URLs`, `Google Sheets - Update Data`, `Google Sheets - Update Data - Error`):**
  - Tạo kết nối `Google Sheets OAuth2 API`.
  - Trỏ đến file Google Sheet template đã chuẩn bị và chọn đúng tab **Channel URLs**.
- **Switch Node (`Switch - Detect URL Type`):**
  - Node này dùng để phân loại xem link đầu vào là dạng **Full URL** hay **Custom URL** để điều hướng sang nhánh API phù hợp. Giữ nguyên cấu hình mặc định nếu dùng template chuẩn.
- **HTTP Request Nodes (`HTTP Request - Get Channel Info By Full URL`, `HTTP Request - Get Channel Info By Custom URL`):**
  - Cấu hình thông tin xác thực `YouTube OAuth2 API` hoặc API Key qua Google Cloud Console. Đảm bảo dự án trên Google Cloud đã bật **YouTube Data API v3**.
- **Loop Node (`Loop Over Items` / `splitInBatches`):**
  - Giúp duyệt qua từng dòng trong bảng tính có trạng thái là `Ready` để tránh quá tải API.

#### 3. Kích hoạt ⚡️
- Điền một vài link kênh YouTube vào cột URL trong Google Sheets và đặt trạng thái ở cột Status thành **Ready**.
- Quay lại n8n, nhấn **Test workflow** để chạy thử nghiệm.
- Kiểm tra lại Google Sheets xem dữ liệu đã được lấp đầy và trạng thái đổi thành `Finished` chưa. Nếu mọi thứ OK, hãy bật công tắc **Active** để hoàn tất!

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa hoàn toàn:** Thay vì dùng nút `Manual Trigger`, các sếp có thể thay thế bằng **Google Sheets Trigger** hoặc **Schedule Trigger** (chạy định kỳ hàng tuần/hàng tháng) để cào dữ liệu tự động.
- **Cảnh báo lỗi:** Kết hợp thêm node **Telegram** hoặc **Slack** để nhận thông báo ngay lập tức nếu có lỗi (`Error`) xảy ra trong quá trình crawl dữ liệu kênh lớn.
- **Mở rộng kho dữ liệu:** Có thể nối thêm các workflow phân tích video gần nhất, lấy bình luận (comments) của kênh đó để nghiên cứu sâu hơn về Insight khán giả.

### 📌 Kết luận
Workflow thu thập dữ liệu kênh YouTube này là một vũ khí cực kỳ lợi hại cho các đội ngũ Digital Marketing và Research. Hãy "lên đồ" ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!