---
title: "🚀 Tự động Tạo và Tối ưu Câu chuyện Thương hiệu với Ollama LLMs và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống AI Agent hoàn toàn miễn phí trên n8n để tự động sáng tạo, đánh giá và lưu trữ câu chuyện thương hiệu sử dụng Ollama và Google Sheets."
slug: "tao-va-toi-uu-cau-chuyen-thuong-hieu-voi-ollama-va-google-sheets"
tags: [n8n, automation, no-code, AI, Marketing, Ollama, Google Sheets]
keywords: [n8n workflow, brand story, Ollama LLM, Google Sheets automation, AI Agent, marketing automation]
---

# 🚀 Tự động Tạo và Tối ưu Câu chuyện Thương hiệu với Ollama LLMs và Google Sheets

Trong thời đại số, việc xây dựng một câu chuyện thương hiệu (Brand Story) hấp dẫn là chìa khóa sống còn để chạm đến trái tim khách hàng. Tuy nhiên, quá trình nghĩ ý tưởng, viết nháp, đánh giá rồi chỉnh sửa thường ngốn rất nhiều thời gian và công sức của đội ngũ marketing.

Được thiết kế bởi chuyên gia AI **Aashit Sharma**, workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách kết hợp sức mạnh của **AI Agent**, mô hình ngôn ngữ chạy cục bộ **Ollama** và **Google Sheets**. Hệ thống tự động hóa này không chỉ viết bài mà còn tự đánh giá, tối ưu và lưu trữ kết quả một cách mượt mà mà không tốn một đồng chi phí API nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Từ khâu nhận yêu cầu ý tưởng, viết câu chuyện thương hiệu, kiểm tra chất lượng đến lưu trữ.
- **Tiết kiệm chi phí tối đa:** Sử dụng Ollama chạy local (hoặc qua server riêng), không tốn tiền mua token từ OpenAI hay Anthropic.
- **Quy trình khép kín thông minh:** Tích hợp cơ chế Agent tự đánh giá (Evaluation Check) và tối ưu nội dung trước khi xuất bản.
- **Đồng bộ dữ liệu mượt mà:** Mọi câu chuyện hoàn thiện đều được lưu tự động vào Google Sheets để đội ngũ dễ dàng kiểm duyệt và sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted trên VPS).
- **Ollama:** Đã cài đặt Ollama trên máy tính cá nhân hoặc VPS kèm theo các mô hình ngôn ngữ (như Llama 3, Mistral...).
- **Google Account:** Tài khoản Google để kết nối và ghi dữ liệu vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chủ n8n (Link gốc: [n.io/workflows/4765](https://n.io/workflows/4765)), sau đó chọn **Import from File** hoặc copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình kỹ các node sau trong danh sách 9 nodes của workflow:

- **Chat Input: Start Story Flow (`chatTrigger`):** Điểm khởi đầu để người dùng nhập yêu cầu hoặc chủ đề thương hiệu cần viết.
- **Set Brand variable (`set`):** Node dùng để thiết lập các biến môi trường hoặc thông tin cốt lõi của thương hiệu (như tên, lĩnh vực, tone of voice). Hãy tuỳ chỉnh lại cho phù hợp với doanh nghiệp của mình.
- **Ollama Chat Model & Ollama Chat Model1 (`lmChatOllama`):** Kết nối tới server Ollama của các sếp. Đảm bảo cấu hình đúng URL của Ollama (ví dụ: `http://localhost:11434` hoặc IP của VPS chạy Ollama) và chọn đúng tên mô hình (Model Name).
- **Brand Storytelling Agent, Evaluator Agent, Optimizer Agent (`agent`):** Các AI Agent thực hiện nhiệm vụ sáng tác, đóng vai trò chuyên gia đánh giá và tối ưu hóa nội dung câu chuyện.
- **Evaluation Check (`if`):** Node điều kiện kiểm tra xem câu chuyện thương hiệu đã đạt chuẩn chất lượng chưa trước khi đi tới bước lưu trữ.
- **Save Brand Story to Sheets (`googleSheets`):** Kết nối tài khoản Google của các sếp, chọn đúng file Google Sheets và Sheet Name để hệ thống tự động ghi lại các câu chuyện thương hiệu đã hoàn thiện.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhập yêu cầu ở node chat trigger để kiểm tra xem AI phản hồi có chính xác không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau node Google Sheets để gửi thông báo ngay cho sếp hoặc team content mỗi khi có một câu chuyện thương hiệu mới được tạo xong.
- **Mở rộng nguồn dữ liệu:** Thay vì nhập tay qua Chat Input, các sếp có thể kết nối node Google Forms hoặc Webhook từ website để tự động nhận yêu cầu sáng tạo nội dung từ các phòng ban khác.
- **Lưu lịch sử prompt:** Tinh chỉnh lại node Google Sheets để lưu lại cả lịch sử các lần tối ưu (iteration logs) nhằm phục vụ việc phân tích và cải tiến prompt về sau.

### 📌 Kết luận
Workflow **Generate & Optimize Brand Stories with Ollama LLMs and Google Sheets** là một giải pháp mẫu mực cho việc ứng dụng AI mã nguồn mở vào marketing doanh nghiệp. Không tốn phí API, hoàn toàn làm chủ dữ liệu và tự động hóa khép kín — hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa sức sáng tạo của đội ngũ ngay hôm nay!