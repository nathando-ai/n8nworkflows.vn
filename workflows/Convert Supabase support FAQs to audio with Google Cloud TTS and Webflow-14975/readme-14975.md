---
title: "🎧 Tự Động Chuyển FAQ Supabase Sang Âm Thanh + Embed Trên Webflow (Google Cloud TTS + Microsoft Teams)"
description: "Workflow tự động hóa hoàn toàn không-code chuyển đổi tất cả câu hỏi thường gặp (FAQ) từ cơ sở dữ liệu Supabase thành âm thanh bằng Google Cloud Text-to-Speech, lưu trữ trên CDN, và tự động embed vào trang hỗ trợ Webflow. Kết hợp với báo cáo Teams để theo dõi tiến trình 24/7."
slug: "tự-dộng-chuyển-faq-supabase-sang-am-than-webflow"
tags: [n8n, automation, support-chatbot, multimodal-ai, google-cloud-tts, webflow, supabase, microsoft-teams]
keywords: [n8n workflow tự động hóa FAQ, chuyển FAQ sang âm thanh, Google Cloud TTS, Webflow tự động embed audio, Supabase automation, Microsoft Teams báo cáo tự động]
---

# 🚀 **Tự Động Chuyển FAQ Supabase Sang Âm Thanh + Embed Trên Webflow (Google Cloud TTS + Microsoft Teams)**

### **Giải pháp cho các sếp:**
Hết sức khó khăn phải không? Khi phải **tạo âm thanh cho từng FAQ thủ công**, cập nhật liên tục trên trang hỗ trợ, và theo dõi tiến trình bằng cách check từng file một? **Workflow này tự động hóa toàn bộ quy trình** chỉ với một cú nhấp chuột, giúp:
- **Tiết kiệm 10+ giờ/lần** so với cách làm thủ công.
- **Cập nhật tự động** âm thanh mới lên trang Webflow khi có FAQ mới.
- **Theo dõi toàn bộ tiến trình** qua Microsoft Teams với báo cáo chi tiết.
- **Tránh trùng lặp** và đảm bảo **mỗi FAQ chỉ được xử lý một lần**.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100%**: Không cần viết code, chỉ cần cấu hình 1 lần là workflow chạy 24/7.
✅ **Âm thanh chuyên nghiệp**: Sử dụng **Google Cloud TTS WaveNet** (người nói tự nhiên, giọng đẹp) với SSML để tối ưu trải nghiệm người dùng.
✅ **Embed tự động trên Webflow**: Âm thanh được lưu trên CDN và tự động embed vào trang hỗ trợ, không cần can thiệp thủ công.
✅ **Báo cáo Teams chi tiết**: Sau khi xử lý xong, workflow gửi **báo cáo adaptable card** với danh sách FAQ đã chuyển đổi, link âm thanh, và trạng thái.
✅ **Idempotent (an toàn)**: Không reprocess FAQ đã có âm thanh (trừ khi bật chế độ `force_regenerate`).
✅ **Dedup & Sort tự động**: Loại bỏ trùng lặp và sắp xếp FAQ theo danh mục trước khi xử lý.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (khuyến nghị cài trên VPS để chạy 24/7).
2. **Supabase**:
   - Project URL + **Service Role Key**.
   - Bảng `faqs` với các cột: `id`, `question`, `answer`, `category`, `audio_url`, `audio_generated_at`, `status`, `webflow_item_id`.
3. **Google Cloud TTS**:
   - **API Key** (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
   - **Enable Text-to-Speech API**.
4. **UploadToURL**:
   - Endpoint để lưu trữ file MP3 (ví dụ: Cloudflare R2, AWS S3, hoặc CDN khác).
5. **Webflow**:
   - **API Token** (tạo tại **Project Settings > API**).
   - **Collection ID** của trang FAQ hỗ trợ (để update `audio-embed-url`).
6. **Microsoft Teams**:
   - **Incoming Webhook URL** cho channel hỗ trợ (không cần OAuth).
7. **Webhook Trigger**:
   - URL của node Webhook trong workflow (`http://<your-n8n-server>/faq-audio-generate`).
   - Kết nối từ CMS (Webflow, Typeform, hoặc button manual).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/14975) hoặc copy toàn bộ JSON từ canvas.
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor**.
  - Nhấn **Import** > **Paste JSON** và dán toàn bộ mã.
  - Hoặc tải file `.json` từ link trên và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **16 node**, các sếp cần **cấu hình chi tiết** như sau:

