---
title: "🌟 **Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày Từ RSS & YouTube Sang Telegram Với AI (Không Cần Code)**"
description: "Workflow này tự động thu thập tin tức từ TechCrunch, The Verge, BBC World và YouTube, xử lý bằng AI (Google Gemini), sau đó gửi tóm tắt văn bản + file âm thanh podcast sang Telegram hàng ngày. Giúp các sếp tiết kiệm 2+ giờ mỗi ngày theo dõi tin tức, đồng thời nhận được bản tóm tắt cá nhân hóa và dễ nghe qua âm thanh."
slug: "tieu-dong-hoa-tom-tat-tin-tuc-rss-you-tube-sang-telegram-voi-ai"
tags: [n8n, automation, content-creation, multimodal-ai, telegram-bot, google-gemini, openai-tts]
keywords: [n8n workflow tin tức, tự động hóa tin tức hàng ngày, AI tổng hợp tin tức, Telegram bot tin tức, RSS YouTube tự động, Google Gemini n8n, OpenAI TTS tự động]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin Tức Hàng Ngày Từ RSS & YouTube Sang Telegram Với AI**

## **🔥 Bạn đang mất quá nhiều thời gian mỗi ngày để:**
- **Lọc tin tức** từ hàng chục nguồn khác nhau (TechCrunch, The Verge, BBC, YouTube...)?
- **Đọc và ghi chú** những tin quan trọng trong khi làm việc?
- **Tìm kiếm video YouTube** liên quan đến lĩnh vực của bạn?
- **Chưa có thời gian** để nghe tin tức qua âm thanh trong khi đi lại hoặc làm việc?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** tin tức từ RSS và YouTube trong 24h.
✅ **Xử lý bằng AI** (Google Gemini) để lọc, tổng hợp và viết tóm tắt chuyên nghiệp.
✅ **Chuyển văn bản thành âm thanh** (OpenAI TTS) để bạn có thể **nghe tin tức như podcast**.
✅ **Gửi kết quả** sang Telegram hàng ngày (7h sáng) với **văn bản + file âm thanh**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và không bị giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2+ giờ mỗi ngày** (không cần theo dõi tin tức thủ công).
- **Nhận tin tức được lọc và tổng hợp** bởi AI (Google Gemini) với logic cá nhân hóa.
- **Nghe tin tức như podcast** trong khi làm việc, đi lại (OpenAI TTS).
- **Tin tức được gửi tự động** vào Telegram hàng ngày (không quên).
- **Cập nhật liên tục** từ nhiều nguồn (RSS + YouTube) mà không cần can thiệp.
- **Dễ dàng tùy chỉnh** để phù hợp với sở thích cá nhân (thay đổi nguồn tin, AI prompt, thời gian gửi...).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản & API Keys:**
- **Google Cloud API** (Google Gemini) → [Cài đặt API](https://aistudio.google.com/app/apikey)
- **OpenAI API** (TTS) → [Cài đặt API](https://platform.openai.com/account/api-keys)
- **Telegram Bot Token** → [Tạo Bot Telegram](https://core.telegram.org/bots#botfather)
- **YouTube Data API** → [Cài đặt API](https://developers.google.com/youtube/v3/getting-started)

✔ **Tham số Telegram:**
- **`TELEGRAM_CHAT_ID`** (ID của chat cá nhân hoặc nhóm Telegram để nhận tin tức).

✔ **Nguồn tin tức (RSS & YouTube):**
- Các sếp có thể **thay đổi URL RSS** (TechCrunch, The Verge, BBC) và **từ khóa YouTube** để phù hợp với sở thích.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/12141](https://n8n.io/workflows/12141).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn "Import Workflow".

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/12141](https://n8n.io/workflows/12141).
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 1. Cấu hình Credentials (API Keys)**
Các node **quan trọng** cần cấu hình:
| **Node** | **Yêu cầu** | **Hướng dẫn** |
|----------|------------|----------------|
| **Google Gemini** | API Key Google Cloud | Đăng ký tại [Google Cloud Console](https://console.cloud.google.com/apis/credentials) → Thêm API Key vào n8n dưới tên `googlePalmApi`. |
| **OpenAI TTS** | API Key OpenAI | Đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys) → Thêm vào n8n dưới tên `openAiApi`. |
| **YouTube Search** | OAuth 2.0 API | Tạo OAuth 2.0 Client ID tại [Google Cloud Console](https://console.cloud.google.com/apis/credentials) → Thêm vào n8n dưới tên `youTubeOAuth2Api`. |
| **Telegram Bot** | Bot Token + Chat ID | Tạo Bot tại [@BotFather](https://t.me/BotFather) → Thêm `telegramApi` vào n8n. **Chat ID** có thể lấy từ [@userinfobot](https://t.me/userinfobot). |

#### **🔹 2. Cấu hình RSS & YouTube**
- **RSS Feed Read (TechCrunch, The Verge, BBC):** Thay đổi URL trong node `rssFeedRead` nếu muốn theo dõi nguồn khác.
  *Ví dụ:*
  ```json
  "url": "https://feeds.techcrunch.com/techcrunch"
  ```
- **YouTube Search:** Thay đổi `keywords` trong node `YouTube - Search (Latest 24h)` để lọc video theo chủ đề.
  *Ví dụ:*
  ```json
  "keywords": "AI, blockchain, startup"
  ```

#### **🔹 3. Cấu hình AI (Google Gemini)**
- Mở node **`Google Gemini Chat (AI Analysis)`** và chỉnh sửa **prompt** để điều chỉnh:
  - Số lượng tin tức được lọc (`top 10 stories`).
  - Độ dài tóm tắt (`keep it concise`).
  - Tính cách của văn bản (`professional tone`).
  *Gợi ý prompt:*
  ```json
  "prompt": "Analyze the following news articles and create a concise daily briefing (max 500 words). Highlight key points, trends, and actionable insights. Use a professional yet engaging tone."
  ```

#### **🔹 4. Cấu hình Telegram**
- Đảm bảo **`TELEGRAM_CHAT_ID`** được đặt trong **Global Variables** của n8n.
- Kiểm tra node **`Telegram - Send Briefing Text`** và **`Telegram - Send Briefing Audio`** để xác nhận **Bot Token** và **Chat ID** đúng.

#### **🔹 5. Schedule Trigger**
- Mặc định, workflow chạy **lúc 7h sáng hàng ngày**.
- Nếu muốn thay đổi thời gian, mở node **`Schedule Trigger`** và chỉnh `cron` expression:
  *Ví dụ:*
  ```json
  "cron": "0 7 * * *"  // 7h sáng hàng ngày
  ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Test workflow):**
   - Nhấn **"Test"** để chạy workflow với dữ liệu mẫu.
   - Kiểm tra **Telegram** để xem kết quả.

2. **Bật Active:**
   - Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tùy chỉnh nguồn tin tức**
- **Thêm/loại bỏ RSS:** Mở node `RSS Feed Read` và thay đổi URL.
- **Tăng giảm số lượng YouTube:** Chỉnh `maxResults` trong node `YouTube - Search`.

### **2. Cải thiện AI Prompt**
- **Điều chỉnh logic AI** trong node `Google Gemini` để:
  - Lọc tin tức theo **chủ đề cụ thể** (ví dụ: "chỉ tin tức về AI").
  - Thêm **các yêu cầu đặc biệt** (ví dụ: "bỏ qua tin tức tài chính").

### **3. Gửi tin tức qua Slack/Email**
- Thay thế node **Telegram** bằng:
  - **Slack Webhook** (n8n-nodes-base.slack).
  - **Email (SMTP)** (n8n-nodes-base.email).

### **4. Lưu log & báo cáo**
- Thêm node **`StickyNote`** để lưu lịch sử tin tức.
- Sử dụng **`Code` node** để ghi log vào file CSV/Google Sheets.

### **5. Chuyển đổi âm thanh thành file MP3**
- Nếu OpenAI TTS không hoạt động, thay thế bằng **ElevenLabs API** hoặc **Microsoft Azure TTS**.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp, nhà quản lý hoặc người làm việc cần **tin tức được tổng hợp, cá nhân hóa và dễ tiếp cận** mà không tốn thời gian thủ công.

👉 **Bắt đầu ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình API Keys** và **Telegram Chat ID**.
3. **Chạy test** và **bật Active** để nhận tin tức hàng ngày!

**💡 Mẹo cuối:** Nếu muốn **tăng cường tính cá nhân hóa**, hãy chỉnh sửa **prompt AI** để phù hợp với ngành nghề của bạn (tech, finance, startup...).

---
**🚀 Hãy tự động hóa tin tức của mình ngay hôm nay!** 🚀