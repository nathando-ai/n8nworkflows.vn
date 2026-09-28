---
title: "🚀 Đánh giá độ chính xác của AI Agent bằng OpenAI và Cosine Similarity trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đo lường độ liên quan (Answer Relevance) của AI Agent sử dụng OpenAI và thuật toán Cosine Similarity."
slug: "danh-gia-do-chinh-xac-ai-agent-openai-cosine-similarity"
tags: [n8n, automation, ai-agent, openai, ragas, evaluation]
keywords: [n8n workflow, đánh giá AI agent, answer relevance, cosine similarity, openai trong n8n]
---

# 🚀 Đánh giá độ chính xác của AI Agent bằng OpenAI và Cosine Similarity

Các sếp đang phát triển các trợ lý AI (AI Agent) nhưng thường xuyên đau đầu vì không biết câu trả lời của bot có thực sự bám sát câu hỏi của người dùng hay không? Việc kiểm tra thủ công từng câu trả lời là bất khả thi khi dữ liệu lớn. 

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, tự động hóa toàn bộ quá trình đo lường độ liên quan (**Answer Relevance**) của AI Agent dựa trên phương pháp tiên tiến từ Ragas framework (kết hợp OpenAI và độ tương đồng Cosine).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đánh giá tự động hóa:** Chạy test hàng loạt câu hỏi từ Google Sheets mà không cần thao tác thủ công.
- **Đo lường chuẩn xác:** Sử dụng mô hình Jeopardy! (AI đọc câu trả lời để đoán lại câu hỏi, sau đó so sánh với câu hỏi gốc bằng Cosine Similarity).
- **Phát hiện sớm lỗi:** Nhận diện ngay các trường hợp AI trả lời lan man,a bịa đặt thông tin (hallucination) hoặc đi lạc đề.
- **Tối ưu prompt liên tục:** Dựa trên điểm số metrics để cải thiện chất lượng AI Agent của doanh nghiệp.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- n8n phiên bản `1.94+` trở lên.
- Tài khoản **OpenAI API Key** (dùng cho các node LLM và Get Embeddings).
- Tài khoản **Google Sheets** để lưu trữ bộ dữ liệu test (dataset).
- Tham khảo mẫu Google Sheet chuẩn tại: [Sample Dataset Google Sheet](https://docs.google.com/spreadsheets/d/1YOnu2JJjlxd787AuYcg-wKbkjyjyZFgASYVV0jsij5Y/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template (ID: 4425) hoặc copy toàn bộ mã nguồn JSON và paste trực tiếp vào màn hình n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **When fetching a dataset row & Update Output:** Kết nối tài khoản Google Sheets của các sếp (`googleSheetsOAuth2Api`), trỏ tới file Google Sheet chứa bộ dữ liệu test mẫu.
- **OpenAI Chat Model & OpenAI Chat Model1:** Thêm credentials OpenAI API của các sếp và giữ nguyên model `gpt-4.1-mini` (hoặc thay đổi tùy theo nhu cầu kinh phí).
- **Get Embeddings:** Cấu hình gọi API OpenAI để tạo vector embedding cho câu hỏi gốc và câu hỏi được tạo ngược lại từ câu trả lời của AI.
- **Calculate Similarity Score (Node Code):** Xử lý thuật toán toán học Cosine Similarity để chấm điểm độ tương đồng giữa 2 vector.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công thông qua **Evaluation Trigger** (`When fetching a dataset row`) để kiểm tra luồng dữ liệu đọc/ghi Google Sheets.
- Sau khi kiểm tra kết quả điểm số trả về chính xác, các sếp có thể lưu và quản lý bộ test cases của mình.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thiết lập thêm node thông báo để mỗi khi chạy xong một đợt evaluation, kết quả tổng quan (điểm trung bình) sẽ được bắn thẳng về nhóm chat của team kỹ thuật.
- **Lưu trữ lịch sử:** Lưu lại kết quả đánh giá vào một sheet riêng theo mốc thời gian để theo dõi độ tiến bộ của AI Agent sau mỗi lần tinh chỉnh Prompt.
- **Mở rộng metric:** Kết hợp thêm các tiêu chí đánh giá khác như độ trung thực (Faithfulness) hoặc độ đầy đủ (Context Recall).

### 📌 Kết luận
Việc kiểm thử AI Agent không còn là bài toán khó nếu các sếp biết tận dụng sức mạnh của n8n kết hợp với AI evaluations. Hãy áp dụng ngay workflow này để nâng tầm chất lượng các ứng dụng AI của doanh nghiệp mình nhé!