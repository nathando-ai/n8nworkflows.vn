---
title: "🚀 Tự động trích xuất thông tin tài chính từ Google News và gửi cảnh báo Slack bằng Gemini Pro"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động lấy tin tức báo cáo thu nhập từ Google News RSS, sử dụng AI Gemini Pro để phân tích và gửi cảnh báo thông minh qua Slack."
slug: "tu-dong-trich-xuat-thong-tin-tai-chinh-google-news-gemini-slack"
tags: [n8n, automation, ai-summarization, google-gemini, slack, finance]
keywords: [n8n workflow, trích xuất thông tin tài chính, google news rss, gemini pro, slack automation, ai summarization]
keywords: [n8n workflow, tự động hóa, google news rss, gemini pro, slack, financial analysis]
---

# 🚀 Tự động trích xuất thông tin tài chính từ Google News và gửi cảnh báo Slack bằng Gemini Pro

Các sếp làm trong lĩnh vực tài chính, đầu tư hay crypto chắc chắn hiểu cảm giác mệt mỏi khi phải thủ công lướt hàng đống tin tức báo cáo thu nhập (earnings reports), đọc từng bài báo dài dằng dặc để tìm ra doanh thu, hướng dẫn (guidance) hay các bất ngờ về lợi nhuận. Việc này không tốn thời gian mà còn dễ bỏ lỡ các cơ hội giao dịch quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ thay các sếp làm toàn bộ công việc nặng nhọc đó: Tự động gom tin tức từ Google News RSS, dùng trí tuệ nhân tạo **Gemini Pro** để phân tích, lọc ra các thông tin thực sự có giá trị cao (High-Signal) và bắn thẳng cảnh báo gọn gàng lên **Slack**!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần đọc thủ công hàng chục bài báo cáo mỗi ngày.
- **Phân tích chuẩn xác bằng AI:** Gemini Pro tự động trích xuất các chỉ số cốt lõi như Doanh thu (Revenue), Hướng dẫn (Guidance) và các khoản bất ngờ (Surprises).
- **Chống "ngợp" thông tin (Alert Fatigue):** Bộ lọc thông minh chỉ gửi tin khi có dữ liệu tài chính thực sự chất lượng, loại bỏ các thông báo họp báo chung chung.
- **Lưu trữ tự động:** Mọi kết quả phân tích đều được ghi lại vào Database để dễ dàng tra cứu về sau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google AI API Key** (cho node Gemini Pro).
- **Slack Workspace** và quyền tạo Bot/Webhook để gửi tin nhắn vào kênh chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc import file JSON gốc từ nguồn) vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành 3 tầng xử lý chính, các sếp cần cấu hình kỹ các node sau:

- **Node `Fetch: Google News RSS` (HTTP Request):** 
  - Cần cập nhật tham số truy vấn `q=` trong URL để nhắm mục tiêu vào các công ty hoặc mã cổ phiếu mà các sếp quan tâm (ví dụ: Apple, Tesla, Bitcoin...).
- **Node `Model: Gemini Pro`:** 
  - Chọn hoặc thêm mới credentials `googlePalmApi`, sau đó điền Google AI API Key của các sếp vào.
- **Node `Send a message` (Slack):** 
  - Kết nối tài khoản Slack của các sếp (`slackApi`) và chọn kênh (channel) đích sẽ nhận thông báo.
- **Node `Database: Log Results` (Data Table):** 
  - Map các trường dữ liệu từ node `Formatter: Clean AI Output` khớp với các cột trong bảng dữ liệu n8n của các sếp để ghi log chính xác.

#### 3. Kích hoạt ⚡️
- Bấm nút **`Start: Manual Trigger`** để chạy thử (Test run) với dữ liệu mẫu xem hệ thống gom tin và AI phản hồi thế nào.
- Sau khi kiểm tra mọi thứ mượt mà, hãy gạt công tắc sang **Active** để workflow chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể tùy biến:
1. **Thay thế Trigger thủ công:** Đổi node `Manual Trigger` thành `Schedule Trigger` để n8n tự động quét tin tức mỗi sáng lúc 8:00 AM.
2. **Đa kênh thông báo:** Kết hợp thêm node Telegram hoặc Discord bên cạnh Slack để đội ngũ nhận tin ở bất cứ đâu.
3. **Mở rộng bộ lọc AI:** Tinh chỉnh Prompt trong node `Prompt Builder: Financial Analyst` để yêu cầu AI phân tích thêm về xu hướng thị trường hoặc tâm lý nhà đầu tư (Market Sentiment).

### 📌 Kết luận
Một workflow cực kỳ thực chiến giúp tự động hóa hoàn toàn quy trình cập nhật tin tức tài chính. Hãy triển khai ngay hôm nay để không bỏ lỡ bất kỳ tin tức đắt giá nào từ thị trường!