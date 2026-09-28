---
title: "🎙️ Tự Động Chuyển Bài Viết Web Thành Audio Documentary Siêu Chất Với ElevenLabs & AI"
description: "Workflow tự động hóa 100% không code chuyển bài viết từ URL thành audio documentary chuyên nghiệp, với giọng đọc tự nhiên từ ElevenLabs và nội dung được tối ưu hóa bởi AI. Giúp các sếp tiết kiệm thời gian và nâng cao giá trị nội dung cho kênh Telegram, podcast hay video."
slug: "tieu-dong-chuyen-bai-viet-web-thanh-audio-documentary"
tags: [n8n, automation, no-code, ai-content-creation, elevenlabs, browseract, telegram-bot]
keywords: [tự động hóa nội dung, chuyển bài viết thành audio, elevenlabs n8n, ai tạo podcast, browseract scrap text, telegram bot tự động]
---

# 🚀 **Chuyển Bài Viết Web Thành Audio Documentary Siêu Chất Với AI**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 10+ giờ/ngày** viết script và đọc audio cho podcast, video, hoặc nội dung marketing.
- **Nâng cao giá trị nội dung** bằng giọng đọc tự nhiên, chuyên nghiệp từ ElevenLabs.
- **Tự động hóa hoàn toàn** quá trình từ scrap text đến gửi audio cho khách hàng qua Telegram.
- **Cá nhân hóa nội dung** cho từng bài viết, phù hợp với nhiều lĩnh vực: giáo dục, marketing, nghiên cứu, hoặc giải trí.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ cần gửi URL bài viết qua Telegram, workflow sẽ tự động xử lý toàn bộ quá trình.
- **Chất lượng chuyên nghiệp**: Giọng đọc tự nhiên từ ElevenLabs, nội dung được tối ưu hóa bởi AI (Google Gemini + Claude).
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy liên tục trên VPS.
- **Cá nhân hóa nội dung**: AI tự động chuyển bài viết thành script hấp dẫn, phù hợp với từng chủ đề.
- **Tích hợp Telegram**: Gửi audio kết quả cùng caption tự động sinh ra cho khách hàng.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Telegram Bot**: Tạo bot Telegram và lấy `API Token` (dùng để nhận URL từ người dùng).
   - **BrowserAct**: API Key và **Template "AI Summarization & Eleven Labs Podcast Generation"** (cần tải từ [đây](https://docs.browseract.com)).
   - **ElevenLabs**: API Key (đăng ký tại [elevenlabs.io](https://elevenlabs.io/)).
   - **Google Gemini API**: API Key (đăng ký tại [Google Cloud](https://cloud.google.com/)).
   - **OpenRouter (Claude)**: API Key (đăng ký tại [openrouter.ai](https://openrouter.ai/)).

2. **Cài đặt n8n**:
   - Cài n8n trên **VPS** (không dùng phiên bản cloud để đảm bảo hoạt động 24/7).
   - Cài đặt **n8n BrowserAct** và **n8n ElevenLabs** nodes (hướng dẫn tại [n8n.io](https://n8n.io/)).

3. **Hệ thống hỗ trợ**:
   - **Telegram**: Bot cần được kết nối với nhóm hoặc cá nhân để nhận URL.
   - **BrowserAct**: Template đã được tải và cấu hình sẵn trong tài khoản.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12347](https://n8n.io/workflows/12347) (hoặc copy toàn bộ JSON từ link này).
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Lưu ý**: Đảm bảo phiên bản n8n trên VPS **cập nhật mới nhất** để tránh lỗi node.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **15 node** quan trọng, các sếp cần cấu hình như sau:

#### **A. Cấu hình Credentials (Bắt buộc)**
| Node Name               | Loại Node                     | Credentials Cần Thiết               | Hướng Dẫn Cấu Hình                                                                 |
|-------------------------|-------------------------------|-------------------------------------|------------------------------------------------------------------------------------|
| User Sends Message      | `telegramTrigger`             | `telegramApi`                      | Điền `API Token` của bot Telegram (lấy từ [@BotFather](https://t.me/BotFather)).   |
| Notify User / Answer    | `telegram`                    | `telegramApi`                      | Giữ nguyên `API Token` như trên.                                            |
| Get Article Data        | `browserAct`                  | `browserActApi`                    | Điền `API Key` và chọn **Template "AI Summarization & Eleven Labs Podcast Generation"**. |
| OpenRouter               | `lmChatOpenRouter`            | `openRouterApi`                    | Điền `API Key` từ OpenRouter (mô hình `anthropic/claude-haiku-4.5`).          |
| Google Gemini            | `lmChatGoogleGemini`          | `googlePalmApi`                    | Điền `API Key` từ Google Cloud (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)). |
| Convert text to speech  | `elevenLabs`                  | `elevenLabsApi`                   | Điền `API Key` từ ElevenLabs và chọn **Voice Model** (ví dụ: "Eliot" hoặc "Emma"). |

#### **B. Cấu hình Node Quan Trọng**
1. **Node "Check For Input Type" (`switch`)**:
   - **Condition**: Kiểm tra xem message có chứa URL không.
   - **Nếu có URL**: Chuyển sang branch **scraping & scripting**.
   - **Nếu không**: Chuyển sang branch **chatting với user** (hỗ trợ tương tác).

2. **Node "Write Script for ElevenLabs" (`agent`)**:
   - **Prompt**: AI sẽ tự động viết script từ text scraped bằng BrowserAct.
   - **Lưu ý**: Đảm bảo **template BrowserAct** đã được cấu hình đúng (scrap toàn bộ nội dung bài viết).

3. **Node "Convert text to speech" (`elevenLabs`)**:
   - **Parameters**:
     - `voiceSettings.voiceId`: Chọn giọng đọc phù hợp (ví dụ: `Eliot`).
     - `voiceSettings.stability`: 0.5 (giá trị mặc định).
     - `voiceSettings.similarityBoost`: 0.5 (giá trị mặc định).

4. **Node "Send an audio file To User" (`telegram`)**:
   - **Operation**: `sendAudio`.
   - **File**: Chọn output từ node `elevenLabs`.
   - **Caption**: AI tự động sinh caption (có thể chỉnh sửa trong node `structuredOutput`).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một URL bài viết qua Telegram bot.
   - Kiểm tra:
     - AI có scrap text thành công không?
     - Script có logic hấp dẫn không?
     - Audio có tải lên Telegram không?

2. **Bật Active Workflow**:
   - Nhấn **Active** trên tab workflow.
   - **Lưu ý**: Đảm bảo VPS **không ngắt kết nối** (sử dụng VPS 24/7 như TinoHost hoặc Xeon).

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp với Slack/Email**:
   - Thay vì chỉ Telegram, có thể gửi audio kết quả qua **Slack** hoặc **Email** bằng node `n8n-nodes-base.email`.
   - **Cách làm**: Thêm node `email` sau node `sendAudio` và cấu hình SMTP.

2. **Lưu log hoạt động**:
   - Sử dụng node `n8n-nodes-base.stickyNote` để ghi lại lịch sử scrap và sinh audio.
   - **Lợi ích**: Theo dõi hiệu suất và debug lỗi dễ dàng.

3. **Tối ưu hóa script AI**:
   - Chỉnh sửa **prompt** trong node `Write Script for ElevenLabs` để phù hợp với lĩnh vực cụ thể (ví dụ: giáo dục, marketing).
   - **Ví dụ**:
     ```json
     "prompt": "Tôi là một nhà sản xuất podcast chuyên nghiệp. Viết một script audio documentary từ bài viết sau về [chủ đề], với giọng điệu hấp dẫn, câu chuyện logic và kết thúc mạnh mẽ. Đảm bảo nội dung phù hợp với khán giả [đối tượng mục tiêu]."
     ```

4. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng node `n8n-nodes-base.cron` để gửi báo cáo thống kê (số lượng bài viết xử lý, thời gian trung bình) qua Email hoặc Telegram.
   - **Cách làm**:
     - Thêm node `cron` với lịch chạy hàng ngày (ví dụ: `0 0 * * *`).
     - Kết nối với node `email` hoặc `telegram` để gửi báo cáo.

5. **Chọn giọng đọc phù hợp**:
   - ElevenLabs cung cấp nhiều voice model. Các sếp có thể thử nghiệm và chọn giọng phù hợp với nội dung:
     - **Eliot**: Giọng nam trung tính, phù hợp cho podcast.
     - **Emma**: Giọng nữ tự nhiên, phù hợp cho nội dung giáo dục.
     - **Matthew**: Giọng nam ấm áp, phù hợp cho marketing.

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình chuyển bài viết thành audio documentary **không cần viết code**. Với sự hỗ trợ của **AI (Google Gemini + Claude)**, **ElevenLabs** và **BrowserAct**, nội dung của các sếp sẽ được chuyển đổi thành sản phẩm âm thanh chuyên nghiệp, tiết kiệm thời gian và nâng cao giá trị.

### **Hành động ngay hôm nay:**
1. **Đăng ký VPS** để self-host n8n (không dùng phiên bản cloud):
   👉 [TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
   👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)

2. **Cài đặt và cấu hình** workflow theo hướng dẫn trên.
3. **Test với 1-2 bài viết** và tối ưu hóa prompt AI nếu cần.

**🚀 Chúc các sếp thành công!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với **Madame AI Team** qua Telegram.