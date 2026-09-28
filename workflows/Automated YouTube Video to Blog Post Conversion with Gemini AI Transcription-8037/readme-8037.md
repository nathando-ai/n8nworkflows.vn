---
title: "🚀 Tự Động Chuyển Video YouTube Sang Bài Blog Chuyên Nghiệp Với Gemini AI (Không Cần Code)"
description: "Workflow tự động hóa chuyển đổi video YouTube thành bài blog hoàn chỉnh với tiêu đề, nội dung, mô tả, danh mục và thẻ bằng trí tuệ nhân tạo Gemini, tiết kiệm thời gian lên đến 80% cho các sếp content creator."
slug: "tuy-dong-hoa-chuyen-doi-video-youtube-sang-blog-voi-gemini-ai"
tags: [n8n, automation, content-creation, ai-gemini, no-code, youtube-to-blog]
keywords: [n8n workflow youtube, tự động hóa blog, gemini ai chuyển đổi video, tự động hóa nội dung, chuyển video youtube thành bài viết]
---

# 🚀 **Tự Động Chuyển Video YouTube Sang Bài Blog Chuyên Nghiệp Với Gemini AI**

### **Giải pháp hoàn hảo cho các sếp content creator, blogger hoặc marketer muốn tiết kiệm thời gian và tạo nội dung chất lượng cao mà không cần viết tay**

Hiện nay, việc tạo nội dung blog từ video YouTube vẫn là một công việc **mệt mỏi và tốn thời gian** với các bước:
✅ Tải video từ YouTube
✅ Chuyển đổi thành văn bản (transcription)
✅ Tóm tắt và cấu trúc lại thành bài viết blog
✅ Thêm tiêu đề, mô tả, danh mục và thẻ SEO
✅ Đăng tải lên WordPress hoặc CMS khác

**Workflow này tự động hóa toàn bộ quá trình chỉ với một cú nhấp chuột!** Bằng trí tuệ nhân tạo **Google Gemini**, video YouTube của bạn sẽ được chuyển đổi thành **bài blog hoàn chỉnh** với:
📌 **Tiêu đề hấp dẫn**
📌 **Nội dung chi tiết và logic**
📌 **Mô tả ngắn gọn**
📌 **Danh mục và thẻ SEO**
📌 **Cấu trúc chuẩn SEO**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với viết bài thủ công.
- **Nội dung chất lượng cao** với cấu trúc logic và SEO friendly.
- **Hoạt động liên tục 24/7** khi kết nối với webhook.
- **Cá nhân hóa** theo yêu cầu của từng video.
- **Không cần kỹ năng code** – chỉ cần copy/paste và chạy.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Cloud** (để sử dụng API Gemini)
✔ **API Key Google Cloud** (cấp quyền cho `https://www.googleapis.com/auth/gemini-api`)
✔ **URL YouTube** (cần gửi qua webhook để workflow xử lý)
✔ **CMS hoặc nền tảng blog** (nếu muốn tự động đăng bài, ví dụ: WordPress, Ghost, hoặc API của CMS)

---
:::info[CHUẨN BỊ]
- **N8n Self-hosted** (không dùng phiên bản cloud)
- **Node LangChain** (đã cài đặt trong n8n)
- **Dung lượng lưu trữ** (để lưu file audio tạm thời)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/) và chọn **Import Workflow**.
2. Chọn file JSON từ [link gốc](https://n8n.io/workflows/8037) hoặc copy toàn bộ JSON từ đây.
3. Nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Webhook (Node: "Get Youtube Url")**
- **Key Parameters**:
  - `path`: `57fddbda-a118-4546-a223-8e91a7d53ff6` (không thay đổi)
  - `httpMethod`: `POST` (không thay đổi)
- **Credentials**: Không cần thiết (webhook sẽ nhận dữ liệu từ bên ngoài).

##### **B. Cấu hình API Google Gemini (Node: "Google Gemini Chat Model" & "Transcribe a recording")**
- **Credentials**:
  - Tên: `googlePalmApi`
  - Thêm **API Key** từ Google Cloud vào n8n.
  - Cấp quyền: `https://www.googleapis.com/auth/gemini-api`
- **Key Parameters**:
  - **Node "Transcribe a recording"**:
    - `resource`: `audio` (không thay đổi)
  - **Node "Google Gemini Chat Model"**:
    - **Prompt**: Sử dụng mặc định hoặc tùy chỉnh:
      ```json
      {
        "task": "Convert YouTube video transcript into a structured blog post with title, description, category, tags, and content."
      }
      ```

##### **C. Cấu hình AI Agent (Node: "AI Agent")**
- **Input**: Nhận dữ liệu từ **Structured Output Parser**.
- **Output**: Trả về JSON có cấu trúc như:
  ```json
  {
    "title": "Tiêu đề bài blog",
    "description": "Mô tả ngắn gọn",
    "category": "Danh mục",
    "tags": ["thẻ1", "thẻ2"],
    "content": "Nội dung bài viết chi tiết..."
  }
  ```

##### **D. Cấu hình Node "Download the Youtube Audio"**
- **Command**: Sử dụng `youtube-dl` (cài đặt trước trên VPS):
  ```bash
  sudo apt-get install youtube-dl
  ```
- **Parameters**:
  - `url`: `{json["url"]}` (lấy từ webhook)
  - `format`: `bestaudio/best` (chọn chất lượng audio tốt nhất)
  - `output`: `temp/audio.mp3` (lưu tạm thời)

##### **E. Cấu hình Node "Respond The Blog Post"**
- **Response**: Trả về JSON kết quả cuối cùng (có thể gửi qua Slack, Telegram hoặc lưu vào Google Sheets).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một URL YouTube qua webhook (ví dụ: `POST https://[your-n8n-url]/webhook/57fddbda-a118-4546-a223-8e91a7d53ff6` với body JSON:
     ```json
     {
       "url": "https://www.youtube.com/watch?v=EXAMPLE_VIDEO_ID"
     }
     ```
   - Kiểm tra kết quả trong **n8n Dashboard**.

2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả chuyển đổi.

2. **Lưu log vào Google Sheets**:
   - Sử dụng node **Google Sheets** để ghi lại lịch sử chuyển đổi (URL, tiêu đề, thời gian xử lý).

3. **Tự động đăng bài lên WordPress**:
   - Kết nối với **WordPress REST API** để đăng bài tự động sau khi chuyển đổi.

4. **Tùy chỉnh prompt cho AI**:
   - Để nội dung phù hợp với phong cách blog của các sếp, chỉnh sửa **prompt** trong node `Google Gemini Chat Model`.

5. **Xử lý video dài**:
   - Nếu video quá dài, chia thành nhiều phần và xử lý từng phần riêng biệt.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa nội dung blog từ video YouTube** mà không cần viết tay. Với **Gemini AI**, nội dung sẽ được **cấu trúc logic, SEO friendly** và **tiết kiệm thời gian đáng kể**.

**Hành động ngay!**
1. Import workflow vào n8n.
2. Cấu hình API Google Cloud.
3. Gửi URL YouTube qua webhook và xem kết quả **bài blog hoàn chỉnh** chỉ trong vài giây!

**Cần hỗ trợ?** Đừng ngần ngại liên hệ với tác giả [Atta](https://n8n.io/workflows/8037) để được tư vấn chi tiết! 🚀