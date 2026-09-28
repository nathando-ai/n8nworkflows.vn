---
title: "🚀 Giám sát giá cạnh tranh & Cảnh báo tự động với Bright Data, Google Sheets & Slack"
description: "Tự động thu thập giá sản phẩm của đối thủ, so sánh, lưu vào Google Sheets và gửi cảnh báo qua Slack/email khi giá giảm, giúp các sếp luôn nắm bắt thị trường."
slug: "giam-sat-gia-canh-tranh-tudong"
tags: [n8n, automation, no-code, market-research, price-monitoring, slack, google-sheets]
keywords: [n8n workflow, tự động hóa, giám sát giá, Bright Data, báo cáo Slack]
---

# 🚀 Giám sát giá cạnh tranh & Cảnh báo tự động với Bright Data, Google Sheets & Slack

Trong môi trường thương mại điện tử ngày càng cạnh tranh, việc **theo dõi giá của đối thủ** một cách thủ công là một công việc tốn thời gian, dễ sai sót và không thể phản hồi kịp thời. Các sếp thường phải mở hàng tá tab, sao chép dữ liệu, tính toán thủ công để quyết định có cần điều chỉnh giá hay không.  

**Workflow này** sẽ giải quyết toàn bộ quy trình: tự động thu thập giá từ các URL đối thủ bằng Bright Data, so sánh với mức giá của bạn, lưu lịch sử vào Google Sheets và **gửi cảnh báo ngay lập tức** qua Slack hoặc email khi phát hiện đối thủ hạ giá vượt ngưỡng đã định. Tất cả diễn ra 100 % không cần viết code, chỉ cần cấu hình một lần và để nó chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn nhập liệu thủ công, workflow tự động chạy hàng ngày.  
- **Độ chính xác cao**: Dữ liệu lấy từ Bright Data luôn cập nhật và chuẩn xác.  
- **Cảnh báo kịp thời**: Slack & email thông báo ngay khi đối thủ giảm giá vượt ngưỡng.  
- **Theo dõi lịch sử**: Tất cả kết quả được ghi lại trong Google Sheets để phân tích xu hướng.  
- **Hoạt động liên tục**: Chạy trên VPS hoặc Docker, không phụ thuộc máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Bright Data** (API Key, Project ID) – dùng cho node **Scrape with Bright Data** và **Fetch Scraped Data**.  
- **Google Sheets**: một bảng tính với sheet tên `PriceLog` (hoặc tùy chỉnh) và quyền chỉnh sửa cho tài khoản service.  
- **Slack**: workspace, channel (ví dụ `#price-alerts`) và **Slack Bot Token** để node **Send Slack Alert** và **Send Daily Report to Slack** hoạt động.  
- **Email SMTP**: thông tin máy chủ, tài khoản, mật khẩu để node **Send Email Alert** gửi mail.  
- **Danh sách URL đối thủ** và **ngưỡng cảnh báo** (phần trăm chênh lệch) – sẽ nhập vào node **Load Competitor URLs**.  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud) và có quyền tạo/đọc credentials trên các dịch vụ trên.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (được cung cấp trong mục **Download** trên trang n8n.io).  
2. Vào n8n → **Workflows** → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import**, workflow sẽ xuất hiện trên canvas với tên *Competitive Price Monitoring & Alerts with Bright Data, Sheets & Slack*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hành động cần cấu hình | Ghi chú |
|------|------------------------|---------|
| **Load Competitor URLs** (Set) | Thêm danh sách URL, tên sản phẩm và ngưỡng % (ví dụ `threshold: 5`). | Dữ liệu này sẽ được truyền cho node **Loop Through Competitors**. |
| **Loop Through Competitors** (Split In Batches) | Đặt **Batch Size** = 1 để xử lý từng URL một. | Đảm bảo không vượt quá giới hạn API Bright Data. |
| **Scrape with Bright Data** (HTTP Request) | Chọn **Credentials → Bright Data API**; nhập **Endpoint**: `https://api.brightdata.com/v1/scrape`; truyền `url` từ batch. | Kiểm tra quota API trước khi chạy. |
| **Wait for Scraping** (Wait) | Đặt thời gian chờ **10 seconds** (hoặc tùy theo thời gian xử lý thực tế). | Có thể tăng nếu scraper cần thời gian dài hơn. |
| **Fetch Scraped Data** (HTTP Request) | Sử dụng **Credentials → Bright Data API**; endpoint lấy kết quả dựa trên `taskId` trả về từ node trước. | Đảm bảo trả về JSON chứa trường `price`. |
| **Parse Price Data** (Code) | Script JavaScript: trích xuất giá, tính % chênh lệch so với giá của bạn (có thể hard‑code hoặc lấy từ sheet). | Kiểm tra console để debug nếu giá không đúng. |
| **Log to Google Sheets** (Google Sheets) | **Operation**: `Append` hoặc `Append Or Update`; chọn **Spreadsheet ID** và **Sheet Name** (`PriceLog`). | Đặt **Key Column** = `URL` để cập nhật nếu đã tồn tại. |
| **Check If Alert Needed** (If) | Điều kiện: `percentageDiff < -threshold` (giá đối thủ thấp hơn ngưỡng). | Tham chiếu biến `threshold` từ node **Load Competitor URLs**. |
| **Send Slack Alert** (Slack) | Chọn **Credentials → Slack Bot**; **Channel** = `#price-alerts`; nội dung tin nhắn sử dụng biến `{{ $json["message"] }}`. | Tùy chỉnh mẫu tin nhắn để hiển thị sản phẩm, giá hiện tại, % chênh lệch. |
| **Send Email Alert** (Email Send) | Cấu hình **SMTP credentials**; **To**, **Subject**, **HTML body** sử dụng dữ liệu JSON. | Dùng khi muốn lưu lịch sử email hoặc thông báo tới nhóm không dùng Slack. |
| **Aggregate All Results** (Aggregate) | Thu thập toàn bộ kết quả từ các batch để tạo báo cáo tổng hợp. | Đặt **Mode** = `Append` và **Field** = `data`. |
| **Create Daily Summary** (Code) | Tính thống kê: giá thấp nhất, cao nhất, trung bình; tạo chuỗi markdown cho báo cáo. | Kiểm tra output `summaryText`. |
| **Send Daily Report to Slack** (Slack) | Gửi `summaryText` tới kênh Slack (có thể dùng channel `#daily-reports`). | Đảm bảo bot có quyền post trong kênh. |
| **Schedule Trigger** (Schedule Trigger) | Đặt lịch chạy **hàng ngày** (ví dụ 02:00 AM) hoặc **hàng giờ** tùy nhu cầu. | Đừng quên bật **Timezone** phù hợp với doanh nghiệp. |

