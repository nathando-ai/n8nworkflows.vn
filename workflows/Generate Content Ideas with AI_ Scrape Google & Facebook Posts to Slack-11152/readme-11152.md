---
title: "🚀 Tự động tạo ý tưởng nội dung xu hướng bằng AI: Thu thập Google & Facebook gửi thẳng vào Slack"
description: "Khám phá cách tự động hóa quy trình nghiên cứu thị trường, thu thập tin tức Google và bài viết Facebook, phân tích bằng AI để gửi ý tưởng nội dung mới mỗi tuần lên Slack."
slug: "tu-dong-tao-y-tuong-noi-dung-bang-ai-scraper-google-facebook-slack"
tags: [n8n, automation, ai-agent, content-marketing, apify, openrouter, slack]
keywords: [n8n workflow, tự động hóa marketing, AI content ideas, Apify scraper, OpenRouter AI, Slack automation]
---

# 🚀 Tự động tạo ý tưởng nội dung xu hướng bằng AI: Thu thập Google & Facebook gửi thẳng vào Slack

Các sếp làm Content Marketing hay Social Media chắc chắn đã quá quen thuộc với nỗi khổ "cạn kiệt ý tưởng" mỗi tuần. Việc phải ngồi hàng giờ lướt Google News, đọc từng bài viết trên Facebook đối thủ hay các trang tin tức để tìm xu hướng vừa tốn thời gian, vừa dễ bị bỏ lỡ thông tin quan trọng.

Đừng lo, workflow n8n này sinh ra là để giải phóng các sếp khỏi công việc thủ công nhàm chán đó. Hệ thống sẽ tự động quét các chủ đề hot trên Google và Facebook, nhờ AI phân tích và tổng hợp thành các ý tưởng nội dung sáng tạo, sau đó "giao tận tay" các sếp trên Slack theo định kỳ hàng tuần. Hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và hỗ trợ các node tùy chỉnh bên thứ ba như Apify, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Không cần thủ công lướt web tìm trend, AI sẽ tổng hợp sẵn sàng.
- **Bắt trend cực nhanh:** Tự động thu thập tin tức mới nhất từ Google News và các trang Facebook mục tiêu.
- **Ý tưởng chất lượng cao:** AI Agent phân tích sâu và đề xuất các góc nhìn nội dung (content angles) độc đáo, phù hợp với thương hiệu.
- **Tự động hóa 24/7:** Chạy ngầm theo lịch hẹn (Schedule Trigger) và báo cáo trực tiếp qua Slack mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted Instance:** Do workflow sử dụng cộng đồng `@apify/n8n-nodes-apify`.
- **Apify Account & API Token:** Để sử dụng các Actor cào dữ liệu từ Google News và Facebook.
- **OpenRouter API Key:** Cung cấp sức mạnh cho AI Agent phân tích và tổng hợp nội dung (có thể thay thế bằng OpenAI/Anthropic nếu thích).
- **Slack Workspace & Bot:** Nơi nhận báo cáo tổng hợp ý tưởng nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và paste toàn bộ mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình các điểm sau:
- **Workflow Configuration:** Mở node này và điền Apify API Token cùng OpenRouter API Key vào các biến cấu hình.
- **Apify Google News Scraper:** Thay đổi từ khóa tìm kiếm (`search query`) mặc định thành chủ đề hoặc ngành hàng mà các sếp đang quan tâm (ví dụ: "Digital Marketing Trends", "AI technology").
- **Apify Facebook Scraper:** Cập nhật danh sách URL trang Facebook (`startUrls`) mà các sếp muốn theo dõi đối thủ hoặc fanpage ngành.
- **AI Agent & OpenRouter Chat Model:** Kiểm tra kết nối với OpenRouter. Có thể tùy chỉnh System Prompt trong AI Agent nếu muốn AI trả về định dạng hoặc ngôn ngữ khác (ví dụ: Tiếng Việt, văn phong hài hước hoặc chuyên gia).
- **Slack Post Content Ideas:** Kết nối tài khoản Slack (OAuth2) và chọn kênh (Channel) mà bot sẽ gửi tin nhắn báo cáo.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** trên từng node để kiểm tra luồng dữ liệu mẫu chạy từ Apify qua AI Agent đến Slack.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch hẹn hàng tuần (`Weekly Schedule Trigger`).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Có thể bổ sung thêm các node cào Twitter/X, LinkedIn hoặc RSS Feed báo chí để ý tưởng nội dung đa dạng hơn.
- **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Notion** sau bước AI Agent để lưu lại toàn bộ kho ý tưởng phục vụ cho việc lên lịch content calendar dài hạn.
- **Nhắc nhở qua Telegram:** Ngoài Slack, có thể duplicate nhánh gửi tin nhắn để bắn thêm một bản sao sang kênh Telegram của team content.

### 📌 Kết luận
Việc bắt trend và sáng tạo nội dung chưa bao giờ dễ dàng đến thế khi có sự trợ giúp của AI và Automation. Hãy "lên đồ" ngay workflow này trên hệ thống n8n của các sếp để tối ưu hóa đội ngũ content ngay hôm nay!