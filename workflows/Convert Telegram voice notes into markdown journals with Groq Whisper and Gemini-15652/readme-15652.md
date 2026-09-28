---
title: "🎙️ Chuyển Ghi Âm Telegram Sang Bài Nhật Ký Markdown Tự Động Với Groq Whisper & Gemini AI"
description: "Workflow tự động hóa hoàn toàn không cần code chuyển đổi ghi âm Telegram (voice notes, audio files) thành bài nhật ký Markdown sạch sẽ, được cải tiến bởi AI Groq Whisper và Gemini. Lưu trữ tự động lên Telegram + Google Drive (tùy chọn)."
slug: "chuyen-gi-am-telegram-sang-markdown-voi-groq-gemini"
tags: [n8n, automation, no-code, ai, telegram, google-drive, groq, gemini, markdown, voice-to-text]
keywords: [n8n workflow telegram voice note, tự động hóa ghi âm sang nhật ký, groq whisper gemini markdown, lưu trữ nhật ký google drive, convert audio to markdown]
---

# 🚀 **Chuyển Ghi Âm Telegram Sang Bài Nhật Ký Markdown Tự Động Với AI**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 100% thời gian ghi chép** bằng cách chuyển đổi ghi âm Telegram thành bài nhật ký sạch sẽ chỉ trong vài giây.
- **Tự động hóa nhật ký cá nhân** với chất lượng cao như viết tay, nhưng không cần gõ chữ.
- **Lưu trữ an toàn** bài nhật ký lên Google Drive (tùy chọn) để truy cập mọi lúc.
- **Hỗ trợ nhiều định dạng âm thanh** (MP3, M4A, OGG, OPUS...) với hệ thống fallback tự động.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho Groq/Gemini)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Chuyển đổi ghi âm thành bài nhật ký chỉ trong **5-10 giây** thay vì mất giờ viết tay.
✅ **Chất lượng cao**: AI **Gemini** tự động **sửa lỗi, cải thiện ngữ pháp, loại bỏ từ lặp** trong ghi âm.
✅ **Dữ liệu sạch sẽ**: Kết quả là **bài nhật ký Markdown** dễ dàng **chỉnh sửa, lưu trữ, chia sẻ**.
✅ **Hỗ trợ nhiều định dạng**: **MP3, M4A, OGG, OPUS...** đều được xử lý nhờ **CloudConvert fallback**.
✅ **Lưu trữ tự động**: **Google Drive** (tùy chọn) giúp **không mất bài nhật ký** dù điện thoại bị reset.
✅ **Hoạt động liên tục**: Workflow **chạy 24/7** trên VPS, không phụ thuộc vào điện thoại.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ**               | **Thao tác cần làm**                                                                 | **Link tham khảo**                          |
|---------------------------|--------------------------------------------------------------------------------------|---------------------------------------------|
| **Telegram Bot**          | Tạo bot Telegram và lấy **API Token** (để nhận ghi âm).                            | [@BotFather](https://t.me/BotFather)        |
| **Groq API**              | Đăng ký tài khoản và lấy **API Key** để transcribe âm thanh.                          | [Groq Console](https://console.groq.com/)    |
| **Google Gemini API**     | Đăng ký tài khoản **Google Cloud** và bật **Vertex AI API** (miễn phí 300$ thử nghiệm). | [Google Cloud](https://cloud.google.com/)   |
| **Google Drive** (tùy chọn) | Lấy **OAuth 2.0 Client ID** để lưu bài nhật ký.                                    | [Google Cloud Console](https://console.cloud.google.com/) |
| **CloudConvert** (tùy chọn) | Đăng ký tài khoản và lấy **API Key** để chuyển đổi âm thanh (fallback).              | [CloudConvert](https://cloudconvert.com/)     |

### **2. Cài đặt Node bổ sung**
- **CloudConvert Node**: N8n có sẵn node **@cloudconvert/n8n-nodes-cloudconvert**, nhưng cần **cài đặt từ Community** trong n8n Editor.
- **LangChain Nodes**: N8n hỗ trợ **@n8n/n8n-nodes-langchain** (cài đặt từ **Settings > Community Nodes**).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/15652) (hoặc copy JSON từ link trên).
2. Trong **n8n Editor**, nhấn **Import** → Chọn file JSON → **Import**.
3. **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/15652](https://n8n.io/workflows/15652).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán và **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Telegram Bot**
1. **Tạo bot Telegram**:
   - Mở @BotFather, gửi `/newbot` và theo hướng dẫn.
   - Lưu **API Token** (dùng để kết nối với n8n).
2. **Cấu hình Credential Telegram**:
   - Trong n8n, đi đến **Credentials** → **Add** → Chọn **Telegram API**.
   - Nhập **API Token** và **Chat ID** (lấy từ bot khi gửi `/start`).
   - **Lưu** và chọn credential này cho các node:
     - `Telegram Voice Trigger`
     - `Download Telegram Audio File`
     - `Send Markdown Journal to Telegram`

#### **B. Cấu hình Groq Whisper (Transcribe âm thanh)**
1. Mở node **`Transcribe Audio with Groq Whisper`**.
2. Trong **HTTP Request**, tìm **Authorization Header** và thay thế:
   ```
   Bearer YOUR_GROQ_API_KEY
   ```
   (Thay `YOUR_GROQ_API_KEY` bằng API Key từ [Groq Console](https://console.groq.com/keys)).
3. **Lưu** và test với một file âm thanh nhỏ.

#### **C. Cấu hình Google Gemini (Sửa lỗi & cải thiện bài nhật ký)**
1. Mở node **`Clean Transcript with Gemini`**.
2. Trong **Credentials**, chọn **googlePalmApi** (nếu chưa có, tạo mới trong **Credentials**).
3. Nhập **Google Cloud API Key** (lấy từ **Google Cloud Console** → **APIs & Services** → **Credentials**).
4. **Lưu** và kiểm tra **prompt** trong node **`Format Timestamped Transcript`** (nếu cần chỉnh sửa).

#### **D. Cấu hình CloudConvert (Fallback cho âm thanh không hỗ trợ)**
1. Cài đặt **CloudConvert Node** (nếu chưa có):
   - Đi đến **Settings** → **Community Nodes** → Tìm `@cloudconvert/n8n-nodes-cloudconvert` → **Install**.
2. Tạo **Credential CloudConvert**:
   - Trong **Credentials**, chọn **Add** → **CloudConvert API**.
   - Nhập **API Key** từ [CloudConvert Dashboard](https://cloudconvert.com/dashboard/api/v2/keys).
3. **Kiểm tra node**:
   - `Convert Audio to MP3 with CloudConvert` → Chọn credential CloudConvert.
   - `Transcribe Converted MP3 with Groq Whisper` → Đảm bảo Groq API đã cấu hình.

#### **E. Cấu hình Google Drive (Lưu trữ tự động)**
1. **Tạo Credential Google Drive**:
   - Trong **Credentials**, chọn **Add** → **Google Drive OAuth2 API**.
   - Theo hướng dẫn để **lấy Client ID & Secret** từ [Google Cloud Console](https://console.cloud.google.com/).
2. **Cấu hình node**:
   - `Find “Personal Journal (n8n)” Folder` → Chọn credential Google Drive.
   - `Create “Personal Journal (n8n)” Folder` → Chọn credential Google Drive.
   - `Upload Journal to New/Existing Folder` → Chọn credential Google Drive.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một **ghi âm Telegram** (voice note) đến bot.
   - Kiểm tra **Log** trong n8n để đảm bảo workflow chạy trơn tru.
2. **Bật Active**:
   - Nhấn **Active** ở góc trên bên phải của canvas.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa chất lượng bài nhật ký**
- **Chỉnh sửa Prompt Gemini**:
  Mở node **`Clean Transcript with Gemini`** và thay đổi **prompt** để phù hợp với phong cách viết của bạn. Ví dụ:
  ```json
  {
    "role": "user",
    "content": "Tôi muốn bạn chuyển đổi đoạn ghi âm sau thành bài nhật ký cá nhân, giữ nguyên ý nghĩa nhưng cải thiện ngữ pháp và loại bỏ từ lặp. Bài viết nên có cấu trúc rõ ràng, với tiêu đề và đoạn mở đầu ngắn gọn. Không thêm ý tưởng mới, chỉ sửa lỗi và làm cho bài viết dễ đọc hơn."
  }
  ```

### **2. Lưu trữ bài nhật ký lên Obsidian/Notion**
- Sau khi workflow gửi bài nhật ký về Telegram, các sếp có thể:
  - **Copy Markdown** và dán vào **Obsidian** (sử dụng plugin **Telegram Integration**).
  - **Xuất file Markdown** và lưu vào **Notion** (sử dụng template Markdown).

### **3. Tự động gửi báo cáo định kỳ**
- **Kết hợp với Slack/Telegram**:
  - Thêm node **`Slack`** hoặc **`Telegram`** sau khi hoàn thành workflow để gửi **tin nhắn thông báo** khi có bài nhật ký mới.
- **Lưu log hoạt động**:
  - Thêm node **`StickyNote`** để ghi lại **thời gian, tên file, và nội dung tóm tắt** của mỗi bài nhật ký.

### **4. Hỗ trợ nhiều ngôn ngữ**
- **Groq Whisper** tự động phát hiện ngôn ngữ, nhưng nếu cần **chuyển đổi ngôn ngữ**, thêm node **`Translate`** (sử dụng API Google Translate hoặc DeepL).

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa nhật ký cá nhân** mà không cần viết tay.
✔ **Lưu trữ an toàn** bài nhật ký trên Google Drive.
✔ **Hỗ trợ nhiều định dạng âm thanh** với hệ thống fallback tự động.
✔ **Tiết kiệm thời gian** cho công việc hàng ngày.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một ghi âm** để đảm bảo hoạt động.
3. **Bật Active** và bắt đầu **nhật ký AI** của mình!

---
**Cần hỗ trợ?** Liên hệ với tác giả [Atha Ahsan Xavier Haris](https://www.linkedin.com/in/athaahsan/) qua LinkedIn hoặc để lại comment bên dưới! 🚀