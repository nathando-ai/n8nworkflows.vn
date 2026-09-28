---
title: "🚀 Tự động hóa sáng tạo và xuất bản bài viết chuẩn SEO lên Blogger với OpenRouter AI & Mediastack"
description: "Xây dựng hệ thống content marketing tự động 100%: Lấy tin tức nóng hổi từ Mediastack, viết bài chuẩn SEO bằng OpenRouter AI Agent, tạo ảnh minh họa và đăng trực tiếp lên Blogger mà không cần động tay."
slug: "tu-dong-hoa-tao-va-dang-bai-viet-seo-blogger-openrouter-ai-mediastack"
tags: [n8n, automation, no-code, ai-agent, content-creation, openrouter, blogger]
keywords: [n8n workflow, tự động hóa blogger, viết bài seo bằng ai, openrouter ai agent, mediastack news, n8n content automation]
---

# 🚀 Tự động hóa sáng tạo và xuất bản bài viết chuẩn SEO lên Blogger với OpenRouter AI & Mediastack

Các sếp có bao giờ cảm thấy mệt mỏi khi phải liên tục cập nhật tin tức hot, ngồi nghĩ tiêu đề, viết bài chuẩn SEO rồi lại ì ạch tạo hình ảnh minh họa để đăng lên blog mỗi ngày không? Công việc này ngốn rất nhiều thời gian, sức lực mà đôi khi hiệu quả mang lại chưa chắc đã đều đặn.

Đừng lo, giải pháp ở đây rồi! Với workflow n8n cực kỳ thông minh mang tên **Generate & Publish SEO Blog Posts to Blogger using OpenRouter AI & Mediastack News**, toàn bộ quy trình từ "săn" tin tức nóng hổi, phân tích, viết bài chuẩn SEO, tạo ảnh đại diện cho đến xuất bản bài viết lên Blogger và thông báo qua Telegram sẽ được tự động hóa 100%. Các sếp chỉ việc ngồi nhâm nhi ly cà phê và chờ độc giả ghé thăm blog thôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% quy trình Content:** Không cần tốn hàng giờ viết bài thủ công hay thuê biên tập viên cho các nội dung tin tức tổng hợp.
- **Chuẩn SEO & Hấp dẫn:** Ứng dụng sức mạnh của OpenRouter AI Agent để tạo tiêu đề, slug, thẻ meta và nội dung bài viết tối ưu hóa cho công cụ tìm kiếm.
- **Đa phương tiện sinh động:** Tự động tạo hoặc tích hợp hình ảnh minh họa chất lượng cao cho từng bài viết.
- **Kiểm soát thời gian thực:** Nhận thông báo tức thì qua Telegram ngay khi bài viết được lên sóng thành công hoặc có sự cố xảy ra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt sẵn (khuyến nghị dùng VPS riêng).
- **Mediastack API:** Dùng để lấy nguồn tin tức nóng hổi, cập nhật liên tục.
- **OpenRouter API Key:** Để kết nối với các mô hình ngôn ngữ lớn (LLM) thông qua node `OpenRouter Chat Model` (sử dụng model miễn phí `microsoft/mai-ds-r1:free` hoặc tùy chỉnh).
- **Telegram Bot Token & Chat ID:** Dùng cho các node `Send a text message` và `Send a text message1` để gửi thông báo.
- **Blogger API / Credentials:** Tài khoản và thông tin kết nối để HTTP Request đăng bài viết trực tiếp lên blog của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đã import thành công, các sếp cần cấu hình lại các thông số cốt lõi sau trên canvas:
- **Schedule Trigger:** Thiết lập lịch chạy tự động (ví dụ: mỗi ngày 1 bài, hoặc 3 bài/ngày tùy chiến lược nội dung).
- **Mediastack News (Node `httpRequest`):** Cung cấp API Key của Mediastack và cấu hình từ khóa tìm kiếm tin tức phù hợp với lĩnh vực blog của các sếp.
- **Copywriter AI Agent & AI Agent (Langchain Agents):** Liên kết với **OpenRouter Chat Model** và **OpenRouter Chat Model2** bằng cách điền thông tin `OpenRouter API Key`. Kiểm tra lại các Prompt hệ thống (System Prompt) trong phần ghi chú canvas:
  - *Create Title, Slug & Meta:* Đảm bảo AI tạo ra đúng cấu trúc tiêu đề, đường dẫn thân thiện và thẻ mô tả chuẩn SEO.
  - *Write SEO Optimized Blog Post:* Hướng dẫn AI viết bài chi tiết, bố cục rõ ràng bằng HTML/Markdown.
- **Cleanup HTML (`set`) & Parsing (`code`):** Tinh chỉnh lại đoạn code JavaScript ngắn để làm sạch định dạng HTML trước khi gửi sang bước đăng bài.
- **Genarate image & HTTP Request (Đăng Blogger):** Cấu hình các thông tin API kết nối với Blogger hoặc dịch vụ lưu trữ ảnh để hoàn thiện bài viết trước khi xuất bản.
- **Send a text message & Send a text message1 (`telegram`):** Điền `Telegram API Credentials` và Chat ID của các sếp để nhận thông báo trạng thái thành công/thất bại.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** từng node để kiểm tra luồng dữ liệu (đặc biệt là bước gọi API tin tức và AI viết bài).
- Sau khi test chạy mượt mà, gạt công tắc **Active** ở góc trên bên phải để hệ thống tự động làm việc 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh phân phối:** Thêm node đăng bài tự động lên Facebook Page, Twitter/X hoặc LinkedIn ngay sau khi bài viết xuất bản lên Blogger.
- **Lưu lịch sử bài viết:** Kết nối thêm một node **Google Sheets** hoặc **Notion** để lưu lại lịch sử các bài đã viết, giúp dễ dàng quản lý và kiểm tra nội dung.
- **Kiểm duyệt con người (Human-in-the-loop):** Thay vì đăng thẳng lên Blogger, các sếp có thể cấu hình gửi bản nháp bài viết qua Telegram kèm 2 nút bấm "Phê duyệt" hoặc "Từ chối" trước khi gọi API xuất bản.

### 📌 Kết luận
Workflow tự động hóa tạo và xuất bản bài viết SEO với OpenRouter AI và Mediastack là một "vũ khí tối thượng" giúp các sếp tiết kiệm hàng đống thời gian vận hành blog. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm content marketing của doanh nghiệp!