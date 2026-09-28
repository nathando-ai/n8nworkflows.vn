---
title: "🚀 Đánh giá độ chính xác sử dụng công cụ trong Multi-Agent AI với n8n Evaluation Nodes"
description: "Hướng dẫn xây dựng hệ thống tự động đánh giá (Evaluation) hiệu suất gọi tool của Multi-Agent AI workflows bằng n8n, đảm bảo AI dùng đúng công cụ, đúng thời điểm."
slug: "danh-gia-do-chinh-xac-su-dung-cong-cu-multi-agent-ai-n8n"
tags: [n8n, automation, no-code, ai-agent, openrouter, evaluation]
keywords: [n8n workflow, evaluation nodes, multi-agent AI, tự động hóa, openrouter, qdrant, ai agent accuracy]
---

# 🚀 Đánh giá độ chính xác sử dụng công cụ trong Multi-Agent AI với n8n Evaluation Nodes

Các sếp khi xây dựng hệ thống trợ lý ảo thông minh (Multi-Agent AI) thường gặp phải một nỗi đau lớn: AI đôi khi "nhiệt tình hơn năng lực", tự ý gọi nhầm tool, gọi lặp lại hoặc phớt lờ các công cụ chuyên biệt mà chúng ta đã vất vả cấu hình. Việc kiểm tra thủ công từng câu trả lời của AI để đo lường độ chính xác vừa tốn thời gian vừa kém khách quan.

Được thiết kế bởi chuyên gia Angel Menendez từ n8n, workflow này sinh ra để giải quyết triệt để bài toán trên. Nó tận dụng sức mạnh của các **Evaluation Nodes** kết hợp cùng mô hình ngôn ngữ cao cấp qua OpenRouter để tự động hóa việc chấm điểm, kiểm tra hành vi gọi tool của AI một cách chuẩn xác 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn quy trình kiểm thử:** Đánh giá hàng loạt tập dữ liệu (dataset) câu hỏi và hành vi gọi tool của Agent mà không cần con người can thiệp thủ công.
- **Tối ưu hóa Prompt & Agent:** Biết chính xác Agent đang dùng sai tool nào, thiếu sót ở điểm nào để tinh chỉnh prompt kịp thời.
- **Tích hợp linh hoạt:** Kết hợp mượt mà các mô hình AI mạnh mẽ (OpenRouter, OpenAI Embeddings) cùng kho dữ liệu Vector (Qdrant) và công cụ tìm kiếm bên ngoài.
- **Đo lường trực quan:** Xuất kết quả đánh giá chi tiết lưu trực tiếp vào Google Sheets để dễ dàng theo dõi và báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Tài khoản n8n** (phiên bản hỗ trợ AI Agent và Evaluation nodes).
- **Google Sheets API / OAuth2 credentials** (để quản lý dataset đánh giá và lưu kết quả).
- **OpenRouter API Key** (dùng cho model `openai/o3` tại node `OpenRouter Chat Model`).
- **OpenAI API Key** (dùng cho `Embeddings OpenAI`).
- **Qdrant API Key & Endpoint** (cho `Search_db` vector store).
- **HTTP Bearer Token** (cho `Web search` tool).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON theo cách truyền thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần chú ý cấu hình các thành phần trọng yếu sau:
- **When fetching a dataset row (`evaluationTrigger`):** Kết nối tài khoản Google Sheets của sếp, trỏ tới file chứa tập dữ liệu test các câu lệnh và công cụ mong đợi.
- **OpenRouter Chat Model:** Chọn credential OpenRouter, đảm bảo model được cấu hình chính xác (`openai/o3` hoặc model tương đương) để AI Agent có tư duy logic tốt nhất khi gọi tool.
- **Search Agent & Các Tools (`Calculator`, `Web search`, `Summarizer`, `Search_db`):** Kiểm tra lại các kết nối API Key tương ứng (Qdrant, OpenAI Embeddings, Web search Bearer Token) để đảm bảo các công cụ con hoạt động trơn tru.
- **Evaluation & Set Outputs:** Cấu hình đúng các thông số metric và trỏ lại file Google Sheets nhận kết quả đánh giá từ node `Set Outputs`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách thủ công kích hoạt `Evaluation Trigger` với một vài dòng dữ liệu mẫu để kiểm tra xem hệ thống có chấm điểm chính xác không.
- Sau khi test thành công và kết quả trả về Google Sheets ngon lành, các sếp bấm nút **Active** để workflow sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay lập tức nếu tỷ lệ chính xác khi gọi tool của Agent rớt xuống dưới mức kỳ vọng (ví dụ: < 80%).
- **Lưu lịch sử chạy:** Mở rộng việc lưu trữ kết quả đánh giá không chỉ ở Google Sheets mà đẩy vào PostgreSQL hoặc Airtable để làm biểu đồ theo dõi hiệu suất theo thời gian.
- **A/B Testing Prompt:** Nhân bản Search Agent thành 2 phiên bản với 2 prompt khác nhau và dùng Evaluation Node để so sánh xem prompt nào giúp AI gọi tool chính xác hơn.

### 📌 Kết luận
Việc kiểm soát chất lượng hành vi của AI Agent là chìa khóa sống còn khi đưa các ứng dụng AI vào thực tế doanh nghiệp. Với workflow đánh giá tự động này, các sếp hoàn toàn có thể yên tâm về độ chính xác và hiệu suất của hệ thống Multi-Agent AI của mình. Triển khai ngay thôi nào!