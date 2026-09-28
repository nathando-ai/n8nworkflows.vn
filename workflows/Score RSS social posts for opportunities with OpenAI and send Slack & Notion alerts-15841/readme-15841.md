---
title: "🚀 Tự Động Hóa Xác Định Cơ Hội Kinh Doanh Từ RSS + AI OpenAI & Gửi Báo Cáo Slack + Notion (Mỗi Ngày 9h)"
description: "Workflow tự động hóa 100% không code để theo dõi, phân tích và cảnh báo cơ hội kinh doanh từ các bài đăng xã hội qua RSS, sử dụng AI OpenAI để đánh giá tiềm năng, gửi thông báo Slack thời gian thực và lưu trữ dữ liệu trong Notion. Giúp các sếp tiết kiệm 10+ giờ/ngày theo dõi thị trường."
slug: "tieu-dong-hoa-xac-dinh-co-hoi-rss-ai-openai-slack-notion"
tags: [n8n, automation, no-code, market-research, ai-summarization, slack-integration, notion-database, openai-api]
keywords: [n8n workflow rss, tự động hóa cơ hội kinh doanh, ai đánh giá bài đăng xã hội, cảnh báo slack từ rss, lưu trữ cơ hội trong notion, tự động hóa growth marketing]
---

# 🚀 **Tự Động Hóa Xác Định Cơ Hội Kinh Doanh Từ RSS + AI OpenAI & Gửi Báo Cáo Slack + Notion**

