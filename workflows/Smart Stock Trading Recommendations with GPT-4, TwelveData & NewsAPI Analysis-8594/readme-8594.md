---
title: "🚀 Tự động hóa phân tích cổ phiếu với GPT-4, TwelveData & NewsAPI - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động hóa phân tích cổ phiếu, theo dõi xu hướng thị trường và nhận gợi ý giao dịch thông minh bằng công nghệ AI"
slug: "tu-dong-hoa-phan-tich-co-phieu-voi-gpt4-twelvedata-newsapi"
tags: [n8n, automation, no-code, crypto trading, ai summarization, multimodal ai]
keywords: [n8n workflow, tự động hóa cổ phiếu, phân tích thị trường, AI trading, GPT-4, TwelveData, NewsAPI]
---

# 🚀 Tự động hóa phân tích cổ phiếu với GPT-4, TwelveData & NewsAPI - Workflow n8n hoàn chỉnh

[Các sếp] đang gặp khó khăn khi phải theo dõi hàng chục cổ phiếu, phân tích xu hướng thị trường và tìm kiếm thông tin tin tức liên quan? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này chỉ trong vài phút, với kết quả chính xác và cá nhân hóa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập dữ liệu thị trường và tin tức trong vài giây
- **Phân tích thông minh**: Sử dụng công nghệ AI GPT-4 để đánh giá xu hướng và cảm xúc thị trường
- **Gợi ý giao dịch**: Nhận báo cáo chi tiết về cơ hội mua/bán cổ phiếu
- **Hoạt động liên tục**: Workflow chạy tự động 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI (để sử dụng GPT-4)
- API Key từ [TwelveData](https://twelvedata.com/) (miễn phí)
- API Key từ [NewsAPI](https://newsapi.org/) (miễn phí)
- API Key từ [Chart-Img](http://chart-img.com/) (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8594](https://n8n.io/workflows/8594)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When chat message received"**:
   - Cấu hình webhook để nhận tin nhắn từ ứng dụng chat (Slack, Telegram, Discord...)

2. **Node "4h trend", "1day trend", "1week trend"**:
   - Thêm credentials "httpQueryAuth" với API Key từ TwelveData
   - Thay đổi tham số "symbol" trong URL request để theo dõi cổ phiếu mong muốn

3. **Node "Get News"**:
   - Thêm credentials "httpQueryAuth" với API Key từ NewsAPI
   - Cấu hình tham số tìm kiếm tin tức (q, sources, domains...)

4. **Node "News Sentiment Analyzer"**:
   - Thêm credentials "openAiApi" với API Key OpenAI
   - Tùy chỉnh prompt để phân tích cảm xúc tin tức theo nhu cầu

5. **Node "OpenAI Chat Model"**:
   - Thêm credentials "openAiApi" với API Key OpenAI
   - Đảm bảo chọn model "gpt-4o" để có kết quả tốt nhất

6. **Node "Get Stock Sentiment"**:
   - Thêm credentials "perplexityApi"
   - Model đã được cấu hình sẵn là "sonar"

7. **Node "Get Chart Image for Stock"**:
   - Thêm credentials "httpHeaderAuth" với API Key từ Chart-Img
   - Tùy chọn: Có thể xóa node này nếu không cần biểu đồ

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả ở các node cuối cùng ("Respond to Chat")
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi báo cáo tự động vào kênh chat
2. **Lưu log giao dịch**: Thêm node để lưu lịch sử giao dịch vào Google Sheets
3. **Cảnh báo thị trường**: Thiết lập ngưỡng cảnh báo khi thị trường có biến động lớn
4. **Phân tích nhiều cổ phiếu**: Sử dụng vòng lặp để theo dõi nhiều cổ phiếu cùng lúc

### 📌 Kết luận
Workflow này đã biến quá trình phân tích thị trường từ công việc thủ công mất nhiều giờ thành một quy trình tự động chỉ trong vài phút. Các sếp có thể tập trung vào chiến lược giao dịch thay vì mất thời gian thu thập dữ liệu. Hãy thử ngay và nâng cấp chiến lược giao dịch của các sếp!