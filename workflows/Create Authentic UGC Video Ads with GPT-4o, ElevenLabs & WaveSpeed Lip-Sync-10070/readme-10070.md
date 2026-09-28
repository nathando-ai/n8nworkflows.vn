---
title: "🎬 Tự Động Hoà Chất Video Quảng Cáo UGC (User-Generated Content) Siêu Chất Với GPT-4o, ElevenLabs & WaveSpeed – Không Cần Code!"
description: "Workflow tự động hóa 100% AI tạo video testimonial chân thực, lip-sync tự nhiên, giọng nói nhân tạo với chất lượng 480p – hoàn hảo cho TikTok/Instagram. Giúp các sếp tiết kiệm 10+ giờ/lần so với cách làm thủ công."
slug: "tieu-dong-hoa-video-ugc-ai-gpt-4o-elevenlabs"
tags: [n8n, automation, content-creation, ai-multimodal, video-advertising]
keywords: [tự động hóa video quảng cáo, n8n workflow ai, tạo video testimonial tự động, ElevenLabs n8n, WaveSpeed lip-sync, GPT-4o tự động hóa]
---

# 🚀 **Tự Động Hoà Video Quảng Cáo UGC Chân Thật – Từ Ảnh Sản Phẩm Đến Video Testimonial Chất 480p**

## **💥 Nỗi Đau Của Các Sếp Khi Tạo Video Testimonial Thủ Công**
Hiện nay, video quảng cáo **User-Generated Content (UGC)** là một trong những hình thức marketing hiệu quả nhất, giúp tăng độ tin cậy và engagement cho sản phẩm. Tuy nhiên, việc tạo video testimonial thủ công gặp nhiều khó khăn:
- **Tốn thời gian**: Từ viết script, lồng giọng, lip-sync đến chỉnh sửa video mất **5-10 giờ/lần**.
- **Chất lượng không đồng nhất**: Giọng nói nhân tạo thường nghe giả, lip-sync không tự nhiên.
- **Khó cá nhân hóa**: Khó tạo ra video phù hợp với từng sản phẩm hoặc đối tượng khách hàng.
- **Không hoạt động 24/7**: Phải làm thủ công, không thể tự động hóa cho nhiều sản phẩm.

**Workflow này giải quyết tất cả!** Dùng **AI Multimodal** (GPT-4o, ElevenLabs, WaveSpeed) để tự động tạo video testimonial **chân thực, lip-sync tự nhiên** chỉ trong **3-5 phút**, với chất lượng 480p phù hợp cho TikTok/Instagram.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/lần** so với cách làm thủ công.
✅ **Video testimonial chân thực** với giọng nói và lip-sync tự nhiên.
✅ **Cá nhân hóa hoàn toàn** theo sản phẩm, màu sắc, và đối tượng khách hàng.
✅ **Hoạt động 24/7** – không cần can thiệp thủ công.
✅ **Chất lượng 480p** phù hợp cho TikTok, Instagram Reels, và Facebook Ads.
✅ **Gửi tự động qua Telegram** – không cần quản lý thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **API Keys & Credentials**:
   - **OpenAI API Key** (để sử dụng GPT-4o Vision và Chat Model).
   - **ElevenLabs API Key** (để voice cloning và text-to-speech).
     - **Voice IDs**:
       - Nam: `UcqZLa941Kkt8ZhEEybf`
       - Nữ: `lMSqoJeA0cBBNA9FeHAs`
   - **WaveSpeed API Key** (để tạo video lip-sync).
   - **Cloudinary API Key** (để upload file tạm).
   - **Telegram Bot Token** (để nhận ảnh sản phẩm và gửi video kết quả).
     - **Chat ID** của bot (để gửi video cuối cùng).

2. **Dịch vụ cần thiết**:
   - **n8n Self-hosted** (để workflow hoạt động 24/7).
   - **Telegram Bot** (để trigger và nhận kết quả).