### **Giải pháp cho các sếp Growth Marketing, Founder và SDR:**
Hết thời gian phải **quét thủ công** hàng trăm bài đăng xã hội mỗi ngày để tìm kiếm cơ hội kinh doanh? **Workflow này tự động:**
✅ **Lấy dữ liệu** từ RSS feed (Facebook, LinkedIn, Reddit, hay blog của đối thủ).
✅ **Đánh giá tiềm năng** bằng AI OpenAI (đánh giá độ tương quan, ý định mua hàng, và tiềm năng tương tác).
✅ **Lọc và cảnh báo** các cơ hội cao nhất qua **Slack** (cảnh báo thời gian thực + nút phản hồi 1-click).
✅ **Lưu trữ** tất cả cơ hội vào **Notion** (dữ liệu sạch, dễ tìm kiếm, và cập nhật liên tục).
✅ **Gửi báo cáo tổng hợp** mỗi ngày qua Slack (tóm tắt tất cả cơ hội để team review).

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** theo dõi thị trường và bài đăng xã hội.
- **Chính xác cao** với AI OpenAI đánh giá tiềm năng cơ hội (không phụ thuộc vào cảm nhận cá nhân).
- **Cảnh báo thời gian thực** qua Slack (không bỏ lỡ cơ hội quan trọng).
- **Dữ liệu trung tâm** trong Notion (dễ dàng phân tích, báo cáo và theo dõi lịch sử).
- **Hoạt động 24/7** (không cần can thiệp thủ công).
- **Tùy chỉnh dễ dàng** (điều chỉnh ngưỡng lọc, prompt AI, hoặc kênh thông báo).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **RSS Feed URL**:
   - Lấy từ trang web, blog, hoặc cộng đồng (Facebook Groups, LinkedIn, Reddit) hỗ trợ RSS.
   - Ví dụ: `https://example.com/feed.xml` (kiểm tra trên trang web hoặc sử dụng [rss.com](https://rss.com/) để tạo feed từ URL).

2. **API Key OpenAI**:
   - Đăng ký tại [OpenAI Platform](https://platform.openai.com/) và lấy **API Key**.
   - **Lưu ý**: Workflow sử dụng **GPT-3.5** để phân tích bài đăng. Chi phí phụ thuộc vào số lượng bài đăng được xử lý (tính theo token).

3. **Slack OAuth2 Credentials**:
   - Tạo **Slack App** tại [api.slack.com/apps](https://api.slack.com/apps) và cấp quyền:
     - `chat:write` (gửi tin nhắn).
     - `chat:write.public` (nếu gửi đến channel công khai).
   - Chọn **channel** để gửi cảnh báo và báo cáo hàng ngày.

4. **Notion OAuth2 Credentials**:
   - Tạo **Notion Integration** tại [notion.so/developers](https://www.notion.so/my-integrations) và cấp quyền:
     - `pages:create` (tạo trang mới).
   - Chọn **database Notion** để lưu cơ hội (cần định nghĩa các **property** phù hợp với schema AI trả về).

5. **VPS cho n8n (khuyến nghị)**:
   - Workflow chạy **daily at 9 AM**, nên cần **self-hosted** để ổn định.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15841](https://n8n.io/workflows/15841) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** > Chọn file JSON vừa tải.
3. Chọn **workspace** muốn import và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/15841](https://n8n.io/workflows/15841) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** > Chọn **Paste JSON** và dán mã.
3. Chọn **workspace** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Node "Edit Fields" (Node 02)**
- **Tham số cần chỉnh**:
  - `rssFeedUrl`: Điền URL RSS của feed bạn muốn theo dõi (ví dụ: `https://example.com/feed.xml`).
  - `openAiModel`: Chọn `gpt-3.5-turbo` (mặc định) hoặc `gpt-4` (nếu có budget).
  - `openAiMaxTokens`: Điều chỉnh theo nhu cầu (mặc định 500 token).
  - `slackAlertChannel`: ID của channel Slack muốn gửi cảnh báo (lấy từ URL channel, ví dụ: `C123ABC`).
  - `slackDigestChannel`: ID của channel Slack muốn gửi báo cáo hàng ngày.
  - `notionDatabaseId`: ID của database Notion bạn muốn lưu cơ hội (lấy từ URL database, ví dụ: `12345678-90ab-cdef-1234-567890abcdef`).

#### **B. Cấu hình Node "OpenAI" (Node 06)**
1. Nhấn **Add Credentials** và chọn **OpenAI**.
2. Điền **API Key** từ OpenAI vào trường `apiKey`.
3. **Prompt AI** (mặc định đã tối ưu):
   ```json
   "prompt": "Analyze the following social media post for sales or growth opportunities. Return a structured JSON with:
   - relevanceScore (0-100): How relevant is this post to our ICP?
   - intentScore (0-100): Does the poster show buying intent or engagement potential?
   - engagementPotential (0-100): How likely is this post to generate interaction?
   - summary: A 2-sentence summary of the post's key points.
   - actionRecommendation: Suggest next steps (e.g., 'Engage', 'Monitor', 'Ignore').
   Post: {postContent}
   JSON response only."
   ```
   - **Lưu ý**: Nếu ICP (Ideal Customer Profile) của bạn khác, hãy **tùy chỉnh prompt** để AI hiểu rõ hơn.

#### **C. Cấu hình Node "Slack" (Node 11 & 14)**
1. **Node 11 (Alert Growth Team)**:
   - Chọn **credentials** `slackOAuth2Api` đã cấu hình trước.
   - Đảm bảo **channel ID** trong `slackAlertChannel` đúng với channel bạn muốn gửi cảnh báo.
   - **Message Template** (mặc định):
     ```json
     {
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*🚀 New Opportunity Alert!*\n<{{postUrl}}|Post Link>"
           }
         },
         {
           "type": "divider"
         },
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "📊 **Scores**\nRelevance: {{relevanceScore}}/100\nIntent: {{intentScore}}/100\nEngagement: {{engagementPotential}}/100"
           }
         },
         {
           "type": "actions",
           "elements": [
             {
               "type": "button",
               "text": {
                 "type": "plain_text",
                 "text": "Engage"
               },
               "value": "engage",
               "action_id": "engage_button"
             }
           ]
         }
       ]
     }
     ```
   - **Nút "Engage"** sẽ gửi **Slack Interaction Payload** để team có thể phản hồi nhanh chóng.

2. **Node 14 (Post Daily Digest)**:
   - Chọn **credentials** `slackOAuth2Api` cùng với `slackDigestChannel`.
   - **Message Template** (mặc định):
     ```json
     {
       "blocks": [
         {
           "type": "header",
           "text": {
             "type": "plain_text",
             "text": "📊 Daily Opportunity Digest - {{date}}",
             "emoji": true
           }
         },
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*Total Opportunities:* {{totalOpportunities}}"
           }
         },
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*Highlights:*"
           }
         },
         {
           "type": "divider"
         },
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "{{opportunitySummary}}"
           }
         }
       ]
     }
     ```

#### **D. Cấu hình Node "Create a database page" (Notion)**
1. Chọn **credentials** `notionOAuth2Api`.
2. **Property Mapping** (đảm bảo khớp với schema AI trả về):
   - `title`: `{{postTitle}}` (tên bài đăng).
   - `url`: `{{postUrl}}` (link bài đăng).
   - `relevanceScore`: `{{relevanceScore}}` (điểm tương quan).
   - `intentScore`: `{{intentScore}}` (điểm ý định mua).
   - `engagementPotential`: `{{engagementPotential}}` (tiềm năng tương tác).
   - `summary`: `{{summary}}` (tóm tắt AI).
   - `actionRecommendation`: `{{actionRecommendation}}` (gợi ý hành động).
   - **Lưu ý**: Nếu Notion của bạn có **property custom**, cần chỉnh sửa trong **Code Node 13** để trích xuất dữ liệu.

#### **E. Cấu hình Node "Schedule" (Node 01)**
- **Cron Expression**: `0 0 9 * * ?` (chạy hàng ngày lúc 9h00 AM).
- **Timezone**: Chọn **timezone** phù hợp với team (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).
- **Lưu ý**: Nếu muốn chạy ở giờ khác, chỉnh sửa cron theo [crontab.guru](https://crontab.guru/).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra cấu hình):
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra **log** để đảm bảo:
     - RSS feed được lấy đúng.
     - AI phân tích và trả về JSON hợp lệ.
     - Slack/Notion nhận được dữ liệu.
   - **Nếu có lỗi**, kiểm tra:
     - URL RSS có đúng không?
     - API Key OpenAI có hiệu lực không?
     - Slack/Notion credentials có cấu hình đúng không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.
   - Workflow sẽ chạy tự động hàng ngày lúc 9h00 AM.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tùy chỉnh Prompt AI cho ICP riêng**
- Nếu ICP của bạn là **startup tech**, hãy chỉnh prompt như sau:
  ```json
  "prompt": "Analyze this post for opportunities related to tech startups. Focus on:
  - Funding needs (e.g., 'raising seed round').
  - Pain points (e.g., 'struggling with scalability').
  - Community engagement (e.g., 'looking for co-founders').
  Post: {postContent}
  JSON response only."
  ```

### **2. Gửi báo cáo định kỳ qua Email**
- Thêm **Node Email** (ví dụ: **SendGrid** hoặc **Gmail SMTP**) sau Node 13 để gửi báo cáo hàng ngày qua Email.

### **3. Lưu log vào Google Sheets/Excel**
- Thêm **Node Google Sheets** sau Node 12 để lưu tất cả cơ hội vào bảng tính.

### **4. Cảnh báo qua Telegram**
- Thêm **Node Telegram Bot** (cấu hình từ [@BotFather](https://t.me/BotFather)) để gửi cảnh báo qua Telegram.

### **5. Điều chỉnh ngưỡng lọc**
- Trong **Node 08 (Filter - High Relevance Opportunities Only)**, điều chỉnh `relevanceScore` từ `>= 70` sang `>= 80` để giảm số lượng cảnh báo.

### **6. Tích hợp với CRM (HubSpot, Salesforce)**
- Thêm **Node HubSpot API** sau Node 12 để tự động tạo **Deal** hoặc **Contact** từ cơ hội cao.

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp Growth Marketing, Founder và SDR muốn:
✔ **Tiết kiệm thời gian** theo dõi thị trường.
✔ **Tăng hiệu quả** với AI phân tích tiềm năng cơ hội.
✔ **Tập trung vào cơ hội thực sự** (không bỏ lỡ bất kỳ cơ hội nào).