---
title: "🚀 Tự động nhận diện và kích hoạt Influencer từ danh sách khách hàng Salesforce Loyalty"
description: "Khám phá cách tự động hóa quy trình quét email khách hàng thân thiết trên Salesforce, làm giàu dữ liệu mạng xã hội với Influencers Club, phân tích bằng GPT-4o-mini và tự động gửi email cá nhân hóa qua SendGrid."
slug: "tu-dong-nhan-dien-influencer-salesforce-loyalty-influencers-club"
tags: [n8n, automation, no-code, salesforce, openai, sendgrid, influencer-marketing]
keywords: [n8n workflow, salesforce influencer automation, influencers club api, gpt-4o-mini n8n, sendgrid automation]
---

# 🚀 Tự động nhận diện và kích hoạt Influencer từ khách hàng Salesforce Loyalty

Các sếp có bao giờ nghĩ rằng ngay trong danh sách khách hàng thân thiết (loyalty program) của doanh nghiệp đang ẩn chứa rất nhiều creator/influencer tiềm năng nhưng chưa được khai thác? Làm thủ công việc kiểm tra từng email khách hàng xem họ có kênh TikTok, Instagram, YouTube hay không thực sự là một "cực hình" tốn hàng trăm giờ đồng hồ.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100%: Lắng nghe contact mới trên Salesforce 👉 Quét và làm giàu thông tin mạng xã hội qua **Influencers Club API** 👉 AI (**GPT-4o-mini**) phân loại và đánh giá tiềm năng 👉 Phân luồng chiến dịch & cập nhật 20+ trường dữ liệu về CRM 👉 Tự động gửi email chăm sóc, mời hợp tác cá nhân hóa qua **SendGrid**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chuyển đổi khách hàng loyalty thành đại sứ thương hiệu (Ambassador) mà không cần nhân sự rà soát thủ công.
- **Dữ liệu CRM cực chi tiết:** Tự động đồng bộ hơn 20 trường thông tin (Niche, Follower count, Engagement rate, Value Score...) trực tiếp vào Salesforce.
- **Cá nhân hóa đỉnh cao:** Sử dụng GPT-4o-mini để tạo nội dung email phù hợp với từng tier (Elite, Core, Rising Star...) mà không mang văn phong marketing sáo rỗng.
- **Tối ưu chuyển đổi:** Gửi email qua SendGrid từ tài khoản cá nhân thay vì email hệ thống chung, giúp tăng tỷ lệ mở và phản hồi.
:::

### 📦 Các loại Nodes chính trong Workflow
- **Trigger & Data:** `Salesforce Trigger`, `Set` (Extract Data Fields), `Code` (Route Logic, Activation).
- **Enrichment:** `Influencers Club` (Enrich by Email).
- **AI Agents & LLM:** `@n8n/n8n-nodes-langchain.agent` (AI Creator Classification & Personalization), `@n8n/n8n-nodes-langchain.lmChatOpenAi` (GPT-4o-mini), `@n8n/n8n-nodes-langchain.outputParserStructured`.
- **Logic & Routing:** `Switch`, `Merge`.
- **Action & CRM:** `Salesforce` (Update a contact), `SendGrid` (Send Email).

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
1. **Tài khoản Salesforce** đã cấu hình custom field `loyalty_tier` và các trường Creator (xem danh sách bên dưới).
2. **Influencers Club API Key** (đăng ký tại influencers.club để lấy API key).
3. **OpenAI API Key** (sử dụng model `gpt-4o-mini`).
4. **Tài khoản SendGrid** đã xác thực Sender Domain để gửi email.
:::

---

### 📋 Salesforce Setup Checklist (BẮT BUỘC)
Trước khi chạy workflow, các sếp nhớ tạo các Custom Field sau trên đối tượng **Contact** trong Salesforce:

- ✅ **Creator Info:** `Is_Creator__c`, `Creator_Tier__c`, `Creator_Niche__c`, `Creator_Subcategory__c`, `Primary_Platform__c`
- ✅ **Metrics:** `Follower_Count__c`, `Engagement_Rate__c`, `Social_Username__c`, `Profile_URL__c`, `Creator_Bio__c`
- ✅ **Value:** `Value_Score__c`, `Brand_Fit_Score__c`, `Content_Themes__c`, `Audience_Demographics__c`
- ✅ **Ambassador:** `Ambassador_Tier__c`, `Activation_Level__c`, `Activation_Date__c`, `Next_Activation_Action__c`
- ✅ **Tracking:** `Outreach_Strategy__c`, `Outreach_Priority__c`, `Outreach_Sent_Date__c`, `Personalization_Used__c`

---

### 🚀 Cách import & Lưu ý khi cấu hình

#### 1. Import Workflow 📥
- Copy đoạn JSON của workflow (hoặc tải file JSON).
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON**.

#### 2. Các cấu hình quan trọng cần lưu ý 📌
- **Salesforce Trigger & Update nodes:** Chọn đúng Salesforce Credential của sếp. Đảm bảo Object được cấu hình là `Contact`.
- **Enrich by Email (Influencers Club node):** Thêm Influencers Club API Key vào phần Header Auth để gọi endpoint `/public/v1/creators/enrich/email/`.
- **OpenAI Classifier Models (GPT-4o-mini):** Cấu hình OpenAI API Key. Model được chỉ định sẵn là `gpt-4o-mini` giúp tối ưu chi phí và tốc độ phân tích (chỉ mất 2-4 giây xử lý mỗi creator).
- **SendGrid Node:** Chọn SendGrid API Credential, cấu hình email người gửi (Sender Email) phù hợp.

#### 3. Kích hoạt hệ thống ⚡️
- Test thử với 1-2 contact mẫu trên Salesforce để kiểm tra toàn bộ luồng data từ việc làm giàu thông tin, phân loại AI cho tới khi cập nhật CRM và gửi email.
- Sau khi test thành công, bật nút **Active** trên góc phải n8n để hệ thống chạy ngầm tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thêm node **Slack** hoặc **Telegram** sau bước phân loại AI để báo ngay cho sales/partnership team khi phát hiện một Influencer "cá mập" (Macro/Mid tier) vừa đăng ký tài khoản.
- **Tùy chỉnh Prompt AI:** Các sếp có thể tinh chỉnh system prompt trong các AI Agent để ép AI nói chuyện theo đúng giọng điệu (Tone of Voice) của thương hiệu mình.
- **Tạo Automation Follow-up:** Kết hợp thêm node **Wait** và nhánh gửi email lần 2 (Follow-up email) sau 7 ngày nếu creator chưa phản hồi.

---

### 📌 Kết luận
Việc kết hợp Salesforce, Influencers Club, AI và n8n mở ra một cỗ máy tự động hóa săn tìm creator cực kỳ mạnh mẽ mà không tốn nhiều nhân lực vận hành. Hãy cài đặt ngay hôm nay để biến những khách hàng thân thiết thành những đại sứ thương hiệu đắc lực cho doanh nghiệp các sếp!