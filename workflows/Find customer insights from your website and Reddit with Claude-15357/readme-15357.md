---
title: "🚀 Tìm kiếm Insights khách hàng từ website và Reddit tự động bằng Claude AI"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin website, quét thảo luận Reddit và phân tích customer insights bằng Claude AI phục vụ Marketing."
slug: "tim-kiem-customer-insights-tu-website-va-reddit-bang-claude-ai"
tags: [n8n, automation, ai-agents, anthropic, reddit, market-research]
keywords: [n8n workflow, customer insights, phân tích thị trường ai, claude sonnet, reddit automation]
---

# 🚀 Tìm kiếm Insights khách hàng từ website và Reddit tự động bằng Claude AI

Các sếp có bao giờ đau đầu khi viết content quảng cáo, lên chiến lược landing page hay làm market research mà nội dung cứ chung chung, thiếu chiều sâu? Nguyên nhân lớn nhất là do dữ liệu đầu vào (input) quá yếu, chỉ dựa vào văn bản tự biên tự diễn trên website mà quên mất khách hàng ngoài kia thực sự đang nói gì, phàn nàn gì.

Giải pháp thủ công là ngồi cào website, lướt từng ngóc ngách của Reddit, đọc hàng trăm comment rồi tổng hợp lại – tốn cả tuần lễ! Giờ đây, với workflow n8n kết hợp sức mạnh của **Claude AI (Anthropic)** và **Reddit**, các sếp có thể tự động hóa 100% quy trình này chỉ với một URL website.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hiểu thấu khách hàng:** Kết hợp "giọng điệu thương hiệu" từ website với "ngôn ngữ thực tế" từ các cuộc thảo luận trên Reddit.
- **Tiết kiệm 90% thời gian:** Tự động crawl website, trích xuất trang con (product, feature, about), tìm kiếm bài viết và bóc tách comment trên Reddit trong vài phút.
- **Tạo chiến lược bài bản:** AI tự động phân tích pain points (nỗi đau), trigger events (sự kiện kích thích mua hàng), aspirations (khát vọng) và trích dẫn đắt giá (quotes) để viết ad hook, landing page cực bén.
- **Hoạt động tự động:** Kích hoạt qua form đơn giản, dễ dàng mở rộng và tích hợp vào quy trình marketing hiện tại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản cloud hoặc self-hosted).
- **Anthropic API Key:** Dành cho các node sử dụng mô hình `Claude Sonnet 4.5` để phân tích ngữ cảnh, chấm điểm relevance và tạo insights.
- **Reddit OAuth2 API:** Tài khoản kết nối với Reddit để thực hiện tìm kiếm bài viết (Search) và lấy bình luận (Get Comments).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn workflow từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 55 nodes được chia thành 3 giai đoạn chính, các sếp cần lưu ý cấu hình sau:
- **Form Input:** Node `Form Input` (`formTrigger`) là điểm khởi đầu, sếp nhập URL website cần nghiên cứu.
- **Credentials:** 
  - Gán API Key cho các node **Anthropic Chat Model** (Anthropic Chat Model 4, 5, 6, 7...).
  - Kết nối tài khoản Reddit cho các node **Reddit2**, **Reddit3**, và **Get many comments in a post** (`redditOAuth2Api`).
- **Xử lý trang web (Giai đoạn 1):** Các node `Fetch Homepage1`, `Get website (text)1`, kết hợp với các Agent AI (`Extract Website Copy1`, `Extract Sub-Website Copy1`) sẽ tự động quét trang chủ và các trang quan trọng (Product, Features, About). Hãy đảm bảo website đầu vào là Public và có thể truy cập được.
- **Đào sâu Reddit (Giai đoạn 2 & 3):** AI sẽ tự tạo từ khóa tìm kiếm dựa trên nội dung website để quét các bài post liên quan trên Reddit, lọc bài viết chất lượng qua `Check relevance of posts` (Agent) và bóc tách comment chi tiết.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một URL website thực tế thông qua Form.
- Kiểm tra kết quả trả về ở các node cuối cùng (Return / Aggregate).
- Sau khi kiểm tra mọi thứ chạy mượt mà, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack / Telegram:** Thêm một node thông báo vào cuối workflow để gửi bản tóm tắt customer insights thẳng vào nhóm chat của team marketing ngay khi chạy xong.
- **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Notion** để lưu toàn bộ pain points và quotes khách hàng vào cơ sở dữ liệu nội bộ, làm kho tài nguyên viết content lâu dài.
- **Tự động hóa sinh nội dung:** Kết hợp output của workflow này làm đầu vào cho một LLM khác để sinh kịch bản quảng cáo Facebook/TikTok hoặc viết bài chuẩn SEO hàng loạt.

### 📌 Kết luận
Workflow này là cỗ máy tự động hoàn hảo giúp các sếp giải quyết triệt để bài toán "bí ý tưởng" và "lệch pha ngôn ngữ" với khách hàng. Hãy triển khai ngay trên hệ thống n8n của mình để nâng tầm chất lượng các chiến dịch marketing!