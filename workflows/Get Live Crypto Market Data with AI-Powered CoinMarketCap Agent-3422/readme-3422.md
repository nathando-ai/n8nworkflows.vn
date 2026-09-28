---
title: "🚀 Tự động hóa dữ liệu thị trường Crypto Real-time với AI Agent và CoinMarketCap"
description: "Hướng dẫn cài đặt workflow n8n tích hợp OpenAI GPT-4o Mini và CoinMarketCap API để phân tích, tra cứu giá, vốn hóa và chuyển đổi tiền mã hóa tự động."
slug: "crypto-market-data-ai-agent-coinmarketcap-n8n"
tags: [n8n, automation, ai-agent, openai, coinmarketcap, crypto, web3]
keywords: [n8n workflow, coinmarketcap api, ai agent crypto, gpt-4o-mini, tu dong hoa crypto, tich hop ai]
---

# 🚀 Xây dựng AI Agent phân tích thị trường Crypto với CoinMarketCap và n8n

Các sếp làm trong ngành Web3 hoặc đầu tư tài chính chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải liên tục tra cứu giá, vốn hóa thị trường, quy đổi tiền tệ hoặc tìm kiếm thông tin metadata của hàng ngàn đồng coin trên CoinMarketCap thủ công. 

Workflow n8n này do chuyên gia Blockchain Don Jayamaha Jr thiết kế sẽ giải quyết triệt để vấn đề đó. Đây là một **AI Agent thông minh** được trang bị đầy đủ các công cụ (Tools) kết nối trực tiếp với 6 endpoints quan trọng của CoinMarketCap API, sử dụng bộ não **GPT-4o Mini** để hiểu câu lệnh tiếng người và trả về dữ liệu thị trường crypto theo thời gian thực (real-time) một cách chính xác tuyệt đối.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu thông minh bằng ngôn ngữ tự nhiên:** Không cần nhớ cú pháp API phức tạp, chỉ cần hỏi AI như "Top 10 token theo vốn hóa" hoặc "Quy đổi 1000 DOGE sang BTC".
- **Tự động hóa 6 nghiệp vụ crypto:** Lấy giá, xem bản đồ coin (map), thông tin chi tiết (info), danh sách niêm yết (listings), chỉ số toàn cầu (global metrics) và quy đổi giá (price conversion).
- **Duy trì ngữ cảnh (Memory):** Tích hợp Buffer Window Memory giúp AI ghi nhớ lịch sử hội thoại trong phiên làm việc.
- **Mô-đun hóa linh hoạt:** Có thể hoạt động độc lập hoặc đóng vai trò là một Agent con (Sub-agent) nhận lệnh từ Supervisor AI trong các hệ thống tự động lớn hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain / Advanced AI).
- **OpenAI API Key:** Cho node `Crypto Agent Brain` (sử dụng model `gpt-4o-mini`).
- **CoinMarketCap API Key:** Đăng ký tài khoản miễn phí trên CoinMarketCap Developer Portal để lấy API Key xác thực cho các HTTP Request Tool nodes.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON từ nguồn cung cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> **Import from File** hoặc **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thành phần sau để hệ thống hoạt động mượt mà:

- **When Executed by Another Workflow (`executeWorkflowTrigger`):** Node kích hoạt nhận dữ liệu đầu vào (bao gồm `message` là câu hỏi của người dùng và `sessionId` để quản lý bộ nhớ). Nếu chạy độc lập test trực tiếp, các sếp có thể thay thế bằng Chat Trigger hoặc Manual Trigger tùy ý.
- **Crypto Agent Brain (`lmChatOpenAi`):** 
  - Chọn Credentials OpenAI của các sếp.
  - Đảm bảo tham số model được đặt là `gpt-4o-mini` (hoặc model tương đương).
- **6 Công cụ CoinMarketCap (`toolHttpRequest`):**
  - Gồm các node: `CoinMarketCap Price`, `Crypto Map`, `Crypto Info`, `Crypto Listings`, `Global Metrics`, `Price Conversion`.
  - Cần tạo **Credential kiểu Header Auth** với tên Header là `X-CMC_PRO_API_KEY` và giá trị là API Key lấy từ trang CoinMarketCap của các sếp, sau đó gán vào tất cả 6 node công cụ này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một câu lệnh mẫu (ví dụ: *"Convert 5 ETH to USD"*) vào node kích hoạt để kiểm tra phản hồi từ AI Agent.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động.

---

### 💡 Các câu lệnh mẫu (Sample Prompts) có thể dùng cho Agent:
- *“What is the CoinMarketCap ID for ETH?”* (Sử dụng node Crypto Map)
- *“Convert 1000 DOGE to BTC.”* (Sử dụng node Price Conversion)
- *“Show top 10 tokens by market cap in EUR.”* (Sử dụng node Crypto Listings)
- *“What is the current Bitcoin dominance and total market cap?”* (Sử dụng node Global Metrics)

---

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram / Slack Bot:** Nối node kích hoạt với Telegram Trigger để tạo một Crypto Bot trực tiếp trên nhóm chat Telegram của cộng đồng.
- **Lưu lịch sử chat:** Thêm node lưu trữ (Google Sheets hoặc PostgreSQL) để lưu lại các câu hỏi và câu trả lời phục vụ việc phân tích nhu cầu người dùng.
- **Xử lý Rate Limit:** Gói API miễn phí của CoinMarketCap có giới hạn số lượng request (Rate limit). Các sếp nên chú ý thêm độ trễ (delay) nếu gọi liên tục để tránh lỗi mã `429 Rate limit exceeded`.

### 📌 Kết luận
Workflow tích hợp AI Agent và CoinMarketCap này là một "vũ khí" cực mạnh cho bất kỳ ai làm việc trong lĩnh vực tài chính phi tập trung (DeFi) và Crypto. Hãy triển khai ngay lên VPS của các sếp để sở hữu một trợ lý ảo phân tích thị trường 24/7 hoàn toàn tự động!