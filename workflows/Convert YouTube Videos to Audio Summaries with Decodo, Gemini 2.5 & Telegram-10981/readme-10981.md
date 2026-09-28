---
title: "🎙️ Tự Động Chuyển Video YouTube Sang Tóm Tắt Âm Thanh (MP3) Với Decodo, Gemini 2.5 & Telegram – Cách Làm Chi Tiết"
description: "Workflow tự động hóa hoàn toàn không cần code chuyển bất kỳ video YouTube nào thành tóm tắt âm thanh MP3 chất lượng cao, với transcript từ Decodo, tóm tắt thông minh bằng Gemini 2.5, và phát âm bằng OpenAI – tất cả được gửi trực tiếp qua Telegram. Tiết kiệm thời gian lên đến 80% cho công việc nghiên cứu nội dung."
slug: "tuy-dong-hoa-chuyen-video-youtube-sang-tom-tat-am-than"
tags: [n8n, automation, content-creation, ai-multimodal, youtube-automation, telegram-bot]
keywords: [tự động hóa YouTube sang âm thanh, Decodo API, Gemini 2.5 tóm tắt video, OpenAI TTS, Telegram bot tự động, workflow n8n không code]
---

# 🚀 **Chuyển Video YouTube Sang Tóm Tắt Âm Thanh (MP3) – Cách Tự Động Hóa 100% Không Code**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tìm kiếm** video YouTube liên quan đến chủ đề nghiên cứu.
- **Chuyển đổi** video thành văn bản (transcript) bằng cách tải xuống hoặc sử dụng công cụ như 4K Video Downloader.
- **Tóm tắt** nội dung dài hàng giờ thành những điểm chính bằng tay (hay bằng ChatGPT – nhưng vẫn tốn thời gian).
- **Phát âm** tóm tắt bằng giọng nhân tạo (hay thu âm bằng giọng của mình – mất thời gian và không chuyên nghiệp).
- **Gửi kết quả** cho đồng nghiệp qua email hoặc Telegram – dễ bị mất hoặc không được theo dõi.

**Kết quả?** Thời gian nghiên cứu tăng gấp 3-5 lần so với thời gian thực sự cần thiết.

---
### **🎯 Kết Quả Các Sếp Nhận Được Với Workflow Này**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công (không cần tải video, tóm tắt bằng tay, hoặc thu âm).
- **Chất lượng chuyên nghiệp**: Tóm tắt được tạo bởi **Gemini 2.5** (AI mạnh nhất hiện nay), phát âm bằng **OpenAI TTS** (giọng nhân tạo tự nhiên).
- **Tự động hóa hoàn toàn**: Chỉ cần gửi URL YouTube qua Telegram, workflow sẽ tự động:
  - Lấy transcript từ video.
  - Tóm tắt nội dung thành JSON có cấu trúc (Tiêu đề, Thể loại, Tóm tắt, Script phát âm).
  - Chuyển script thành âm thanh MP3.
  - Gửi kết quả (âm thanh + tóm tắt văn bản) về Telegram.