#### **🔹 Node 1: Webhook — Receive FAQ Audio Job Request**
- **Path**: `faq-audio-generate` (không đổi).
- **HTTP Method**: `POST`.
- **Credentials**: Không cần, nhưng lưu ý **URL này phải được expose** (nếu self-hosted, sử dụng Nginx Reverse Proxy).
- **Payload Example**:
  ```json
  {
    "category": "billing",  // (tùy chọn: lọc theo danh mục)
    "faq_ids": ["123", "456"], // (tùy chọn: chỉ xử lý những FAQ này)
    "force_regenerate": false // (true để reprocess FAQ đã có âm thanh)
  }
  ```

#### **🔹 Node 2 & 3: Supabase — Read Unprocessed FAQs + Code — Filter & Split FAQ Rows**
- **Supabase HTTP Request**:
  - **URL**: `https://<your-supabase-url>/rest/v1/faqs?select=*&status=neq.audio_published`.
  - **Headers**:
    ```json
    {
      "apikey": "<your-supabase-service-role-key>",
      "Authorization": "Bearer <your-supabase-service-role-key>"
    }
    ```
  - **Query Parameters**:
    - Nếu có `category` trong payload, thêm `&category=eq.<category>`.
    - Nếu có `faq_ids`, thêm `&id=in.(<id1>,<id2>)`.
  - **Code Node**:
    - **Lọc bỏ** các FAQ đã có `audio_url` (trừ khi `force_regenerate=true`).

#### **🔹 Node 4 & 5: Item Lists — Deduplicate & Sort**
- **Remove Duplicates**:
  - **Key**: `id` (loại bỏ trùng lặp FAQ).
- **Sort**:
  - **Field**: `category` (sắp xếp theo danh mục).
  - **Order**: `asc` (A-Z).

#### **🔹 Node 6 & 7: Code — Build SSML + Loop Over Items**
- **SSML Template** (được build trong Code Node):
  ```xml
  <speak>
    <prosody rate="slow">
      <break time="0.5s"/>
      <emphasis level="strong">Question:</emphasis> <say-as interpret-as="characters">[question]</say-as>
      <break time="0.5s"/>
      <emphasis level="moderate">Answer:</emphasis> [answer]
    </prosody>
  </speak>
  ```
  - **Lưu ý**: Thay thế `[question]` và `[answer]` bằng dữ liệu từ Supabase.

#### **🔹 Node 8: Google Cloud TTS — Synthesize FAQ Audio**
- **URL**: `https://texttospeech.googleapis.com/v1/text:synthesize`.
- **Headers**:
  ```json
  {
    "Authorization": "Bearer <your-google-cloud-api-key>",
    "Content-Type": "application/json"
  }
  ```
- **Body**:
  ```json
  {
    "input": { "ssml": "<your-ssml-here>" },
    "voice": { "languageCode": "en-US", "name": "en-US-WaveNet-D" },
    "audioConfig": { "audioEncoding": "MP3" }
  }
  ```
- **Output**: Trả về **base64-encoded MP3**.

#### **🔹 Node 9 & 10: Code — Decode Base64 + UploadToURL**
- **Decode Base64**:
  - Sử dụng **JavaScript** trong Code Node để chuyển base64 thành binary:
    ```javascript
    const base64Data = $input.all()[0].json.audioContent;
    const binaryString = atob(base64Data);
    const bytes = new Uint8Array(binaryString.length);
    for (let i = 0; i < binaryString.length; i++) {
      bytes[i] = binaryString.charCodeAt(i);
    }
    return { binaryData: bytes.buffer };
    ```
