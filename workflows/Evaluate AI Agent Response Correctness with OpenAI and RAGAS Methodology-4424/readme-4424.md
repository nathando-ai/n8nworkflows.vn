---
title: "🚀 Đánh Giá Độ Chính Xác Phản Hồi Của AI Agent Với OpenAI Và Phương Pháp RAGAS Trong n8n"
description: "Hướng dẫn xây dựng hệ thống tự động đánh giá độ chính xác câu trả lời của AI Agent dựa trên phương pháp RAGAS và OpenAI GPT-4.1-mini thông qua n8n."
slug: "danh-gia-do-chinh-xac-ai-agent-ragas-openai"
tags: [n8n, automation, ai-agent, openai, ragas, evaluation]
keywords: [n8n workflow, đánh giá AI agent, RAGAS methodology, OpenAI API, tự động hóa n8n, tính F1 score]
---

# 🚀 Đánh Giá Độ Chính Xác Phản Hồi Của AI Agent Với OpenAI Và Phương Pháp RAGAS Trong n8n

Việc phát triển các ứng dụng AI Agent thường gặp một thử thách lớn: Làm thế nào để biết câu trả lời của AI có chính xác, trung thực và đúng với thực tế dữ liệu (Ground Truth) hay không? Việc kiểm thử thủ công từng câu hỏi là vô cùng tốn thời gian và thiếu khách quan. 

Workflow n8n tuyệt vời này từ tác giả **Jimleuk** sẽ giúp các sếp tự động hóa toàn bộ quá trình đánh giá độ chính xác phản hồi của AI Agent dựa trên phương pháp **RAGAS (Retrieval Augmented Generation Assessment)** nổi tiếng, kết hợp sức mạnh của OpenAI GPT-4.1-mini.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn quy trình đánh giá:** Chấm điểm hàng loạt câu trả lời của AI Agent từ Google Sheets mà không cần thao tác thủ công.
- **Phương pháp chuẩn quốc tế:** Áp dụng mô hình RAGAS chia câu trả lời thành các nhóm True Positive, False Positive, False Negative kết hợp tính điểm Similarity Score và F1 Score.
- **Cải thiện chất lượng AI:** Phát hiện chính xác liệu AI Agent đang bịa đặt thông tin (hallucination) hay dữ liệu huấn luyện có vấn đề.
- **Tách biệt môi trường:** Sử dụng `Evaluation Trigger` chạy độc lập, không làm ảnh hưởng đến luồng Production chính của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n version:** Phiên bản 1.94 trở lên.
- **OpenAI API Key:** Để kết nối với các node `OpenAI Chat Model` (sử dụng model `gpt-4.1-mini`) và gọi Embeddings.
- **Google Sheets account:** Để lưu trữ dataset câu hỏi mẫu, ground truth và kết quả đánh giá. Tham khảo [Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1YOnu2JJjlxd787AuYcg-wKbkjyjyZFgASYVV0jsij5Y/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn dấu ba chấm ở góc trên bên phải -> **Import from File / Clipboard** và dán nội dung vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thành phần trọng yếu sau trong workflow:
- **OpenAI Chat Model & OpenAI Chat Model1:** Thêm credential `openAiApi` của các sếp vào các node này. Đảm bảo model được cấu hình là `gpt-4.1-mini` để tối ưu chi phí và tốc độ.
- **When fetching a dataset row (Evaluation Trigger):** Kết nối tài khoản Google Sheets của các sếp (`googleSheetsOAuth2Api`) và trỏ tới file Google Sheet chứa dataset cần đánh giá.
- **Get Embeddings & Get Embeddings1 (HTTP Request):** Kiểm tra cấu hình kết nối tới OpenAI API để tạo vector embedding phục vụ việc tính toán độ tương đồng (Similarity Score).
- **Update Outputs:** Đảm bảo node này trỏ đúng đến Google Sheet ghi nhận kết quả điểm số đánh giá (Evaluation Metrics) trả về sau mỗi lần chạy test.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại trigger đánh giá để chạy thử nghiệm với tập dữ liệu mẫu.
- Kiểm tra kết quả trả về ở các node tính toán như `Calculate F1 Score`, `Correctness Score` và Google Sheets.
- Khi mọi thứ hoạt động mượt mà, bật công tắc **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Slack/Telegram:** Thêm node gửi tin nhắn để nhận báo cáo tổng kết điểm số Correctness ngay sau khi quá trình đánh giá hoàn tất.
- **Lưu trữ lịch sử đánh giá:** Lưu log điểm số theo thời gian vào cơ sở dữ liệu (PostgreSQL/Supabase) để theo dõi xu hướng cải thiện chất lượng của AI Agent.
- **Mở rộng tập dữ liệu:** Thêm hàng trăm kịch bản test case vào Google Sheet để kiểm tra độ bền vững (robustness) của AI Agent trước khi đưa lên production.

### 📌 Kết luận
Việc kiểm thử và đánh giá AI Agent không còn là nỗi ác mộng thủ công nhờ vào template n8n tích hợp phương pháp RAGAS này. Hãy áp dụng ngay vào hệ thống của các sếp để đảm bảo các trợ lý ảo luôn cung cấp thông tin chính xác và đáng tin cậy nhất cho khách hàng!