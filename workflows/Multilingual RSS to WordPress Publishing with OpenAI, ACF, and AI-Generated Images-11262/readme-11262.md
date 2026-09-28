---
title: "🚀 Tự động đa ngôn ngữ RSS → WordPress với OpenAI, ACF & Hình ảnh AI"
description: "Giải pháp n8n kéo RSS, trích xuất nội dung, viết lại, dịch đa ngôn ngữ, tạo ảnh bìa AI và đăng tự động lên WordPress có ACF."
slug: "tudong-rss-wordpress-multilingual-openai-acf"
tags: [n8n, automation, no-code, content-creation, ai, wordpress]
keywords: [n8n workflow, tự động hóa, RSS, WordPress, OpenAI, ACF, đa ngôn ngữ]
---

# 🚀 Tự động đa ngôn ngữ RSS → WordPress với OpenAI, ACF & Hình ảnh AI

Bạn đã từng phải **chép‑dán, dịch thủ công, tạo ảnh bìa và đăng bài** cho từng ngôn ngữ trên WordPress?  
Công việc này tiêu tốn hàng giờ mỗi ngày, dễ sai sót và không thể mở rộng.  
Workflow này sẽ **tự động 100 %**: đọc RSS, lấy nội dung, viết lại, dịch sang nhiều ngôn ngữ, tạo ảnh bìa AI và đăng lên WordPress (cùng ACF) chỉ trong vài giây – không cần một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: một RSS mới được xử lý trong < 30 giây.  
- **Độ chính xác cao**: OpenAI loại bỏ quảng cáo, HTML rác và viết lại nội dung chuẩn SEO.  
- **Đa ngôn ngữ**: cùng một bài viết xuất hiện ở mọi ngôn ngữ bạn cấu hình.  
- **Hình ảnh độc đáo**: AI tạo ảnh bìa phù hợp với phong cách thương hiệu.  
- **Hoạt động liên tục**: chạy 24/7, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **WordPress** (cài ACF) và **REST API** bật, tạo **Application Password** hoặc JWT.  
- **OpenAI API key** (để viết lại, dịch và tạo prompt).  
- **Replicate.com API key** (hoặc DALL·E) để sinh ảnh bìa.  
- **Firecrawl / HTTP Bearer token** (hoặc bất kỳ dịch vụ scrape nào) để lấy HTML của bài gốc.  
- **RSS feed URL** muốn theo dõi (ví dụ: `https://www.aljazeera.com/xml/rss/all.xml`).  
- **Ngôn ngữ chính** + **danh sách ngôn ngữ dịch** (ví dụ: `["english","italian"]`).  
- **Tên trường ACF** cho mỗi ngôn ngữ (ví dụ: `title_english`, `content_english`, `title_italian`, `content_italian`).  
- **n8n** đã cài đặt (Self‑hosted hoặc Cloud) và quyền **Import workflow**.  
:::

