---
title: "🚀 Tự Động Hoà SEO: Tạo Bố Cục Nội Dung SEO-Friendly Từ Kết Quả Google Top 1 Với SerpAPI & GPT-4o"
description: "Workflow tự động hóa 100% không code giúp các sếp content và SEO nhanh chóng phân tích top 5 bài viết Google, trích xuất nội dung, và tạo ra bố cục SEO MECE (Mutually Exclusive, Collectively Exhaustive) thông minh bằng AI. Giúp tiết kiệm 80% thời gian nghiên cứu và đảm bảo nội dung phù hợp với xu hướng tìm kiếm."
slug: "tay-dong-hoa-seo-tao-bo-cuc-noi-dung-seo-friendly"
tags: [n8n, automation, content-creation, seo, ai-multimodal, serpapi, openai]
keywords: [n8n workflow seo, tự động hóa content marketing, tạo bố cục bài viết seo, serpapi n8n, gpt-4o cho seo, phân tích đối thủ google]
---

# 🚀 **Tự Động Hoà SEO: Tạo Bố Cục Nội Dung SEO-Friendly Từ Kết Quả Google Top 1**

## **Nỗi Đau Của Các Sếp Content & SEO**
Hàng ngày, các sếp phải:
- **Tìm kiếm và đọc** hàng chục bài viết top Google để hiểu xu hướng nội dung.
- **Tập hợp thông tin** từ nhiều nguồn khác nhau, dễ bị bỏ sót hoặc mất thời gian.
- **Viết bố cục** một cách chủ quan, không đảm bảo tính **MECE** (mỗi chủ đề độc lập, toàn bộ nội dung được bao quát).
- **Lo ngại nội dung không phù hợp** với yêu cầu SEO, dẫn đến xếp hạng thấp.

