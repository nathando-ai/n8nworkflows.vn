---
title: "🚀 Chuyển Video YouTube Sang Bài Blog SEO Tự Động Với Wayin + GPT-4o-mini (Không Cần Code)"
description: "Tự động hóa quy trình chuyển video YouTube thành bài blog SEO hoàn chỉnh với tiêu đề, slug, nội dung chi tiết, FAQ và thẻ meta - chỉ cần gửi URL video qua Webhook. Kết quả được lưu vào Google Sheets với cấu trúc chuẩn SEO."
slug: "chuyen-video-youtube-sang-blog-seo-tu-dong"
tags: [n8n, automation, content-creation, ai-multimodal, seo, wayin, gpt-4o-mini]
keywords: [n8n workflow youtube seo, tự động hóa bài blog từ video, wayin ai transcription, gpt-4o-mini blog generator, google sheets seo template]
---

# 🚀 **Chuyển Video YouTube Sang Bài Blog SEO Tự Động Với Wayin + GPT-4o-mini**

### **Giải pháp hoàn hảo cho các sếp Content Marketer**
Bạn đã bao giờ phải mất **giờ đồng hồ** để transcribe video YouTube, nghiên cứu từ khóa, và viết bài blog SEO từ đầu? Hay thậm chí phải **lặp lại công việc này hàng tuần** cho nhiều video? **Workflow này sẽ tự động hóa toàn bộ quy trình** chỉ với một cú nhấp chuột!