:::note[💡 Mẹo]
👉 **Đăng ký VPS TinoHost** (Self-hosted n8n) với mã giảm giá **VPSN8N** (giảm tới 39%):
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
👉 **VPS Xeon 4GB chỉ 50k/tháng** (đủ cho workflow này):
🔗 [https://my.bnix.one/aff.php?aff=172](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10070](https://n8n.io/workflows/10070) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON.
  3. Chọn **Create Workflow**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **34 nodes**, nhưng các sếp chỉ cần chú ý đến các node **quan trọng** sau:

#### **🔹 Node Cấu Hình API (BẮT BUỘC)**
| **Node**               | **Tham Số Cần Điền**                          | **Lưu Ý**                                                                 |
|------------------------|-----------------------------------------------|---------------------------------------------------------------------------|
| **OpenAI Chat Model4** | `openAiApi` (API Key)                         | Điền API Key từ [OpenAI](https://platform.openai.com/api-keys).           |
| **Analyze YAML**       | `openAiApi` (API Key)                         | Cùng API Key với node trên.                                               |
| **CLONING AUDIO CE/CO**| `YOUR_ELEVENLABS_API_KEY`                     | Điền API Key từ [ElevenLabs](https://elevenlabs.io/app/settings/api-keys). |
| **UPLOAD AUDIO LIPSYNC**| `httpBasicAuth` (Cloudinary Credentials)      | Điền `cloud_name` và `api_key` từ [Cloudinary](https://cloudinary.com/). |
| **CREATE LIPSYNC V1**  | `YOUR_WAVESPEED_API_KEY`                      | Điền API Key từ [WaveSpeed](https://wavespeed.ai/).                      |
| **Telegram Trigger**   | `telegramApi` (Bot Token)                     | Điền Token từ `@BotFather` trên Telegram.                                |
| **Send a video/photo** | `telegramApi` (Bot Token) + `chat_id`         | Điền `chat_id` của bot (để gửi video kết quả).                          |

#### **🔹 Node Cấu Hình Voice (ElevenLabs)**
- Trong node **`CLONING AUDIO CE`** và **`CLONING AUDIO CO`**, các sếp **không cần thay đổi gì** (sẵn sàng với Voice ID đã chỉ định).
- Nếu muốn thay đổi giọng nói, chỉnh sửa trong **`keyParameters`** của node `httpRequest`:
  ```json
  "voiceSettings": {
    "stability": 0.5,
    "similarity_boost": 0.5,
    "voice_id": "lMSqoJeA0cBBNA9FeHAs" // Nữ
  }
  ```

#### **🔹 Node Cấu Hình WaveSpeed (Lip-Sync)**
- Trong node **`CREATE LIPSYNC V1`**, đảm bảo:
  - `YOUR_WAVESPEED_API_KEY` được điền chính xác.
  - Tham số `model` là `"wavespeed/v1"` (không cần thay đổi).

#### **🔹 Node Telegram (Trigger & Gửi Kết Quả)**
- **Telegram Trigger**: Đảm bảo bot đã được tạo và `chat_id` đúng.
- **Send a video/photo**: Điền `chat_id` của bot (để nhận video kết quả).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một ảnh sản phẩm mẫu:
   - Gửi ảnh qua Telegram bot (đã cấu hình trong `Telegram Trigger`).
   - Kiểm tra workflow có chạy không lỗi hay không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - Đảm bảo **n8n Self-hosted** đang chạy 24/7.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tối Ưu Hóa Cho Nhiều Sản Phẩm**
- **Sử dụng StickyNote** để lưu các **template script** cho từng sản phẩm (ví dụ: script cho sản phẩm A khác với sản phẩm B).
- **Tạo nhiều Telegram bot** cho từng nhóm sản phẩm (ví dụ: `bot_testimonial_food`, `bot_testimonial_electronics`).

### **🔹 Lưu Log & Theo Dõi**
- **Thêm node `Set`** sau `CREATE LIPSYNC V1` để lưu **status** của video (thành công/thất bại) vào **Google Sheets** hoặc **Database**.
- **Gửi báo cáo định kỳ** qua Telegram/Email khi workflow hoàn thành.

### **🔹 Kết Hợp Với Slack/Email**
- Thay vì chỉ gửi qua Telegram, **cấu hình node `telegram`** để gửi kết quả qua **Slack** hoặc **Email** (sử dụng node `n8n-nodes-base.email`).
- **Ví dụ**:
  ```json
  "keyParameters": {
    "to": "marketing@example.com",
    "subject": "Video Testimonial Đã Hoàn Thành",
    "html": "<p>Xin chào! Video testimonial đã được tạo thành công.</p>"
  }
  ```

### **🔹 Tăng Tốc Độ Xử Lý**
- **WaveSpeed** có thời gian chờ **140s** cho video lip-sync. Nếu cần nhanh hơn, thử **WaveSpeed Pro** (nếu có API Key).
- **Optimize OpenAI Prompt**: Nếu video không chất lượng, chỉnh sửa **`PROMPT PRODUK REVIEW`** để AI sinh script **phù hợp hơn**.

---

## 📌 **Kết Luận & Kêu Gọi Áp Dụng Ngay**

Workflow này **giải phóng thời gian** cho các sếp khỏi việc tạo video testimonial thủ công, đồng thời **tăng chất lượng** với **giọng nói tự nhiên, lip-sync chân thực**. Dùng cho:
✔ **E-commerce** (Amazon, Shopee, Lazada).
✔ **Marketing Digital** (TikTok, Instagram, Facebook Ads).
✔ **Branding** (tạo video UGC cho chiến dịch quảng cáo).

**🚀 Hành động ngay!**
1. **Chuẩn bị API Keys** (OpenAI, ElevenLabs, WaveSpeed, Cloudinary).
2. **Import workflow** và cấu hình như hướng dẫn.
3. **Test với 1 ảnh sản phẩm** và xem kết quả!
4. **Bật Active** và để workflow chạy tự động 24/7.

**💬 Cần hỗ trợ?**
- **Email**: mfarooqiqbal143@gmail.com
- **LinkedIn**: [Muhammad Farooq Iqbal](https://linkedin.com/in/muhammadfarooqiqbal)
- **Portfolio**: [n8n Workflows của anh](https://mfarooqone.github.io/n8n/)

**🎁 Bonus**: Các sếp có thể **tùy chỉnh workflow** để tạo **video review cho nhiều ngôn ngữ** (Việt, Anh, Trung...) bằng cách thay đổi **prompt** trong node `PROMPT PRODUK REVIEW`.

---
**🔥 Chúc các sếp thành công với video testimonial AI siêu chất!** 🚀