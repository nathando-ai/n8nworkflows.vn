---
title: "🚀 Tự Động Chuyển Đổi Bài Blog Thành Nội Dung Mạng Xã Hội Sáng Tạo Với Google Gemini AI (Không Cần Code)"
description: "Workflow tự động hóa chuyển đổi bài viết blog thành các bài post đa dạng cho Facebook, Instagram, LinkedIn, Twitter với AI Google Gemini - tiết kiệm thời gian lên tới 80% cho các sếp marketing. Hỗ trợ tự động hóa nội dung 24/7, cá nhân hóa và tối ưu SEO."
slug: "tieu-dong-bai-blog-thanh-noi-dung-mang-xa-hoi-voi-google-gemini"
tags: [n8n, automation, no-code, google-gemini, social-media, ai-chatbot, content-marketing]
keywords: [n8n workflow tự động hóa, chuyển đổi bài blog thành post mạng xã hội, google gemini ai, tự động hóa nội dung marketing, công cụ tạo nội dung tự động]
---

# 🚀 **Tự Động Chuyển Đổi Bài Blog Thành Nội Dung Mạng Xã Hội Sáng Tạo Với Google Gemini AI**

### **Giải pháp cho các sếp marketing: Tiết kiệm 80% thời gian viết post, tối ưu nội dung cho mọi nền tảng**

