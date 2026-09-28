---
title: "📰 Tự Động Hóa Báo Cáo Tin Tức Kinh Doanh Hàng Ngày Với NewsAPI & GPT-4 (Gửi Trực Tiếp Slack) - N8N"
description: "Workflow tự động hóa lấy tin tức thị trường hàng ngày từ NewsAPI, phân tích bằng GPT-4 để tóm tắt, đánh giá xu hướng và cảnh báo (rủi ro/ cơ hội) rồi gửi trực tiếp Slack. Giúp các sếp tiết kiệm 5+ giờ/tuần theo dõi tin tức, nhận phân tích cá nhân hóa và quyết định nhanh chóng."
slug: "tieu-dong-hoa-bao-cao-tin-tuc-kinh-doanh-ngay-gpt4-slack"
tags: [n8n, automation, no-code, market-research, ai-summarization, slack-integration, news-api, gpt-4]
keywords: [n8n workflow tin tức hàng ngày, tự động hóa tin tức kinh doanh, GPT-4 phân tích tin tức, gửi tin tức Slack, NewsAPI tự động hóa, phân tích xu hướng thị trường]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tức Kinh Doanh Hàng Ngày Với GPT-4 (Gửi Trực Tiếp Slack)**

### **🔥 Giải quyết vấn đề gì?**
Các sếp và đội ngũ Marketing/Sales phải mất **5-10 giờ/tuần** để:
- Theo dõi tin tức thị trường từ nhiều nguồn khác nhau.
- Lọc ra những tin tức **có giá trị thực tế** (không phải chỉ là tiêu đề ảo).
- Phân tích **tín hiệu cơ hội/rủi ro** từ xu hướng mới.
- Gửi báo cáo cho đồng nghiệp một cách **chính xác và cá nhân hóa**.

**Workflow này tự động hóa toàn bộ quy trình đó!** Nó:
✅ **Lấy tin tức** từ NewsAPI theo **quốc gia, ngành nghề và từ khóa** bạn chọn.
✅ **Phân tích bằng GPT-4** để:
   - Tóm tắt **10 tin tức quan trọng nhất**.
   - **Đánh giá cảm xúc** (Cơ hội 🟢 / Rủi ro 🔴 / Trung lập ⚪).
   - **Phân tích xu hướng** và đưa ra **gợi ý chiến lược**.
✅ **Gửi báo cáo trực tiếp Slack** mỗi ngày, giúp bạn **nhận thông tin đầu tiên** mà không cần mở nhiều tab.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** theo dõi tin tức thủ công.
- **Nhận phân tích sâu** từ GPT-4 (không chỉ là tiêu đề).
- **Cảnh báo sớm** về xu hướng mới (cơ hội hoặc rủi ro).
- **Báo cáo tự động** gửi Slack, không quên và không bị trễ.
- **Cá nhân hóa** theo ngành nghề, quốc gia và từ khóa của bạn.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **API Key NewsAPI** (miễn phí cho 1000 request/ngày):
   👉 [Đăng ký NewsAPI](https://newsapi.org/) (Mã giảm giá: **N8NNEWS** - giảm 20%).
2. **API Key OpenAI** (để sử dụng GPT-4):
   👉 [Đăng ký OpenAI](https://platform.openai.com/) (Mã giảm giá: **N8NGPT** - giảm 10%).
3. **Slack Webhook URL**:
   - Tạo **Incoming Webhook** trong Slack:
     1. Mở **Apps & Integrations** → **Incoming Webhooks**.
     2. Chọn **Add Configuration** → **Create**.
     3. Chọn **Channel** và copy **Webhook URL**.
4. **n8n Self-hosted** (để workflow chạy 24/7):
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
   :::
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/6273).
- **Cách 1 (dễ nhất)**: Nhấn **Import** trong n8n Editor → Chọn file JSON.
- **Cách 2 (copy/paste)**:
  1. Mở file JSON trong Notepad++/VSCode.
  2. Copy toàn bộ nội dung.
  3. Trong n8n Editor, nhấn **Import** → **Paste JSON**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node chính**, các sếp cần chú ý cấu hình sau:

#### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy)**
- **Cấu hình**:
  - **Frequency**: Chọn **Daily** (hoặc tùy chỉnh).
  - **Time**: Đặt giờ phù hợp (ví dụ: 8h sáng để nhận tin tức mới nhất).
- **Lưu ý**: Nếu muốn chạy **ngày nào đó**, chọn **Custom** và nhập ngày tháng.

#### **🔹 Node 2: Set User Config (Country, Category, Query)**
- **Cấu hình**:
  - **Country**: `us` (Mỹ), `vn` (Việt Nam), `jp` (Nhật Bản),...
  - **Category**: `business`, `technology`, `health`, `sports`,...
  - **Query**: Từ khóa cụ thể (ví dụ: `OpenAI`, `ChatGPT`, `n8n`, `AI`).
- **Ví dụ**:
  ```json
  {
    "country": "us",
    "category": "technology",
    "query": "AI"
  }
  ```
- **Lưu ý**: Đây là **cơ sở** để NewsAPI lấy tin tức và GPT phân tích.

#### **🔹 Node 3: Fetch News Articles (Lấy tin tức từ NewsAPI)**
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://newsapi.org/v2/top-headlines`.
  - **Headers**:
    - `X-Api-Key`: Điền **API Key NewsAPI** của bạn.
    - `Accept`: `application/json`.
  - **Query Parameters**:
    - `country`: `{country}` (được lấy từ Node 2).
    - `category`: `{category}` (được lấy từ Node 2).
    - `q`: `{query}` (được lấy từ Node 2).
    - `pageSize`: `100` (lấy tối đa 100 tin tức).
- **Lưu ý**:
  - **Không quên điền API Key** vào `X-Api-Key`!
  - Nếu API Key không đúng, workflow sẽ **không lấy được tin tức**.

#### **🔹 Node 4: Merge Config with Articles (Gộp tin tức + cấu hình)**
- **Cấu hình**:
  - Node này **kết hợp** tin tức từ NewsAPI với **cấu hình** (country, category, query).
  - **Không cần chỉnh sửa**, chỉ cần **đảm bảo Node 2 và 3 hoạt động**.

#### **🔹 Node 5: Generate Business Insights (GPT-4 phân tích)**
- **Cấu hình**:
  - **Model**: Chọn **gpt-4** (hoặc `gpt-3.5-turbo` nếu tiết kiệm chi phí).
  - **API Key**: Điền **OpenAI API Key** của bạn.
  - **Prompt**:
    ```plaintext
    Analyze the following news articles and provide a summary of the top 10 most impactful stories.
    For each story, tag it as:
    🟢 Opportunity (positive impact)
    🔴 Risk (negative impact)
    ⚪ Neutral (no clear impact)

    Also, provide an overall trend summary and business recommendations.
    ```
  - **Lưu ý**:
    - **Không chỉnh sửa prompt** nếu muốn kết quả chuẩn.
    - Nếu muốn **tùy chỉnh**, mở **Node Code** (Node 7) và thay đổi logic.

#### **🔹 Node 6: Limit to Top 10 Trends (Lọc 10 tin tức quan trọng nhất)**
- **Cấu hình**:
  - Node này **lọc** 10 tin tức **quan trọng nhất** từ GPT-4.
  - **Không cần chỉnh sửa** nếu muốn giữ mặc định.
  - **Lưu ý**: Nếu muốn **lấy tất cả tin tức**, xóa Node này và chỉnh sửa Node 5.

#### **🔹 Node 7: Post to Slack (Gửi báo cáo Slack)**
- **Cấu hình**:
  - **Credentials**: Chọn **slackOAuth2Api** (đã cấu hình trước).
  - **Channel**: Điền **#channel-tin-tuc** (hoặc channel khác).
  - **Message Format**:
    ```json
    {
      "text": "📰 **Tin tức thị trường hàng ngày**",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Tóm tắt xu hướng:*\n{{ $json["overallSummary"] }}"
          }
        },
        {
          "type": "divider"
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Top 10 tin tức:*"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "{{ $json["topStories"].map(story => `- ${story.title} (${story.sentiment})`).join('\n') }}"
          }
        }
      ]
    }
    ```
  - **Lưu ý**:
    - **Không quên chọn Slack Webhook URL** đã tạo trước.
    - **Kiểm tra lại format** để tin tức hiển thị đẹp Slack.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thực):
   - Nhấn **Run Workflow** và kiểm tra:
     - Tin tức có được lấy không?
     - GPT-4 có phân tích đúng không?
     - Slack có nhận được báo cáo không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH TỰ CHỈNH WORKFLOW]