**Workflow này giải quyết tất cả!** Chỉ cần nhập **1 từ khóa**, hệ thống sẽ:
✅ **Scrape** top 5 bài viết Google (bỏ qua forum, UGC như Quora).
✅ **Trích xuất nội dung** từ body HTML, chuyển sang Markdown sạch.
✅ **Phân tích AI** (GPT-4o) để tìm **chủ đề chính** và tạo bố cục SEO **cân bằng, logic**.
✅ **Cung cấp kết quả** sẵn sàng để viết bài hoặc tối ưu nội dung hiện có.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị giới hạn API, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian nghiên cứu** so với cách làm thủ công.
- **Bố cục SEO chính xác** theo xu hướng tìm kiếm thực tế (không phải chủ quan).
- **Nội dung MECE** (mỗi chủ đề rõ ràng, không trùng lặp, toàn bộ nội dung được bao quát).
- **Hoạt động tự động** khi có keyword mới, không cần can thiệp.
- **Dữ liệu sạch** (HTML → Markdown) để AI phân tích hiệu quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản SerpAPI** (miễn phí tier có giới hạn):
   - [Đăng ký SerpAPI](https://serpapi.com/) (API key để lấy kết quả Google).
   - **Lưu ý**: Cần **bỏ qua domain** của mình (nếu có) bằng cách thêm `-site:tendomain.com` trong node "Get search results".
2. **Tài khoản OpenAI** (API key cho GPT-4o):
   - [Đăng ký OpenAI](https://openai.com/api/) và lấy **API Key**.
3. **Credentials trong n8n**:
   - Thêm **2 credentials** trong n8n:
     - `serpApi`: Điền API key từ SerpAPI.
     - `openAiApi`: Điền API key từ OpenAI.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9056](https://n8n.io/workflows/9056) hoặc copy JSON từ canvas.
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
  - **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 node**, các sếp cần chú ý cấu hình sau:

| **Node**                     | **Loại Node**               | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Số Quan Trọng**                          |
|------------------------------|-----------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **On form submission**       | `formTrigger`               | Cấu hình **form** để nhập **keyword** (ví dụ: `keyword: "tự động hóa content marketing"`). | `formData` (cần định nghĩa trường input).     |
| **Get search results**       | `httpRequest` (SerpAPI)     | **Tham số quan trọng**:
   - `url`: `https://serpapi.com/search`
   - **Query params**:
     - `q`: `${keyword}` (được truyền từ form).
     - `engine`: `google`.
     - `hl`: `vi` (ngôn ngữ Việt Nam).
     - `gl`: `vi` (quốc gia Việt Nam).
     - **Bỏ qua domain** (nếu cần): `exclude: "site:tendomain.com"`.
     - **Lọc kết quả**: `filter`: `"all"` (trừ forum/UGC).                          | `serpApi` (credentials).                     |
| **Extract URLs from JSON**   | `set`                        | **Lọc chỉ URL** từ JSON trả về của SerpAPI. Cấu hình:
   - **Key**: `urls`
   - **Value**: `$.organic_results[*].link` (trích xuất danh sách URL).               | `urls` (mảng URL).                           |
| **Split out URLs**           | `splitOut`                   | **Chia URL thành 5 item** (do 5 URL sẽ được scrape).                              | `urls` (truyền từ node trước).                |
| **Scrape Content**           | `httpRequest`               | **Tham số quan trọng**:
   - `url`: `${item.url}` (URL từ node trước).
   - **Headers**:
     - `User-Agent`: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`.
   - **Lưu ý**: **Không scrape quá 5 URL cùng lúc** để tránh bị chặn IP.              | `item.url` (truyền động).                   |
| **Limit**                     | `limit`                      | **Giới hạn 3 bài viết** (do context window của GPT-4o).                           | `3` (số lượng tối đa).                       |
| **Extract body content**     | `html`                       | **Chọn operation**: `extractHtmlContent` để lấy nội dung `<body>`.                  | `html` (truyền từ node scrape).                |
| **Clean up Text**            | `markdown`                   | **Chuyển HTML → Markdown** để loại bỏ tag HTML.                                  | `html` (truyền từ node trước).                |
| **Put all articles into one item** | `aggregate`          | **Gộp 3 bài viết** thành 1 item để truyền cho AI.                                | `$.body` (nội dung Markdown).                 |
| **Create outline**           | `openAi`                     | **Prompt AI**:
   - **Model**: `gpt-4o` (hoặc `gpt-4` nếu không có).
   - **Prompt**:
     ```
     Analyze the following articles and create a MECE outline for a comprehensive blog post about "{keyword}".
     Focus on the most common topics and subtopics mentioned in all articles.
     Structure the outline in a hierarchical format with H1, H2, and H3 headings.
     Ensure the outline is SEO-friendly and covers all key aspects.
     ```
   - **Parameters**:
     - `temperature`: `0.7` (để AI không quá ngẫu nhiên).
     - **Input**: `${aggregatedData.body}` (nội dung gộp từ node trước).               | `openAiApi` (credentials).                   |

#### **3. Kích Hoạt ⚡️**
- **Test run**:
  - Nhập **keyword** vào form (ví dụ: `"tự động hóa content marketing"`).
  - Chạy **manual run** để kiểm tra kết quả.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để hoạt động tự động khi có form submission.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu kết quả vào Google Docs/Notion**:
   - Thêm node **Google Sheets** hoặc **Notion API** sau node `noOp` để tự động lưu bố cục.
   - **Cách làm**:
     - Sau node `Create outline`, thêm node `httpRequest` gọi API của Google Docs/Notion.
     - **Headers**: `Authorization: Bearer ${notionApiKey}` (nếu dùng Notion).
     - **Body**: JSON chứa bố cục từ AI.

2. **Gửi kết quả qua Slack/Email**:
   - Thêm node **Slack Webhook** hoặc **Send Email** sau node `noOp` để thông báo kết quả.
   - **Ví dụ Slack**:
     - Node `httpRequest` → URL: `https://hooks.slack.com/services/...`.
     - **Body**:
       ```json
       {
         "text": "Bố cục SEO cho keyword '{{$keyword}}' đã hoàn thành!",
         "attachments": [{
           "title": "Outline",
           "text": "{{$json}}"
         }]
       }
       ```

3. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Database** để ghi lại lịch sử keyword và kết quả.
   - **Cách làm**:
     - Sau node `Create outline`, thêm node `httpRequest` gọi API của Google Sheets.
     - **Headers**: `Authorization: Bearer ${googleSheetsApiKey}`.
     - **Body**: JSON chứa keyword, URL, và bố cục.

4. **Tối ưu prompt cho AI**:
   - Nếu kết quả AI không phù hợp, **cập nhật prompt** trong node `openAi` để rõ ràng hơn:
     ```
     You are an SEO expert. Create a MECE outline for a blog post about "{keyword}".
     Focus on:
     1. The most frequently mentioned topics in the articles.
     2. Logical hierarchy (H1, H2, H3).
     3. Include meta description ideas and internal linking suggestions.
     ```

---

### 📌 **Kết Luận**
Workflow này là **công cụ thần thánh** cho các sếp content và SEO, giúp:
✔ **Tiết kiệm thời gian** từ 80% so với cách làm thủ công.
✔ **Nội dung SEO chính xác** theo xu hướng thực tế.
✔ **Bố cục logic** (MECE) sẵn sàng viết bài.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** (SerpAPI + OpenAI).
3. **Nhập keyword** và **chạy thử** để thấy kết quả thần kỳ!

**Nếu có vấn đề**, các sếp có thể liên hệ tác giả **Robin Geuens** trên [LinkedIn](https://www.linkedin.com/in/rgeuens/) để hỗ trợ.

---
**🚀 Chúc các sếp tự động hóa thành công!** 🚀