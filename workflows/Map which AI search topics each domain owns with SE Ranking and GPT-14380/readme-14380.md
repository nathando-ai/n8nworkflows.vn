---
title: "🚀 Bản đồ Chủ đề Tìm kiếm AI: Phân tích Thị phần & Đối thủ với SE Ranking và GPT"
description: "Tự động trích xuất từ khóa tìm kiếm AI của bạn và 2 đối thủ cạnh tranh bằng SE Ranking, gom cụm bằng OpenAI GPT và xuất báo cáo chiến lược ra Google Sheets."
slug: "ban-do-chu-de-tim-kiem-ai-se-ranking-gpt"
tags: [n8n, automation, seo, ai-search, openai, google-sheets, seranking]
keywords: [n8n workflow, se ranking api, openai gpt, phân tích seo ai, market research, tự động hóa marketing]
---

# 🚀 Tự động lập bản đồ chủ đề tìm kiếm AI: Vượt mặt đối thủ cùng SE Ranking và GPT

Việc phân tích thủ công các từ khóa (prompts) trên các công cụ tìm kiếm tích hợp AI (ChatGPT, Perplexity, Gemini, AI Overviews...) của bạn và các đối thủ cạnh tranh là một cơn ác mộng thực sự tốn hàng giờ đồng hồ. Các sếp có đang cảm thấy mệt mỏi khi phải copy-paste dữ liệu rời rạc và cố gắng tìm ra khoảng trống nội dung (content gap)?

Workflow n8n này sẽ giải quyết triệt để vấn đề đó! Nó tự động hóa 100% quy trình thu thập dữ liệu từ **SE Ranking**, xử lý thông minh qua **OpenAI GPT** để gom cụm chủ đề, xác định xem đối thủ hay thương hiệu của các sếp đang "vô địch" ở ngách nào, và lưu kết quả trực tiếp lên **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảng xếp hạng tìm kiếm AI:** Đo lường thị phần hiển thị (Share of Voice) trên các nền tảng ChatGPT, Perplexity, Gemini, AI Overviews...
- **Bản đồ cạnh tranh theo chủ đề:** Biết rõ domain nào đang thống trị chủ đề nào, đâu là điểm mạnh/yếu.
- **Dữ liệu định lượng chi tiết:** Số lượng prompt của từng domain trên mỗi chủ đề giúp nhận diện chính xác vị thế.
- **Insight hành động:** Nhận một dòng phân tích chiến lược tự động cho từng chủ đề để định hướng kế hoạch nội dung (content plan).
- **Lưu trữ tự động:** Toàn bộ bảng xếp hạng và bản đồ chủ đề được đổ gọn gàng vào các tab tương ứng trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Cài đặt SE Ranking community node trong n8n.
- Tài khoản SE Ranking và **API Token** ([Lấy API tại đây](https://online.seranking.com/admin.api.dashboard.html)).
- Tài khoản và **OpenAI API Key**.
- Tài khoản Google Sheets để lưu trữ dữ liệu báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cung cấp, mở n8n Editor, chọn **Import from File** hoặc dán trực tiếp mã JSON vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, hãy kiểm tra kỹ các node sau:
- **Domain Input Form (formTrigger):** Node khởi chạy bằng form. Các sếp có thể lấy Production URL để chia sẻ cho team hoặc nhúng vào website qua iframe.
- **Configuration (set):** Nơi cấu hình giới hạn số lượng prompt (`prompts_limit`) hoặc thị trường vùng miền (`source` như us, uk, de...).
- **Get your target/brand prompts & Các node của SE Ranking:** Cần kết nối thông tin tài khoản thông qua **seRankingApi** Credentials.
- **GPT topic clustering (openAi):** Chọn credential **openAiApi** và tùy chỉnh System Prompt nếu muốn thay đổi cách GPT gom cụm chủ đề hoặc viết insight.
- **Export to Sheets: Topic Analysis (googleSheets):** Kết nối tài khoản Google Sheets thông qua OAuth2 và điền chính xác URL bảng tính Google Sheets của các sếp.
- **Các node Wait (3s, 6s, 9s...):** Giúp giãn cách thời gian gọi API để tránh bị nghẽn hệ thống hoặc chạm rate limit từ SE Ranking.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách submit form mẫu để kiểm tra dữ liệu trả về ở từng node.
- Bật công tắc **Active** góc trên bên phải để đưa workflow vào trạng thái vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo:** Thêm node Slack hoặc Telegram để bắn thông báo ngay về máy mỗi khi có một báo cáo phân tích mới hoàn tất.
- **Mở rộng đối thủ:** Có thể tùy chỉnh thêm các nhánh lấy dữ liệu cho competitor thứ 3 hoặc thứ 4 nếu cần phân tích sâu hơn.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để tự động chạy quét từ khóa hàng tháng, giúp theo dõi biến động thị phần AI search theo thời gian.

### 📌 Kết luận
Việc thấu hiểu thị phần trên các công cụ tìm kiếm tích hợp AI không còn là bài toán khó hay tốn kém nhân lực. Hãy "lên đồ" ngay workflow này trên hệ thống n8n của các sếp để tối ưu hóa chiến lược SEO và chiếm lĩnh mọi ngách tìm kiếm ngay hôm nay!