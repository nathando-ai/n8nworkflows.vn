---
title: "🚀 Tự động quét, lọc và tóm tắt tin tức AI từ TechCrunch gửi thẳng vào Slack bằng n8n & OpenAI"
description: "Xây dựng hệ thống Market Intelligence tự động 100%: Cào dữ liệu TechCrunch bằng Firecrawl, lọc tin chuẩn AI với OpenAI gpt-4o-mini và bắn báo cáo tinh gọn vào Slack mỗi ngày."
slug: "tu-dong-tom-tat-tin-tuc-ai-techcrunch-slack-openai"
tags: [n8n, automation, openai, slack, firecrawl, ai-news]
keywords: [n8n workflow, tóm tắt tin tức AI, techcrunch firecrawl, openai gpt-4o-mini, tự động hóa slack, market intelligence bot]
---

# 🚀 Tự động hóa bản tin AI Market Intelligence từ TechCrunch lên Slack

Các sếp có đang tốn hàng giờ mỗi ngày chỉ để lướt TechCrunch, lọc ra các bài viết về Trí tuệ nhân tạo (AI), đọc lướt qua và tóm tắt lại để gửi cho team không? Việc làm thủ công này cực kỳ mất thời gian, dễ bỏ lỡ thông tin và làm gián đoạn dòng chảy công việc cốt lõi.

Đừng lo! Bài viết này sẽ hướng dẫn các sếp triển khai một **AI Market Intelligence Bot** chạy tự động trên n8n. Workflow này sẽ thay thế hoàn toàn con người trong việc: tự động quét tin tức, sử dụng AI để lọc bỏ rác, tóm tắt ý chính thành 3 bullet points sắc bén và bắn thẳng kết quả vào kênh Slack của team. Tất cả diễn ra hoàn toàn tự động mà không tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần tự tay duyệt web, đọc tin tức công nghệ mỗi ngày.
- **Loại bỏ nhiễu động (Noise Reduction):** AI tự động phân loại và chỉ giữ lại những bài viết chuẩn xác về AI, Machine Learning, bỏ qua các tin tức không liên quan.
- **Cập nhật tức thì trên Slack:** Đội ngũ nhận được bản tóm tắt 3 ý chính súc tích kèm link gốc TechCrunch ngay trên kênh chat quen thuộc.
- **Hoạt động bền bỉ 24/7:** Bot tự kích hoạt theo lịch trình cố định, đảm bảo team luôn dẫn đầu xu hướng thị trường.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **OpenAI API Key:** Để chạy Agent tóm tắt và lọc tin (`gpt-4o-mini`).
- **Firecrawl API Key:** Dịch vụ cào web mạnh mẽ hỗ trợ chuyển đổi dữ liệu sạch dạng Markdown.
- **Slack Bot Token / Webhook:** Để gửi tin nhắn thông báo vào kênh chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm **9 nodes** được thiết kế mạch lạc, trực quan.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, hãy chú ý cấu hình các node quan trọng sau:

- **Daily Market Research Trigger (`scheduleTrigger`):** Cấu hình thời gian chạy định kỳ mỗi ngày (ví dụ: 8h sáng) để thu thập tin tức mới nhất.
- **Crawl TechCrunch (`httpRequest`):** Node này gọi API của Firecrawl để quét trang `https://techcrunch.com`. 
  - *Lưu ý:* Mặc định giới hạn (`limit`) là 20 bài viết để tiết kiệm tài nguyên. Bộ lọc thời gian (`includePaths`) trỏ đến năm hiện tại (ví dụ: `2025/`). Hãy nhớ cập nhật lại đường dẫn này theo năm vận hành thực tế.
- **Receive Firecrawl Results (`httpRequest`):** Nhận kết quả trả về từ Firecrawl (cần cấu hình `HTTP Bearer Auth` với API Key của Firecrawl).
- **Split Output & Filter Messages (`code`):** Các node xử lý code JavaScript giúp bóc tách danh sách bài viết, phân chia dòng dữ liệu và lọc bỏ các bài không đạt tiêu chuẩn.
- **OpenAI Summarizer (`lmChatOpenAi`):** Kết nối thông tin xác thực OpenAI (`openAiApi`) và chọn mô hình **`gpt-4o-mini`** để tối ưu chi phí mà vẫn đảm bảo chất lượng phân tích.
- **Summarizer Agent (`agent`):** Node LangChain Agent đóng vai trò chuyên gia nghiên cứu thị trường, kiểm tra xem bài viết có liên quan đến AI hay không (nếu không, trả về `NOT_AI_RELATED`), đồng thời viết tóm tắt 3 ý chính nếu đúng chủ đề.
- **Send Summary To Slack (`slack`):** Chọn Credentials Slack của sếp, cấu hình kênh nhận tin (Channel) và định dạng tin nhắn hiển thị tên bài viết, bullet points tóm tắt kèm link nguồn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu (Test run) và kiểm tra kết quả trả về trên Slack.
- Nếu mọi thứ hiển thị đẹp đẽ và chính xác, hãy gạt công tắc sang **Active** để bot chính thức "làm việc thay người".

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Slack, các sếp có thể bổ sung thêm node Telegram hoặc Discord để bắn tin tức AI tới nhiều cộng đồng khác nhau cùng lúc.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable ngay sau bước lọc tin để lưu lại lịch sử các bài báo AI đã tổng hợp phục vụ việc tra cứu sau này.
- **Tùy biến Prompt cho AI:** Tinh chỉnh prompt bên trong Agent để định hình phong cách tóm tắt (vui tươi, trang trọng, hoặc chuyên sâu về kỹ thuật).

### 📌 Kết luận
Tự động hóa quy trình nghiên cứu thị trường với n8n và OpenAI không chỉ giúp tiết kiệm khối lượng lớn thời gian mà còn giữ cho tổ chức luôn nhanh nhạy trước các làn sóng công nghệ mới. Hãy triển khai ngay workflow này để nâng tầm hiệu suất làm việc cho toàn đội ngũ các sếp nhé!