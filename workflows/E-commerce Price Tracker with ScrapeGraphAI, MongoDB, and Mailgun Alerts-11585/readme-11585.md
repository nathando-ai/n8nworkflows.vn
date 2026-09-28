---
title: "🚀 Tự động theo dõi giá thương mại điện tử với ScrapeGraphAI, MongoDB và Mailgun"
description: "Xây dựng hệ thống giám sát giá đối thủ tự động 100% sử dụng AI ScrapeGraphAI, lưu trữ dữ liệu MongoDB và gửi cảnh báo qua Mailgun khi có biến động."
slug: "tu-dong-theo-doi-gia-thuong-mai-dien-tu-scrapegraphai-mongodb-mailgun"
tags: [n8n, automation, scrapegraphai, mongodb, mailgun, e-commerce]
keywords: [n8n workflow, theo dõi giá đối thủ, scrapegraphai, tự động hóa giá sản phẩm, mongodb n8n, mailgun alert]
---

# 🚀 Tự động theo dõi giá thương mại điện tử với ScrapeGraphAI, MongoDB và Mailgun

Các sếp kinh doanh online chắc chắn hiểu rõ cảm giác "đau đầu" khi phải thủ công kiểm tra giá đối thủ mỗi ngày, hoặc bất lực khi các code cào web truyền thống (CSS/XPath) cứ gãy liên tục mỗi khi website đổi giao diện. 

Workflow n8n này chính là "vũ khí tối thượng" giúp tự động hóa toàn bộ quy trình: nhận danh sách URL, cào dữ liệu thông minh bằng AI, lưu trữ lịch sử vào MongoDB và tự động bắn email cảnh báo qua Mailgun ngay khi có sản phẩm giảm giá sốc! Hoàn toàn không cần code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhân viên click từng link web để check giá.
- **Chống gãy code cào (Anti-breaking):** Nhờ tích hợp AI từ ScrapeGraphAI, workflow tự hiểu cấu trúc trang dù đối thủ có đổi giao diện hay chèn banner quảng cáo.
- **Lưu trữ dữ liệu lịch sử:** Mọi biến động giá đều được ghi nhận vào MongoDB phục vụ việc phân tích xu hướng thị trường.
- **Cảnh báo tức thì:** Nhận email báo động ngay lập tức qua Mailgun khi giá giảm đạt ngưỡng kỳ vọng để kịp thời điều chỉnh chiến lược.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đang hoạt động.
- Tài khoản và API Key của **ScrapeGraphAI**.
- Tài khoản **Mailgun** đã cấu hình và xác thực tên miền gửi email.
- Cơ sở dữ liệu **MongoDB** (Atlas hoặc Self-hosted) để lưu log giá sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà vận hành, các sếp cần cấu hình chính xác các node sau:
- **Scrape Product Page (ScrapeGraphAI)**: Thêm ScrapeGraphAI credentials vào mục `Credentials → ScrapeGraphAI API`. Node này dùng prompt tự nhiên để lấy tên sản phẩm, giá, tiền tệ và trạng thái còn hàng.
- **Define Product Sources (Code)**: Mở node này và điền danh sách URL sản phẩm cần theo dõi kèm mức % giảm giá kích hoạt cảnh báo.
- **Store to MongoDB (MongoDB)**: Kết nối tới cụm MongoDB của các sếp và chọn operation là `insert` để lưu trữ dữ liệu thô.
- **Prepare Alert Email (Set) & Send Mailgun Alert (Mailgun)**: Cấu hình tài khoản Mailgun, xác thực tên miền "from" và chỉnh sửa danh sách người nhận email cảnh báo.
- **Incoming Monitor Request (Webhook)**: Lấy URL công khai để kích hoạt workflow từ các công cụ lập lịch (cron job) hoặc ứng dụng bên ngoài.

#### 3. Kích hoạt ⚡️
- Thực hiện một request POST thủ công tới Webhook để test run dữ liệu mẫu.
- Kiểm tra kết quả trả về và dữ liệu được ghi vào MongoDB.
- Bật công tắc **Active** để workflow chạy tự động theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatops:** Thay vì chỉ gửi email qua Mailgun, các sếp có thể nối thêm node **Slack** hoặc **Telegram** để bắn tin nhắn thẳng vào nhóm chiến lược kinh doanh khi có đối thủ hạ giá sốc.
- **Tạo Dashboard trực quan:** Kết nối MongoDB với các công cụ như Metabase hoặc Retool để vẽ biểu đồ lịch sử biến động giá theo thời gian thực.
- **Tự động hóa lịch chạy:** Kết hợp node **Schedule Trigger** trước bước gọi webhook để hệ thống tự động quét giá mỗi ngày 2 lần mà không cần gọi thủ công.

### 📌 Kết luận
Workflow này là giải pháp toàn diện giúp tự động hóa khâu nghiên cứu thị trường và theo dõi giá đối thủ. Hãy triển khai ngay hôm nay để tối ưu hóa năng lực cạnh tranh cho cửa hàng thương mại điện tử của các sếp!