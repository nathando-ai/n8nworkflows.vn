---
title: "🚀 Tự động phát hiện khoảng trống nội dung đối thủ trên ChatGPT, Perplexity & Gemini bằng SE Ranking"
description: "Hướng dẫn chi tiết workflow n8n giúp phân tích đối thủ cạnh tranh, tìm kiếm khoảng trống nội dung trên AI Search (ChatGPT, Perplexity, Gemini) và SEO truyền thống để tối ưu chiến lược."
slug: "tu-dong-phan-tich-khoang-trong-noi-dung-ai-se-ranking-n8n"
tags: [n8n, automation, se-ranking, ai-seo, market-research, google-sheets]
keywords: [n8n workflow, phân tích đối thủ AI, content gap seo, se ranking api, tich hop ai search n8n]
---

# 🚀 Tự động phát hiện khoảng trống nội dung đối thủ trên ChatGPT, Perplexity & Gemini với SE Ranking

Trong kỷ nguyên tìm kiếm bằng AI (AI Search), việc xuất hiện trên ChatGPT, Perplexity hay Gemini quan trọng không kém gì Google truyền thống. Tuy nhiên, việc theo dõi thủ công xem đối thủ đang vượt mặt chúng ta ở những prompt nào, từ khóa nào là một cơn ác mộng thực sự đối với các SEOer và Content Marketer. 

Workflow n8n này ra đời như một giải pháp tự động hóa 100% không cần code, giúp các sếp quét toàn bộ dữ liệu hiển thị AI, từ khóa, backlink và tự động chấm điểm cơ hội (Opportunity Scoring) để lên chiến lược nội dung vượt mặt đối thủ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Báo cáo khoảng trống AI Visibility:** So sánh độ hiển thị giữa website của bạn và đối thủ trên 3 nền tảng lớn: ChatGPT, Perplexity và Gemini.
- **Khoảng trống từ khóa & Backlink:** Tự động lọc ra các từ khóa top của đối thủ kèm theo lưu lượng tìm kiếm (Search Volume), độ khó (Keyword Difficulty) và chỉ số thẩm quyền backlink.
- **Chấm điểm ưu tiên thông minh:** Phân loại cơ hội thành các mức `HIGH`, `MEDIUM`, `LOW` kèm đề xuất hành động cụ thể.
- **Đồng bộ dữ liệu tự động:** Xuất toàn bộ kết quả phân tích thẳng vào Google Sheets để team content triển khai ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **Self-hosted n8n instance** (vì workflow có sử dụng các node cộng đồng).
2. **SE Ranking Community Node**: Cài đặt package `@seranking/n8n-nodes-seranking` vào n8n của các sếp.
3. **SE Ranking API Token**: Lấy API key từ tài khoản SE Ranking của sếp.
4. **Google Sheets**: Một file Google Sheet trống để lưu kết quả xuất ra (tùy chọn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** hoặc copy trực tiếp mã JSON dán vào workspace của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, hãy chú ý cấu hình các node cốt lõi sau:
- **Node `Configuration` (Set):** Đây là nơi các sếp điền thông tin domain của mình, domain đối thủ và mã quốc gia (`us`, `vn`, `uk`, `de`, v.v.) để hệ thống tiến hành quét.
- **Các node SE Ranking (`Your Domain - ChatGPT`, `Competitor - ChatGPT`, v.v.):** Chọn đúng thông tin `Credentials` bằng SE Ranking API Token đã chuẩn bị.
- **Node `Export to Google Sheets`:** Kết nối tài khoản Google OAuth2 của sếp, chọn đúng file Google Sheets và sheet đích để lưu dữ liệu tổng hợp.
- **Các node `Wait (Rate Limit)`:** Giúp giãn cách thời gian gọi API để tránh bị giới hạn lượt gọi (Rate Limit) từ SE Ranking.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử công đoạn thủ công (`Manual Trigger`) để kiểm tra dữ liệu trả về ở từng node (`Calculate AI Gaps`, `Final Opportunity Scoring`).
- Sau khi kiểm tra dữ liệu sạch sẽ, gạt nút **Active** ở góc trên bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để bắn tin nhắn báo cáo ngay lập tức về group chat mỗi khi quét xong bộ từ khóa khoảng trống.
- **Lên lịch định kỳ (Schedule Trigger):** Thay thế `Manual Trigger` bằng `Schedule Trigger` để workflow tự động chạy hàng tuần hoặc hàng tháng, giúp tracking biến động AI Search liên tục.
- **Kết hợp AI Content Generation:** Sau bước `Final Opportunity Scoring`, có thể gắn thêm node OpenAI/Claude để tự động viết dàn ý (outline) chi tiết cho các từ khóa đạt điểm `HIGH`.

### 📌 Kết luận
Việc tối ưu hóa hiện diện trên các công cụ tìm kiếm tích hợp AI (AI Search Engine Optimization) đang là xu hướng sống còn của Digital Marketing. Với workflow n8n này, các sếp có thể tiết kiệm hàng chục giờ nghiên cứu thủ công và nhanh chóng nắm bắt các "mỏ vàng" nội dung mà đối thủ đang bỏ quên. Triển khai ngay thôi các sếp!