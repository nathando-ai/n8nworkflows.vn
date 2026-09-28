---
title: "🚀 Đánh giá độ chính xác của AI Agent tự động với n8n và OpenAI (Correctness Metric)"
description: "Hướng dẫn xây dựng hệ thống tự động đánh giá độ chính xác (Correctness) của AI Agent dựa trên dữ liệu mẫu bằng n8n, giúp tối ưu hóa chất lượng câu trả lời."
slug: "danh-gia-do-chinh-xac-ai-agent-n8n-openai"
tags: [n8n, automation, ai-agent, openai, workflow-evaluation, no-code]
keywords: [n8n workflow, đánh giá ai agent, correctness metric, tự động hóa n8n, openai gpt-4o-mini]
---

# 🚀 Đánh giá độ chính xác của AI Agent tự động với n8n và OpenAI (Correctness Metric)

Các sếp có bao giờ đau đầu khi xây dựng các ứng dụng AI Agent hay chatbot nhưng không biết làm sao để kiểm tra xem câu trả lời của AI có thực sự chính xác so với kỳ vọng hay không? Việc kiểm thử thủ công từng câu hỏi vừa tốn thời gian, vừa chủ quan và không thể scale khi dữ liệu lớn.

Workflow này do tác giả **David Roberts** thiết kế sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa việc chấm điểm độ chính xác (**Correctness**) của AI Agent dựa trên tập dữ liệu mẫu (dataset) thông qua OpenAI. Toàn bộ quy trình hoàn toàn tự động, giúp các sếp tiết kiệm thời gian và chi phí tối đa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đánh giá:** So sánh tự động câu trả lời của AI Agent với đáp án mẫu (reference answers) xem có cùng ý nghĩa hay không.
- **Tối ưu chi phí:** Chỉ kích hoạt tính năng tính toán metrics khi hệ thống thực sự trong quá trình đánh giá (Evaluating), tránh lãng phí API token không cần thiết.
- **Tiêu chuẩn hóa chất lượng:** Dễ dàng đo lường độ chính xác của các mô hình LLM trước khi đưa vào ứng dụng thực tế.
- **Linh hoạt mở rộng:** Dựa trên cấu trúc này, các sếp có thể thay đổi tập dữ liệu (dataset) và các tiêu chí đánh giá khác nhau tùy theo nhu cầu doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (để cấu hình cho model `gpt-4o-mini` và node tính toán metric).
- **Google Sheets Credentials (OAuth2 API):** Để kết nối và đọc tập dữ liệu câu hỏi/đáp án mẫu từ Google Sheets.
- **Test Dataset:** [Tham khảo cấu trúc dataset mẫu tại đây](https://docs.google.com/spreadsheets/d/1uuPS5cHtSNZ6HNLOi75A2m8nVWZrdBZ_Ivf58osDAS8/edit?gid=662663849#gid=662663849).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy đoạn JSON của workflow này hoặc tải file từ nguồn gốc.
- Vào giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:
- **When fetching a dataset row (`evaluationTrigger`):** Kết nối với tài khoản Google Sheets của các sếp và trỏ tới file dataset mẫu chứa danh sách câu hỏi về sự kiện lịch sử.
- **OpenAI Chat Model (`lmChatOpenAi`):** Chọn model `gpt-4o-mini` và điền OpenAI API Credentials của các sếp. Node này cung cấp "bộ não" cho **AI Agent**.
- **Calculate correctness metric (`openAi`):** Node này chịu trách nhiệm chấm điểm xem câu trả lời của AI có cùng ý nghĩa với đáp án chuẩn hay không. Các sếp nhớ chọn đúng Credentials của OpenAI ở đây.
- **Evaluating? (`evaluation` - `checkIfEvaluating`) & Set metrics (`evaluation` - `setMetrics`):** Đảm bảo các node evaluation hoạt động đúng logic lọc điều kiện đánh giá để tiết kiệm chi phí gọi API.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách bấm nút `Execute Workflow` để kiểm tra quá trình đọc dataset và AI chấm điểm hoạt động trơn tru.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** vào cuối workflow để nhận báo cáo tổng kết điểm số Correctness ngay lập tức sau mỗi lần chạy đánh giá.
- **Lưu lịch sử đánh giá:** Lưu kết quả trả về từ node `Set metrics` ngược lại vào một sheet khác trong Google Sheets để theo dõi sự tiến bộ (hoặc suy giảm) chất lượng của AI Agent qua thời gian.
- **Đa dạng hóa Metric:** Tham khảo thêm tài liệu chính thức của n8n về [Evaluation Metrics](https://docs.n8n.io/advanced-ai/evaluations/metric-based-evaluations/#2-calculate-metrics) để bổ sung thêm các chỉ số đánh giá khác như độ liên quan, tính trung thực...

### 📌 Kết luận
Việc đánh giá chất lượng AI Agent không còn là bài toán phức tạp nhờ workflow tự động hóa này trên n8n. Hãy áp dụng ngay vào dự án của các sếp để kiểm soát tốt chất lượng câu trả lời của AI, mang lại trải nghiệm tuyệt vời nhất cho người dùng!