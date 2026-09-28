---
title: "🚀 Tự động lọc rác AI (AI Slop) trên LinkedIn feed cực thông minh với n8n và RAG"
description: "Xây dựng backend hoàn chỉnh cho tiện ích mở rộng Chrome StopSlopIn để tự động nhận diện, lọc bỏ các bài đăng AI rác trên LinkedIn và tự học theo gu thẩm mỹ của bạn."
slug: "loc-rac-ai-linkedin-feed-n8n-rag"
tags: [n8n, automation, ai, rag, qdrant, openai, linkedin]
keywords: [n8n workflow, loc ai slop linkedin, stopslopin, qdrant vector store, ai automation, lang-chain n8n]
---

# 🚀 Tự động lọc rác AI (AI Slop) trên LinkedIn feed cực thông minh với n8n và RAG

Mỗi khi lướt LinkedIn, các sếp có cảm thấy mệt mỏi vì tràn lan các bài viết rác do AI tạo ra (AI slop) với văn phong sáo rỗng, công thức rập khuôn và đầy rẫy sự câu tương tác không? Việc lọc thủ công vừa tốn thời gian vừa làm tụt cảm xúc làm việc. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n đóng vai trò là backend cho extension Chrome **StopSlopIn**, sử dụng công nghệ RAG (Retrieval-Augmented Generation) kết hợp Vector Database (Qdrant) và OpenAI để tự động phân tích, đánh giá chất lượng bài đăng, thậm chí "tự học" theo sở thích cá nhân của các sếp theo thời gian thực!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với các extension trình duyệt, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lọc sạch feed LinkedIn:** Tự động loại bỏ các bài viết kém chất lượng, sáo rỗng (AI slop) trước khi chúng kịp làm phiền các sếp.
- **Tự học theo gu cá nhân:** Hệ thống lưu trữ lại mọi lượt vote (thích/ghét) của các sếp thành các embedding trong Qdrant để các lần phân tích sau thông minh và chính xác hơn.
- **Tự động hóa toàn diện:** Hoạt động qua Webhook kết hợp linh hoạt với Chrome Extension với 2 hành động chính (`analyze` và `vote`).
- **Cấu trúc dữ liệu chuẩn chỉnh:** Trả về kết quả dạng JSON (`pass`/`fail`) gọn gàng cho ứng dụng client xử lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản cloud hoặc self-hosted).
- **OpenAI API Key:** Dành cho mô hình chat LLM và tạo Embedding.
- **Qdrant Vector Database Cloud/Local:** Dành cho việc lưu trữ và truy vấn vector tương tự.
- **StopSlopIn Chrome Extension:** Tiện ích mở rộng trên trình duyệt để kết nối tới webhook của workflow này.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã nguồn JSON của workflow từ n8n (hoặc file mẫu từ link gốc) và chọn **Import from JSON** vào trong trình chỉnh sửa n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 23 nodes hoạt động tinh vi qua một Webhook duy nhất nhận tham số truy vấn `?action=`. Các điểm cần cấu hình cốt lõi gồm:

- **Node `Webhook` & `Switch by action`:** Nhận request từ extension. Switch sẽ phân chia luồng dựa trên tham số `action` (`analyze` hoặc `vote`).
- **Nodes `Embeddings OpenAI` & `OpenAI Chat Model`:** 
  - Thêm Credentials tài khoản OpenAI của các sếp.
  - Tại node `OpenAI Chat Model`, chọn model phù hợp (ví dụ: `gpt-5.1-chat-latest` hoặc `gpt-4o`).
- **Nodes `Retrieve similar posts` & `Store post` (Qdrant Vector Store):**
  - Thêm Qdrant API Credentials vào cả hai node này.
  - Tạo sẵn một collection trong Qdrant tên là `stopslopin`.
- **Node `Analyze posts` (Chain LLM) & `Structured Output Parser`:** Kiểm tra system prompt bên trong để tinh chỉnh tiêu chuẩn đánh giá bài viết theo đúng "gu" lọc rác của các sếp.
- **Node `Filter by similarity score`:** Mặc định ngưỡng tương đồng (similarity threshold) đang để là `0.7`. Các sếp có thể điều chỉnh con số này nếu muốn siết chặt hoặc nới lỏng việc tìm kiếm bài viết cũ tương tự.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách gửi một payload mẫu vào Webhook.
- Sau khi test thành công, bật công tắc **Active workflow** và copy URL Webhook dán vào phần cài đặt của extension StopSlopIn trên Chrome.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Kết hợp thêm node Telegram hoặc Slack để nhận báo cáo định kỳ về số lượng bài đăng "rác" đã bị chặn mỗi ngày.
- **Tùy biến Model:** Các sếp hoàn toàn có thể thay thế OpenAI Chat Model bằng các mô hình LangChain-compatible khác như Claude (Anthropic) hoặc Ollama (chạy local miễn phí).
- **Tinh chỉnh Prompt liên tục:** Thêm các ví dụ cụ thể về bài viết hay/dở vào prompt của node `Analyze posts` để AI hiểu sâu hơn về tiêu chuẩn của công ty hoặc cá nhân bạn.

### 📌 Kết luận
Việc tự động hóa lọc bỏ rác AI trên mạng xã hội không chỉ giúp tiết kiệm hàng giờ đồng hồ mỗi tuần mà còn giữ cho môi trường tiếp nhận thông tin của các sếp luôn trong sạch, chất lượng. Hãy setup ngay workflow này và tận hưởng một chiếc feed LinkedIn thông minh hơn hẳn!