- **UploadToURL**:
  - **URL**: Endpoint của CDN (ví dụ: `https://<your-cdn-url>/upload`).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer <your-cdn-api-key>"
    }
    ```
  - **Body**: Binary data từ node trước.

#### **🔹 Node 11 & 12: Webflow & Supabase — Update Audio URL**
- **Webflow HTTP Request**:
  - **URL**: `https://<your-webflow-site>/api/v1/collections/<collection-id>/items/<webflow-item-id>`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer <your-webflow-api-token>",
      "Content-Type": "application/json"
    }
    ```
  - **Method**: `PATCH`.
  - **Body**:
    ```json
    {
      "audio-embed-url": "<audio-url-from-cdn>",
      "audio-published": true
    }
    ```
- **Supabase Update**:
  - **URL**: `https://<your-supabase-url>/rest/v1/faqs/<faq-id>`.
  - **Method**: `PATCH`.
  - **Body**:
    ```json
    {
      "audio_url": "<audio-url-from-cdn>",
      "audio_generated_at": $datetime.now().toISOString(),
      "status": "audio_published"
    }
    ```

#### **🔹 Node 13 & 14: Code — Build Summary + Microsoft Teams**
- **Summary Object**:
  ```json
  {
    "processed_count": $node["Loop Over Items"].json.length,
    "successes": $node["Loop Over Items"].json.filter(item => item.error === null),
    "failures": $node["Loop Over Items"].json.filter(item => item.error !== null),
    "faq_details": $node["Loop Over Items"].json.map(item => ({
      id: item.json.id,
      question: item.json.question,
      category: item.json.category,
      audio_url: item.json.audio_url
    }))
  }
  ```
- **Teams Adaptive Card**:
  - **URL**: `<your-teams-incoming-webhook-url>`.
  - **Body**: JSON Adaptive Card với danh sách FAQ và link âm thanh.

#### **🔹 Node 15: Respond to Webhook**
- **Trả về JSON**:
  ```json
  {
    "status": "success",
    "processed_count": $node["Code — Build Summary"].json.processed_count,
    "timestamp": $datetime.now().toISOString(),
    "faq_ids": $node["Code — Build Summary"].json.faq_details.map(item => item.id),
    "audio_urls": $node["Code — Build Summary"].json.faq_details.map(item => item.audio_url)
  }
  ```

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi **payload mẫu** đến Webhook:
     ```json
     {
       "category": "billing"
     }
     ```
   - Kiểm tra **Teams** và **Webflow** để xác nhận âm thanh đã được tạo và embed.
2. **Bật Active**:
   - Nhấn **Active** trên workflow trong n8n Editor.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì Teams, có thể gửi báo cáo qua **Slack Webhook** hoặc **Telegram Bot** bằng node `httpRequest`.
2. **Lưu log tự động**:
   - Sử dụng **Google Sheets** hoặc **Airtable** để lưu lịch sử xử lý FAQ bằng node `httpRequest`.
3. **Chế độ reprocess tự động**:
   - Tạo **cron job** trong n8n để reprocess FAQ đã có âm thanh sau 1 tháng (để cập nhật giọng nói mới).
4. **Tối ưu Google TTS**:
   - Thử **ngôn ngữ khác** (ví dụ: `en-US-Wavenet-C` cho giọng nữ) hoặc **tốc độ khác** (`rate="fast"`).
5. **CDN miễn phí**:
   - Sử dụng **Cloudflare R2** hoặc **AWS S3** với **UploadToURL** để lưu trữ âm thanh rẻ hơn.
6. **Báo cáo email**:
   - Gửi **email tự động** (ví dụ: Gmail API) khi workflow hoàn thành bằng node `httpRequest`.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi công việc thủ công chuyển FAQ sang âm thanh, đồng thời **tự động hóa embed** trên Webflow và **báo cáo tiến trình** qua Teams. **Chỉ cần cấu hình 1 lần**, workflow sẽ chạy 24/7, đảm bảo **mọi FAQ đều có âm thanh chuyên nghiệp** và **trang hỗ trợ luôn cập nhật mới nhất**.

👉 **Bắt đầu ngay!**
1. **Cài n8n trên VPS** (khuyến nghị [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Kết nối Webhook** từ CMS hoặc Typeform.
4. **Nhấn Active** và **chờ workflow làm việc!**

**Hỏi gì về workflow này không?** Các sếp có thể comment bên dưới hoặc liên hệ với tôi qua [LinkedIn](https://linkedin.com/in/yourprofile) để được hỗ trợ chi tiết! 🚀