> **Lưu ý:** Sau khi cấu hình xong, nhấn **Execute Workflow** lần đầu để kiểm tra dữ liệu mẫu. Kiểm tra log của các node **Parse Price Data**, **Log to Google Sheets** và **Check If Alert Needed** để chắc chắn mọi giá trị được tính đúng.

#### 3. Kích hoạt ⚡️
- Chạy **Test Run** với một vài URL để xác nhận không lỗi.  
- Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải trên cùng).  
- Kiểm tra Slack và email để xác nhận nhận được cảnh báo và báo cáo hàng ngày.  

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Telegram**: Dùng node **Telegram** để gửi cảnh báo tới nhóm Telegram nếu đội ngũ không dùng Slack.  
- **Lưu log chi tiết**: Kết nối **n8n Execution Log** với một bảng Google Sheets khác để lưu toàn bộ request/response cho mục đích audit.  
- **Dynamic Threshold**: Đưa ngưỡng cảnh báo vào một sheet riêng, cho phép các sếp điều chỉnh mà không cần mở workflow.  
- **Multiple Products**: Mở rộng node **Load Competitor URLs** để chứa nhiều sản phẩm, mỗi sản phẩm có URL và giá gốc riêng, sau đó dùng **Split In Batches** theo sản phẩm.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn lo lắng về việc bỏ lỡ cơ hội giảm giá** của đối thủ. Tự động thu thập, so sánh, lưu trữ và cảnh báo giúp tối ưu chiến lược giá, tăng lợi nhuận và duy trì vị thế cạnh tranh. Hãy **import ngay**, cấu hình các credentials cần thiết và để workflow chạy 24/7 – doanh nghiệp của bạn sẽ luôn “đánh trúng” thời điểm thay đổi giá! 🚀