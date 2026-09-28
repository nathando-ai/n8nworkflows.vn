---
title: "🚀 Tự động hóa ý tưởng đầu tư hàng ngày với Yahoo Finance và Google Gemini trong n8n"
description: "Xây dựng pipeline tự động hoàn toàn quét danh sách theo dõi tài sản, lấy dữ liệu giá & tin tức từ Yahoo Finance và dùng AI Gemini để chắt lọc cơ hội đầu tư chất lượng."
slug: "tu-dong-hoa-y-tuong-dau-tu-yahoo-finance-gemini-n8n"
tags: [n8n, automation, ai-summarization, crypto-trading, google-gemini, yahoo-finance]
keywords: [n8n workflow, ý tưởng đầu tư tự động, yahoo finance api, google gemini ai agent, n8n data table]
---

# 🚀 Tự động hóa ý tưởng đầu tư hàng ngày với Yahoo Finance & Google Gemini

Việc theo dõi thị trường tài chính, đọc tin tức, kiểm tra giá và phân tích dữ liệu thủ công mỗi ngày để tìm kiếm cơ hội đầu tư (cổ phiếu hoặc crypto) ngốn rất nhiều thời gian và dễ bỏ lỡ thời điểm vàng. Bài toán này hoàn toàn có thể được giải quyết triệt để bằng một pipeline tự động hóa không cần code (No-code automation) sử dụng n8n, kết hợp sức mạnh dữ liệu của Yahoo Finance và khả năng phân tích siêu việt của Google Gemini AI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Quét toàn bộ danh sách mã theo dõi (watchlist) và tạo báo cáo đầu tư mà không cần đụng tay.
- **Dữ liệu thời gian thực:** Lấy giá live và tin tức mới nhất trực tiếp từ Yahoo Finance API.
- **AI thông minh:** Google Gemini phân tích tâm lý thị trường, các sự kiện xúc tác (catalysts) để chọn ra 2-3 ý tưởng đầu tư có độ tin cậy cao nhất.
- **Lưu trữ khoa học:** Tự động định dạng và lưu kết quả vào n8n Data Table để dễ dàng xem lại bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản/API Key của **Google Gemini API** (Google Palm API).
- Kết nối mạng ổn định để n8n có thể gọi tới các endpoint công khai của Yahoo Finance (`query1.finance.yahoo.com` và `query2.finance.yahoo.com` - không yêu cầu API Key riêng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow (Mã workflow gốc: `15066` được phát triển bởi WeblineIndia) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:
- **Node `Google Gemini Chat Model`**: Cần chọn đúng Credentials là **Google Palm API** và điền API Key cá nhân của các sếp vào.
- **Node `Get Tickers from Watchlist` (Data Table)**: 
  - Tạo một n8n Data Table tên là `PT-HarshalS_Coins-WatchList` với các cột gồm `Ticker` và `Status` (được set giá trị là `"Active"` cho các mã muốn theo dõi).
- **Node `DB-Table Daily Ideas` (Data Table)**:
  - Tạo bảng thứ hai tên là `Crypto_Daily_Ideas` với cấu trúc cột gồm: `Ticker`, `Idea_Title`, `Catalyst_Summary` và `Conviction_Level`.
- **Node `Get Price` & `Get News` (HTTP Request)**: Kiểm tra các endpoint gọi tới Yahoo Finance để đảm bảo request trả về dữ liệu chuẩn xác theo cấu trúc mã ticker trong Data Table của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node `Start` (Manual Trigger) để chạy thử nghiệm lần đầu và kiểm tra luồng dữ liệu qua từng bước (`Split In Batches` -> `HTTP Request` -> `AI Agent`).
- Sau khi kiểm tra kết quả hiển thị chính xác trong Data Table, hãy gạt công tắc sang **Active** để hệ thống tự động chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thay vì chỉ lưu vào Data Table, các sếp có thể gắn thêm node Telegram hoặc Slack ở cuối workflow để bắn tin nhắn báo cáo ý tưởng đầu tư nóng hổi thẳng vào điện thoại mỗi sáng.
- **Mở rộng nguồn dữ liệu:** Kết hợp thêm các API tin tức khác như CoinMarketCap hoặc NewsAPI để AI có cái nhìn đa chiều hơn.
- **Lịch chạy tự động:** Thay thế node `Start` (Manual Trigger) bằng `Schedule Trigger` để hệ thống tự động quét thị trường vào 8:00 sáng mỗi ngày.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho bất kỳ nhà đầu tư crypto hay chứng khoán nào muốn ứng dụng AI vào quy trình phân tích hàng ngày. Hãy cài đặt ngay lên VPS của các sếp để tối ưu hóa thời gian và bắt trọn những cơ hội đầu tư tiềm năng nhất!