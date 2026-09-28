---
title: "🚀 Tự Động Hóa Chia Sẻ Video YouTube Trên Tất Cả Mạng Xã Hội Với Gemini AI & ContentDrips - Khai Phóng 100% Không Code"
description: "Workflow này tự động lấy video mới từ YouTube, tạo nội dung miêu tả bằng Gemini AI, thiết kế hình ảnh chuyên nghiệp với ContentDrips, và chia sẻ trên Facebook, Instagram, TikTok, LinkedIn... chỉ trong vài giây. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng tầm tiếp cận 300% cho nội dung."
slug: "tu-dong-hoa-chia-se-youtube-voi-gemini-ai"
tags: [n8n, automation, no-code, ai-gemini, content-marketing, social-media, youtube-automation]
keywords: [tự động hóa youtube, chia sẻ video trên mạng xã hội, gemini ai n8n, contentdrips automation, tự động hóa marketing, chia sẻ video tự động]
---

# 🚀 **Tự Động Hóa Chia Sẻ Video YouTube Trên Tất Cả Mạng Xã Hội Với Gemini AI & ContentDrips**

## **🔥 Giải Pháp Cho Các Sếp Bận Rộn**
Bạn đã bao giờ phải **quét qua hàng chục video mới trên YouTube**, sau đó **tự tay viết mô tả**, **tạo hình ảnh thú vị**, rồi **chia sẻ trên Facebook, Instagram, TikTok, LinkedIn...** một cách thủ công? Thời gian và công sức bạn bỏ ra có thể **tăng gấp 10 lần** nếu nội dung đó được chia sẻ trên **5+ nền tảng** cùng một lúc!

**Workflow này sẽ:**
✅ **Tự động lấy video mới** từ YouTube (thông qua RSS hoặc webhook)
✅ **Tạo mô tả chuyên nghiệp** bằng **Gemini AI** (không cần viết tay)
✅ **Thiết kế hình ảnh hấp dẫn** với **ContentDrips** (trong 10 giây)
✅ **Chia sẻ trên tất cả mạng xã hội** (Facebook, Instagram, TikTok, LinkedIn, Twitter, Pinterest...)
✅ **Gửi báo cáo thành công/lỗi** qua **Discord** (để theo dõi 24/7)

