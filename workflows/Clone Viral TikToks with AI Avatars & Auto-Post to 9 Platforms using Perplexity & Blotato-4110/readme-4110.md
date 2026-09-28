---
title: "🚀 Tự Động Hóa Clone Video TikTok Viral → AI Avatar + Đăng Trên 9 Mạng Xã Hội (Perplexity + Blotato)"
description: "Workflow n8n tự động hóa việc clone video TikTok viral thành video mới với avatar AI, tối ưu nội dung bằng Perplexity, và đăng tự động lên 9 nền tảng xã hội (Instagram, YouTube, TikTok, Facebook, Threads, Twitter, LinkedIn, Bluesky, Pinterest). Giúp các sếp tiết kiệm 100+ giờ công/tháng và tăng engagement 3x."
slug: "tieu-dong-hoa-clone-tiktok-ai-avatar-9-platform"
tags: [n8n, automation, ai, marketing, social-media, no-code, tiktok, openai, perplexity]
keywords: [tự động hóa tiktok, clone video tiktok, ai avatar, đăng video tự động, n8n workflow, marketing tự động, content automation, viral content]
---

# 🚀 **Tự Động Hóa Clone Video TikTok Viral → AI Avatar + Đăng Trên 9 Mạng Xã Hội (Perplexity + Blotato)**

## **💥 Nỗi Đau Của Các Sếp Trong Marketing TikTok**
Các sếp đang phải:
- **Tìm kiếm và clone** video TikTok viral thủ công → tốn thời gian và không đảm bảo chất lượng.
- **Tạo nội dung mới** từ video cũ bằng trí tuệ nhân tạo → khó tối ưu hóa nội dung cho từng nền tảng.
- **Đăng video lên 9+ nền tảng** (Instagram, YouTube, TikTok, Facebook, Threads, Twitter, LinkedIn, Bluesky, Pinterest) → phải làm thủ công, dễ sai sót.
- **Không có avatar AI** để cá nhân hóa video → nội dung trông chung chung, không thu hút.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Clone video TikTok viral** → **tạo video mới với avatar AI cá nhân hóa**.
✅ **Tối ưu nội dung** bằng Perplexity (AI tìm kiếm thông minh) và GPT-4o (OpenAI).
✅ **Đăng tự động lên 9 nền tảng** trong 1 lần setup.
✅ **Gửi preview qua Telegram** để review trước khi đăng.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 100+ giờ/tháng** so với làm thủ công.
- **Tăng engagement 3x** với video cá nhân hóa bằng avatar AI.
- **Tối ưu nội dung** cho từng nền tảng (caption, script, overlay text).
- **Hoạt động 24/7** mà không cần can thiệp.
- **Dữ liệu theo dõi** trên Google Sheets (video gốc, video mới, URL đăng).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản & API Keys**:
   - **Telegram Bot** (để nhận URL TikTok từ người dùng).
   - **OpenAI API Key** (để sử dụng GPT-4o, GPT-4 Vision, và transcribe audio).
   - **Google Sheets OAuth 2.0** (để lưu trữ dữ liệu video).
   - **Cloudinary API** (để upload thumbnail).
   - **Blotato API Key** (để tạo video từ avatar).
   - **JSON2Video API Key** (để thêm overlay text).
   - **Tài khoản API RapidAPI** (để download TikTok video & audio).
   - **Tài khoản API của 9 nền tảng xã hội** (Instagram, YouTube, TikTok, Facebook, Threads, Twitter, LinkedIn, Bluesky, Pinterest).