Hiện nay, các sếp marketing phải mất **giờ đồng hồ** để viết lại bài blog thành các bài post phù hợp cho **Facebook, Instagram, LinkedIn, Twitter**... với nội dung đa dạng, hấp dẫn và tối ưu SEO. Kết quả? **Nội dung trùng lặp, mất thời gian, và không tối ưu hóa** cho từng nền tảng.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động chuyển đổi** bài blog thành **5-10 bài post đa dạng** (tóm tắt, câu hỏi thách thức, quote, post hình ảnh, post video, post carousel...)
✅ **Sử dụng Google Gemini AI** để **tối ưu nội dung** cho từng nền tảng khác nhau
✅ **Cá nhân hóa** theo tone voice của brand
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết lại bài blog từ đầu cho từng nền tảng.
- **Nội dung đa dạng**: Tạo ra **5-10 biến thể post** từ một bài blog duy nhất.
- **Tối ưu SEO & engagement**: AI Google Gemini **tự động điều chỉnh** nội dung phù hợp với từng nền tảng.
- **Hoạt động tự động**: Chỉ cần **gửi URL bài blog** là workflow sẽ **tự động xử lý** và trả về nội dung sẵn sàng đăng.
- **Cá nhân hóa brand**: Đặt tone voice, style và hashtag riêng cho mỗi post.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **API Key Google Gemini** (trong `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`)
✔ **Tài khoản n8n** (đăng ký tại [n8n.io](https://n8n.io/))
✔ **URL bài blog** (cần gửi qua Webhook để workflow xử lý)
✔ **(Tùy chọn) Tài khoản Slack/Telegram** (để nhận kết quả thông báo)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow được cung cấp dưới dạng **JSON**, các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13334](https://n8n.io/workflows/13334) và **import** vào n8n Editor.
- **Copy & Paste JSON** từ file vào **n8n Editor** (tab **Import/Export**).

**Cách import:**
1. Mở **n8n Editor** (trang chủ của workflow).
2. Nhấn **Import** (hoặc **Import/Export** > **Import from JSON**).
3. Dán JSON từ file vào và nhấn **Import**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **🔹 Node 1: Receive Blog URL (Webhook)**
- **Cấu hình Webhook** để nhận URL bài blog từ bên ngoài.
- **Method:** `POST`
- **Trigger:** `Body` (JSON hoặc form-data)
- **Lưu ý:**
  - Các sếp cần **bật Webhook** và **lưu URL Webhook** để gửi request từ bên ngoài.
  - Ví dụ: `https://tên-domain-n8n.com/webhook/receive-blog-url`

##### **🔹 Node 2: Config (Set)**
- **Không cần chỉnh sửa** (nếu không muốn tùy chỉnh).
- Nếu muốn **cá nhân hóa tone voice**, các sếp có thể chỉnh sửa **JSON Config** trong node này:
  ```json
  {
    "socialPlatforms": ["facebook", "instagram", "linkedin", "twitter"],
    "toneVoice": "professional",
    "hashtags": ["#Marketing", "#ContentCreation", "#AIAutomation"]
  }
  ```

##### **🔹 Node 3: Fetch Blog Article (HTTP Request)**
- **Không cần chỉnh sửa** (nếu muốn lấy nội dung từ URL blog).
- Nếu blog **không cho phép fetch tự động**, các sếp cần:
  - **Chỉnh sửa URL** trong node này để trỏ đến **API của CMS** (WordPress, Ghost, etc.).
  - **Thêm headers** (nếu cần) như `Authorization` hoặc `User-Agent`.

##### **🔹 Node 4 & 5: Generate Social Posts (ChainLLM + Google Gemini Chat Model)**
- **BẮT BUỘC điền API Key Google Gemini** trong node `lmChatGoogleGemini`:
  1. Mở node `Google Gemini Chat Model`.
  2. Nhấn **Add Credential** > **Google Gemini**.
  3. Điền **API Key** từ [Google AI Studio](https://makersuite.google.com/app/apikey).
  4. Chọn **Model** (ví dụ: `gemini-pro`).

- **Prompt mặc định** đã được tối ưu để tạo **5-10 biến thể post** từ bài blog.
- Nếu muốn **tùy chỉnh prompt**, chỉnh sửa trong node `Generate Social Posts`:
  ```json
  {
    "prompt": "Tôi có bài blog về {{blogTitle}}. Hãy tạo ra 5 bài post đa dạng cho các nền tảng mạng xã hội (Facebook, Instagram, LinkedIn, Twitter) với nội dung tối ưu SEO và engagement. Mỗi post phải có tone voice chuyên nghiệp và phù hợp với nền tảng."
  }
  ```

##### **🔹 Node 6: Format Social Media Output (Code)**
- **Không cần chỉnh sửa** (nếu muốn kết quả ra dạng JSON chuẩn).
- Nếu muốn **thêm hoặc chỉnh sửa format**, mở node `Format Social Media Output` và chỉnh sửa **JavaScript**:
  ```javascript
  // Ví dụ: Thêm trường "postType" vào output
  return {
    ...item.json,
    postType: item.json.socialPlatform
  };
  ```

##### **🔹 Node 7: Return Generated Content (RespondToWebhook)**
- **Không cần chỉnh sửa** (trả về kết quả dưới dạng JSON).
- Nếu muốn **gửi kết quả qua Slack/Telegram**, các sếp có thể:
  - Thêm node **Slack/Telegram** trước node này.
  - Chỉnh sửa **Response Body** để phù hợp với format của dịch vụ.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một URL bài blog mẫu:
   - Gửi request POST đến Webhook với body:
     ```json
     {
       "blogUrl": "https://example.com/blog/tieu-dong-noi-dung-marketing"
     }
     ```
   - Kiểm tra **output** trong node `Return Generated Content`.

2. **Bật Active workflow**:
   - Nhấn **Active** trên tab **Workflow Overview**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**
   - Thêm node **Slack/Telegram** sau `Return Generated Content` để **nhận thông báo kết quả** ngay khi workflow hoàn thành.
   - Ví dụ:
     ```json
     {
       "text": "🚀 Đã tạo thành công {{item.json.length}} bài post từ bài blog: {{item.json.blogUrl}}"
     }
     ```

2. **Lưu log vào Google Sheets/Notion**
   - Thêm node **Google Sheets** hoặc **Notion** để **lưu lịch sử các bài post** đã tạo.
   - Cấu hình:
     - **Sheet Name**: `Social Media Posts`
     - **Columns**: `Blog URL, Post Type, Content, Platform, Created At`

3. **Tự động đăng lên các nền tảng**
   - Sử dụng **API của Meta (Facebook/Instagram), Twitter API, LinkedIn API** để **tự động đăng post**.
   - Ví dụ:
     - Node **HTTP Request** để gửi post lên **Meta Business API**.
     - Node **Twitter API** để đăng tweet tự động.

4. **Tối ưu cho SEO**
   - Sử dụng **node `n8n-nodes-base.google-search`** để **kiểm tra từ khóa** trong bài post và **cải thiện nội dung**.
   - Ví dụ:
     ```json
     {
       "query": "{{item.json.content}}",
       "searchType": "web"
     }
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing khỏi việc **viết lại bài blog** cho từng nền tảng. Với **Google Gemini AI**, nội dung được **tối ưu hóa tự động**, **đa dạng và hấp dẫn**, giúp **tăng engagement và SEO**.

**Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Chỉnh sửa API Key Google Gemini**.
3. **Test với một bài blog** và **nhận kết quả ngay!**

👉 **Bắt đầu tự động hóa nội dung mạng xã hội của mình ngay hôm nay!** 🚀

---
**Cần hỗ trợ?** Đăng ký **hỗ trợ kỹ thuật n8n** tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với **TinoHost** để cài đặt VPS n8n ổn định!