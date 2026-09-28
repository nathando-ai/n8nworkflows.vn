---
title: "🚀 Tự động cảnh báo giảm giá phòng khách sạn qua email & lưu trữ DB"
description: "Giải pháp n8n kiểm tra giá phòng khách sạn mỗi 6 giờ, phát hiện giảm giá, gửi email ngay cho đại lý du lịch và cập nhật lịch sử giá trong cơ sở dữ liệu."
slug: "tudong-canh-bao-giam-gia-phong-khach-san-email-db"
tags: [n8n, automation, no-code, hotel, price-monitoring, email-notifications, database]
keywords: [n8n workflow, tự động hóa, giảm giá khách sạn, email alert, tracking price, API price check]
---

# 🚀 Tự động cảnh báo giảm giá phòng khách sạn qua email & lưu trữ DB

Doanh nghiệp du lịch thường phải **kiểm tra giá phòng** của hàng chục, hàng trăm khách sạn mỗi ngày. Công việc này tốn thời gian, dễ bỏ sót và khi giá giảm thì **cơ hội bán hàng bị mất**.  
Workflow **“Automated Hotel Price Drop Alerts”** giải quyết hoàn toàn vấn đề: tự động lấy giá hiện tại từ API, so sánh với giá đã lưu, gửi email cảnh báo ngay khi có giảm giá và đồng thời cập nhật giá mới vào cơ sở dữ liệu – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Kiểm tra giá tự động mỗi 6 giờ, không cần nhân viên thủ công.  
- **Phát hiện nhanh**: Email cảnh báo ngay khi giá giảm, nắm bắt cơ hội bán ngay lập tức.  
- **Độ chính xác 100 %**: So sánh giá hiện tại với dữ liệu lịch sử trong DB, tránh lỗi nhập liệu.  
- **Lưu trữ lịch sử**: Mỗi lần cập nhật giá đều được ghi lại, hỗ trợ phân tích xu hướng.  
- **Hoạt động liên tục 24/7**: Không ngừng chạy trên VPS, không bị gián đoạn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản SMTP** (Gmail, SendGrid, hoặc máy chủ SMTP nội bộ) để gửi email.  
- **API endpoint** của nhà cung cấp giá phòng (URL, API key nếu có).  
- **Database endpoint** (REST API hoặc webhook) để **GET/POST** dữ liệu giá cũ và cập nhật giá mới.  
- **Danh sách khách sạn** (JSON hoặc mảng trong node “Load Hotel List”).  
- **Địa chỉ email đại lý du lịch** nhận cảnh báo.  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Nhấn **“Import” → “From File”** và chọn file JSON của workflow (hoặc **Copy/Paste** JSON vào ô nhập).  
3. Xác nhận để workflow xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là **cấu hình chi tiết** cho từng node quan trọng. Đặt **tên node** đúng như trong workflow để tránh lỗi.

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Schedule - Every 6 Hours** | `scheduleTrigger` | - **Cron**: `0 */6 * * *` (mỗi 6 giờ). <br> - Đánh dấu **Active**. |
| **Load Hotel List** | `code` | - Thay đoạn `const hotels = [...]` bằng danh sách thực tế (ID, tên, API endpoint, phòng). <br> - Đảm bảo trả về **array** JSON. |
| **Fetch Current Price from API** | `httpRequest` | - **Method**: `GET`. <br> - **URL**: `{{ $json["apiUrl"] }}` (sử dụng biến từ node trước). <br> - Thêm **Header** `Authorization: Bearer <API_KEY>` nếu cần. |
| **Parse Price Data** | `code` | - Viết logic **extract price** và **availability** từ response. <br> - Đảm bảo output: `{ "hotelId": ..., "price": ..., "available": true }`. |
| **Get Previous Price from DB** | `httpRequest` | - **Method**: `GET`. <br> - **URL**: `https://your-db.com/prices/{{ $json["hotelId"] }}`. <br> - Cấu hình **Authentication** (API Key hoặc Basic). |
| **Compare Prices** | `code` | - Tính **priceDiff** và **percentDiff**. <br> - Output: `{ "priceDiff": ..., "percentDiff": ..., "isReduced": priceDiff > 0 }`. |
| **Check if Price Reduced** | `if` | - **Condition**: `{{$json["isReduced"]}} === true`. <br> - Nhánh **True** → “Format Alert Email”. <br> - Nhánh **False** → “Log No Alert Needed”. |
| **Format Alert Email** | `code` | - Tạo **HTML** email: tên khách sạn, phòng, giá cũ (gạch ngang), giá mới (highlight), % tiết kiệm, link đặt phòng. <br> - Output: `{ "subject": "...", "html": "..." }`. |
| **Send Email to Travel Agent** | `emailSend` | - Chọn **Credentials**: `smtp`. <br> - **To**: địa chỉ email đại lý (có thể dùng biến). <br> - **Subject** & **HTML** lấy từ node trước. |
| **Log Alert Sent** | `code` | - Ghi log thành công (ví dụ: `console.log("Alert sent for", $json.hotelId)`). |
| **Log No Alert Needed** | `code` | - Ghi log khi không có giảm giá (ví dụ: `console.log("No price drop for", $json.hotelId)`). |
| **Merge All Logs** | `merge` | - **Mode**: `Append`. <br> - Kết hợp output của “Log Alert Sent” và “Log No Alert Needed”. |
| **Update Price in Database** | `httpRequest` | - **Method**: `POST` hoặc `PUT`. <br> - **URL**: `https://your-db.com/prices/{{ $json["hotelId"] }}`. <br> - **Body**: `{ "price": {{ $json["price"] }}, "timestamp": "{{ $now }}" }`. |
| **Create Execution Summary** | `code` | - Tổng hợp số lượng khách sạn kiểm tra, số cảnh báo gửi, thời gian chạy. <br> - Output: `{ "summary": "..."} ` (có thể gửi Slack/Telegram nếu muốn). |

> **Lưu ý:**  
> - Đảm bảo **Credentials** (SMTP, API, DB) đã được tạo trong **n8n → Credentials** và được gán cho các node tương ứng.  
> - Kiểm tra **định dạng JSON** đầu ra của mỗi node bằng **“Execute Node”** trước khi kết nối tiếp.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, **Run Workflow** một lần với **“Execute Workflow”** để kiểm tra dữ liệu mẫu.  
2. Nếu không có lỗi, bật **“Active”** trên node **Schedule - Every 6 Hours**.  
3. Kiểm tra hộp thư của đại lý để xác nhận email cảnh báo đã tới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: dùng node `Slack` hoặc `Telegram` để gửi thông báo nhanh cho đội ngũ bán hàng.  
- **Lưu log vào Google Sheets**: thay node “Log Alert Sent” bằng `Google Sheets` để có bảng theo dõi trực quan.  
- **Báo cáo định kỳ**: tạo một workflow phụ chạy hàng ngày, lấy dữ liệu từ DB và gửi báo cáo tổng hợp qua email.  
- **Đánh dấu “Urgent”**: nếu % giảm > 20 % thì thêm nhãn **URGENT** trong tiêu đề email.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn lo lắng về việc bỏ lỡ giảm giá** nữa – mọi thay đổi giá phòng được phát hiện, thông báo và lưu trữ tự động, giúp tăng doanh thu và tối ưu quy trình bán hàng. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc thay bạn! 🚀