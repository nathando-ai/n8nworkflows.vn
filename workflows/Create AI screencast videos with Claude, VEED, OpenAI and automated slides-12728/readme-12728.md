---
title: "🎬 Tự Động Hoà Video AI Chuyên Nghiệp Với Claude, VEED, OpenAI & Slides Tự Động - Không Cần Code!"
description: "Workflow này tự động tạo video screencast chuyên nghiệp với avatar AI lip-sync, giọng nói tự nhiên và slides trình bày AI, tiết kiệm thời gian lên đến 90% so với thủ công. Đơn giản chỉ cần nhập chủ đề và cấu hình, hệ thống sẽ tự hoàn thành toàn bộ quá trình từ viết kịch bản đến xuất video sẵn sàng chia sẻ."
slug: "tay-dong-hoa-video-ai-claude-veed-openai"
tags: [n8n, automation, content-creation, ai-video, multimodal-ai, veed, openai, claudie, elevenlabs, google-drive, google-sheets]
keywords: [tự động hóa video AI, workflow n8n video, tạo video screencast tự động, avatar AI lip-sync, slides trình bày AI, claudie, veed, openai, elevenlabs]
---

# 🚀 **Tự Động Hoà Video AI Chuyên Nghiệp Với Claude, VEED, OpenAI & Slides Tự Động**

## **💡 Giải Pháp Cho Người Sáng Tạo & Marketing**
Bạn đã bao giờ phải mất **giờ đồng hồ** để viết kịch bản, thiết kế slides, thu âm giọng nói và chèn avatar vào video trình bày? Hay phải **đầu tư hàng triệu đồng** để thuê người làm video chuyên nghiệp? **Workflow này sẽ giải quyết tất cả!**

Với **AI + Tự Động Hoà**, bạn chỉ cần **nhập chủ đề và cấu hình**, hệ thống sẽ tự động:
✅ **Viết kịch bản** với Claude AI (Anthropic)
✅ **Tạo avatar AI lip-sync** với OpenAI + VEED
✅ **Sinh giọng nói tự nhiên** với ElevenLabs
✅ **Thiết kế slides trình bày** với FAL Flux Pro
✅ **Gộp video chuyên nghiệp** với Creatomate (PIP overlay)
✅ **Tải lên Google Drive** và **ghi log vào Google Sheets**

**Kết quả?** Một **video screencast chuyên nghiệp** sẵn sàng chia sẻ trong **vài phút**, với chất lượng cao như video của Fortune 500!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian lên đến 90%** so với làm thủ công.
- **Chất lượng video chuyên nghiệp** (lip-sync chính xác, slides đẹp mắt).
- **Cá nhân hóa hoàn toàn** (chỉ cần thay đổi chủ đề và cấu hình).
- **Hoạt động 24/7** (không cần can thiệp người dùng).
- **Dữ liệu theo dõi** (tất cả video và log được lưu trên Google Drive & Sheets).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản API** (cần đăng ký và lấy API Key):
   - **Anthropic (Claude)** – Để viết kịch bản.
   - **OpenAI (DALL·E 3)** – Tạo avatar AI.
   - **ElevenLabs** – Sinh giọng nói tự nhiên.
   - **FAL.ai (FAL Flux Pro)** – Tạo slides trình bày.
   - **Creatomate** – Ghép video (PIP overlay).
   - **VEED** – Tạo video lip-sync.

✔ **Tài khoản Google** (để lưu video và log):
   - **Google Drive (OAuth2)** – Lưu video cuối cùng.
   - **Google Sheets (OAuth2)** – Ghi log kết quả.

