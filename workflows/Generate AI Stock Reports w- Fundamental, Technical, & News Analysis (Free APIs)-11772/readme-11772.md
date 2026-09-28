---
title: "🚀 Tự động hóa phân tích cổ phiếu toàn diện với AI Agent và n8n (Fundamental, Technical & News)"
description: "Xây dựng hệ thống đa tác nhân (Multi-agent) tự động phân tích cổ phiếu chuyên sâu từ cơ bản, kỹ thuật đến tin tức, gửi báo cáo trực quan qua email hoàn toàn miễn phí."
slug: "tu-dong-hoa-phan-tich-co-phiieu-voi-ai-agent-n8n"
tags: [n8n, automation, ai-agent, crypto-trading, stock-analysis, finance]
keywords: [n8n workflow, phân tích cổ phiếu tự động, AI stock report, alpha vantage api, technical analysis n8n]
---

# 🚀 Tự động hóa phân tích cổ phiếu toàn diện với AI Agent và n8n

Việc phân tích thị trường chứng khoán thủ công đòi hỏi nhà đầu tư phải tổng hợp dữ liệu từ vô số nguồn: báo cáo tài chính (Fundamental), biểu đồ kỹ thuật (Technical), và tin tức thị trường (News Sentiment). Quá trình này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ lỡ các cơ hội giao dịch quan trọng.

Workflow n8n nâng cao này sẽ giải quyết triệt để vấn đề đó. Bằng cách ứng dụng hệ thống Multi-Agent (Đa tác nhân) kết hợp các mô hình AI mạnh mẽ (Gemini, OpenAI/OpenRouter), hệ thống tự động cào dữ liệu, phân tích chuyên sâu và gửi báo cáo HTML cực kỳ chuyên nghiệp thẳng vào hộp thư của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ AI phức tạp mà không lo bị ngắt kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chạy định kỳ hàng tuần danh sách cổ phiếu quan tâm hoặc kích hoạt thủ công qua Form bất cứ lúc nào.
- **Phân tích đa chiều:** Tổng hợp dữ liệu từ Báo cáo tài chính (Alpha Vantage), Chỉ báo kỹ thuật & Biểu đồ (Twelve Data, Chart-Img), và Tâm lý tin tức thị trường.
- **Báo cáo chuyên nghiệp:** AI tổng hợp thông tin, đưa ra nhận định (Mua/Giữ/Bán) và dựng sẵn báo cáo dạng HTML trực quan, gửi trực tiếp qua Email.
- **Hoàn toàn miễn phí API:** Sử dụng các API miễn phí thông dụng, tiết kiệm tối đa chi phí vận hành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance:** Đã bật tính năng AI Nodes (LangChain).
- **AI Credentials:** Google Gemini API Key, OpenAI / OpenRouter API Key.
- **Financial APIs (Miễn phí):** Alpha Vantage API Key, Twelve Data API Key, Chart-Img API Key.
- **Dịch vụ thông báo:** Tài khoản SMTP (để gửi email báo cáo) và tùy chọn Alpaca (nếu muốn auto trade).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Do đây là một hệ thống Multi-Agent lớn (gồm 58 nodes), workflow trên canvas được chia thành 5 module chính tương ứng với 5 sub-workflows. Các sếp hãy tách và tạo thành 5 workflows riêng biệt trên n8n của mình như sau:
1. **Main AI Agent Orchestrator:** Nhận trigger (Schedule hoặc Form) và điều phối các tool.
2. **Technical Analysis Sub-workflow:** Lấy dữ liệu TA (MACD, Bollinger Bands) và phân tích ảnh biểu đồ.
3. **Fundamental Analysis Sub-workflow:** Kéo báo cáo tài chính từ Alpha Vantage.
4. **Trends Analysis Sub-workflow:** Phân tích tin tức và đo lường tâm lý thị trường.
5. **Execution & Delivery:** Tổng hợp dữ liệu, dựng HTML và gửi Email.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Google Gemini Chat Model` / `ChatGPT 4o`:** Điền API Keys tương ứng cho nhà cung cấp AI.
- **Các node `Get Company Overview`, `Get Income Statement`, `Get News Data`:** Nhập Alpha Vantage API Key của các sếp vào phần Header hoặc Query Parameters.
- **Node `Get Chart URL`, `Get Price History`, `Get Bollinger Bands`:** Cấu hình Twelve Data và Chart-Img API Keys.
- **Node `Send Stock Analysis` (SMTP):** Điền thông tin SMTP của email cá nhân/doanh nghiệp để hệ thống gửi báo cáo.
- **Liên kết Sub-workflows:** Đảm bảo các node `Technical Analysis Tool`, `Fundamental Analysis Tool`, và `Trends Analysis Tool` (kiểu `toolWorkflow`) trỏ chính xác đến ID của các sub-workflows con đã tách ở bước 1.

#### 3. Kích hoạt ⚡️
- Sử dụng node `On form submission` để test nhanh với 1 mã cổ phiếu (ví dụ: AAPL, TSLA, NVDA).
- Kiểm tra kết quả trả về qua email.
- Bật **Active** cho toàn bộ 5 workflows để chạy tự động theo lịch (`Schedule Trigger`).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì chỉ gửi qua Email, các sếp có thể gắn thêm node Telegram Bot để nhận nhanh cảnh báo mua/bán ngay trên điện thoại.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets hoặc Supabase để lưu lại toàn bộ lịch sử phân tích, tiện theo dõi biến động theo thời gian.
- **Auto Trading:** Kết hợp node `Buy in Alpaca` để tự động hóa lệnh mua khi AI đưa ra khuyến nghị "Buy" với độ tin cậy cao.

### 📌 Kết luận
Workflow phân tích cổ phiếu tích hợp AI này là trợ thủ đắc lực cho bất kỳ nhà đầu tư nào muốn tiết kiệm thời gian nghiên cứu mà vẫn sở hữu góc nhìn đa chiều, chuyên nghiệp. Hãy cài đặt ngay lên VPS của các sếp để tối ưu hóa chiến lược đầu tư ngay hôm nay!