2. **Dữ liệu ban đầu**:
   - **URL TikTok viral** (gửi qua Telegram).
   - **Avatar AI** (cung cấp từ Blotato).
   - **Google Sheet** để lưu trữ lịch sử video (cấu trúc mẫu sẽ được hướng dẫn).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4110](https://n8n.io/workflows/4110) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/4110) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **4 bước chính** (được đánh dấu trên canvas). Dưới đây là hướng dẫn chi tiết cho từng phần quan trọng:

##### **🟫 STEP 1 — Clone a Viral TikTok Video**
- **Trigger: Get TikTok URL via Telegram**
  - **Cấu hình**:
    - Chọn **credentials**: `telegramApi`.
    - **Webhook URL**: Cung cấp từ n8n (để Telegram gửi URL TikTok).
    - **Chat ID**: ID chat của Telegram Bot (lấy từ `@BotFather`).
  - **Lưu ý**: Đảm bảo **Telegram Bot** được kích hoạt và có quyền gửi tin nhắn.

- **Download TikTok Video (RapidAPI)**
  - **Cấu hình**:
    - **URL**: `https://tiktok-download.p.rapidapi.com/download/`
    - **Headers**:
      - `X-RapidAPI-Key`: API Key từ RapidAPI.
      - `X-RapidAPI-Host`: `tiktok-download.p.rapidapi.com`.
    - **Query Parameters**:
      - `url`: `$json["url"]` (URL TikTok từ Telegram).

- **Extract Video Thumbnail**
  - **Cấu hình**:
    - Sử dụng **FFmpeg** (n8n có sẵn node `n8n-nodes-base.code` để extract thumbnail).
    - **Mã JavaScript**:
      ```javascript
      const { execSync } = require('child_process');
      const fs = require('fs');
      const path = require('path');

      const videoPath = $input.all()[0].json.thumbnailUrl;
      const outputPath = path.join(__dirname, 'thumbnail.jpg');

      execSync(`ffmpeg -i ${videoPath} -ss 00:00:01 -vframes 1 -q:v 2 ${outputPath}`);
      return { thumbnailUrl: outputPath };
      ```

- **Upload Thumbnail to Cloudinary**
  - **Cấu hình**:
    - **Credentials**: `httpBasicAuth` (API Key & Secret từ Cloudinary).
    - **URL**: `https://api.cloudinary.com/v1_1/{account}/image/upload`
    - **Body**:
      ```json
      {
        "file": $input.all()[0].json.thumbnailUrl,
        "upload_preset": "your_preset_name"
      }
      ```

##### **🟦 STEP 2 — Suggest New Content Idea**
- **Suggest Similar Idea (Perplexity)**
  - **Cấu hình**:
    - **URL**: `https://api.perplexity.ai/chat/completions`
    - **Headers**:
      - `Authorization`: `Bearer YOUR_PERPLEXITY_API_KEY`.
    - **Body**:
      ```json
      {
        "model": "llama-3.1-sonar-large-128k-online",
        "messages": [
          {"role": "system", "content": "You are a TikTok content strategist."},
          {"role": "user", "content": "Suggest 3 new angles for this viral TikTok: $json["video_url"]"}
        ]
      }
      ```

- **Clean Perplexity Response**
  - **Cấu hình**:
    - Sử dụng **node `n8n-nodes-base.code`** để loại bỏ ký tự đặc biệt:
      ```javascript
      return $input.all()[0].json.choices[0].message.content.replace(/[^\w\s]/g, '');
      ```

- **Rewrite Script, Caption, Overlay (GPT-4o)**
  - **Cấu hình**:
    - **Model**: `gpt-4o`.
    - **Prompt**:
      ```
      Rewrite this TikTok script for [PLATFORM] in a more engaging way:
      Original: $json["original_script"]
      Target: Make it shorter, add humor, and include trending sounds.
      ```

##### **🟪 STEP 3 — Create the New Video with Your Avatar**
- **Fetch Available Avatars (Blotato)**
  - **Cấu hình**:
    - **URL**: `https://api.blotato.com/v1/avatars`
    - **Headers**:
      - `Authorization`: `Bearer YOUR_BLOTATO_API_KEY`.

- **Generate Video with Avatar**
  - **Cấu hình**:
    - **URL**: `https://api.blotato.com/v1/videos`
    - **Body**:
      ```json
      {
        "avatar_id": $json["avatar_id"],
        "video_url": $json["video_url"],
        "script": $json["rewritten_script"]
      }
      ```

- **Wait for Avatar Rendering (3 min)**
  - **Cấu hình**:
    - Thời gian chờ: **180 giây** (3 phút).

- **Add Overlay Text with JSON2Video**
  - **Cấu hình**:
    - **Credentials**: `httpCustomAuth` (API Key từ JSON2Video).
    - **URL**: `https://api.json2video.com/v1/add-text`
    - **Body**:
      ```json
      {
        "video_url": $json["video_url"],
        "text": $json["overlay_text"],
        "position": "center",
        "font_size": 48
      }
      ```

##### **🟥 STEP 4 — Publish to 9 Platforms**
- **Upload Video to Blotato** (đã xử lý ở Step 3).
- **Đăng lên từng nền tảng** (ví dụ: Instagram, YouTube, TikTok...):
  - **Cấu hình chung**:
    - **URL API**: Mỗi nền tảng có URL riêng (ví dụ:
      - **Instagram**: `https://graph.facebook.com/v18.0/{user-id}/media`
      - **YouTube**: `https://www.googleapis.com/youtube/v3/videos`
      - **TikTok**: `https://open-api.tiktokv.com/v2/video/upload/`
    - **Headers**:
      - **Access Token** (OAuth 2.0) từ mỗi nền tảng.
    - **Body**:
      ```json
      {
        "video_url": $json["final_video_url"],
        "caption": $json["caption"],
        "thumbnail_url": $json["thumbnail_url"]
      }
      ```

- **Send Video URL via Telegram**
  - **Cấu hình**:
    - **Credentials**: `telegramApi`.
    - **Message**: `Video đã được đăng lên tất cả nền tảng. Link: $json["video_url"]`.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa avatar**:
   - Chọn avatar phù hợp với brand của doanh nghiệp (ví dụ: avatar CEO cho video marketing).
   - Sử dụng **Blotato Studio** để tạo avatar cá nhân hóa trước.

2. **Lưu log hoạt động**:
   - Thêm **node `n8n-nodes-base.googleSheets`** để ghi lại:
     - Thời gian clone.
     - URL video gốc & video mới.
     - Nền tảng đã đăng.
     - Trạng thái (success/fail).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.email`** để gửi báo cáo tuần/month về:
     - Số video đã clone.
     - Engagement trung bình.
     - Nền tảng có traffic cao nhất.

4. **Kết hợp với Slack/Telegram**:
   - Thêm **node `n8n-nodes-base.slack`** để thông báo khi video được đăng thành công.

---
### 📌 **Kết Luận**
Workflow này là **công cụ hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa toàn bộ quy trình** từ clone TikTok đến đăng video.
✔ **Tăng hiệu suất marketing** với nội dung cá nhân hóa.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược lớn hơn.

**Hành động ngay!**
1. **Setup n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và cấu hình API keys.
3. **Gửi URL TikTok đầu tiên** qua Telegram và xem kết quả!

**Chia sẻ kết quả của bạn với #n8nAutomation trên Twitter/X để hỗ trợ cộng đồng!** 🚀