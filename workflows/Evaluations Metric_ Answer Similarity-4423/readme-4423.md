---
title: "🚀 Đánh giá độ tương đồng câu trả lời AI (Answer Similarity) tự động trên n8n"
description: "Hướng dẫn xây dựng và cấu hình workflow n8n đo lường độ chính xác và tính nhất quán của AI Agent bằng phương pháp đo độ tương đồng vector (Cosine Similarity) với OpenAI."
slug: "danh-gia-do-tuong-dong-cau-tra-loi-ai-n8n"
tags: [n8n, automation, ai-agent, openai, rag, evaluation]
keywords: [n8n workflow, answer similarity, đánh giá ai agent, ragas similarity, openAI embeddings, tự động hóa n8n]
---

# 🚀 Đánh giá độ tương đồng câu trả lời AI (Answer Similarity) tự động trên n8n

Trong quá trình phát triển các ứng dụng AI, chatbot hay hệ thống RAG (Retrieval-Augmented Generation), việc kiểm tra xem câu trả lời của AI có thực sự chính xác so với kỳ vọng (Ground Truth) hay không luôn là một "cơn ác mộng" nếu làm thủ công. Các sếp thường phải đọc từng đoạn chat để chấm điểm, vừa mất thời gian vừa chủ quan. 

Workflow n8n này từ tác giả Jimleuk sẽ giúp các sếp tự động hóa 100% việc đo lường độ tương đồng giữa câu trả lời của AI và dữ liệu chuẩn thông qua **OpenAI Embeddings** và thuật toán **Cosine Similarity** (được lấy cảm hứng từ thư viện RAGAS nổi tiếng).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [An toàn, tiết kiệm: Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đánh giá khách quan:** Tự động chấm điểm độ nhất quán của AI dựa trên toán học (Cosine Similarity) thay vì cảm tính.
- **Phát hiện ảo giác (Hallucination):** Dễ dàng nhận diện khi nào mô hình LLM trả lời lệch lạc so với thực tế (Ground Truth) thông qua điểm số thấp.
- **Tiết kiệm thời gian:** Thay vì test thủ công hàng trăm câu hỏi, hệ thống sẽ tự kéo dữ liệu từ Google Sheets, chạy đánh giá và cập nhật kết quả tự động.
- **Tối ưu hóa prompt/model:** Giúp các sếp biết được liệu thay đổi prompt hay đổi model (như `gpt-4.1-mini`) có thực sự làm tăng chất lượng câu trả lời hay không.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- n8n phiên bản **1.94+** trở lên (hỗ trợ tính năng Evaluations Trigger).
- Tài khoản **OpenAI API Key** (dùng cho LLM chat model và tạo Embeddings).
- Tài khoản **Google Sheets** (để chứa dataset câu hỏi mẫu và Ground Truth).
- Tham khảo file mẫu Google Sheet chuẩn tại đây: [Sample Dataset Google Sheet](https://docs.google.com/spreadsheets/d/1YOnu2JJjlxd787AuYcg-wKbkjyjyZFgASYVV0jsij5Y/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc tải file JSON từ nguồn gốc về rồi import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:
- **OpenAI Chat Model1 (`lmChatOpenAi`):** Kết nối credentials OpenAI của sếp và chọn model (mặc định là `gpt-4.1-mini` hoặc model tương đương).
- **When fetching a dataset row (`evaluationTrigger`) & Update Output (`evaluation`):** Kết nối tài khoản Google Sheets OAuth2 API, sau đó trỏ tới file Google Sheet chứa tập dữ liệu test của các sếp.
- **Get Embeddings (`httpRequest`) & Get Embeddings1 (`httpRequest`):** Đảm bảo hai node gọi API tạo vector embedding của OpenAI được cấu hình đúng API Key và endpoint chuẩn để chuyển đổi text thành vector.
- **Calculate Similarity Score (`code`):** Node này chứa đoạn mã Python/JavaScript tính toán khoảng cách cosine giữa vector của câu trả lời AI và Ground Truth. Các sếp không cần sửa code bên trong trừ khi muốn tinh chỉnh công thức.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) thông qua Evaluations Trigger để kiểm tra kết quả trả về trong Google Sheets.
- Sau khi kiểm tra mọi thứ chạy mượt mà, các sếp có thể lưu lại và sử dụng bất cứ lúc nào cần đánh giá chất lượng agent.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo về kênh chat nhóm ngay sau khi hoàn thành đợt đánh giá, giúp team nắm bắt điểm số trung bình (Average Score) tức thì.
- **Lưu lịch sử đánh giá:** Kết hợp thêm một bảng Google Sheets phụ hoặc Database (như PostgreSQL, Supabase) để lưu vết lịch sử điểm số theo thời gian, giúp theo dõi sự tiến bộ của AI Agent.
- **Cảnh báo tự động:** Thiết lập điều kiện (If node) nếu điểm số tương đồng dưới mức 0.7 thì tự động gửi báo cáo chi tiết để kỹ sư AI kiểm tra lại prompt.

### 📌 Kết luận
Việc kiểm thử định lượng chất lượng AI không còn là bài toán khó khi đã có sẵn bộ công cụ Evaluations trong n8n kết hợp cùng template Answer Similarity này. Hãy áp dụng ngay vào quy trình phát triển AI Agent của các sếp để nâng tầm chất lượng sản phẩm lên mức chuyên nghiệp nhất!