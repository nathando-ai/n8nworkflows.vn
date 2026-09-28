---
title: "🚀 Tự động tìm kiếm Lookalike Influencer và đẩy về HubSpot bằng Influencers.club & GPT-4o-mini"
description: "Hướng dẫn xây dựng workflow n8n tự động phát hiện creator tiềm năng từ HubSpot, tìm kiếm influencer tương tự qua Influencers.club API, phân tích bằng GPT-4o-mini và đồng bộ dữ liệu."
slug: "tu-dong-tim-kiem-lookalike-influencer-hubspot-influencers-club-gpt-4o-mini"
tags: [n8n, automation, hubspot, influencers-club, openai, ai-agent, lead-generation]
keywords: [n8n workflow, lookalike influencer, influencers.club, gpt-4o-mini, hubspot automation, tìm kiếm KOL KOC]
---

# 🚀 Tự động tìm kiếm Lookalike Influencer và đẩy về HubSpot bằng Influencers.club & GPT-4o-mini

Việc tìm kiếm và mở rộng mạng lưới Influencer (KOL/KOC) tương tự như những nhà sáng tạo nội dung hiệu quả nhất của bạn thường tốn rất nhiều thời gian làm thủ công: từ việc check profile, so sánh lượng followers, lọc dữ liệu đến phân tích mức độ phù hợp với thương hiệu. 

Workflow n8n này sẽ tự động hóa 100% quy trình đó! Khi có một contact mới được tạo trong HubSpot, hệ thống sẽ tự động kiểm tra xem họ có phải là creator không, khai thác dữ liệu từ **Influencers.club API**, dùng **GPT-4o-mini** để phân tích chuyên sâu và đẩy những influencer "lookalike" (tương tự) chất lượng cao trở lại CRM HubSpot của bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn quy trình tìm kiếm KOL:** Không cần tìm kiếm thủ công từng profile trên Instagram, TikTok hay YouTube.
- **AI phân tích chuyên sâu:** Sử dụng GPT-4o-mini đánh giá độ tương thích, điểm mạnh, rủi ro, mức độ chân thực của audience và khả năng phù hợp thương hiệu.
- **Đồng bộ CRM mượt mà:** Tự động tạo hoặc cập nhật (upsert) thông tin lookalike influencer trực tiếp vào HubSpot để đội ngũ outreach dễ dàng tiếp cận.
- **Hoạt động liên tục 24/7:** Chạy ngầm mỗi khi có contact mới trên HubSpot, tiết kiệm hàng chục giờ làm việc mỗi tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản HubSpot** kèm quyền truy cập Developer App & App Token.
- **Tài khoản Influencers.club** để lấy API Key (nền tảng dữ liệu creator hàng đầu).
- **OpenAI API Key** (dùng cho model GPT-4o-mini).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor của các sếp, hoặc import file JSON thông qua giao diện quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình các credentials và tham số quan trọng sau:

- **HubSpot Trigger & Get Contact by ID:** Kết nối tài khoản HubSpot của các sếp. Đảm bảo trigger bắt sự kiện `contact.creation` (có thể cấu hình thêm `contact.propertyChange` nếu muốn bắt sự kiện cập nhật).
- **Enrich by Email, Find Similar Creators, Enrich by Handle (Full):** Điền `Influencers.club API Key` vào phần credentials của các node này để gọi dữ liệu mạng xã hội (Instagram, TikTok, YouTube, Twitter...).
- **Normalize (Code in JS):** Node này dùng Javascript để tự động nhận diện nền tảng chính (`main_platform`) dựa trên số lượng follower cao nhất, đồng thời tính toán các chỉ số như `follower_tier`, `engagement_tier`, `growth_trend`.
- **Filter — Is Creator?:** Kiểm tra điều kiện `is_creator === true`. Chỉ những tài khoản thực sự là creator mới được tiếp tục đi tiếp vào luồng tìm kiếm lookalike.
- **AI Agent (Lookalike) & OpenAI Model (Lookalike)1:** Kết nối `OpenAI API`. System prompt của AI Agent sẽ phân tích profile và trả về cấu trúc JSON gồm: tóm tắt, điểm mạnh, rủi ro, độ chân thực của audience, độ phù hợp thương hiệu (`brand_fit`), hành động đề xuất (`recommended_action`) và ước tính reach mỗi bài (`estimated_reach_per_post`).
- **HubSpot — Lookalike Creator:** Cấu hình mapping các trường dữ liệu trả về từ AI vào các custom properties tương ứng trong HubSpot để phục vụ cho việc gửi chuỗi email outreach.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với một contact mẫu trong HubSpot có chứa email của một creator thực tế để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật công tắc **Active** để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Slack/Telegram:** Thêm một node thông báo mỗi khi hệ thống tìm thấy và thêm một lookalike influencer chất lượng cao vào HubSpot để team sales/marketing nắm bắt ngay.
- **Tạo Custom Properties trong HubSpot:** Tạo thêm các trường dữ liệu như *Brand Fit*, *Estimated Reach*, *AI Summary* trên HubSpot để phân loại chiến dịch dễ hơn.
- **Tinh chỉnh Prompt AI:** Điều chỉnh system prompt trong AI Agent để phù hợp với ngôn ngữ và tiêu chí chấm điểm riêng của ngành hàng công ty các sếp.

### 📌 Kết luận
Workflow tích hợp giữa HubSpot, Influencers.club và GPT-4o-mini là giải pháp tối ưu giúp doanh nghiệp scale-up chiến dịch Influencer Marketing một cách tự động, chính xác và chuyên nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa nguồn lực cho đội ngũ của bạn!