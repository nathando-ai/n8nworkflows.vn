---
title: "🚀 Xây dựng Chatbot Q&A Luật Cricket IPL tự động với RAG và Google Gemini trong n8n"
description: "Hướng dẫn chi tiết từng bước xây dựng hệ thống hỏi đáp thông minh áp dụng công nghệ RAG kết hợp Google Gemini API và n8n LangChain nodes."
slug: "chatbot-qa-luat-cricket-ipl-rag-google-gemini"
tags: [n8n, automation, no-code, ai-agent, google-gemini, langchain, rag]
keywords: [n8n workflow, rucksack ai agent, google gemini api, rag chatbot, tự động hóa n8n, langchain n8n]
---

# 🚀 Xây dựng Chatbot Q&A Luật Cricket IPL tự động với RAG và Google Gemini trong n8n

Chào các sếp! Việc tra cứu các quy định, luật lệ phức tạp từ các tài liệu PDF dài dằng dặc thủ công luôn khiến chúng ta đau đầu và tốn nhiều thời gian. Giờ đây, với sức mạnh của **n8n LangChain nodes** kết hợp cùng **Google Gemini API**, các sếp hoàn toàn có thể tự động hóa toàn bộ quy trình này bằng một Chatbot thông minh ứng dụng công nghệ **RAG (Retrieval-Augmented Generation)**. 

Workflow này sẽ tự động đọc tài liệu luật thi đấu (PDF), cắt nhỏ, chuyển đổi thành vector, lưu trữ bộ nhớ đệm và trả lời chính xác mọi thắc mắc của người dùng dựa trên ngữ cảnh thực tế mà không lo bịa đặt thông tin (hallucination).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn việc xử lý tài liệu:** Tự động tải, phân tích và nạp dữ liệu từ file PDF vào Vector Store chỉ bằng 1 cú click.
- **Trả lời chính xác tuyệt đối (Grounding RAG):** Chatbot chỉ trả lời dựa trên tài liệu được cung cấp, nếu không có thông tin sẽ từ chối lịch sự ("Sorry I don’t know"), loại bỏ hoàn toàn tình trạng AI tự chế câu trả lời.
- **Duy trì ngữ cảnh trò chuyện:** Lưu giữ lịch sử 20 câu hỏi/trả lời gần nhất nhờ tích hợp `Simple Memory`.
- **Giao diện chat trực quan:** Tích hợp sẵn khung chat native của n8n để test nhanh chóng và mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain nodes).
- **Google Gemini API Key:** Cần có API key từ Google AI Studio để kết nối với các node Google Gemini Chat Model và Embeddings.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy file JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ nguồn cấp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được chia làm 2 giai đoạn chính rõ ràng:

- **Giai đoạn 1: Nạp tài liệu (Step 1 - Chạy thủ công 1 lần)**
  - **`When clicking ‘Execute workflow’` (Manual Trigger):** Dùng để kích hoạt quá trình nạp dữ liệu thủ công ban đầu.
  - **`HTTP Request`:** Trỏ tới link tải file PDF "Match Playing Conditions" của giải đấu IPL.
  - **`Default Data Loader`:** Xử lý dữ liệu dạng nhị phân (binary) từ file PDF tải về.
  - **`Recursive Character Text Splitter`:** Chia nhỏ văn bản thành các đoạn (chunks) có độ trùng lặp (overlap) nhất định nhằm giảm thiểu tối đa hiện tượng AI bịa thông tin.
  - **`Embeddings Google Gemini 1` & `Simple Vector Store 1`:** Chuyển đổi các đoạn văn bản thành vector bằng mô hình Gemini và lưu trữ tạm thời vào bộ nhớ RAM. *Lưu ý nhớ kỹ tên của Vector Store này để đồng bộ với Giai đoạn 2.*

- **Giai đoạn 2: Vận hành Chatbot (Step 2 - Tự động)**
  - **`When chat message received` (Chat Trigger):** Cung cấp giao diện chat trực tiếp cho người dùng.
  - **`AI Agent`:** Bộ não điều phối trung tâm. Cần cấu hình System Prompt với nội dung ví dụ: *"You are a cricket expert… If info is missing, say ‘Sorry I don’t know’"*. Agent này sẽ kết nối với bộ nhớ và công cụ RAG.
  - **`Google Gemini Chat Model`:** Chọn mô hình ngôn ngữ Gemini, cấu hình **Credentials** bằng cách nhập Google Gemini API Key của các sếp.
  - **`Simple Memory`:** Giúp lưu trữ 20 lượt hội thoại gần nhất để chatbot hiểu ngữ cảnh ngữ pháp.
  - **`Simple Vector Store` (Retrieve-as-tool mode):** Đóng vai trò là công cụ RAG. Cần đặt **tên Vector Store** và **Quy tắc Embedding** khớp chính xác với Step 1 để hệ thống có thể truy vấn top 10 đoạn văn bản liên quan nhất.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) **Step 1** để hệ thống nạp dữ liệu PDF vào Vector Store.
- Kiểm tra lại **Step 2** bằng cách gõ câu hỏi vào khung chat (`Chat Trigger`) để test khả năng phản hồi của Bot.
- Khi mọi thứ mượt mà, bật công tắc **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Nâng cấp Vector Store:** Khi đưa ứng dụng vào môi trường thực tế (production), các sếp nên thay thế `Simple Vector Store (In-Memory)` bằng các vector database chuyên nghiệp hơn như Pinecone, Qdrant hoặc Chroma.
- **Mở rộng kênh giao tiếp:** Thay vì dùng khung chat mặc định của n8n, các sếp có thể thay thế node `Chat Trigger` bằng Webhook kết nối Telegram Bot, Slack, hoặc Zalo OA để phục vụ người dùng thực tế.
- **Tự động cập nhật tài liệu:** Kết hợp thêm Google Drive node hoặc Cron node để tự động quét và cập nhật file PDF luật mới định kỳ hàng tuần/tháng.

### 📌 Kết luận
Chỉ với vài thao tác kéo thả và cấu hình đơn giản trên n8n, các sếp đã sở hữu ngay một trợ lý AI thông minh chuyên biệt tra cứu tài liệu nội bộ hoặc luật lệ thi đấu. Áp dụng ngay vào doanh nghiệp của mình để tiết kiệm hàng giờ tra cứu thủ công nhé!