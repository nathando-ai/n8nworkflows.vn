---
title: "🎙️ Chuyển Ghi Chú Obsidian Sang Podcast Tự Động Hóa Với AI - Cung Cấp Dòng Feeds RSS"
description: "Tự động hóa việc đọc ghi chú Obsidian bằng giọng nói AI và xuất ra podcast feed chuẩn RSS, giúp các sếp tiết kiệm thời gian và tối ưu hóa nội dung cho Spotify, Apple Podcasts, Google Podcasts..."
slug: "chuyen-ghi-chu-obsidian-sang-podcast-voi-ai"
tags: [n8n, automation, ai, obsidian, podcast, no-code, google-sheets, openai]
keywords: [n8n workflow podcast, tự động hóa obsidian, đọc ghi chú bằng giọng nói AI, tạo podcast feed RSS, cloudinary obsidian]
---

# 🎙️ **Chuyển Ghi Chú Obsidian Sang Podcast Tự Động Hóa Với AI**

### **Giải pháp hoàn hảo cho các sếp muốn chuyển đổi ghi chú Obsidian thành podcast tự động, không cần code!**
Hãy tưởng tượng: Một ghi chú Obsidian của bạn được đọc bằng giọng nói AI tự nhiên, xuất ra podcast feed chuẩn RSS và được chia sẻ trên Spotify, Apple Podcasts, hoặc Google Podcasts chỉ trong vài giây. **Không cần viết code, không cần kỹ năng kỹ thuật cao!** Workflow này giúp các sếp:
- **Tiết kiệm thời gian** lên đến 80% trong việc tạo nội dung podcast từ ghi chú.
- **Tối ưu hóa SEO** bằng cách xuất podcast feed chuẩn RSS, giúp nội dung được phát hiện và xếp hạng trên các nền tảng.
- **Cá nhân hóa giọng nói** với OpenAI TTS, tạo trải nghiệm nghe chuyên nghiệp.
- **Quản lý nội dung** một cách hệ thống với Google Sheets và Cloudinary.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Podcast tự động hóa 100%**: Chỉ cần gửi ghi chú Obsidian qua webhook, hệ thống sẽ tự động chuyển đổi thành audio và feed RSS.
- **Nội dung đa nền tảng**: Phù hợp với Spotify, Apple Podcasts, Google Podcasts, và các nền tảng khác.
- **Lưu trữ và quản lý**: Audio được lưu trên Cloudinary, metadata được ghi vào Google Sheets.
- **Tối ưu SEO**: Feed RSS chuẩn giúp nội dung được phát hiện và xếp hạng trên các công cụ tìm kiếm.
- **Giọng nói tự nhiên**: Sử dụng OpenAI TTS để tạo giọng đọc chuyên nghiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Obsidian** và cài đặt [Post Webhook Plugin](https://github.com/Masterb1234/obsidian-post-webhook/) để gửi ghi chú qua webhook.
2. **API Key OpenAI** (để sử dụng OpenAI TTS và mô hình AI).
3. **Tài khoản Google Sheets** và OAuth 2.0 API đã kích hoạt.
4. **Tài khoản Cloudinary** (để lưu trữ audio và lấy metadata thời lượng).
5. **n8n Self-hosted** (để workflow chạy 24/7 ổn định).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và tạo một workflow mới.
2. Nhấp vào **Import** và chọn file JSON hoặc dán JSON từ [link gốc](https://n8n.io/workflows/2699).
3. Hoặc copy toàn bộ JSON từ [đây](https://n8n.io/workflows/2699) và nhấp vào **Import from JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Cấu hình Webhook**
- **Webhook GET Note** (để nhận ghi chú từ Obsidian):
  - Đảm bảo **path** là `64fac784-9b98-4bbc-aaf2-dd45763d3362`.
  - Chọn **HTTP Method: POST**.
- **Webhook GET Podcast Feed** (để trả về feed RSS):
  - Đảm bảo **path** là `2f0a6706-54da-4b89-91f4-5e147b393bd8h`.

##### **B. Cấu hình OpenAI**
- Tạo **credentials** mới trong n8n với tên `openAiApi` và điền:
  - **API Key**: API Key của OpenAI (tạo tại [OpenAI Dashboard](https://platform.openai.com/account/api-keys)).
  - **Model**: Chọn `tts-1` (cho OpenAI TTS) và `gpt-3.5-turbo` (cho mô hình tạo mô tả).

##### **C. Cấu hình Cloudinary**
- Tạo **credentials** mới với tên `httpCustomAuth` và điền:
  - **URL**: `https://api.cloudinary.com/v1_1/[your-cloud-name]/image/upload`
  - **Headers**:
    - `Authorization`: `Bearer [your-cloudinary-api-key]`
    - `Content-Type`: `application/json`
  - **Environment**: Đặt biến môi trường `CLOUDINARY_ENV` trong n8n với giá trị là tên môi trường Cloudinary của bạn.

##### **D. Cấu hình Google Sheets**
- Tạo **credentials** mới với tên `googleSheetsOAuth2Api` và kết nối với Google Sheets.
- Đảm bảo **Sheet Name** trong node `Append Item to Google Sheet` và `Get Items from Google Sheets` trùng với tên sheet của bạn.

##### **E. Cấu hình Podcast Feed**
- Trong node **Manually Enter Other Data for Podcast Feed**, điền thông tin podcast như:
  - `title`: Tên podcast (ví dụ: "Podcast của tôi").
  - `description`: Mô tả podcast.
  - `language`: Ngôn ngữ (ví dụ: `vi`).
  - `image`: Link ảnh bìa podcast (nên là URL công khai).

##### **F. Cấu hình RSS Feed (Node Code)**
- Trong node **Write RSS Feed**, các sếp có thể chỉnh sửa mã JavaScript để đảm bảo feed RSS đúng định dạng. Dưới đây là một ví dụ cơ bản:
  ```javascript
  const items = $input.all();
  const feed = {
    rssVersion: "2.0",
    channel: {
      title: $input.current().json.title,
      description: $input.current().json.description,
      language: $input.current().json.language,
      link: $input.current().json.link,
      image: $input.current().json.image,
      items: items.map(item => ({
        title: item.json.title,
        description: item.json.description,
        link: item.json.link,
        enclosure: {
          url: item.json.audioUrl,
          length: item.json.duration,
          type: "audio/mpeg"
        }
      }))
    }
  };
  return { json: feed };
  ```

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một ghi chú mẫu từ Obsidian qua webhook để kiểm tra workflow.
   - Kiểm tra:
     - Audio có được tạo không?
     - Feed RSS có đúng định dạng không?
     - Dữ liệu có được ghi vào Google Sheets không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi có ghi chú mới được chuyển đổi thành podcast.
2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** để ghi lại lịch sử hoạt động của workflow.
3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow phụ để gửi báo cáo số lượng podcast được tạo mỗi tuần qua email.
4. **Tối ưu giọng nói**:
   - Thử nghiệm các mô hình TTS khác của OpenAI (ví dụ: `tts-1-hd`) để giọng nói trở nên chuyên nghiệp hơn.
5. **Tự động chia sẻ trên mạng xã hội**:
   - Sử dụng node **Twitter** hoặc **Facebook** để tự động chia sẻ link podcast mới.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc chuyển đổi ghi chú Obsidian thành podcast, tiết kiệm thời gian và tối ưu hóa nội dung. **Không cần code, không cần kỹ thuật cao!** Hãy **import ngay** và bắt đầu tạo podcast từ ghi chú của mình trong vài phút.

🚀 **Bắt đầu ngay!**
1. Chuẩn bị các tài khoản và API keys.
2. Import workflow và cấu hình theo hướng dẫn.
3. Test và bật workflow.

**Chia sẻ kết quả của bạn với chúng tôi!** 🎤✨