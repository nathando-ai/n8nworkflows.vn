---
title: "🚀 Tự động định giá cổ phiếu & tạo tín hiệu MUA - BÁN với GPT-5, Gemini và Alpha Vantage"
description: "Xây dựng hệ thống phân tích tài chính và định giá cổ phiếu tự động 100% bằng n8n, kết hợp Alpha Vantage, Google Gemini, OpenAI và Google Sheets."
slug: "tu-dong-dinh-gia-co-phieu-va-tao-tin-hieu-mua-ban-voi-ai"
tags: [n8n, automation, ai-summarization, stock-trading, google-sheets, openai, gemini]
keywords: [n8n workflow, tự động hóa chứng khoán, định giá cổ phiếu AI, Alpha Vantage n8n, OpenAI Gemini stock analysis]
---

# 🚀 Tự động định giá cổ phiếu & tạo tín hiệu MUA - BÁN chuẩn tổ chức với AI

Các nhà đầu tư cá nhân thường tốn hàng giờ đồng hồ mỗi ngày để tổng hợp báo cáo tài chính, đọc tin tức thị trường từ Seeking Alpha, tính toán các chỉ số và đưa ra quyết định mua bán bị chi phối bởi cảm xúc. Quá trình thủ công này vừa chậm chạp lại vừa dễ bỏ lỡ cơ hội.

Workflow n8n mạnh mẽ này sẽ thay thế hoàn toàn công việc đó! Hệ thống tự động thu thập dữ liệu tài chính từ **Alpha Vantage**, quét tin tức mới nhất từ **Seeking Alpha**, sử dụng sức mạnh phân tích của các mô hình AI hàng đầu (**OpenAI GPT** và **Google Gemini**) để đánh giá tâm lý thị trường, tính toán mục tiêu giá, đưa ra tín hiệu **BUY - HOLD - SELL** và ghi nhận kết quả trực tiếp vào **Google Sheets**, đồng thời gửi thông báo qua **Telegram**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ để cập nhật danh mục đầu tư mà không cần can thiệp thủ công.
- **Loại bỏ cảm xúc:** Ra quyết định dựa trên dữ liệu tài chính chuẩn xác (Balance Sheet, Income Statement, Cash Flow) và phân tích tâm lý AI.
- **Tối ưu chi phí API:** Tích hợp cơ chế Cache thông minh trên Google Sheets giúp kiểm tra dữ liệu cũ, tránh gọi API Alpha Vantage trùng lặp.
- **Cảnh báo tức thì:** Nhận ngay báo cáo chi tiết và tín hiệu giao dịch qua Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Google Cloud & Google Sheets** (Để lưu danh sách mã cổ phiếu và kết quả phân tích).
- **Alpha Vantage API Key** (Lấy dữ liệu tài chính & giá cổ phiếu).
- **OpenAI API Key** và **Google Gemini API Key** (Dùng cho các node AI Agent).
- **Telegram Bot Token** (Để nhận tin nhắn cảnh báo tín hiệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc copy toàn bộ JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số sau trong các node:
- **`Read_tickers_from_Sheet` & `write_sentiment_to_sheets`**: Kết nối với tài khoản Google Sheets của các sếp. Đảm bảo tên file Google Sheet khớp với cấu hình (mặc định là "Stock Sentiment") với sheet chứa danh sách mã cổ phiếu (`stocks`) và nơi ghi kết quả (`Sheet1`).
- **`Schedule Trigger`**: Mặc định workflow chạy 3 ngày một lần vào lúc 4:00 chiều để tiết kiệm lượt gọi API Alpha Vantage. Các sếp có thể thay đổi thời gian tùy nhu cầu.
- **`alphavantage - Balance Sheet`, `alphavantage - Profile`, `alphavantage - Income Statement`, `alphavantage - CashFlow`, `alphavantage - Current Price`**: Điền Alpha Vantage API Key vào phần Header hoặc Query Parameters của các HTTP Request nodes.
- **`Message a model` (OpenAI)** & **`Message a model1` (Google Gemini)**: Chọn đúng Credentials đã liên kết với tài khoản OpenAI và Google Gemini của các sếp.
- **`Send a text message` (Telegram)**: Cấu hình Bot Token và Chat ID để nhận thông báo kết quả định giá.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài mã cổ phiếu mẫu để kiểm tra dữ liệu trả về từ Alpha Vantage và AI.
- Sau khi kiểm tra mọi thứ chạy mượt mà, bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể nối thêm node Slack hoặc Discord để gửi báo cáo phân tích vào nhóm chat của team đầu tư.
- **Quản lý Cache hiệu quả:** Tận dụng hệ thống `Cache Lookup` và `Is Cache Valid?` có sẵn trong workflow để tinh chỉnh thời gian lưu trữ cache tài chính, tránh vượt quá giới hạn gọi API miễn phí của Alpha Vantage.
- **Tùy chỉnh Prompt AI:** Các sếp có thể tinh chỉnh system prompt trong các node AI Agent để thêm các tiêu chí định giá riêng (ví dụ: khẩu vị rủi ro, P/E mục tiêu, trường phái đầu tư giá trị hay tăng trưởng).

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo giúp các sếp số hóa quy trình phân tích và định giá cổ phiếu như một quỹ đầu tư chuyên nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa danh mục đầu tư của mình!