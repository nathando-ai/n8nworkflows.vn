---
title: "🚀 Đánh giá AI Agent trong n8n: Kiểm tra tool đã được gọi hay chưa"
description: "Hướng dẫn xây dựng hệ thống đánh giá (Evaluation) tự động cho n8n AI Agent để kiểm tra xem một công cụ (tool) cụ thể có được gọi chính xác hay không."
slug: "danh-gia-ai-agent-trong-n8n-kiem-tra-tool"
tags: [n8n, automation, ai-agent, evaluation, openai, langchain]
keywords: [n8n workflow, ai agent evaluation, kiem tra tool ai agent, n8n evaluation metric, tu dong hoa ai]
---

# 🚀 Đánh giá AI Agent trong n8n: Kiểm tra tool đã được gọi hay chưa

Các sếp đang phát triển các ứng dụng AI Agent phức tạp trên n8n nhưng gặp khó khăn trong việc kiểm tra xem Agent có thực thi đúng các công cụ (tools) được giao hay không? Việc kiểm thử thủ công từng câu hỏi tốn rất nhiều thời gian và không đảm bảo độ chính xác khi hệ thống scale lớn.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow mẫu từ tác giả David Roberts, giúp tự động hóa quá trình đánh giá (Evaluation) xem AI Agent có gọi đúng công cụ mong muốn dựa trên tập dữ liệu kiểm thử (test dataset) hay không.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đánh giá:** Chạy hàng loạt các câu hỏi test từ Google Sheets để đo lường hiệu suất của AI Agent.
- **Độ chính xác cao:** Xác định chính xác Agent có gọi đúng công cụ (như Calculator hoặc Fetch a webpage) theo kịch bản hay không.
- **Tiết kiệm thời gian:** Thay vì test thủ công từng prompt, hệ thống tự động chấm điểm và trả về kết quả evaluation chi tiết.
- **Cải tiến liên tục:** Dễ dàng tinh chỉnh prompt và cấu hình agent dựa trên dữ liệu đánh giá thực tế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (hỗ trợ các tính năng Advanced AI và Evaluation).
- **OpenAI API Key:** Để sử dụng model `gpt-4o-mini` cho AI Agent.
- **Google Sheets:** Tài khoản kết nối OAuth2 để đọc tập dữ liệu kiểm thử (test dataset) chứa các câu hỏi và tool mong đợi. Các sếp có thể tham khảo [mẫu dataset tại đây](https://docs.google.com/spreadsheets/d/1uuPS5cHtSNZ6HNLOi75A2m8nVWZrdBZ_Ivf58osDAS8/edit?gid=969651976#gid=969651976).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) -> **Import from File / Clipboard** và dán nội dung vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **OpenAI Chat Model:** Cấu hình credentials OpenAI API của các sếp và chọn model `gpt-4o-mini`.
- **AI Agent Node:** Quan trọng! Các sếp nhớ bật tính năng **'Return intermediate steps'** trong cấu hình của Agent để hệ thống lấy được danh sách các công cụ đã được thực thi (`executed tools`).
- **When fetching a dataset row (Evaluation Trigger):** Kết nối tài khoản Google Sheets OAuth2 và trỏ tới file Google Sheet chứa bộ dữ liệu test mẫu.
- **Check if tool called (Set Node):** Kiểm tra logic xem danh sách các tool được thực thi có chứa tool mục tiêu (`target tool`) hay không.
- **Evaluating? & Evaluation Nodes:** Các node này chịu trách nhiệm kích hoạt chế độ đánh giá và thiết lập các metric đo lường.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Test step` hoặc `Execute workflow`) với một vài dòng dữ liệu mẫu từ dataset.
- Kiểm tra kết quả trả về ở các node Evaluation để đảm bảo metric hoạt động chính xác.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng công cụ:** Thêm các tool hữu ích khác như Slack, Telegram, hoặc truy vấn cơ sở dữ liệu để test khả năng gọi tool đa dạng của Agent.
- **Lưu log kết quả:** Kết nối thêm một node Google Sheets hoặc cơ sở dữ liệu (PostgreSQL/Supabase) để lưu lịch sử các lần chạy evaluation, giúp theo dõi sự thay đổi hiệu suất qua từng phiên bản prompt.
- **Cảnh báo tự động:** Tích hợp gửi thông báo qua Telegram hoặc Slack mỗi khi điểm số evaluation của Agent rớt xuống dưới ngưỡng cho phép.

### 📌 Kết luận
Việc xây dựng hệ thống tự động đánh giá AI Agent với metric kiểm tra tool call là bước đi quan trọng giúp các sếp kiểm soát chất lượng ứng dụng AI trước khi đưa vào sản phẩm thực tế. Hãy áp dụng ngay workflow này vào hệ thống n8n của các sếp nhé!