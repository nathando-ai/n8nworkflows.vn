---
title: "🚀 Tự Động Hóa Sáng Tạo & Phát Hành Video Tin Tức AI Trên Mạng Xã Hội Với GPT-4o & HeyGen"
description: "Workflow này tự động chuyển đổi tin tức từ RSS thành video AI với avatar, tự động chỉnh sửa caption cho từng nền tảng (Instagram, Facebook, YouTube) và phát hành 24/7. Giúp doanh nghiệp tiết kiệm 40-60% thời gian sản xuất nội dung, đồng thời duy trì tính nhất quán và chuyên nghiệp trên tất cả kênh xã hội."
slug: "tieu-dong-hoa-video-tin-tuc-ai-HeyGen"
tags: [n8n, automation, content-creation, multimodal-ai, social-media, gpt-4o, HeyGen, google-sheets, postiz]
keywords: [tự động hóa video tin tức AI, workflow n8n GPT-4o, tự động hóa mạng xã hội, tự động hóa nội dung AI, HeyGen API, Postiz API, RSS feed automation]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video Tin Tức AI & Phát Hành Trên Instagram, Facebook & YouTube**

## **Giải Phóng Tay Các Sếp Từ Công Việc Sáng Tạo Nội Dung Tin Tức**
Hãy tưởng tượng một ngày không cần phải:
- **Lựa chọn** tin tức phù hợp từ hàng trăm bài viết trên CNN, BBC hay Reuters.
- **Viết** caption dài dòng, phải tuân thủ quy định của từng nền tảng (Instagram 2200 ký tự, YouTube mô tả chi tiết).
- **Chỉnh sửa** video để phù hợp với định dạng của mỗi nền tảng.
- **Phát hành** đồng thời trên Instagram, Facebook và YouTube mà không lo lặp lại nội dung.

Workflow này **tự động hóa toàn bộ quy trình** từ **tin tức → video AI → caption thông minh → phát hành đa nền tảng** chỉ trong **vài phút**, giúp các sếp:
✅ **Tiết kiệm 40-60% thời gian** so với cách làm thủ công.
✅ **Duy trì tính nhất quán** trên tất cả kênh xã hội.
✅ **Tăng cường engagement** với video AI hấp dẫn hơn so với hình ảnh static.
✅ **Theo dõi toàn bộ quá trình** trên Google Sheets (tin tức, video, metadata).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn API và đảm bảo tính ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình** từ tin tức đến video phát hành (không cần code).
- **Caption thông minh** được AI tối ưu cho từng nền tảng (Instagram, Facebook, YouTube).
- **Video AI hấp dẫn** với avatar và giọng nói tự động từ HeyGen.
- **Phát hành đồng thời** trên 3 nền tảng lớn (Instagram, Facebook, YouTube).
- **Theo dõi toàn bộ quá trình** trên Google Sheets (tin tức, video, metadata).
- **Tiết kiệm chi phí** so với việc thuê nhân viên sáng tạo nội dung.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản & API Keys:**
- **OpenAI API Key** (để sử dụng GPT-4o-mini trong LangChain).
- **HeyGen API Key** (để tạo video AI).
- **Google Sheets** (để lưu log tin tức và video).
- **Google Drive** (để lưu trữ video).
- **Postiz API Key** (để phát hành video trên Instagram, Facebook, YouTube).