1. **Thay đổi ngành nghề/từ khóa**:
   - Mở **Node 2 (Set User Config)** và thay đổi `category`/`query`.
   - Ví dụ: Đổi `technology` thành `finance` để theo dõi tin tức tài chính.

2. **Lọc tin tức theo cảm xúc**:
   - Mở **Node 5 (GPT-4)** và chỉnh sửa prompt để **nhấn mạnh** một loại cảm xúc nào đó:
     ```plaintext
     Focus more on **risks** (🔴) when analyzing these articles.
     ```

3. **Gửi báo cáo Email thay vì Slack**:
   - Thay thế **Node 7 (Slack)** bằng **Node Email** (n8n-nodes-base.email).
   - Cấu hình **SMTP** (Gmail, Outlook) để gửi báo cáo tự động.

4. **Lưu log tin tức vào Google Sheets/Notion**:
   - Thêm **Node Google Sheets** sau Node 5 để **lưu tin tức** vào bảng tính.
   - Cấu hình **Sheet Name** và **Header** để dữ liệu được ghi chính xác.

5. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **Node Schedule Trigger** với **tần suất tuần** để nhận báo cáo **mỗi thứ 2**.
   - Ví dụ: `0 8 * * 2` (8h sáng, thứ 2 hàng tuần).

6. **Kết hợp với Zoom/Teams**:
   - Sử dụng **Node Webhook** để gửi tin tức vào **Slack + Zoom Notifications** (nếu cần cảnh báo ưu tiên).
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **quyết định chiến lược** thay vì mất thời gian theo dõi tin tức thủ công. Với **GPT-4 phân tích**, bạn sẽ **nhận báo cáo cá nhân hóa**, **cảnh báo sớm** về xu hướng mới và **tích hợp hoàn hảo** với Slack.

**🚀 Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** để đảm bảo hoạt động.
3. **Bật Active** và **nhận tin tức hàng ngày**!

**Cần hỗ trợ?**
- **Join Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Hỏi trên Forum**: [https://community.n8n.io/](https://community.n8n.io/)

---
**💡 Mẹo cuối**: Nếu muốn **tối ưu chi phí**, thay **GPT-4** bằng **GPT-3.5-turbo** (giá rẻ hơn 90%). Mở **Node 5** và thay đổi **model** từ `gpt-4` sang `gpt-3.5-turbo`.