**Kết quả?** **Tiết kiệm 10+ giờ/ngày**, **tăng tầm tiếp cận 300%**, và **tự động hóa toàn bộ quy trình** mà **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** (không cần viết mô tả, thiết kế hình ảnh thủ công)
- **Tăng tầm tiếp cận 300%** (chia sẻ trên **Facebook, Instagram, TikTok, LinkedIn, Twitter, Pinterest...**)
- **Nội dung cá nhân hóa** (mô tả và hình ảnh được tạo tự động từ video)
- **Hoạt động liên tục 24/7** (không phụ thuộc vào thời gian làm việc)
- **Báo cáo lỗi tự động** (qua Discord, giúp phát hiện vấn đề ngay lập tức)
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản YouTube** (để lấy video mới)
✔ **Tài khoản Google** (để sử dụng **Gemini AI**)
✔ **Tài khoản ContentDrips** ([Đăng ký miễn phí](https://contentdrips.com/)) (để tạo hình ảnh)
✔ **Tài khoản SocialBu** ([Đăng ký](https://socialbu.com/)) (để chia sẻ trên mạng xã hội)
✔ **Tài khoản Discord** (để nhận báo cáo thành công/lỗi)
✔ **API Keys & Credentials** (xem chi tiết dưới đây)

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8338](https://n8n.io/workflows/8338) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **30 node**, nhưng các sếp chỉ cần chú ý đến **các phần quan trọng sau**:

##### **🔹 Node 1: "📡 Subscribe to YouTube Notifications" (httpRequest)**
- **Chức năng:** Đăng ký nhận thông báo video mới từ YouTube (sử dụng **PubSubHubbub**).
- **Cách cấu hình:**
  - Thay đổi **channel_id** trong URL thành **ID kênh YouTube** của bạn (ví dụ: `UC6ZligwnOYKDjgKFHEPTXzg`).
  - **hub.verify_token** = `lakshit` (có thể thay đổi nếu cần).
  - **hub.lease_seconds** = `86400` (1 ngày, thay vì 10 ngày để tránh lỗi).

##### **🔹 Node 2: "🎣 YouTube Webhook Listener" (webhook)**
- **Chức năng:** Nhận thông báo từ YouTube khi có video mới.
- **Cách cấu hình:**
  - Đảm bảo **webhook URL** (`https://tên-domain-n8n.com/youtube-trigger`) **không bị chặn** (n8n phải chạy 24/7).
  - **Test webhook** bằng cách gửi một yêu cầu POST từ Postman với payload:
    ```json
    {
      "hub.mode": "subscribe",
      "hub.topic": "https://www.youtube.com/feeds/videos.xml?channel_id=UC6ZligwnOYKDjgKFHEPTXzg",
      "hub.callback": "https://tên-domain-n8n.com/youtube-trigger",
      "hub.verify_token": "lakshit"
    }
    ```

##### **🔹 Node 3: "Generate Description" (googleGemini)**
- **Chức năng:** Tạo mô tả video bằng **Gemini AI**.
- **Cách cấu hình:**
  - Đăng ký **Google AI Studio** ([Đăng ký miễn phí](https://makersuite.google.com/)) và lấy **API Key**.
  - Thêm **credentials** trong n8n:
    - **Name:** `googlePalmApi`
    - **API Key:** (Copy từ Google AI Studio)
  - **Prompt mẫu:**
    ```
    Tạo một mô tả video YouTube chuyên nghiệp, hấp dẫn và SEO-friendly cho video có tiêu đề "[TITLE]". Mô tả phải:
    1. Giới thiệu ngắn gọn về nội dung (1-2 câu).
    2. Danh sách các chủ đề chính trong video (dùng dấu *).
    3. Kêu gọi hành động (CTA) như "Like, Share, Subscribe".
    4. Thêm từ khóa liên quan (ví dụ: "tự động hóa", "n8n", "AI").
    ```

##### **🔹 Node 4: "Content drips Create Image" (contentdrips)**
- **Chức năng:** Tạo hình ảnh thú vị từ mô tả và thumbnail.
- **Cách cấu hình:**
  - Cài đặt **n8n-nodes-contentdrips** bằng lệnh:
    ```bash
    npm install n8n-nodes-contentdrips
    ```
  - Thêm **credentials** trong n8n:
    - **Name:** `contentdripsApi`
    - **API Key:** (Lấy từ [ContentDrips Dashboard](https://contentdrips.com/dashboard))
    - **Template ID:** (Chọn một template từ [ContentDrips Templates](https://contentdrips.com/templates))
    - **Branding:** (Tùy chọn, có thể bỏ trống)

##### **🔹 Node 5: "Post to SocialBu Connected Accounts" (httpRequest)**
- **Chức năng:** Chia sẻ video trên **Facebook, Instagram, TikTok, LinkedIn...**
- **Cách cấu hình:**
  - Đăng ký **SocialBu** và kết nối tất cả tài khoản mạng xã hội.
  - Thêm **credentials** trong n8n:
    - **Name:** `socialbuApi`
    - **API Key:** (Lấy từ SocialBu)
  - **Payload mẫu:**
    ```json
    {
      "text": "{{ $node["Generate Description"].json.output.description }}",
      "image_url": "{{ $node["Content drips Create Image"].json.output.image_url }}",
      "video_url": "{{ $node["Fetch Youtube Channel Videos"].json.output.video_url }}",
      "platforms": ["facebook", "instagram", "tiktok", "linkedin"]
    }
    ```

##### **🔹 Node 6: "Error Message" & "Success Message" (discord)**
- **Chức năng:** Gửi báo cáo lỗi/thành công qua Discord.
- **Cách cấu hình:**
  - Thêm **credentials Discord OAuth2** trong n8n:
    - **Name:** `discordOAuth2Api`
    - **Token:** (Lấy từ [Discord Developer Portal](https://discord.com/developers/applications))
  - **Message mẫu:**
    - **Thành công:**
      ```
      ✅ Video "{{ $node["Fetch Youtube Channel Videos"].json.output.title }}" đã chia sẻ thành công trên tất cả mạng xã hội!
      ```
    - **Lỗi:**
      ```
      ❌ Lỗi khi chia sẻ video "{{ $node["Fetch Youtube Channel Videos"].json.output.title }}": {{ $node["Error Trigger"].json.output.error }}
      ```

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với một video mẫu:
   - Chọn **Manual Trigger** và nhấn **Execute**.
   - Kiểm tra **Discord** để xem workflow có hoạt động không.
2. **Bật Active workflow**:
   - Đảm bảo **webhook** và **schedule trigger** (10 phút/lần) được kích hoạt.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa theo lịch:**
   - Thay vì chỉ chạy sau 10 phút, các sếp có thể **chỉ chạy vào giờ làm việc** (ví dụ: 8h-18h) bằng cách cấu hình **schedule trigger** phức tạp hơn.
2. **Lưu log vào Google Sheets:**
   - Thêm một node **Google Sheets** để **ghi lại tất cả hoạt động** (video nào đã chia sẻ, thời gian, trạng thái).
3. **Gửi báo cáo email hàng tuần:**
   - Sử dụng **node Email** (ví dụ: Gmail) để **gửi tổng kết hoạt động** cho team.
4. **Tối ưu mô tả bằng AI:**
   - Thay vì dùng **Gemini AI**, các sếp có thể thử **Bard AI** hoặc **Perplexity AI** để mô tả **hơn nữa**.
5. **Chia sẻ trên Pinterest & Reddit:**
   - Mở rộng **SocialBu** để chia sẻ trên **Pinterest** và **Reddit** (nếu nội dung phù hợp).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì **quét video thủ công**. Với **Gemini AI** và **ContentDrips**, nội dung của bạn sẽ **hấp dẫn hơn 100%**, và **chia sẻ tự động** trên **tất cả mạng xã hội** giúp **tăng tầm tiếp cận gấp bội**.

**🚀 Hãy áp dụng ngay và tự động hóa marketing của mình!**
Nếu có vấn đề, các sếp có thể liên hệ với **tác giả Shayan Ali Bakhsh** qua [LinkedIn](https://www.linkedin.com/in/shayan-khan20/) để hỗ trợ.

---
**Happy Automating!** 🤖✨