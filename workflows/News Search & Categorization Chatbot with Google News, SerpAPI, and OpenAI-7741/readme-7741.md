---
title: "🚀 Xây dựng Chatbot tra cứu và phân loại tin tức tự động với Google News, SerpApi và OpenAI trên n8n"
description: "Hướng dẫn chi tiết cách tạo trợ lý AI trò chuyện trực tiếp với Google News, tự động tìm kiếm, tổng hợp và phân loại thông tin chuẩn xác bằng OpenAI và SerpApi."
slug: "chatbot-tra-cuu-va-phan-loai-tin-tuc-google-news-openai"
tags: [n8n, automation, no-code, ai-chatbot, openai, serpapi]
keywords: [n8n workflow, chatbot google news, serpapi n8n, openai langchain n8n, tự động hóa tin tức]
---

# 🚀 Xây dựng Chatbot tra cứu và phân loại tin tức tự động với Google News, SerpApi và OpenAI

Các sếp có bao giờ cảm thấy ngợp trước hàng ngàn thông tin, tin tức cập nhật từng phút trên internet và mất quá nhiều thời gian để tìm kiếm, tổng hợp, lọc ra các bài viết thực sự hữu ích cho công việc? Việc tra cứu thủ công vừa tốn thời gian, lại thiếu hệ thống.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một **AI Chatbot thông minh** bằng n8n. Workflow này cho phép trò chuyện trực tiếp, tự động truy vấn Google News qua SerpApi, sau đó sử dụng sức mạnh của OpenAI để tóm tắt và phân loại thông tin theo đúng ý muốn của các sếp hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu thời gian thực:** Truy vấn trực tiếp các bài báo mới nhất từ Google News dựa trên câu hỏi của người dùng.
- **Tổng hợp & Phân loại thông minh:** AI tự động đọc, lọc kết quả, tóm tắt và phân loại mạch lạc nhờ tích hợp mô hình OpenAI tiên tiến.
- **Giao diện trò chuyện trực quan:** Sử dụng Chat Trigger và Memory Buffer Window giúp chatbot duy trì ngữ cảnh xuyên suốt cuộc hội thoại.
- **Tiết kiệm 90% thời gian:** Không còn phải mở hàng chục tab trình duyệt để đọc tin tức mỗi sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt tay "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản SerpApi**: Đăng ký miễn phí tại [serpapi.com](https://serpapi.com/) để lấy API Key truy xuất Google News.
- **Tài khoản OpenAI**: Có sẵn API Key và đã nạp tiền tối thiểu vào tài khoản OpenAI Platform để gọi các mô hình LLM.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trong n8n, sau đó copy toàn bộ mã JSON của workflow này (hoặc import file JSON trực tiếp) vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được thiết kế tối ưu bởi chuyên gia Robert Breen. Các sếp cần cấu hình kỹ các điểm sau:

- **Node `Google_news search` (SerpApi):** 
  - Chọn operation là `google_news`.
  - Tạo credential mới loại **SerpApi**, dán API Key đã lấy từ trang quản trị SerpApi vào và lưu lại.
- **Node `OpenAI Chat Model6` (OpenAI):** 
  - Chọn model (mặc định cấu hình sẵn `gpt-5-nano` hoặc các model tương thích tùy ý các sếp).
  - Kết nối OpenAI API Key của các sếp vào credential của node này. Đảm bảo tài khoản OpenAI đã có sẵn số dư hoạt động.
- **Nodes `Chat with Google News` (Agent), `Simple Memory2` (Memory Buffer Window), `Split Out Links`, `Combine into one field`, và `Sample Chatbot` (Chat Trigger):** 
  - Các node này đã được liên kết sẵn logic LangChain và xử lý luồng dữ liệu (Data transformation). Các sếp giữ nguyên cấu trúc và chỉ cần test thử giao diện chat.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Chat with node** hoặc mở khung **Sample Chatbot** để gửi tin nhắn thử nghiệm (ví dụ: *"Tìm tin tức mới nhất về trí tuệ nhân tạo tuần này"*).
- Kiểm tra xem kết quả trả về từ Google News và OpenAI có chính xác không.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên bên phải để kích hoạt workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow này trở thành một trợ lý đắc lực thực thụ cho doanh nghiệp, các sếp có thể mở rộng thêm:
- **Tích hợp kênh liên lạc:** Nối thêm node **Slack** hoặc **Telegram** để chatbot chủ động gửi bản tin tổng hợp hàng ngày vào nhóm chat của công ty.
- **Lưu trữ dữ liệu:** Đẩy các tin tức đã được tóm tắt và phân loại vào **Google Sheets** hoặc **Airtable** để tạo cơ sở dữ liệu tri thức riêng cho team.
- **Bộ lọc nguồn tin:** Tùy chỉnh câu lệnh Prompt trong Agent để chỉ tập trung quét tin từ các trang báo uy tín cụ thể.

### 📌 Kết luận
Workflow "News Search & Categorization Chatbot" là một giải pháp mẫu mực ứng dụng AI Agent kết hợp công cụ tìm kiếm bên ngoài trên nền tảng n8n. Hãy áp dụng ngay để tối ưu hóa quy trình cập nhật thông tin và nâng cao năng suất làm việc cho các sếp!