---
title: "🚀 Tự động giám sát giá sản phẩm Amazon với Bright Data và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động cào và cập nhật giá sản phẩm Amazon theo thời gian thực sử dụng Bright Data API và Google Sheets."
slug: "tu-dong-giam-sat-gia-amazon-bright-data-google-sheets"
tags: [n8n, automation, bright-data, google-sheets, e-commerce, web-scraping]
keywords: [n8n workflow, giám sát giá amazon, bright data api, cào dữ liệu amazon, tự động hóa google sheets]
---

# 🚀 Tự động giám sát giá sản phẩm Amazon với Google Sheets & Bright Data

Việc theo dõi giá cả của đối thủ cạnh tranh hoặc danh mục sản phẩm của chính bạn trên Amazon là một công việc cực kỳ tẻ nhạt và mất thời gian nếu làm thủ công. Các sếp thường phải mất hàng giờ mở từng link, copy giá và dán vào Excel. 

Chưa kể, Amazon có cơ chế chống bot (anti-bot) rất gắt gao, khiến việc cào dữ liệu (web scraping) bằng các công cụ thông thường trở nên bất khả thi.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Đọc danh sách sản phẩm từ Google Sheets, gọi API của **Bright Data** để lấy dữ liệu giá mới nhất, và tự động cập nhật ngược lại Google Sheets theo thời gian biểu định sẵn mà không cần các sếp phải nhón tay làm gì!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh dò giá thủ công từng sản phẩm mỗi ngày.
- **Dữ liệu luôn thời gian thực:** Cập nhật giá chính xác từ Amazon nhờ nền tảng trích xuất dữ liệu mạnh mẽ của Bright Data.
- **Xử lý hàng loạt mượt mà:** Tự động chia lô (batching) các URL để tránh quá tải API và hệ thống.
- **Hoạt động tự động 24/7:** Chạy ngầm theo lịch trình (Schedule) cài đặt sẵn, tự động ghi nhận thay đổi giá vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data** kèm API Key để lấy dữ liệu Amazon.
- **Google Account** để tạo và kết nối Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy ngon lành, các sếp cần cấu hình chính xác các thành phần sau:

- **Google Sheets (`Read data from Google Sheet` & `Update the records by ASIN`):**
  - Tạo một Google Sheet mới với các cột: `Product URL`, `ZIP code`, và `ASIN`.
  - Tại cột `ASIN`, các sếp dùng hàm sau để tự động tách mã ASIN từ link sản phẩm:
    ```excel
    =REGEXEXTRACT(A4, "/(?:dp|gp/product|product)/([A-Z0-9]{10})")
    ```
  - Kết nối tài khoản Google thông qua `Google Sheets OAuth2 API` trong 2 node Google Sheets của workflow.

- **Bright Data (`Initiate request from URLs`, `Check Status by Snapshot ID`, `Get the data`):**
  - Đăng ký tài khoản Bright Data, lấy **API Key** và tạo thông tin xác thực dạng **Bearer Token** (`httpBearerAuth`).
  - Đảm bảo cấu hình đúng endpoint của Bright Data Dataset cho Amazon trong node `Initiate request from URLs`.

- **Xử lý hàng loạt (`Process URLs by batch of 10s`, `Space the request by 1 second`, `Wait`):**
  - Workflow sử dụng `Split In Batches` để xử lý 10 URL một lần và node `Wait` / `Space the request by 1 second` để giãn cách các request, giúp tránh bị chặn bởi cơ chế bảo vệ của Amazon.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với 1-2 dòng dữ liệu đầu tiên trên Google Sheets.
- Kiểm tra xem dữ liệu giá đã được cập nhật chính xác vào sheet chưa.
- Nếu mọi thứ mượt mà, hãy bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch trình từ node `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Cảnh báo giá giảm/tăng:** Thêm một node **Slack** hoặc **Telegram** sau bước cập nhật Google Sheets để bắn thông báo ngay lập tức về điện thoại khi có sản phẩm thay đổi giá đột biến.
- **Lưu lịch sử giá:** Thay vì chỉ cập nhật đè lên giá cũ, các sếp có thể tạo thêm một Sheet "Price History" để vẽ biểu đồ biến động giá theo thời gian.
- **Mở rộng nguồn:** Có thể áp dụng cấu trúc workflow này tương tự cho Shopee, Lazada hoặc các sàn thương mại điện tử khác hỗ trợ bởi Bright Data.

### 📌 Kết luận
Với workflow n8n kết hợp Bright Data và Google Sheets này, việc theo dõi biến động giá thị trường trên Amazon chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay và tự động hóa công việc kinh doanh của các sếp ngay hôm nay!