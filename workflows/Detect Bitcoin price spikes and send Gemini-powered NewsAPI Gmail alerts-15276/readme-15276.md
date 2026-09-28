---
title: "🚀 Tự động phát hiện biến động giá Bitcoin & gửi cảnh báo thông minh qua Gmail với Google Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi giá Bitcoin mỗi 30 phút, phát hiện biến động ±3%, tổng hợp tin tức từ NewsAPI và gửi cảnh báo qua Gmail sử dụng AI."
slug: "tu-dong-phat-hien-bien-dong-gia-bitcoin-gmail-gemini"
tags: [n8n, automation, crypto, ai-summarization, google-gemini, gmail]
keywords: [n8n workflow, theo dõi giá bitcoin, tự động hóa crypto, google gemini n8n, cảnh báo giá bitcoin]
---

# 🚀 Tự động phát hiện biến động giá Bitcoin & gửi cảnh báo thông minh qua Gmail với Google Gemini

Các nhà đầu tư crypto chắc chắn hiểu rằng thị trường không bao giờ ngủ, và việc ngồi canh biểu đồ 24/7 là điều bất khả thi. Những cú "sập nguồn" hay "pump" mạnh mẽ 3% trong chớp mắt có thể diễn ra bất cứ lúc nào. Nếu không nắm bắt kịp thời, các sếp có thể bỏ lỡ cơ hội vàng hoặc không kịp cắt lỗ.

Giải pháp ở đây là gì? Workflow n8n tự động 100% này sẽ thay các sếp "trực gác" thị trường Bitcoin mỗi 30 phút, tự động so sánh giá, tìm kiếm nguyên nhân biến động từ tin tức thực tế (NewsAPI), tổng hợp bằng AI (Google Gemini) và gửi thẳng báo cáo chi tiết vào Gmail của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát tự động 24/7:** Chạy đều đặn mỗi 30 phút mà không cần con người can thiệp.
- **Phát hiện biến động thông minh:** Nhận diện chính xác các cú tăng/giảm giá từ 3% trở lên so với chu kỳ trước.
- **Cung cấp ngữ cảnh (News Context):** Tự động cào tin tức mới nhất về Bitcoin và dùng Google Gemini phân tích lý do tại sao giá biến động.
- **Cảnh báo tức thì:** Nhận email báo cáo chi tiết kèm theo phân tích AI trực tiếp qua Gmail cá nhân.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **Google Gemini API Key:** Dành cho các node AI Agent / Google Gemini Chat Model.
- **NewsAPI Key:** Để fetch tin tức liên quan đến Bitcoin.
- **Gmail Account:** Kết nối OAuth2 để gửi email cảnh báo.
- **Bitcoin Price API:** API nguồn (như CoinGecko) để lấy giá BTC thời gian thực.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON trực tiếp vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây cần được cấu hình chuẩn xác:
- **Execute at every 30 minutes (`scheduleTrigger`):** Thiết lập lịch chạy tự động mặc định là 30 phút/lần.
- **Fetch BitCoin Price (`httpRequest`):** Cấu hình URL endpoint (ví dụ: CoinGecko API) để lấy giá BTC hiện tại.
- **Add bitcoin price to sheet / Get all prices from sheet (`dataTable`):** Cấu hình n8n Data Table để lưu trữ lịch sử giá phục vụ việc so sánh biến động.
- **If new price is increased by 3% & If new price is dropped by 3% (`if`):** Thiết lập điều kiện toán học kiểm tra nếu tỷ lệ thay đổi giá $\ge 3\%$ hoặc $\le -3%$.
- **Fetch news about bitcoin & Fetch news about bitcoin1 (`httpRequest`):** Điền API Key của NewsAPI để cào các bản tin mới nhất.
- **Google Gemini Chat Model / AI Agent (`lmChatGoogleGemini` & `agent`):** Kết nối credentials `googlePalmApi` để AI xử lý, lọc tin tức và viết nội dung cảnh báo.
- **Send a message in Gmail / Send a message in Gmail1 (`gmailTool`):** Kết nối tài khoản Gmail qua OAuth2 để hệ thống tự động gửi email khi có tín hiệu cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công với dữ liệu mẫu để kiểm tra kết nối API, Data Table và Gmail.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack để nhận thông báo tức thời ngay trên điện thoại thay vì chỉ check email.
- **Lưu log giao dịch:** Mở rộng n8n Data Table để lưu lại toàn bộ các lần biến động giá lớn làm dữ liệu backtest chiến lược sau này.
- **Tùy chỉnh ngưỡng %:** Các sếp hoàn toàn có thể hạ ngưỡng cảnh báo xuống 1% hoặc 2% nếu muốn lướt sóng ngắn (scalping) nhạy bén hơn.

### 📌 Kết luận
Workflow này là một "trợ lý ảo" cực kỳ đắc lực cho các trader và nhà đầu tư crypto, giúp tiết kiệm thời gian canh biểu đồ mà không lo bỏ lỡ những con sóng lớn của thị trường. Hãy triển khai ngay trên hệ thống n8n của các sếp nhé!