---
title: "🚀 Tự động hóa phân tích cổ phiếu & cảnh báo MUA-GIỮ-BÁN chuẩn tổ chức với ChatGPT & Gemini"
description: "Xây dựng hệ thống định giá cổ phiếu thông minh, phân tích dữ liệu tài chính từ Alpha Vantage, tin tức Seeking Alpha và đối chiếu đa mô hình AI để đưa ra quyết định đầu tư khách quan."
slug: "tu-dong-hoa-phan-tich-co-phieu-chatgpt-gemini"
tags: [n8n, ai-automation, stock-analysis, chatgpt, gemini, google-sheets]
keywords: [n8n workflow, tự động hóa chứng khoán, phân tích cổ phiếu AI, Alpha Vantage n8n, ChatGPT Gemini trading bot]
---

# 🚀 Tự động hóa phân tích cổ phiếu & cảnh báo MUA-GIỮ-BÁN chuẩn tổ chức với ChatGPT & Gemini

Việc theo dõi thị trường tài chính, đọc báo cáo tài chính, tổng hợp tin tức từ Seeking Alpha và đưa ra quyết định Mua/Bán (BUY/HOLD/SELL) thủ công thường ngốn rất nhiều thời gian, dễ bị cảm xúc chi phối và bỏ lỡ các cơ hội vàng. 

Workflow n8n "khủng" với 79 nodes này sinh ra để giải quyết triệt để nỗi đau đó. Hệ thống tự động hóa toàn bộ quy trình: thu thập dữ liệu tài chính doanh nghiệp, phân tích tin tức, đối chiếu đa mô hình AI (ChatGPT & Gemini) để đưa ra mức giá mục tiêu (price target), tín hiệu kỹ thuật (MA, RSI) và bắn cảnh báo trực tiếp về Telegram cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ gọi API tài chính và AI nặng mà không bị treo, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Mô hình định giá chuẩn tổ chức:** Tự động tính toán FCF, biên lợi nhuận, nợ vay, tăng trưởng doanh thu từ Alpha Vantage.
- **AI Đa chiều (ChatGPT + Gemini):** Giảm thiểu ảo giác (hallucination) của AI bằng cơ chế phân tích chéo và giải quyết tranh chấp (Tiebreaker).
- **Tự động hóa hoàn toàn:** Chạy định kỳ, lưu trữ lịch sử vào Google Sheets và bắn tín hiệu qua Telegram (Cảnh báo Mua/Bán, Đảo chiều xu hướng Thesis Reversal).
- **Loại bỏ cảm xúc:** Quyết định dựa trên dữ liệu định lượng và logic đầu tư cấu trúc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Google Sheets API Credentials** (Để đọc danh sách mã cổ phiếu và lưu kết quả).
- **Alpha Vantage API Key** (Lấy dữ liệu tài chính, báo cáo kết quả kinh doanh, giá cổ phiếu, chỉ báo kỹ thuật).
- **OpenAI API Key** (ChatGPT cho phân tích AI vòng 1 và Tiebreaker).
- **Google Gemini API Key** (Gemini cho phân tích AI vòng 1 và Tiebreaker).
- **Telegram Bot Token & Chat ID** (Để nhận tin nhắn cảnh báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **Add workflow** -> Nhấn `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ 79 nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Do workflow có quy mô lớn, các sếp cần chú ý cấu hình các điểm sau:
- **Node `Read_tickers_from_Sheet` & `write_sentiment_to_sheets`**: Kết nối với tài khoản Google Sheets của các sếp, trỏ đúng vào file Google Sheet quản lý danh mục (ví dụ sheet "Stock Sentiment").
- **Các node gọi API Alpha Vantage (`alphavantage - Balance Sheet`, `Profile`, `Income Statement`, `CashFlow`, `Current Price`, v.v.)**: Điền API Key của Alpha Vantage vào phần Header hoặc Credentials tùy theo thiết lập của node HTTP Request.
- **Node `First round ChatGPT` & `Tide Breaker - Bull`**: Chọn OpenAI Credentials chính chủ của các sếp (hỗ trợ GPT-4o để phân tích tài chính chuẩn xác).
- **Node `First round Gemini` & `Tide Breaker - Bear`**: Chọn Google Gemini Credentials.
- **Node `Send a text message` & `Telegram Alert` / `Watchlist Telegram`**: Kết nối với Telegram Bot Credentials và điền Chat ID nhận thông báo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với 1 mã cổ phiếu trong Google Sheets để kiểm tra luồng dữ liệu từ Alpha Vantage -> AI -> Google Sheets -> Telegram.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để hệ thống tự động chạy theo lịch định sẵn (Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng cơ chế Prediction Accuracy Tracker (Ý tưởng số 7):** Tạo thêm một workflow chạy hàng tháng để so sánh giá dự đoán sau 30 ngày với giá thực tế trên thị trường, tự động tính tỷ lệ chính xác (Win-rate) của ChatGPT và Gemini, biến hệ thống thành một cỗ máy học hỏi thực thụ.
- **Tích hợp thêm Slack/Discord:** Ngoài Telegram, có thể nhân bản nhánh thông báo sang kênh Discord hoặc Slack của nhóm đầu tư.
- **Tối ưu hóa tần suất:** Do Alpha Vantage có giới hạn gọi API bản miễn phí, hãy điều chỉnh `Schedule Trigger` chạy 3 ngày/lần hoặc nâng cấp gói API nếu theo dõi số lượng lớn cổ phiếu.

### 📌 Kết luận
Workflow này không chỉ là một kịch bản n8n đơn thuần mà là một hệ thống ra quyết định đầu tư tự động mang phong cách quỹ đầu tư chuyên nghiệp. Hãy cài đặt ngay để nâng tầm chiến lược giao dịch chứng khoán của các sếp lên một đẳng cấp mới!