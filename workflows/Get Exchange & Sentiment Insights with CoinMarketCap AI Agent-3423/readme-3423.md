---
title: "🚀 Xây dựng AI Agent phân tích sàn giao dịch và tâm lý thị trường Crypto với CoinMarketCap"
description: "Hướng dẫn tích hợp n8n AI Agent kết hợp OpenAI GPT-4o-mini và CoinMarketCap API để tự động tra cứu thông tin sàn, tài sản, chỉ số CMC 100 và Fear & Greed Index."
slug: "ai-agent-phan-tich-crypto-coinmarketcap-n8n"
tags: [n8n, automation, ai-agent, openai, crypto, coinmarketcap]
keywords: [n8n workflow, coinmarketcap api, ai agent crypto, fear and greed index n8n, openais gpt-4o-mini]
---

# 🚀 Xây dựng AI Agent phân tích sàn giao dịch và tâm lý thị trường Crypto với CoinMarketCap

Các nhà đầu tư và chuyên gia Web3 thường mất rất nhiều thời gian để tra cứu thủ công thông tin về các sàn giao dịch (Exchange), tài sản nắm giữ, chỉ số thị trường (CMC 100) hay tâm lý nhà đầu tư (Fear & Greed Index) từ nhiều nguồn khác nhau. Việc tổng hợp dữ liệu này bằng tay vừa chậm chạp, vừa khó đưa ra quyết định nhanh chóng trong thị trường crypto biến động từng giây.

Được thiết kế bởi **Don Jayamaha Jr** (Blockchain Strategist với 12 năm kinh nghiệm), workflow n8n này sẽ giúp các sếp tạo ra một **AI Agent thông minh** hoạt động như một chuyên gia tư vấn dữ liệu crypto 24/7. Agent này tự động kết nối với 5 endpoint mạnh mẽ của CoinMarketCap thông qua OpenAI GPT-4o-mini, giúp xử lý mọi câu hỏi phức tạp từ tra cứu ID sàn, tài sản đến chỉ số cảm xúc thị trường chỉ trong vài giây mà không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn việc tra cứu dữ liệu:** Thay vì thao tác thủ công trên web CoinMarketCap, chỉ cần ra lệnh bằng ngôn ngữ tự nhiên.
- **Tích hợp AI thông minh (GPT-4o-mini):** Hiểu ngữ cảnh câu hỏi, tự động gọi đúng API công cụ (Tool Calling) để trả về thông tin chính xác.
- **Quản lý ngữ cảnh thông minh:** Tích hợp bộ nhớ (`Memory Buffer Window`) giúp duy trì mạch hội thoại mượt mà khi chat với Agent.
- **Hoạt động liên tục 24/7:** Dễ dàng kết nối làm sub-workflow (Agent con) cho các hệ thống Telegram Bot, Slack hoặc Dashboard lớn của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Hệ thống n8n:** Đã cài đặt phiên bản hỗ trợ LangChain (n8n v1.0 trở lên).
2. **OpenAI API Key:** Dành cho node `Exchange and Community Agent Brain` (Sử dụng model `gpt-4o-mini`).
3. **CoinMarketCap API Key:** Dành cho các node HTTP Request (`httpHeaderAuth`) để gọi dữ liệu sàn và thị trường.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp hoặc copy trực tiếp mã JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` / `Cmd+V` để paste trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình các thành phần sau:
- **When Executed by Another Workflow (`executeWorkflowTrigger`):** Điểm khởi chạy nhận tham số `message` (câu lệnh) và `sessionId` (mã phiên làm việc) từ workflow giám sát chính (Supervisor Agent).
- **CoinMarketCap Exchange and Community Agent (`agent`):** Node cốt lõi điều phối các công cụ (Tools).
- **Exchange and Community Agent Brain (`lmChatOpenAi`):** Chọn credentials OpenAI của các sếp và đảm bảo model đang trỏ tới `gpt-4o-mini`.
- **Các Tool HTTP Request (Exchange Map, Exchange Info, CMC 100 Index, Fear and Greed Latest, Exchange Assets):** Cấu hình `httpHeaderAuth` với API Key của CoinMarketCap để cấp quyền truy cập các endpoint:
  - `/v1/exchange/map`: Lấy ID, tên và slug của sàn.
  - `/v1/exchange/info`: Lấy metadata (ngày ra mắt, mạng xã hội, vị trí).
  - `/v1/exchange/assets`: Kiểm tra token nắm giữ của sàn.
  - `/v3/index/cmc100-latest`: Thông tin bộ chỉ số CoinMarketCap 100.
  - `/v3/fear-and-greed/latest`: Chỉ số tâm lý thị trường (0–100).

#### 3. Kích hoạt ⚡️
- Tiến hành test thử bằng cách gửi các câu lệnh mẫu (ví dụ: *"Show latest Fear & Greed score"* hoặc *"Get Binance exchange token holdings"*).
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Telegram/Slack Bot:** Biến workflow này thành trợ lý ảo trên nhóm chat cộng đồng crypto, cho phép mọi người gõ lệnh hỏi đáp trực tiếp.
- **Lưu lịch sử tra cứu:** Thêm node Google Sheets hoặc Airtable sau Agent để lưu lại các câu hỏi và kết quả phân tích phục vụ việc thống kê xu hướng quan tâm của người dùng.
- **Tích hợp cảnh báo (Alerts):** Kết hợp thêm điều kiện (If Node) kiểm tra chỉ số Fear & Greed, nếu thị trường rơi vào trạng thái *Extreme Fear* (Quá sợ hãi), tự động gửi thông báo khẩn cấp về Telegram cá nhân.

### 📌 Kết luận
Workflow AI Agent kết hợp CoinMarketCap và OpenAI này là một "vũ khí" cực kỳ mạnh mẽ giúp tối ưu hóa công việc phân tích dữ liệu thị trường crypto. Hãy triển khai ngay trên hệ thống n8n của các sếp để nâng tầm tự động hóa và đón đầu xu hướng công nghệ Web3!