### 🚀 Cách import & Lên đồ

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON file** và tải file `multilingual-rss-wordpress.json` (được cung cấp trong mục tải xuống).  
3. Hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard** → **Import**.  

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách **node quan trọng** và cách cấu hình chúng:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **RSS Feed Trigger** | `rssFeedReadTrigger` | - **Feed URL**: URL RSS của bạn.<br>- **Interval**: `1 hour` (hoặc tùy ý). |
| **Scrape Page** | `httpRequest` (Bearer) | - **Authentication**: chọn credential `httpBearerAuth` (Firecrawl token).<br>- **URL**: `{{$json["link"]}}` (lấy từ trigger). |
| **Detect and Extract Article from Page HTML** | `openAi` | - **Model**: `gpt-4o` (hoặc `gpt-3.5-turbo`).<br>- **Prompt**: “Extract the main article body and title from the following HTML, remove ads and tags.”<br>- **Output**: `article_body`, `article_title`. |
| **Assign URL** | `set` | - Gán `url` → `{{$json["link"]}}` để dùng sau. |
| **Assign and Multilingual Prompt** | `set` | - Tạo biến `translation_prompt` chứa prompt dịch (ví dụ: “Translate the following article to {{language}}, keep the same tone.”). |
| **Translate news** | `openAi` | - **Model**: `gpt-4o-mini`.<br>- **Input**: `{{$json["article_body"]}}` + `{{$json["translation_prompt"]}}`.<br>- **Loop**: chạy cho mỗi ngôn ngữ (sử dụng **Split Out Translate Languages**). |
| **Rewrite article in default language** | `openAi` | - Prompt: “Rewrite the article in {{main_language}} with a tech‑news style.” |
| **Get rewrited article** | `set` | - Lưu kết quả `rewritten_body` và `rewritten_title`. |
| **Generate Image Prompt** | `code` (JavaScript) | - Dùng JS để tạo prompt dựa trên tiêu đề và nội dung (ví dụ: `return {prompt: \`A futuristic illustration of ${title}\`}`); output `image_prompt`. |
| **Generate Featured Image** | `httpRequest` (Header) | - **Credential**: `httpHeaderAuth` (Replicate API).<br>- **Body**: `{ "prompt": "{{$json["image_prompt"]}}", "model": "stability-ai/stable-diffusion" }`.<br>- **Output**: URL ảnh tạm. |
| **Download Image** | `httpRequest` | - **URL**: `{{$json["generated_image_url"]}}`.<br>- **Response Format**: `File`. |
| **Upload image to wordpress** | `httpRequest` (WordPress) | - **Credential**: `wordpressApi`.<br>- **Endpoint**: `/wp/v2/media`.<br>- **Headers**: `Content-Disposition: attachment; filename="featured.jpg"`.<br>- **Output**: `media_id`. |
| **Get Image ID** | `set` | - Lưu `media_id` → `featured_image_id`. |
| **Merge image and articles variables** | `merge` | - Kết hợp `featured_image_id`, `rewritten_*`, và các bản dịch thành một object duy nhất. |
| **Publish article and translations** | `httpRequest` (WordPress) | - **Credential**: `wordpressApi`.<br>- **Endpoint**: `/wp/v2/posts`.<br>- **Body**: JSON chứa `title`, `content`, `acf` (các trường ACF cho từng ngôn ngữ), `featured_media: {{$json["featured_image_id"]}}`.<br>- **Status**: `publish` (hoặc `draft` để test). |
| **Split Out Translate Languages** | `splitOut` | - Tách mảng ngôn ngữ (`["english","italian"]`) để chạy node **Translate news** cho từng ngôn ngữ. |
| **Merge Article with Translations** | `merge` | - Gộp lại các bản dịch vào cùng một payload trước khi gửi tới WordPress. |
| **Clean Data**, **Code in JavaScript**, **Aggregate**, **StickyNote** | `set`/`code`/`aggregate`/`stickyNote` | - Các node này chỉ dùng để chuẩn hoá dữ liệu, tạo log, hoặc ghi chú. Kiểm tra chúng để chắc chắn không có trường rỗng. |

> **Lưu ý:**  
> - Mỗi node **OpenAI** cần chọn **Credential** `openAiApi`.  
> - Đối với **httpRequest** tới Replicate, thêm header `Authorization: Token YOUR_REPLICATE_TOKEN`.  
> - Đảm bảo **WordPress API** có quyền `edit_posts` và `upload_files`.  

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra log từng node, đặc biệt là `Publish article and translations`.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên‑phải).  
3. Kiểm tra WordPress: các bài viết mới xuất hiện, các trường ACF đã được điền đúng ngôn ngữ, ảnh bìa hiển thị.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Publish article` để gửi tin nhắn báo thành công hoặc lỗi.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại `title`, `url`, `status`, `publish_id`.  
- **Tối ưu chi phí OpenAI**: Chỉ dùng `gpt-4o-mini` cho dịch, `gpt-4o` cho viết lại.  
- **Tạo nhiều ảnh**: Dùng vòng lặp `SplitInBatches` để tạo 3‑5 biến thể ảnh, chọn ng