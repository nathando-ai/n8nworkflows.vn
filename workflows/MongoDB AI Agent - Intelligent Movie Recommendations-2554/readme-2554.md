---
title: "🎬 Xây dựng AI Agent gợi ý phim thông minh tích hợp MongoDB trong n8n"
description: "Hướng dẫn xây dựng trợ lý AI thông minh tích hợp MongoDB để gợi ý phim, phân tích dữ liệu và lưu danh sách yêu thích tự động bằng n8n."
slug: "mongodb-ai-agent-goi-y-phim-thong-minh"
tags: [n8n, automation, ai-agent, mongodb, openai, langchain]
keywords: [n8n workflow, ai agent mongodb, gợi ý phim ai, langain n8n, tự động hóa openai]
---

# 🎬 Xây dựng AI Agent gợi ý phim thông minh tích hợp MongoDB trong n8n

Việc tìm kiếm và gợi ý phim dựa trên sở thích cá nhân thường đòi hỏi các hệ thống phức tạp hoặc truy vấn cơ sở dữ liệu thủ công mất thời gian. Các sếp hoàn toàn có thể tự động hóa quy trình này bằng một **AI Agent** tự trị, có khả năng hiểu ngữ cảnh trò chuyện, tự động truy vấn dữ liệu từ MongoDB thông qua aggregation framework và thậm chí lưu lại các bộ phim yêu thích của các sếp vào cơ sở dữ liệu.

Workflow này do chuyên gia Pavel Duchovny thiết kế, tận dụng sức mạnh của LangChain, OpenAI LLM và MongoDB để tạo ra một trợ lý điện ảnh thông minh, hoạt động 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Trợ lý AI tự trị**: Hiểu câu hỏi tự nhiên từ người dùng qua khung chat và tự động chọn công cụ (tool) phù hợp.
- **Truy vấn dữ liệu thông minh**: Khai thác kho dữ liệu phim khổng lồ trên MongoDB sử dụng Aggregation Pipeline mạnh mẽ.
- **Tương tác 2 chiều**: Không chỉ đọc dữ liệu mà còn có khả năng ghi nhận (insert) phim yêu thích ngược lại vào cơ sở dữ liệu.
- **Ghi nhớ ngữ cảnh**: Tích hợp bộ nhớ tạm (Window Buffer Memory) giúp cuộc trò chuyện mượt mà, liên mạch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Phiên bản hỗ trợ LangChain/AI nodes).
- **OpenAI API Key**: Cần thiết cho node OpenAI Chat Model.
- **MongoDB Database**: Cơ sở dữ liệu MongoDB (có chứa collection mẫu về phim - sample movies).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 2554) và import trực tiếp vào giao diện n8n của mình, hoặc tạo mới một workflow và cấu hình các node theo danh sách bên dưới.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **When chat message received (`chatTrigger`)**: 
  - Node này đóng vai trò là cổng tiếp nhận tin nhắn chat từ người dùng. Các sếp có thể nhúng widget chat này lên website hoặc test trực tiếp trên giao diện n8n chat UI.
- **AI Agent - Movie Recommendation (`agent`)**: 
  - Là bộ não trung tâm điều phối các tool. Node này kết nối với Chat Model, Memory, và các MongoDB Tool.
- **OpenAI Chat Model (`lmChatOpenAi`)**: 
  - Cần cấu hình **Credentials** chọn `openAiApi` với API Key hợp lệ của các sếp. Nên chọn các model như `gpt-4o` hoặc `gpt-4o-mini` để có hiệu suất tốt nhất.
- **Window Buffer Memory (`memoryBufferWindow`)**: 
  - Giúp AI ghi nhớ lại lịch sử trò chuyện trong phiên làm việc. Không cần cấu hình phức tạp, để mặc định là đủ dùng.
- **MongoDBAggregate (`mongoDbTool`)**: 
  - Cần cấu hình **Credentials** `mongoDb` trỏ tới cụm MongoDB của các sếp. Node này được AI Agent sử dụng như một tool để thực hiện các truy vấn aggregation tìm kiếm phim.
- **insertFavorite (`toolWorkflow`)**: 
  - Sub-workflow hoặc tool phụ dùng để thực hiện thao tác lưu (`insert`) bộ phim yêu thích mà người dùng vừa chọn vào MongoDB.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Chat** trên giao diện n8n hoặc test thử câu lệnh: *"Gợi ý cho tôi một bộ phim khoa học viễn tưởng hay nhất những năm 2010"* để kiểm tra phản hồi từ AI Agent.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để kích hoạt workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat đa nền tảng**: Thay vì dùng Chat Trigger mặc định, các sếp có thể thay thế bằng node Telegram hoặc Slack để tương tác với AI Agent mọi lúc mọi nơi.
- **Lưu lịch sử chat**: Kết nối thêm node PostgreSQL hoặc Airtable để ghi lại toàn bộ lịch sử trò chuyện phục vụ việc phân tích nhu cầu khách hàng sau này.
- **Mở rộng tool**: Bổ sung thêm các tool tra cứu lịch chiếu rạp, mua vé hoặc đánh giá phim để biến trợ lý này thành một siêu ứng dụng giải trí.

### 📌 Kết luận
Với workflow AI Agent kết hợp MongoDB này, các sếp đã sở hữu một trợ lý dữ liệu thông minh, tự động hóa hoàn toàn việc tra cứu và gợi ý nội dung mà không cần viết hàng ngàn dòng code phức tạp. Hãy triển khai ngay trên hệ thống của mình nhé!