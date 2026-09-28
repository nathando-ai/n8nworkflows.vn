---
title: "🚀 Tự động giám sát Google Reviews và soạn phản hồi bằng AI Gemini kết hợp Slack"
description: "Hướng dẫn cấu hình workflow n8n tự động theo dõi đánh giá Google hàng giờ, phân tích cảm xúc bằng Gemini AI, lưu trữ Google Sheets và cảnh báo Slack."
slug: "tu-dong-giam-sat-google-reviews-gemini-slack"
tags: [n8n, automation, ai-summarization, google-reviews, gemini, slack, google-sheets]
keywords: [n8n workflow, tự động hóa google reviews, gemini ai, slack alert, quản lý đánh giá khách hàng]
---

# 🚀 Tự động giám sát Google Reviews và soạn phản hồi bằng AI Gemini kết hợp Slack

Việc theo dõi thủ công các đánh giá của khách hàng trên Google Maps/Google Business Profile mỗi ngày là một công việc tẻ nhạt nhưng cực kỳ quan trọng. Nếu bỏ quên các đánh giá tiêu cực, doanh nghiệp có thể mất đi cơ hội giữ chân khách hàng. 

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n hoàn toàn tự động giúp giải quyết triệt để bài toán trên: tự động quét đánh giá mỗi giờ, sử dụng Gemini AI để phân tích cảm xúc, soạn sẵn câu trả lời chuyên nghiệp, lưu trữ lịch sử vào Google Sheets, đồng thời gửi cảnh báo tức thì qua Slack cho đánh giá xấu và tổng hợp báo cáo qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian** kiểm tra và phân loại đánh giá thủ công mỗi ngày.
- **Phản hồi khách hàng chớp nhoáng & lịch sự** nhờ AI Gemini tự động viết bản thảo câu trả lời phù hợp với sắc thái đánh giá.
- **Không bỏ lỡ khủng hoảng truyền thông**: Đánh giá dưới 3 sao sẽ bắn chuông báo động ngay lập tức lên kênh Slack của đội ngũ CSKH/Quản lý.
- **Lưu trữ minh bạch**: Mọi dữ liệu đánh giá được đồng bộ tự động vào Google Sheets để phục vụ phân tích dài hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Cloud Platform (GCP)**: API Key cho Google Places API.
- **Google Gemini API Key** (hoặc kết nối Google Gemini thông qua LangChain node).
- **Tài khoản Google Sheets & Google Drive** (để lưu dữ liệu đánh giá).
- **Slack Workspace** (kênh nhận cảnh báo đánh giá tiêu cực).
- **Gmail Account / Credentials** (để gửi báo cáo tổng hợp hằng ngày).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào n8n Editor của các sếp bằng cách chọn **New workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau để hệ thống chạy mượt mà:

- **Setup Variables (Node `set`)**: Khai báo Google Maps Place ID của doanh nghiệp các sếp tại đây để hệ thống biết cần quét đánh giá của địa điểm nào.
- **Get Google Reviews (Node `httpRequest`)**: Cấu hình sử dụng Google Maps API Key thông qua HTTP Header Auth để gọi dữ liệu từ Google Places API theo lịch hẹn.
- **Google Gemini Chat Model & Sentiment Analysis & Draft Response (Nodes `chainLlm` & `lmChatGoogleGemini`)**: Kết nối API Key của Google Gemini. AI sẽ đọc từng đánh giá, chấm điểm cảm xúc từ 1-5 và viết bản thảo phản hồi lịch sự.
- **Log to Google Sheets (Node `googleSheets`)**: Chọn file Google Spreadsheet và cấu hình thao tác `appendOrUpdate` để lưu lại toàn bộ lịch sử review, điểm số và câu trả lời nháp của AI.
- **Filter Negative Reviews & Send Slack Alert (Nodes `filter` & `slack`)**: Thiết lập điều kiện lọc (ví dụ: điểm số < 3) và chọn kênh Slack (Slack Channel) để nhận cảnh báo khẩn cấp.
- **Email Daily Summary (Node `gmail`)**: Điền địa chỉ email của chủ doanh nghiệp hoặc quản lý để nhận báo cáo tổng hợp định kỳ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử nghiệm (Test run) với dữ liệu mẫu để kiểm tra kết nối các API (Google, Gemini, Slack, Gmail).
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động hoạt động 24/7 theo lịch trình của node **Review Check Schedule**.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Ngoài Slack, các sếp có thể kết hợp thêm node Telegram hoặc Zalo ZNS để bắn thông báo đánh giá tiêu cực cho quản lý nhanh hơn.
- **Tự động hóa phản hồi**: Nếu tin tưởng vào AI, các sếp có thể tích hợp thêm bước tự động đăng câu trả lời của Gemini lên Google My Business (nếu có API hỗ trợ).
- **Lưu log lỗi (Error Handling)**: Thêm Error Trigger vào workflow để nhận cảnh báo qua email nếu quá trình gọi API Google Maps hoặc Gemini gặp sự cố.

### 📌 Kết luận
Workflow tự động hóa giám sát Google Reviews kết hợp Gemini AI và Slack là một trợ thủ đắc lực giúp doanh nghiệp nâng cao chất lượng dịch vụ khách hàng, xử lý khủng hoảng truyền thông kịp thời mà không tốn nhiều nhân lực. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho doanh nghiệp của các sếp!