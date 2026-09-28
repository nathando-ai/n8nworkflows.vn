---
title: "🚀 Tích hợp GPT-4 và Nansen MCP: Trợ lý AI phân tích On-chain thông minh"
description: "Hướng dẫn xây dựng chatbot AI kết hợp GPT-4 và Nansen MCP trên n8n để truy vấn, phân tích dữ liệu blockchain và ví crypto tự động qua khung chat."
slug: "get-blockchain-insights-from-chat-gpt4-nansen-mcp"
tags: [n8n, automation, no-code, ai-agent, blockchain, crypto, nansen, openai]
keywords: [n8n workflow, phân tích blockchain, nansen mcp, gpt-4, crypto trading, ai chatbot, on-chain analytics]
---

# 🚀 Tích hợp GPT-4 và Nansen MCP: Trợ lý AI phân tích On-chain thông minh

Các sếp làm trong thị trường Crypto chắc chắn hiểu rõ tầm quan trọng của dữ liệu on-chain. Việc tra cứu dòng tiền, lịch sử ví, hay xu hướng dòng tiền từ các quỹ lớn (Smart Money) thường đòi hỏi phải thao tác thủ công qua nhiều công cụ phức tạp, tốn kém thời gian và dễ bỏ lỡ cơ hội.

Nhưng giờ đây, với workflow n8n tích hợp **AI Agent**, **OpenAI GPT-4** và **Nansen MCP (Model Context Protocol)**, các sếp có thể sở hữu ngay một trợ lý AI thông minh. Trợ lý này sẽ trực tiếp "lắng nghe" câu hỏi của các sếp qua khung chat và tự động truy vấn dữ liệu blockchain chuyên sâu từ Nansen một cách chớp nhoáng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu thời gian thực:** Hỏi đáp trực tiếp về số liệu on-chain, hoạt động của ví whale, và xu hướng token ngay trong giao diện chat.
- **Tiết kiệm thời gian tối đa:** Không cần phải mở nhiều tab trình duyệt hay tự tay lọc dữ liệu phức tạp trên Nansen.
- **AI thông minh tự động hóa:** GPT-4 hiểu ngữ cảnh câu hỏi và gọi đúng công cụ (MCP Tool) cần thiết để trả về kết quả chính xác nhất.
- **Hoạt động 24/7:** Trợ lý ảo luôn sẵn sàng phục vụ mọi lúc mọi nơi trên hạ tầng tự chủ của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted phiên bản hỗ trợ LangChain/AI nodes).
- **OpenAI API Key** (để cấu hình mô hình GPT-4).
- **Tài khoản/API Access Nansen MCP** với thông tin xác thực (`httpHeaderAuth`) để kết nối công cụ phân tích on-chain.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tải file JSON của workflow từ nguồn cấp (hoặc copy toàn bộ JSON workflow) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 node chính hoạt động nhịp nhàng với nhau. Các sếp cần cấu hình kỹ các điểm sau:

- **When chat message received (`chatTrigger`)**: 
  - Node này đóng vai trò là điểm chạm đầu vào (giao diện chat). Các sếp có thể cấu hình giao diện chat widget tích hợp sẵn của n8n hoặc nhúng vào trang web cá nhân.
- **AI Agent (`agent`)**: 
  - Là bộ não trung tâm điều phối. Node này kết nối LangChain Agent để điều phối giữa OpenAI Chat Model và MCP Client Tool nhằm giải quyết câu hỏi của người dùng.
- **OpenAI Chat Model (`lmChatOpenAi`)**: 
  - Chọn model `gpt-4.1-mini` (hoặc các biến thể GPT-4 phù hợp).
  - Kết nối với **OpenAI API Credentials** của các sếp.
- **MCP Client (`mcpClientTool`)**: 
  - Cấu hình **HTTP Header Auth** để kết nối an toàn với dịch vụ Nansen MCP. Đảm bảo endpoint URL và token xác thực được điền chính xác theo tài liệu từ Nansen.

#### 3. Kích hoạt ⚡️
- Bấm **Test step** hoặc **Chat** thử trực tiếp ở node `When chat message received` để kiểm tra khả năng phản hồi của AI.
- Nếu mọi thứ trả về kết quả chính xác, các sếp bấm nút **Active** để chính thức đưa trợ lý ảo vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc:** Nối thêm node Telegram hoặc Slack vào sau AI Agent để các sếp có thể chat trực tiếp với trợ lý blockchain ngay trên nhóm chat công việc.
- **Lưu lịch sử chat:** Kết nối thêm cơ sở dữ liệu (như Supabase hoặc Google Sheets) để lưu lại toàn bộ các câu hỏi và phân tích on-chain quan trọng phục vụ việc tra cứu lại sau này.
- **Tùy chỉnh System Prompt:** Thêm các chỉ dẫn cụ thể cho AI Agent trong node Agent (ví dụ: *"Bạn là một chuyên gia phân tích tài chính crypto hàng đầu..."*) để câu trả lời mang phong cách chuyên nghiệp hơn.

### 📌 Kết luận
Việc kết hợp sức mạnh phân tích dữ liệu đỉnh cao của Nansen với trí tuệ nhân tạo GPT-4 thông qua n8n mở ra một hướng đi cực kỳ mạnh mẽ cho các nhà đầu tư và đội ngũ phát triển crypto. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình làm việc và nắm bắt thông tin thị trường nhanh hơn đối thủ!