---
title: "🚀 Tự Động Theo Dõi Brand Mentions Trên X (Twitter) Bằng Google Gemini AI & Gửi Cảnh Báo Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động quét bài đăng trên X, phân tích đa phương thức (text & hình ảnh) bằng Gemini AI, lọc độ liên quan và bắn thông báo tức thì lên Telegram."
slug: "theo-doi-brand-mentions-tren-x-voi-gemini-ai-va-telegram"
tags: [n8n, automation, ai-agent, google-gemini, telegram, airtable, x-twitter]
keywords: [n8n workflow, theo dõi brand mention, google gemini ai, phân tích hình ảnh ai, telegram alert, tự động hóa marketing]
---

# 🚀 Tự Động Theo Dõi Brand Mentions Trên X (Twitter) Bằng Google Gemini AI & Gửi Cảnh Báo Telegram

Các sếp có đang tốn hàng giờ mỗi ngày để lướt X (Twitter) thủ công chỉ để tìm xem khách hàng đang nói gì về thương hiệu của mình? Việc bỏ lỡ các phản hồi (mentions) quan trọng – dù là khen ngợi hay phàn nàn – đều có thể làm giảm uy tín thương hiệu và bỏ lỡ cơ hội chăm sóc khách hàng vàng.

Workflow n8n tuyệt vời này sẽ giải quyết triệt để bài toán đó cho các sếp. Nó tự động hóa 100% quy trình: Quét bài viết trên X, dùng sức mạnh đa phương thức (Multimodal) của **Google Gemini AI** để đọc hiểu cả nội dung chữ lẫn hình ảnh đính kèm, đánh giá mức độ liên quan, lưu trữ dữ liệu vào **Airtable** và bắn thông báo ngay lập tức lên **Telegram** nếu phát hiện bài viết quan trọng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt trọn mọi thông tin:** Tự động quét từ khóa/thương hiệu liên tục theo lịch trình hoặc kích hoạt thủ công.
- **AI thông minh đa chiều:** Không chỉ đọc text, Gemini AI còn phân tích cả hình ảnh đính kèm trong bài viết để đánh giá chính xác sắc thái (sentiment) và ngữ cảnh.
- **Phân loại tự động:** Tự chia độ liên quan thành 3 mức (High, Medium, Not Relevant) để biết chính xác khi nào cần can thiệp xử lý khủng hoảng hoặc tương tác.
- **Cảnh báo tức thời:** Bắn tin nhắn trực tiếp vào nhóm Telegram khi có bài viết "High Relevance" để team xử lý ngay lập tức.
- **Lưu trữ bài bản:** Tự động ghi log toàn bộ vào Airtable để làm báo cáo và đo lường định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Google Gemini API Key** (Dùng cho các node Google Gemini và LangChain Agent).
- **X (Twitter) Scraping API / HTTP API** (Cấu hình trong node `Scrape X`).
- **Airtable Account & Token** (Để lưu trữ dữ liệu bài viết đã quét).
- **Telegram Bot Token & Chat ID** (Để gửi thông báo tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n, sau đó tại giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào biểu tượng menu (dấu ba chấm) -> **Import from File** và tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Node `Config` & `Scrape X` (HTTP Request):** Cấu hình từ khóa thương hiệu cần theo dõi (`brand name`, `keywords`) và kết nối API Token tại mục Credentials (`httpBearerAuth`).
- **Node `Analyze Text and Photos` (AI Agent) & `Google Gemini Chat Model`:** Cấu hình **Google Gemini API Key** (`googlePalmApi`). Đảm bảo model được chọn hỗ trợ phân tích hình ảnh (multimodal) như Gemini 1.5 Pro hoặc Flash.
- **Node `Structured Output Parser`:** Thiết lập schema chuẩn để AI trả về điểm số liên quan (relevance score từ 1-10) và tóm tắt trạng thái sắc thái (sentiment).
- **Node `Post Exists`, `Log the Medium Relevance Post`, `Log the High Relevance Post` (Airtable):** Kết nối tài khoản Airtable (`airtableTokenApi`), trỏ tới Base và Table dùng để lưu log bài viết.
- **Node `Send High Relevance Post to Monitoring Group` (Telegram):** Kết nối Telegram Bot (`telegramApi`) và điền Chat ID của group/channel nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử bằng `Manual Executing` hoặc `Schedule Trigger` để kiểm tra luồng dữ liệu mẫu.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh thông báo:** Ngoài Telegram, các sếp có thể nhân bản node thông báo để đẩy tin sang Slack hoặc Microsoft Teams của team Marketing.
- **Auto-Reply thông minh:** Kết hợp thêm node viết bình luận tự động bằng AI khi phát hiện bài viết có điểm liên quan cao và sắc thái tích cực.
- **Lọc trùng lặp thông minh:** Node `Post Exists` (Airtable) trong workflow đã giúp chặn việc quét trùng bài cũ, các sếp có thể tối ưu thêm thời gian quét (Schedule Trigger) tùy theo lưu lượng bài viết thực tế trên X.

### 📌 Kết luận
Với workflow n8n tích hợp Gemini AI này, việc lắng nghe mạng xã hội (Social Listening) không còn là nỗi ác mộng tốn kém nhân sự và thời gian. Hãy "lên đồ" ngay cho hệ thống của mình để nắm thế chủ động trong mọi chiến dịch truyền thông!