---
title: "🌍 [Tự động hóa Lập kế hoạch du lịch với MongoDB Atlas & Gemini LLM - Không cần code]"
description: "Hướng dẫn chi tiết cách tự động hóa lập kế hoạch du lịch bằng n8n, MongoDB Atlas và Google Gemini LLM. Tiết kiệm thời gian lên đến 90% cho các sếp du lịch."
slug: "tu-dong-hoa-lap-ke-hoach-du-lich-mongodb-gemini-llm"
tags: [n8n, automation, no-code, MongoDB, AI, travel-planning]
keywords: [n8n workflow, tự động hóa du lịch, Gemini LLM, MongoDB Atlas, vector search]
---

# 🌍 Tự động hóa Lập kế hoạch du lịch với MongoDB Atlas & Gemini LLM - Không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp du lịch khi phải tìm kiếm thông tin, so sánh điểm đến và lập kế hoạch thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên đến 90% khi lập kế hoạch du lịch
- Nhận thông tin điểm đến chính xác và cập nhật mới nhất từ cơ sở dữ liệu vector
- Lưu trữ và truy xuất lịch sử trò chuyện tự động
- Tích hợp dễ dàng với các nền tảng khác như Slack, Telegram
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google API cho Gemini LLM
- Tài khoản OpenAI API
- MongoDB Atlas Cluster với IP Access List được cấu hình (để test dễ dàng, các sếp có thể dùng `0.0.0.0/0`)
- Collection `points_of_interest` với vector search index được tạo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3577](https://n8n.io/workflows/3577)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow vào
4. Click "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When chat message received" (chatTrigger)**:
   - Không cần cấu hình gì thêm, node này sẽ bắt các tin nhắn chat đến.

2. **Node "MongoDB Chat Memory" (memoryMongoDbChat)**:
   - Cấu hình credentials MongoDB với connection string và tên database
   - Đảm bảo collection `threads` và `messages` đã được tạo trong database

3. **Node "Google Gemini Chat Model" (lmChatGoogleGemini)**:
   - Cấu hình credentials Google Palm API với API key
   - Chọn model phù hợp (ví dụ: gemini-pro)

4. **Node "MongoDB Atlas Vector Store" (vectorStoreMongoDBAtlas)**:
   - Cấu hình credentials MongoDB với connection string và tên database
   - Đảm bảo collection `points_of_interest` đã được tạo
   - Tạo vector search index với cấu trúc như sau:
     ```json
     {
       "fields": [
         {
           "type": "vector",
           "path": "embedding",
           "numDimensions": 1536,
           "similarity": "cosine"
         }
       ]
     }
     ```

5. **Node "Embeddings OpenAI" (embeddingsOpenAi)**:
   - Cấu hình credentials OpenAI API với API key
   - Chọn model phù hợp (ví dụ: text-embedding-ada-002)

6. **Node "Webhook"** (webhook):
   - Đảm bảo path là `ingestData` và HTTP method là POST
   - Ví dụ cấu hình:
     ```
     Path: ingestData
     HTTP Method: POST
     ```

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, các sếp cần test workflow:
   - Gửi một yêu cầu POST đến webhook với dữ liệu mẫu:
     ```bash
     curl -X POST "https://<account>.app.n8n.cloud/webhook-test/ingestData" \
       -H "Content-Type: application/json" \
       -d '{
         "raw_body": {
           "point_of_interest": {
             "title": "Eiffel Tower",
             "description": "Iconic iron lattice tower located on the Champ de Mars in Paris, France."
           }
         }
       }'
     ```
   - Thay thế `<account>` bằng tên tài khoản n8n của các sếp

2. Sau khi test thành công, các sếp có thể bật workflow để hoạt động liên tục.

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**: Các sếp có thể thêm node Slack hoặc Telegram để nhận thông báo về kế hoạch du lịch.
2. **Lưu log hoạt động**: Thêm node để lưu log các cuộc trò chuyện để theo dõi và phân tích sau này.
3. **Gửi báo cáo định kỳ**: Tự động gửi báo cáo về các điểm đến được đề xuất hàng tuần/tháng.
4. **Tích hợp với Google Maps**: Kết nối với Google Maps API để hiển thị bản đồ và chỉ đường cho các điểm đến.

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa lập kế hoạch du lịch, giúp các sếp tiết kiệm thời gian và nhận được thông tin chính xác nhất. Với khả năng lưu trữ và truy xuất lịch sử trò chuyện cùng với cơ sở dữ liệu vector mạnh mẽ, các sếp có thể tạo ra những kế hoạch du lịch hoàn hảo mà không cần phải tìm kiếm thông tin thủ công. Hãy áp dụng ngay để nâng cao trải nghiệm du lịch của các sếp!