---
title: "🚀 Đánh giá hiệu suất AI Agent phân loại ticket tự động trong n8n"
description: "Hướng dẫn cấu hình workflow n8n sử dụng Evaluation metric để đo lường độ chính xác của AI Agent khi phân loại ticket hỗ trợ khách hàng."
slug: "danh-gia-hieu-suat-ai-agent-phan-loai-ticket-trong-n8n"
tags: [n8n, automation, no-code, ai-agent, openai, evaluation]
keywords: [n8n workflow, ai agent evaluation, tự động hóa phân loại ticket, đo lường prompt ai, n8n viet nam]
---

# 🚀 Đánh giá hiệu suất AI Agent phân loại ticket tự động

Trong quá trình xây dựng hệ thống AI tự động hóa (như phân loại ticket hỗ trợ khách hàng), việc làm sao để biết AI đang làm tốt đến mức nào là một bài toán khó. Nếu kiểm tra thủ công từng kết quả, các sếp sẽ mất rất nhiều thời gian. Workflow này sẽ giúp tự động hóa toàn bộ quy trình đo lường độ chính xác của AI Agent dựa trên tập dữ liệu mẫu (dataset) có sẵn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đo lường**: Tự động so sánh kết quả phân loại (category/priority) của AI Agent với đáp án chuẩn trong dataset.
- **Tối ưu Prompt hiệu quả**: Dễ dàng kiểm tra xem các thay đổi về prompt hoặc model (GPT-4o-mini) có thực sự cải thiện chất lượng hay không.
- **Tiết kiệm thời gian**: Không cần test thủ công hàng trăm trường hợp, hệ thống tự động chạy và trả về số liệu đánh giá chính xác.
- **Hoạt động liền mạch**: Tích hợp sẵn cơ chế Webhook và Evaluation Trigger linh hoạt cho cả môi trường test lẫn production.
:::

### 📦 Các thành phần chính trong Workflow
1. **AI Agent & OpenAI Chat Model (`gpt-4o-mini`)**: Xử lý nội dung ticket đầu vào và đưa ra kết quả phân loại.
2. **Structured Output Parser**: Đảm bảo AI trả về định dạng cấu trúc chuẩn xác.
3. **Evaluation Nodes (`Evaluating?`, `Set metrics`, `When fetching a dataset row`)**: Bộ công cụ đánh giá chuyên sâu của n8n, dùng để kết nối với dataset và tính toán điểm số metric.
4. **Webhook & Respond to Webhook**: Nhận dữ liệu ticket từ bên ngoài và trả về kết quả qua API.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt n8n (phiên bản hỗ trợ Advanced AI / Evaluations).
- **OpenAI API Key**: Để kết nối với mô hình `gpt-4o-mini`.
- **Google Sheets Credentials**: Tài khoản Google OAuth2 để n8n đọc dữ liệu từ [test dataset mẫu](https://docs.google.com/spreadsheets/d/1uuPS5cHtSNZ6HNLOi75A2m8nVWZrdBZ_Ivf58osDAS8/edit?gid=294497137#gid=294497137).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n chọn **New Workflow**, nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **OpenAI Chat Model**: Chọn lại Credential OpenAI của các sếp và đảm bảo model đang dùng là `gpt-4o-mini` (hoặc model tùy chỉnh khác).
- **When fetching a dataset row**: Kết nối với tài khoản Google Sheets OAuth2 và trỏ tới file Google Sheet chứa bộ dữ liệu test mẫu.
- **Kiểm tra logic đánh giá**: Xem xét các node `Check categorization` và `Evaluating?` để đảm bảo các trường dữ liệu so sánh (category/priority) khớp với cấu trúc cột trong Google Sheet của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) bằng cách nạp một dòng dữ liệu từ dataset hoặc gọi thử qua Webhook.
- Kiểm tra kết quả trả về ở các node evaluation để đảm bảo metric tính toán chính xác.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng Metric**: Ngoài việc kiểm tra category khớp hay không, các sếp có thể viết thêm logic check độ dài phản hồi hoặc thời gian xử lý của AI.
- **Tích hợp thông báo**: Kết nối thêm node Slack hoặc Telegram để nhận báo cáo tự động mỗi khi chạy xong một tiến trình evaluation dataset lớn.
- **Lưu log kết quả**: Đẩy kết quả đánh giá ngược lại vào một sheet Google Sheets khác để vẽ biểu đồ theo dõi hiệu suất AI theo thời gian.

### 📌 Kết luận
Việc đo lường chất lượng AI không còn là mò kim đáy bể với các tính năng Evaluation mạnh mẽ của n8n. Hãy áp dụng ngay workflow này để tối ưu hóa hệ thống tự động hóa chăm sóc khách hàng của doanh nghiệp các sếp nhé!