✔ **Mã giảm giá VPS** (để chạy workflow 24/7):
   👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12728](https://n8n.io/workflows/12728) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **37 node**, nhưng các bước **quan trọng nhất** cần cấu hình là:

#### **🔹 Node 1: "⚙️ Workflow Configuration" (Code)**
- **Cấu hình chủ đề, brand name, target audience và slide style**.
- **Ví dụ:**
  ```json
  {
    "topic": "Cách tự động hóa marketing với n8n",
    "brandName": "TechMarketing",
    "targetAudience": "Marketer mới bắt đầu",
    "slideStyle": "Modern",
    "useCustomAvatar": false,
    "customAvatarUrl": ""
  }
  ```

#### **🔹 Node 2: "🤖 Claude: Generate Content" (HTTP Request)**
- **Điền API Key Claude** vào `Authorization` header.
- **URL:** `https://api.anthropic.com/v1/messages`
- **Headers:**
  ```json
  {
    "Content-Type": "application/json",
    "x-api-key": "SK-YOUR_CLAUDE_API_KEY"
  }
  ```
- **Body (Prompt):**
  ```json
  {
    "model": "claude-2",
    "max_tokens_to_sample": 300,
    "messages": [
      {
        "role": "user",
        "content": "Tạo một kịch bản video trình bày về chủ đề: {{topic}}. Brand name: {{brandName}}. Target audience: {{targetAudience}}. Cấu trúc bao gồm: giới thiệu, 3 điểm chính, kết luận và call-to-action."
      }
    ]
  }
  ```

#### **🔹 Node 3: "🎨 Generate Avatar (OpenAI)" (HTTP Request)**
- **Điền API Key OpenAI** vào `Authorization` header.
- **URL:** `https://api.openai.com/v1/images/generations`
- **Headers:**
  ```json
  {
    "Authorization": "Bearer SK-YOUR_OPENAI_API_KEY"
  }
  ```
- **Body (Prompt):**
  ```json
  {
    "prompt": "A professional {{brandName}} presenter avatar, realistic, 4K, neutral expression, business attire, looking at camera",
    "n": 1,
    "size": "1024x1024"
  }
  ```

#### **🔹 Node 4: "🎵 Generate Audio (ElevenLabs)" (HTTP Request)**
- **Điền API Key ElevenLabs** vào `Authorization` header.
- **URL:** `https://api.elevenlabs.io/v1/text-to-speech/{{voiceId}}`
- **Headers:**
  ```json
  {
    "xi-api-key": "YOUR_ELEVENLABS_API_KEY"
  }
  ```
- **Body (Prompt):**
  ```json
  {
    "text": "{{script}}",
    "voice_settings": {
      "stability": 0.5,
      "similarity_boost": 0.5
    }
  }
  ```

#### **🔹 Node 5: "🎬 Generate Talking Head (VEED)" (VEED Node)**
- **Đăng ký tài khoản VEED** và lấy **API Key**.
- **Cấu hình:**
  - **Input:** Avatar URL + Audio URL.
  - **Output:** Video lip-sync từ VEED.

#### **🔹 Node 6: "📊 Format Slides" (Code)**
- **Đảm bảo Google Sheets URL** được điền chính xác vào `Google Sheets` node cuối cùng.
- **Ví dụ:**
  ```json
  {
    "sheetUrl": "https://docs.google.com/spreadsheets/d/{{SHEET_ID}}"
  }
  ```

#### **🔹 Node 7: "📤 Upload to Drive" (Google Drive)**
- **Chọn folder** muốn lưu video cuối cùng.
- **Cấu hình:**
  - **File Name:** `{{topic}}_video.mp4`
  - **Folder ID:** `{{DRIVE_FOLDER_ID}}`

#### **🔹 Node 8: "📝 Log to Sheets" (Google Sheets)**
- **Chọn sheet** muốn ghi log.
- **Cấu hình:**
  - **Operation:** `append`
  - **Columns:** `Topic, Video URL, Status, Timestamp`

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu (ví dụ: chủ đề "Cách tự động hóa marketing").
2. **Bật Active** workflow.
3. **Chờ kết quả** (thời gian render ~5-15 phút tùy vào chất lượng).

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM HƠN HIỆU QUẢ**]
- **Thêm Slack/Telegram Notification** để được thông báo khi video hoàn thành.
- **Lưu log vào Notion** thay vì Google Sheets.
- **Tự động chia sẻ video** trên LinkedIn/Facebook khi hoàn thành.
- **Cấu hình voice khác nhau** cho từng brand (ví dụ: giọng nam/nữ).
- **Sử dụng custom avatar** thay vì tạo mới (nếu đã có avatar chuyên nghiệp).
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì làm thủ công. **Không cần code**, chỉ cần **cấu hình API và nhập chủ đề**, hệ thống sẽ tự động tạo video **chuyên nghiệp, lip-sync chính xác và slides đẹp mắt**.

**🚀 Hãy thử ngay!**
1. **Import workflow** từ [n8n.io/workflows/12728](https://n8n.io/workflows/12728).
2. **Cấu hình API keys** và Google Drive/Sheets.
3. **Nhấn Execute** và **chờ kết quả!**

**💬 Cần hỗ trợ?** Đăng ký **VPS n8n** để chạy 24/7 và liên hệ với chúng tôi qua [VEED Support](https://www.veed.io/support)!

---
**#TựĐộngHoà #VideoAI #n8n #MarketingAutomation #ContentCreation**