Với **Wayin AI** (API transcribe video chính xác) và **GPT-4o-mini** (AI viết blog SEO chuyên nghiệp), workflow này sẽ:
✅ **Tự động transcribe** video YouTube sang văn bản (bao gồm cả tiếng Việt và nhiều ngôn ngữ khác).
✅ **Tạo bài blog SEO hoàn chỉnh** với tiêu đề, slug, nội dung chi tiết, FAQ, thẻ meta và cấu trúc H2/H3.
✅ **Lưu kết quả vào Google Sheets** với cấu trúc chuẩn SEO (từ khóa, thời gian đọc, thẻ tag, độ dài bài viết...).
✅ **Gửi phản hồi thành công** qua Webhook để bạn có thể tích hợp với hệ thống khác (Slack, Telegram, CRM...).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **30 phút/bài viết** xuống còn **vài giây** (chỉ cần gửi URL video).
- **Nội dung SEO chuyên nghiệp**: Tiêu đề, slug, meta description và nội dung được tối ưu hóa tự động.
- **Cấu trúc bài viết chuẩn**: H2/H3, FAQ, CTA và thẻ tag được AI phân tích và thêm vào.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp thủ công.
- **Dữ liệu tập trung**: Tất cả bài viết được lưu vào **Google Sheets** với cấu trúc chuẩn, dễ quản lý.
- **Tích hợp linh hoạt**: Kết quả có thể được gửi đến **Slack, Telegram, WordPress, Notion...** thông qua Webhook.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✅ **Tài khoản Wayin AI** (để transcribe video):
   - [Đăng ký Wayin](https://wayin.ai/) và lấy **API Key**.
   - [Hướng dẫn sử dụng API Wayin](https://docs.wayin.ai/).

✅ **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.

✅ **Google Sheets** (để lưu kết quả):
   - Tạo một **Google Sheet mới** với các cột sau:
     | Date | Video URL | SEO Title | Slug | Focus Keyword | Meta Description | Secondary Keywords | Read Time | Tags | Word Count | Duration (min) | Status |
   - **Chia sẻ với n8n** (cấu hình OAuth trong node `Save to Google Sheets`).

✅ **VPS hoặc n8n Cloud** (để chạy workflow 24/7):
   - Nếu tự host, các sếp cần **cài đặt n8n** trên VPS (hướng dẫn [tại đây](https://docs.n8n.io/hosting/installation/)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/14263).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
   *Hoặc* copy toàn bộ JSON và dán vào **Import Workflow** (tùy chọn **Paste JSON**).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

##### **🔹 Node 1: Receive Video URL (Webhook)**
- **Method**: POST (đã mặc định).
- **Body**: `{ "url": "https://youtube.com/watch?v=..." }`.
- **Lưu ý**:
  - Đảm bảo **Webhook URL** trong node này **không bị thay đổi** (nếu muốn gọi lại workflow sau này).
  - Test bằng **Postman** hoặc **cURL** để kiểm tra:
    ```bash
    curl -X POST "https://[your-n8n-url]/webhook/43129e0a-92b3-4f28-b2a8-97ef86d287c6" \
    -H "Content-Type: application/json" \
    -d '{"url": "https://youtube.com/watch?v=dQw4w9WgXcQ"}'
    ```

##### **🔹 Node 2 & 3: Submit Transcription & Poll Transcription Status (HTTP Request)**
- **Thêm API Key Wayin**:
  - Trong **Credentials** của node `Submit Transcription — Wayin`, chọn **New Credentials** → **HTTP Request**.
  - Điền:
    - **Name**: `Wayin API Key`
    - **Type**: `Bearer Token`
    - **Token**: `sk_your_wayin_api_key_here`
  - Lặp lại cho node `Poll Transcription Status`.

##### **🔹 Node 4: Wait 5 Seconds (Wait)**
- **Thời gian đợi**: Đã mặc định là **5 giây** (đủ để Wayin xử lý).
- *Không cần chỉnh sửa* trừ khi Wayin trả về kết quả quá nhanh/chậm.

##### **🔹 Node 5: Is Transcription Complete? (If)**
- **Logic**: Nếu trạng thái transcribe là `SUCCEEDED`, workflow tiếp tục.
- *Không cần chỉnh sửa* (đã cấu hình tự động).

##### **🔹 Node 6: Process Transcript Data (Code)**
- **Mã JavaScript**: Đã tối ưu để **ghép các đoạn transcript** và tính **tổng từ và thời gian**.
- *Không cần chỉnh sửa* trừ khi cần thay đổi cách tính toán.

##### **🔹 Node 7 & 8: Generate SEO Blog Post (Agent + GPT Model)**
- **Thêm Credentials OpenAI**:
  - Trong **Credentials** của node `GPT Model — Blog Generator` và `GPT Model — Output Parser`, chọn **New Credentials** → **OpenAI**.
  - Điền:
    - **Name**: `OpenAI API Key`
    - **Type**: `API Key`
    - **Key**: `sk-your-openai-api-key-here`
- **Cấu hình AI**:
  - **Model**: Đã mặc định là `gpt-4o-mini` (rẻ và hiệu quả).
  - *Nếu muốn chất lượng cao hơn*, thay bằng `gpt-4o` (tốn kém hơn).
- **System Prompt (Node Agent)**:
  - Mở node `Generate SEO Blog Post` → **Agent** → **System Prompt**.
  - Điền **prompt SEO chuyên nghiệp** (ví dụ):
    ```json
    {
      "task": "Convert video transcript into a detailed SEO blog post",
      "structure": {
        "title": "SEO Title (50-60 characters)",
        "slug": "URL-friendly slug",
        "meta_description": "Meta description (150-160 characters)",
        "sections": [
          {
            "h2": "Section Title",
            "content": "Detailed content (300+ words)",
            "keywords": ["keyword1", "keyword2"]
          }
        ],
        "faq": ["FAQ 1", "FAQ 2"],
        "cta": "Call-to-action",
        "tags": ["tag1", "tag2"]
      }
    }
    ```

##### **🔹 Node 9 & 10: Parse Blog JSON Output (Output Parser Structured)**
- **Schema JSON**: Đã cấu hình để **kiểm tra và sửa lỗi** JSON từ AI.
- *Không cần chỉnh sửa* trừ khi muốn thay đổi cấu trúc output.

##### **🔹 Node 11: Save to Google Sheets (Google Sheets)**
- **Thêm OAuth Google**:
  - Trong **Credentials**, chọn **New Credentials** → **Google Sheets**.
  - Đăng nhập tài khoản Google và **cho phép quyền truy cập**.
- **Cấu hình Sheet**:
  - Điền **Google Sheet ID** (tìm trong URL của sheet: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - Chọn **Sheet Name**: `Blog Drafts` (hoặc tên sheet đã tạo).
  - **Operation**: `append` (thêm hàng mới).

##### **🔹 Node 12: Return Success Response (Respond To Webhook)**
- **Body**: Đã mặc định trả về:
  ```json
  {
    "status": "success",
    "message": "Blog post generated successfully!",
    "data": {
      "url": "{{$json['Video URL']}}",
      "title": "{{$json['SEO Title']}}",
      "slug": "{{$json['Slug']}}"
    }
  }
  ```
- *Không cần chỉnh sửa* trừ khi muốn thay đổi nội dung phản hồi.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một video mẫu:
   - Gửi URL video qua Webhook (ví dụ: `https://your-n8n-url/webhook/43129e0a-92b3-4f28-b2a8-97ef86d287c6`).
   - Kiểm tra **Google Sheets** xem kết quả có được lưu không.
2. **Bật Active** workflow:
   - Nhấn **Active** trên tab **Workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sau node `Return Success Response`, thêm **node HTTP Request** để gửi thông báo thành công về Slack/Telegram.
   - Ví dụ:
     ```json
     {
       "url": "https://api.telegram.org/bot[BOT_TOKEN]/sendMessage",
       "method": "POST",
       "body": {
         "chat_id": "[CHAT_ID]",
         "text": "🚀 Blog post đã được tạo thành công!\nTitle: {{ $json['SEO Title'] }}\nURL: {{ $json['Slug'] }}"
       }
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm **node `n8n-nodes-base.respondToWebhook`** sau `Save to Google Sheets` để gửi log chi tiết về quá trình chạy.
   - Ví dụ:
     ```json
     {
       "status": "{{ $json['Status'] }}",
       "word_count": "{{ $json['Word Count'] }}",
       "duration": "{{ $json['Duration (min)'] }}",
       "timestamp": "{{ $nodeHelper.getCurrentDate('YYYY-MM-DD HH:mm:ss') }}"
     }
     ```

3. **Tự động publish lên WordPress**:
   - Thay thế node `Save to Google Sheets` bằng **node WordPress REST API** để tự động đăng bài.
   - Cấu hình:
     - Thêm **Credentials WordPress** (API Key hoặc OAuth).
     - Gửi dữ liệu JSON từ AI sang WordPress với `POST /wp-json/wp/v2/posts`.

4. **Chuyển đổi video nhiều ngôn ngữ**:
   - Trong node `Submit Transcription — Wayin`, thay đổi `target_lang` từ `en` sang `vi` (hoặc ngôn ngữ khác) để transcribe video tiếng Việt.

5. **Optimize AI Prompt**:
   - Nếu muốn **blog có cấu trúc khác**, chỉnh sửa **System Prompt** trong node `Generate SEO Blog Post` để thêm/bỏ các phần (ví dụ: thêm "How-to Guide" hoặc "Comparison Table").

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp Content Marketer, giúp họ **tự động hóa quy trình chuyển video thành bài blog SEO** chỉ trong vài giây. **Không cần code**, không cần kiến thức kỹ thuật sâu, chỉ cần **cấu hình đúng các API Key** và **Google Sheets**.

🔥 **Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình các API Key.
2. **Test với 1-2 video** để kiểm tra kết quả.
3. **Tích hợp với Slack/Telegram** để nhận thông báo tự động.
4. **Tự động hóa toàn bộ pipeline** của bạn!

**Nếu có vấn đề**, các sếp có thể:
- **Trả lời ở phần Comments** dưới đây.
- **Gửi tin nhắn** cho [isaWOW](https://n8n.io/workflows/14263) (tác giả workflow) để hỗ trợ.
- **Đăng ký VPS** để chạy workflow ổn định: [TinoHost](https://tino.vn/vps-n8n?affid=388).

**Chúc các sếp thành công với chiến dịch Content Marketing tự động hóa!** 🚀