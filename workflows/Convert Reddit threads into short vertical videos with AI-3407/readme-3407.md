---
title: "🎥 Chuyển Thread Reddit Thành Video Ngắn AI Tự Động - Tiết Kiệm 100h Thời Gian Cho Marketing"
description: "Workflow tự động hóa chuyển đổi bài viết Reddit thành video vertical ngắn với AI, tự động lấy video từ Pexels, tạo subtitle bằng TTS, và render video hoàn chỉnh - không cần kỹ năng code."
slug: "chuyen-thread-reddit-thanh-video-ai"
tags: [n8n, automation, ai-marketing, video-ai, no-code, reddit-automation]
keywords: [n8n workflow reddit video, tự động hóa video từ reddit, tạo video vertical ai, chatgpt video marketing, tự động hóa content marketing]
---

# 🚀 **Chuyển Thread Reddit Thành Video Ngắn AI - Giải Pháp Tự Động Hóa Content Marketing Mới**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp đang mất **từ 50-100 giờ** mỗi tháng để:
- Tìm kiếm và chọn lọc thread Reddit có giá trị.
- Chuyển nội dung text thành video vertical (thích hợp cho TikTok/Reels).
- Tạo subtitle tự động, thêm âm thanh và hiệu ứng.
- Render và phân phối video trên nhiều nền tảng.

**Workflow này giải quyết tất cả bằng AI + tự động hóa 100% không code!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100h/tháng** cho đội ngũ content.
- **Tạo video vertical** từ thread Reddit chỉ trong vài giây.
- **Tự động lấy video miễn phí** từ Pexels phù hợp với nội dung.
- **Subtitle tự động** bằng TTS (Text-to-Speech) với giọng nói tự nhiên.
- **Render video hoàn chỉnh** và lấy link chia sẻ ngay.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Reddit API**:
   - [Đăng ký OAuth2 Reddit](https://www.reddit.com/prefs/apps) để lấy `client_id` và `client_secret`.
2. **API Key OpenAI (ChatGPT)**:
   - [Mở khóa API Key](https://platform.openai.com/account/api-keys) để sử dụng TTS và AI.
3. **Tài khoản ShotStack** (miễn phí):
   - [Đăng ký ShotStack](https://shotstack.com/) để render video.
4. **Tài khoản Pexels** (tùy chọn):
   - [Tải API Key Pexels](https://www.pexels.com/api/) để lấy video miễn phí.
5. **Webhook URL** (n8n Self-hosted):
   - Cài đặt n8n trên VPS để workflow hoạt động liên tục.
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/3407) hoặc copy JSON từ editor n8n.
- **Bước 2**: Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import Workflow"**.
- **Bước 3**: Chọn **"Active"** để bật workflow.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **40 node** phức tạp, nhưng chỉ cần chú ý đến các node **quan trọng** sau:

##### **A. Cấu Hình API & Credentials**
| Node | Tham Số Cần Điền | Ghi Chú |
|------|------------------|---------|
| **Webhook** | URL Webhook | Sử dụng URL từ n8n Self-hosted (ví dụ: `https://tên-doman.com/webhook/reddit-video`) |
| **get reddit token** | `client_id`, `client_secret`, `refresh_token` | Lấy từ [Reddit OAuth2](https://www.reddit.com/prefs/apps) |
| **OpenAI (ChatGPT)** | `apiKey` | Lấy từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys) |
| **Upload TTS to Shotstack** | `apiKey` | Lấy từ [ShotStack](https://shotstack.com/) |
| **Pexels Query** | `apiKey` | Lấy từ [Pexels API](https://www.pexels.com/api/) |

##### **B. Node Cần Chỉnh Sửa Cụ Thể**
1. **`convert url to reddit api url` (Code Node)**
   - **Mã JavaScript**:
     ```javascript
     const redditUrl = $input.all()[0].json.redditLink;
     const apiUrl = `https://oauth.reddit.com/r/all.json?url=${encodeURIComponent(redditUrl)}`;
     return { json: { redditApiUrl: apiUrl } };
     ```
   - **Lưu ý**: Đảm bảo `$input.all()[0].json.redditLink` trỏ đến URL thread Reddit.

2. **`Limit comments length` (Code Node)**
   - **Mã JavaScript**:
     ```javascript
     const text = $input.all()[0].json.text;
     return { json: { text: text.substring(0, 1000) } }; // Giới hạn 1000 ký tự
     ```
   - **Lý do**: Reddit API có giới hạn độ dài, tránh lỗi.

3. **`Generate TTS` (OpenAI Node)**
   - **Chọn Model**: `tts-1` (giọng nói tự nhiên).
   - **Prompt**: `"Narrate this text in a professional Vietnamese voice: {text}"`.

4. **`Render the video` (ShotStack Node)**
   - **Tham Số**:
     - `projectId`: ID project từ ShotStack.
     - `media`: Danh sách video + âm thanh đã upload trước đó.
     - `settings`: Cấu hình render (kích thước vertical 9:16).

##### **C. Test Run Trước Khi Bật Active**
- Nhấn **"Test Workflow"** với một thread Reddit mẫu.
- Kiểm tra:
  - Video từ Pexels có phù hợp không?
  - Subtitle TTS có rõ ràng không?
  - Video render có hoàn chỉnh không?

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**
   - Thêm node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để thông báo khi video render xong.
   - **Cách làm**:
     ```javascript
     // Trong node "If rendered", thêm step:
     const slackWebhook = "https://hooks.slack.com/services/...";
     await $http.request({
       method: "POST",
       url: slackWebhook,
       body: { text: `🎥 Video ready! Link: ${$input.json().url}` }
     });
     ```

2. **Lưu Log & Báo Cáo Định Kỳ**
   - Sử dụng node **`n8n-nodes-base.googleSheets`** để ghi lịch sử video đã tạo.
   - **Cấu hình**:
     - Sheet Name: `Reddit_Video_Logs`
     - Columns: `Thread_URL, Video_Link, Created_At`

3. **Tự Động Chia Sẻ Trên TikTok/Instagram**
   - Sau khi render, tự động post lên **Meta Business API** hoặc **TikTok API**.
   - **Node cần thêm**: `n8n-nodes-base.meta` hoặc `n8n-nodes-base.tiktok`.

4. **Optimize Video Cho SEO**
   - Thêm **meta description** và **hashtag** tự động bằng OpenAI.
   - **Prompt**:
     ```
     "Generate 5 trending hashtags for a Reddit thread about {topic}. Also, write a 150-word meta description for the video."
     ```

---
### 📌 **Kết Luận**
Workflow này **giải phóng đội ngũ marketing** khỏi công việc thủ công, **tăng hiệu suất content** lên gấp 10 lần, và **tạo video vertical** chỉ trong vài giây. **Đừng để thời gian rơi vào tay Reddit nữa!**

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Cài n8n Self-hosted** trên VPS (🎁 Mã giảm giá **VPSN8N** tại [TinoHost](https://tino.vn/vps-n8n?affid=388)).
2. **Import workflow** và cấu hình API theo hướng dẫn.
3. **Test với 1 thread Reddit** và chia sẻ kết quả với team!
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::