✔ **Thông tin cấu hình:**
- **HeyGen Avatar ID** và **Voice ID** (để chọn avatar và giọng nói cho video).
- **Postiz Domain** (ví dụ: `https://postiz.yourdomain.com`).
- **Google Sheets Credentials** (để ghi log tin tức và video).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/6524](https://n8n.io/workflows/6524) và import vào n8n Editor.
- **Copy & Paste** JSON từ file vào n8n Editor (đảm bảo không có lỗi syntax).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **22 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **📰 RSS Feed Read (Lấy Tin Tức)**
- **URL RSS:** `http://rss.cnn.com/rss/edition.rss` (có thể thay đổi thành RSS feed khác).
- **Limiter (Limit1):** Đặt `executeOnce: true` để chỉ lấy **1 tin tức** trong lần test (tránh tiêu tốn API quá nhiều).

##### **🤖 AI Agent & Caption Generation (Sáng Tạo Caption)**
- **Node "AI Agent"** sử dụng LangChain + GPT-4o-mini để tạo caption từ tin tức.
- **Node "write script"** (lmChatOpenAi) cần cấu hình:
  - **Model:** `gpt-4o-mini` (hoặc `gpt-4-turbo` nếu có budget).
  - **Prompt:** Đảm bảo sử dụng template đã định sẵn trong workflow (không cần chỉnh sửa nếu không biết code).

##### **🎬 HeyGen Video Creation (Tạo Video AI)**
- **Node "Setup Heygen Parameters"** cần điền:
  - `avatar_id`: ID avatar của bạn trên HeyGen.
  - `voice_id`: ID giọng nói của bạn trên HeyGen.
  - `api_key`: API Key của HeyGen.
- **Node "Create Avatar Video (HeyGen)"** gọi API HeyGen để tạo video. Đảm bảo:
  - Tham số `caption` (từ AI Agent) và `news_title` được truyền đúng.
  - Thời gian chờ (`Wait for Video`) là **2 phút** (có thể điều chỉnh tùy video dài ngắn).

##### **📤 Upload & Publish to Social Media (Phát Hành)**
- **Node "Upload Video to Postiz"** cần:
  - Địa chỉ Postiz của bạn (ví dụ: `https://postiz.yourdomain.com`).
  - API Key Postiz đã cấu hình trong credentials.
- **Node "Video Platform Router"** tự động phân loại video cho Instagram, Facebook, YouTube.
- **Caption Cleaner** (các node `Clean Instagram Caption`, `Clean Facebook Video Caption`):
  - **Không cần chỉnh sửa** nếu đã cấu hình đúng (chỉ xử lý ký tự đặc biệt và giới hạn ký tự).

##### **📊 Google Sheets Logging (Theo Dõi Tin Tức & Video)**
- **Node "Log news to sheets"** ghi log tin tức vào Sheet `RSS FEEDS`.
- **Node "Log Video Details to Sheets"** ghi log video vào Sheet `Avatar video`.
- **Đảm bảo credentials Google Sheets** đã được cấu hình trong n8n.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 tin tức mẫu** (đảm bảo tất cả node chạy thành công).
2. **Bật Active** workflow sau khi kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH TIẾP CẬN THÊM]
- **Thêm RSS Feed khác:** Thay đổi URL trong node `RSS Read` để lấy tin tức từ BBC, Reuters, hoặc nguồn tin tức chuyên ngành.
- **Tùy chỉnh avatar & giọng nói:** Thử nghiệm với các avatar và giọng nói khác trên HeyGen để phù hợp với brand.
- **Phát hành định kỳ:** Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày (ví dụ: 8h sáng).
- **Lưu log chi tiết:** Thêm node `Set` để ghi thêm metadata như `engagement_rate` (nếu có API của Postiz hỗ trợ).
- **Tích hợp Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` để thông báo khi video được tạo thành công.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc mòn mỏi sáng tạo nội dung tin tức**, đồng thời **tăng cường hiệu quả phát hành trên mạng xã hội** với video AI chuyên nghiệp. **Chỉ cần 1 lần setup**, workflow sẽ tự động chạy 24/7, giúp tiết kiệm **40-60% thời gian** so với cách làm thủ công.

**Hãy áp dụng ngay và bắt đầu tự động hóa nội dung của mình!** 🚀

---
**🔗 [Tải workflow gốc](https://n8n.io/workflows/6524) | 📧 [Liên hệ David Olusola](david@daexai.com) để hỗ trợ tùy chỉnh**