- **Hoạt động 24/7**: Không cần can thiệp của con người, workflow chạy liên tục trên VPS.
- **Cá nhân hóa**: Chỉ cần thay đổi `output_language` trong Config node, workflow sẽ tự động chuyển đổi ngôn ngữ cho transcript và tóm tắt.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Telegram**:
   - Một bot Telegram (cần tạo và thêm vào nhóm/đối thoại cá nhân).
   - **API Key Telegram**: Mở [@BotFather](https://t.me/BotFather) để tạo bot và lấy `API Token`.
2. **API Keys**:
   - **Decodo API Key**: Để lấy transcript từ YouTube.
     - **Ưu đãi đặc biệt**: 80% OFF cho plan **23k Advanced Scraping** với mã `ATTAN8N`.
     - [Đăng ký ngay](https://visit.decodo.com/c/6679292/3071239/17480).
   - **Google Palm API Key**: Để sử dụng **Gemini 2.5 Flash** (miễn phí trong giới hạn).
     - [Cách lấy API Key](https://ai.google.dev/tutorials/quickstart).
   - **OpenAI API Key**: Để chuyển văn bản thành âm thanh (MP3).
     - [Cách lấy API Key](https://platform.openai.com/account/api-keys).
3. **VPS Self-hosted** (khuyến nghị):
   - Để workflow chạy 24/7 mà không bị giới hạn thời gian chạy (n8n Cloud có giới hạn).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
4. **N8n Workflow Editor**:
   - Cài đặt [n8n](https://n8n.io/) trên VPS hoặc sử dụng [n8n Cloud](https://n8n.io/cloud) (miễn phí cho dự án cá nhân).
---

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/10981) hoặc copy toàn bộ JSON từ trang này.
- **Cách import**:
  - Mở **n8n Editor** → Nhấn `Import` → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
  - Hoặc sử dụng **n8n CLI**:
    ```bash
    n8n import workflow.json
    ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **15 node**, nhưng chỉ có **5 node quan trọng** cần cấu hình kỹ lưỡng:

##### **A. Config Node (Thiết Lập Ngôn Ngữ & Cấu Hình AI)**
- **Double-click** vào node `Config` (node thứ 15 trong danh sách).
- Cập nhật tham số:
  ```json
  {
    "output_language": "English",  // Thay đổi thành tiếng Việt, Tiếng Nhật, Tiếng Đức, v.v.
    "gemini_system_prompt": "You are an Audio Summarizer. Extract key points from the transcript and create a concise script for TTS."
  }
  ```
  - **Lưu ý**: `output_language` quyết định ngôn ngữ của transcript và tóm tắt. Ví dụ:
    - `"output_language": "Vietnamese"` → Workflow sẽ tự động chuyển đổi transcript và tóm tắt sang tiếng Việt.

##### **B. Telegram Trigger (Cấu Hình Bot Telegram)**
- **Double-click** vào node `Telegram Trigger` (node thứ 9).
- Chọn:
  - **Credentials**: `telegramApi` (đã tạo trước đó).
  - **Command**: `/youtube` (lệnh để người dùng gửi URL YouTube).
  - **Chat ID**: Chọn `All Chats` để workflow hoạt động với tất cả đối thoại hoặc nhập `Chat ID` cụ thể.

##### **C. Decodo Node (Lấy Transcript từ YouTube)**
- **Double-click** vào node `Decodo (Fetch Transcript)` (node thứ 11).
- Thêm **API Key** vào `decodoApi` (credentials đã tạo trước đó).
- **Lưu ý**:
  - Nếu video không có transcript (ví dụ: video âm nhạc), workflow sẽ tự động gửi thông báo lỗi qua Telegram.
  - **Ưu đãi Decodo**: Sử dụng mã `ATTAN8N` để giảm 80% chi phí API.

##### **D. Google Gemini Chat Model (Tóm Tắt Bằng AI)**
- **Double-click** vào node `Google Gemini Chat Model` (node thứ 2).
- Chọn:
  - **Credentials**: `googlePalmApi`.
  - **Model**: `gemini-1.5-flash` (mô hình mới nhất của Google).
  - **System Prompt**: Đã được cấu hình sẵn trong workflow (tóm tắt thành JSON có cấu trúc).

##### **E. OpenAI TTS (Chuyển Văn Bản Sang Âm Thanh)**
- **Double-click** vào node `OpenAI TTS (Create Audio)` (node thứ 14).
- Chọn:
  - **Credentials**: `openAiApi`.
  - **Model**: `tts-1` (giọng nhân tạo tự nhiên).
  - **Voice**: `alloy` (giọng nam) hoặc `echo` (giọng nữ).
  - **Response Format**: `mp3` (định dạng âm thanh).

##### **F. Telegram Delivery (Gửi Kết Quả Về Telegram)**
- **Double-click** vào node `Send Audio Summary` (node thứ 15).
- Chọn:
  - **Credentials**: `telegramApi`.
  - **Operation**: `sendAudio` (gửi file âm thanh).
  - **Caption**: Thay đổi nội dung caption để hiển thị thông tin video (ví dụ: `Tóm tắt video: [Tiêu đề]`).

---
#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run**:
  - Gửi URL YouTube qua Telegram với lệnh `/youtube <URL>` (ví dụ: `/youtube https://youtu.be/dQw4w9WgXcQ`).
  - Workflow sẽ tự động:
    1. Gửi tin nhắn `"Working on it..."` để thông báo đang xử lý.
    2. Lấy transcript từ Decodo.
    3. Tóm tắt bằng Gemini 2.5.
    4. Chuyển văn bản thành âm thanh MP3.
    5. Gửi kết quả (âm thanh + tóm tắt văn bản) về Telegram.
- **Bật Active**:
  - Nhấn `Active` trên tab `Workflow` để workflow chạy tự động khi nhận lệnh.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM THÊM]
1. **Lưu Log & Theo Dõi Lỗi**:
   - Thêm node `Set` sau `Check for Transcript Error` để lưu lỗi vào Google Sheets hoặc Notion.
   - Cách làm:
     ```json
     {
       "jsonPath": "$",
       "operation": "set",
       "property": "error_log",
       "value": "{{$json.error}}"
     }
     ```
   - Kết nối với node `googleSheets` để lưu dữ liệu.

2. **Kết Nối Với Slack**:
   - Thay thế node `Telegram` bằng `Slack` để gửi kết quả vào kênh Slack.
   - Cách làm:
     - Tạo bot Slack và lấy `API Token`.
     - Thêm node `n8n-nodes-base.slack` và cấu hình tương tự như Telegram.

3. **Tự Động Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node `Set` + `Schedule` để gửi tóm tắt của các video mới nhất hàng tuần.
   - Ví dụ: Gửi báo cáo vào thứ 7 hàng tuần với danh sách video mới nhất.

4. **Cải Thiện Tóm Tắt Bằng Prompt Tùy Chỉnh**:
   - Thay đổi `gemini_system_prompt` trong node `Google Gemini Chat Model` để:
     - Tóm tắt theo phong cách cụ thể (ví dụ: "Tóm tắt như một bài giảng đại học").
     - Bỏ qua các phần không quan trọng (ví dụ: "Không bao gồm phần giới thiệu").
   - Ví dụ:
     ```json
     "gemini_system_prompt": "You are a concise business summarizer. Extract only key takeaways and actionable insights from the transcript."
     ```

5. **Chuyển Đổi Ngôn Ngữ Tự Động**:
   - Sử dụng node `n8n-nodes-base.translate` (nếu cần) để tự động dịch transcript từ tiếng Anh sang tiếng Việt trước khi tóm tắt.
---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào việc phân tích và ứng dụng kiến thức thay vì làm thủ công. Với **Decodo, Gemini 2.5, và OpenAI**, bạn có thể:
✅ **Tóm tắt video dài thành âm thanh MP3 chỉ trong vài giây**.
✅ **Tự động hóa hoàn toàn** quá trình nghiên cứu nội dung.
✅ **Cá nhân hóa** kết quả bằng cách thay đổi ngôn ngữ hoặc prompt AI.

**Hành động ngay**:
1. **Cài đặt VPS** và cài n8n (để workflow chạy 24/7).
2. **Tạo bot Telegram** và lấy API Keys (Decodo, Google, OpenAI).
3. **Import workflow** và cấu hình theo hướng dẫn.
4. **Gửi URL YouTube** qua Telegram và xem kết quả!

**🎁 Bonus**: Sử dụng mã `ATTAN8N` để giảm 80% chi phí API Decodo và tiết kiệm thêm tiền cho dự án của mình.

---
**💬 Câu hỏi?** Các sếp có thể comment bên dưới hoặc liên hệ với tác giả [Atta](https://n8n.io/workflows/10981) để được hỗ trợ chi tiết!