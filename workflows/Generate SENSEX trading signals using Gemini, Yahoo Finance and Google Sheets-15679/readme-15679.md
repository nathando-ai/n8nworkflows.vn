---
title: "🚀 Tự động hóa tạo tín hiệu giao dịch SENSEX với Gemini AI, Yahoo Finance và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n kết hợp phân tích kỹ thuật và tin tức vĩ mô bằng Gemini AI để tự động tạo, chấm điểm và lưu trữ tín hiệu giao dịch chứng khoán."
slug: "tu-dong-hoa-tin-hieu-giao-dich-sensex-gemini-ai"
tags: [n8n, automation, ai-agent, google-sheets, trading-signals, gemini]
keywords: [n8n workflow, tín hiệu giao dịch, SENSEX, Gemini AI, Yahoo Finance, tự động hóa chứng khoán]
keywords: [n8n workflow, tín hiệu giao dịch, SENSEX, Gemini AI, Yahoo Finance, tự động hóa chứng khoán]
---

# 🚀 Tự động hóa tạo tín hiệu giao dịch SENSEX với Gemini AI, Yahoo Finance và Google Sheets

Việc theo dõi thị trường chứng khoán thủ công, tính toán các chỉ báo kỹ thuật (MA, Momentum, Volatility) kết hợp đọc tin tức vĩ mô tốn rất nhiều thời gian và dễ bỏ lỡ cơ hội vàng. Các sếp có đang gặp khó khăn trong việc tổng hợp dữ liệu thị trường để đưa ra quyết định mua/bán chính xác? 

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách ứng dụng mô hình lai (Hybrid Approach): Kết hợp dữ liệu lịch sử từ Yahoo Finance, tin tức mới nhất từ Google News RSS và phân tích siêu việt từ **Google Gemini AI** để tự động tạo, kiểm duyệt và lưu trữ tín hiệu giao dịch SENSEX trực tiếp vào Google Sheets hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân tích toàn diện**: Kết hợp giữa chỉ báo kỹ thuật (Technical) và cảm tính tin tức (Fundamental News Sentiment).
- **Chấm điểm thông minh**: Hệ thống tự động tính điểm tín hiệu dựa trên độ tin cậy, sức mạnh xu hướng và mức độ rủi ro.
- **Lọc tín hiệu nhiễu**: Tự động loại bỏ các tín hiệu "Hold" hoặc có điểm số thấp (<70), chỉ giữ lại các cơ hội hành động cao.
- **Lưu trữ tự động**: Mọi tín hiệu chất lượng đều được ghi nhận trực tiếp vào Google Sheets theo thời gian thực để tracking và backtest.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Google Gemini API Key**: Tài khoản Google AI Studio để cấp quyền cho node LLM.
- **Google Sheets Credentials**: Tài khoản Google có quyền truy cập Google Sheets thông qua OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON từ nguồn cung cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào menu 3 chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thành phần sau để workflow vận hành mượt mà:
- **Google Gemini Chat Model**: Kết nối credentials `googlePalmApi` bằng API Key từ Google AI Studio.
- **Log into sheet (Google Sheets)**: Chọn credentials `googleSheetsOAuth2Api`. Chuẩn bị sẵn một Google Sheet với các cột tiêu đề: `Date | Index | Signal | Confidence | Trend | Reason`. Điền Spreadsheet ID và Sheet Name vào node này.
- **Fetching INDEX data (HTTP Request) & News Fetching (RSS)**: Kiểm tra lại URL của Yahoo Finance API và Google News RSS để đảm bảo dữ liệu trả về đúng định dạng mong đợi.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `Start` (Manual Trigger) để chạy thử nghiệm thủ công lần đầu.
- Kiểm tra dữ liệu trả về ở các node `Code to gain insights`, `AI Agent` và dòng dữ liệu được thêm vào `Log into sheet`.
- Khi mọi thứ chạy trơn tru, hãy chuyển trạng thái workflow sang **Active** để hệ thống chạy tự động theo lịch trình (Cron) hoặc kích hoạt thủ công khi cần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ngay sau node `Validating signal` để nhận cảnh báo ngay lập tức trên điện thoại khi có tín hiệu "Buy" hoặc "Sell" chất lượng cao.
- **Mở rộng danh mục**: Nhân bản các node xử lý để theo dõi thêm các chỉ số khác như NIFTY 50, S&P 500, hoặc VN-Index.
- **Lưu lịch sử chạy**: Sử dụng thêm node Google Sheets ở nhánh phụ để ghi log toàn bộ lịch sử phân tích (kể cả các lệnh bị loại bỏ) phục vụ việc tối ưu thuật toán chấm điểm sau này.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo giúp các nhà đầu tư tiết kiệm hàng giờ nghiên cứu thị trường mỗi ngày. Hãy import ngay vào hệ thống n8n của các sếp và bắt đầu tối ưu hóa quy trình giao dịch chứng khoán của mình ngay hôm nay!