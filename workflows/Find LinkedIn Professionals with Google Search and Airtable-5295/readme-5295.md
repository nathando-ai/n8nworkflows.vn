---
title: "🚀 Tự động tìm kiếm chuyên gia LinkedIn bằng Google Search và Airtable với n8n"
description: "Hướng dẫn xây dựng và cấu hình workflow n8n tự động tìm kiếm profile LinkedIn theo từ khóa, lọc dữ liệu và lưu trữ thông minh vào Airtable không cần code."
slug: "tu-dong-tim-kiem-linkedin-google-search-airtable-n8n"
tags: [n8n, automation, no-code, linkedin, airtable, google-search]
keywords: [n8n workflow, tìm kiếm linkedin tự động, google custom search api, airtable integration, tự động hóa sales, lead generation n8n]
---

# 🚀 Tự động tìm kiếm chuyên gia LinkedIn bằng Google Search và Airtable

Các sếp có đang mệt mỏi vì phải ngồi "cày cuốc" hàng giờ trên LinkedIn để tìm kiếm khách hàng tiềm năng (leads), ứng viên tài năng hay đối tác? Việc copy-paste thủ công từng profile không chỉ tốn thời gian, dễ sai sót mà còn cực kỳ nhàm chán.

Đừng lo, bài toán này sẽ được giải quyết gọn gàng với **workflow n8n tự động hóa 100%**. Workflow này giúp các sếp khai thác sức mạnh của Google Custom Search để quét các profile LinkedIn theo từ khóa mục tiêu, sau đó tự động phân tích và lưu trữ gọn gàng vào Airtable mà không sợ bị trùng lặp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn quá trình tìm kiếm và thu thập dữ liệu profile LinkedIn thay vì làm thủ công.
- **Dữ liệu sạch & thông minh:** Tự động chống trùng lặp (deduplication) nhờ tính năng Upsert của Airtable.
- **Cá nhân hóa mục tiêu:** Dễ dàng thay đổi từ khóa, chức danh, ngành nghề hoặc khu vực để quét đúng đối tượng khách hàng.
- **An toàn, mượt mà:** Tích hợp cơ chế kiểm soát tốc độ (Rate Limit Delay) giúp tránh việc bị Google hay LinkedIn quét và chặn API.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- **Google Custom Search API Key** và **Search Engine ID (CX)** để thực hiện các truy vấn tìm kiếm.
- Tài khoản **Airtable** với một Base và Table được chuẩn bị sẵn các trường (fields) để lưu trữ thông tin.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc (ID: 5295) hoặc copy đoạn JSON tương ứng và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần lưu ý cấu hình kỹ các node sau:
- **⚙️ CUSTOMIZE YOUR SEARCH KEYWORDS HERE** & **Prepare Search Parameters**: Nơi các sếp định nghĩa từ khóa tìm kiếm chính (Ví dụ: *"Marketing Manager SaaS"*, *"Data Scientist Healthcare"*, v.v.). Hãy sửa lại cho đúng tệp khách hàng các sếp đang hướng tới.
- **Google Custom Search API**: Node này yêu cầu cấu hình Credentials loại Header/Query Auth với API Key và Search Engine ID của Google. Hãy đảm bảo quota của Google API đủ dùng nhé.
- **Save to Airtable**: Cần kết nối tài khoản Airtable bằng `airtableTokenApi`. Chọn đúng Base và Table, đồng thời giữ nguyên chế độ **upsert** dựa trên `linkedin_url` để tránh việc lưu trùng một profile nhiều lần.
- **Rate Limit Delay & Loop Over Items**: Quản lý việc phân trang và độ trễ giữa các request, giúp tránh việc gửi quá nhiều request trong thời gian ngắn gây lỗi API.

#### 3. Kích hoạt ⚡️
- Nhấn **"Test workflow"** tại node `When clicking 'Test workflow'` để chạy thử và kiểm tra dữ liệu trả về ở các node trung gian (`Parse LinkedIn Profiles`, `Clean Search Results`).
- Sau khi đã thấy dữ liệu đổ về Airtable chính xác, hãy gạt công tắc sang **Active** để bật workflow chạy tự động theo ý muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node **Slack** hoặc **Telegram** vào sau node `Save to Airtable` để nhận thông báo ngay lập tức về điện thoại mỗi khi hệ thống quét được một lead chất lượng cao.
- **Lên lịch chạy định kỳ (Cron):** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để n8n tự động quét leads mới mỗi ngày hoặc mỗi tuần một lần mà không cần thao tác thủ công.
- **Mở rộng làm giàu dữ liệu (Data Enrichment):** Kết hợp thêm các AI Agent node (như OpenAI/Claude) để tự động phân tích mô tả profile và chấm điểm (Lead Scoring) tiềm năng của từng chuyên gia trước khi lưu vào Airtable.

### 📌 Kết luận
Việc tự động hóa quy trình tìm kiếm khách hàng tiềm năng trên LinkedIn chưa bao giờ dễ dàng đến thế với n8n và Google Custom Search. Hãy triển khai ngay workflow này để tối ưu hóa đội ngũ sales và marketing của doanh nghiệp ngay hôm nay các sếp nhé!