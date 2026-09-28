---
title: "🚀 Tự động hóa định giá cổ phiếu hàng ngày với GPT-4o, Gemini, FMP, Google Sheets và Telegram"
description: "Xây dựng hệ thống định giá cổ phiếu thông minh chạy tự động mỗi ngày bằng n8n, kết hợp AI đa mô hình, dữ liệu tài chính FMP và cảnh báo qua Telegram."
slug: "tu-dong-hoa-dinh-gia-co-phieu-ai-fmp-telegram"
tags: [n8n, automation, ai-trading, stock-screener, openai, google-gemini, telegram]
keywords: [n8n workflow, định giá cổ phiếu tự động, GPT-4o stock analysis, FMP API n8n, telegram stock alert]
---

# 🚀 Tự động hóa định giá cổ phiếu hàng ngày với GPT-4o, Gemini, FMP, Google Sheets và Telegram

Các nhà đầu tư chứng khoán thường phải đối mặt với một khối lượng dữ liệu khổng lồ: báo cáo tài chính, tin tức thị trường, chỉ số định giá và biến động giá kỹ thuật. Việc phân tích thủ công hàng chục mã cổ phiếu mỗi ngày không chỉ tốn thời gian, dễ bỏ lỡ cơ hội mà còn dễ bị chi phối bởi cảm xúc cá nhân.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), đóng vai trò như một **Hệ thống định giá cổ phiếu tổ chức (Institutional Stock Valuation Engine)** thu nhỏ. Hệ thống tự động sàng lọc cổ phiếu, thu thập dữ liệu tài chính từ FMP, chạy phân tích đồng thuận kép bằng AI (GPT-4o và Gemini), đánh giá rủi ro và gửi tín hiệu MUA/BÁN trực tiếp về Telegram cho các sếp mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn quy trình lọc và định giá:** Quét tới 100 cổ phiếu Mỹ mỗi ngày dựa trên các tiêu chí khắt khe (Market Cap, Volume, Beta...).
- **Góc nhìn đa chiều từ AI kép:** Kết hợp tư duy "Bò" (Bull) của GPT-4o và "Gấu" (Bear) của Google Gemini 2.5 Pro để đưa ra mức giá mục tiêu (Bear, Base, Bull) khách quan nhất.
- **Loại bỏ cảm xúc & Quản trị rủi ro:** Tính toán tự động Piotroski F-Score, Graham Number, quy mô vị thế (Position Sizing) theo quy tắc rủi ro 2%.
- **Cảnh báo tức thì:** Nhận báo cáo tổng hợp và các cơảnh báo STRONG BUY / Thesis Reversal trực tiếp qua Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (khuyên dùng Self-hosted trên VPS).
- **Financial Modeling Prep (FMP) API Key:** Gói Starter trở lên (hỗ trợ endpoint `/stable/` và ≥ 300 gọi API/ngày).
- **OpenAI API Key:** Có quyền truy cập GPT-4o.
- **Google Gemini API Key:** Lấy từ Google AI Studio hoặc Vertex AI.
- **Telegram Bot Token & Chat ID:** Tạo qua `@BotFather`.
- **Google Tài khoản (Google Sheets):** Để lưu trữ nhật ký định giá và backtest tín hiệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **FMP API Key:** Thêm key vào tất cả các HTTP Request nodes dưới dạng query parameter (`apikey = {{ your_key }}`) hoặc Header Auth. Đảm bảo các node trỏ tới endpoint `/stable/` thay vì `/api/v3/` cũ.
- **AI Credentials:** 
  - Cấu hình **OpenAI API Key** trong các node `Tide Breaker - Bull`, `First round ChatGPT`.
  - Cấu hình **Google Gemini API Key** trong các node `Tide Breaker - Bear`, `First round Gemini`.
- **Google Sheets Nodes:** 
  - Tạo một Google Sheet có tên `Stock_Signals` với các cột tiêu đề: `stock | date | current_price | sector | pt_bear | pt_base | pt_bull | verdict | confidence | f_score | verdict_chatgpt | verdict_gemini | rationale | previous_verdict | previous_date`.
  - Dán Sheet ID vào tất cả các node `googleSheets` (`write_sentiment_to_sheets`, `Get Previous Verdict`, `Write_Scan_Opportunities`, `Log_Signal_Outcome`).
- **Telegram Nodes:** Cấu hình Telegram API credentials và gắn Chat ID đích cho các node `Send a text message`, `Telegram Alert`, `Watchlist Telegram`, `Thesis Reversal Alert`.
- **n8n Variables:** Thiết lập biến hệ thống cho quản trị rủi ro:
  - `ACCOUNT_SIZE` (ví dụ: `20000`)
  - `RISK_PER_TRADE_PCT` (ví dụ: `2`)

#### 3. Kích hoạt ⚡️
- Kiểm tra lại các thiết lập ở `Schedule Trigger` (mặc định chạy lúc 7:00 sáng các ngày trong tuần).
- Chạy thử nghiệm thủ công (Test run) để kiểm tra luồng dữ liệu qua các node `Score_and_Prefilter`, `Clean Read Financial`, và AI Consensus.
- Bật công tắc **Active** để hệ thống tự động vận hành hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận thông báo:** Ngoài Telegram, các sếp có thể tích hợp thêm node Slack hoặc Discord để gửi báo cáo định giá cho team đầu tư cùng theo dõi.
- **Tùy chỉnh tiêu chí lọc (Screener):** Thay đổi bộ lọc ngành (`ALLOWED_SECTORS`) hoặc nâng/hạ ngưỡng confidence threshold tại node `Alert Filter` cho phù hợp với khẩu vị rủi ro cá nhân.
- **Theo dõi hiệu suất dài hạn:** Tận dụng workflow phụ `Signal Outcome Checker` để hệ thống tự động review lại các tín hiệu sau 30, 60, 90 ngày nhằm tối ưu hóa mô hình.

### 📌 Kết luận
Với hệ thống tự động hóa định giá cổ phiếu tích hợp AI này, các sếp đã sở hữu một trợ lý tài chính thông minh hoạt động 24/7, giúp tiết kiệm hàng giờ nghiên cứu thủ công và đưa ra các quyết định đầu tư dựa trên dữ liệu cứng cáp. Hãy triển khai ngay hôm nay để tối ưu hóa danh mục đầu tư của các sếp!