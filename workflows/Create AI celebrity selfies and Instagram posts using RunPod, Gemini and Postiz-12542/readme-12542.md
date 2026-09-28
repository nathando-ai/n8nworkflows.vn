---
title: "🚀 Tự Động Hóa Tạo Ảnh Selfie AI Với Nghiên Cứu Viên & Bài Post Viral Cho Instagram (N8n + RunPod + Gemini + Postiz)"
description: "Workflow này tự động hóa quá trình tạo ảnh selfie AI với các ngôi sao nổi tiếng, viết caption viral và đăng lên Instagram chỉ trong vài giây. Giúp các sếp tiết kiệm thời gian lên đến 80% trong content marketing, đồng thời tăng tương tác và engagement cho trang cá nhân/doanh nghiệp."
slug: "tay-dong-hoa-tao-selfie-ai-ngoi-sao-va-bai-post-instagram"
tags: [n8n, automation, content-creation, ai-multimodal, instagram-automation, runpod, google-gemini, postiz]
keywords: [tự động hóa n8n, tạo ảnh selfie ai, content marketing tự động, đăng bài instagram tự động, gemini ai, runpod api, postiz instagram]
---

# 🚀 **Tự Động Hóa Tạo Ảnh Selfie AI Với Nghiên Cứu Viên & Bài Post Viral Cho Instagram**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tạo nội dung viral** chỉ với một cú nhấp chuột.
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Tăng tương tác** với hình ảnh AI cá nhân hóa và caption hấp dẫn.
- **Hoạt động 24/7** mà không cần can thiệp.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo ảnh selfie AI** với các ngôi sao nổi tiếng (Taylor Swift, Elon Musk, Cristiano Ronaldo...) chỉ trong vài giây.
- **Caption viral tự động** bằng Google Gemini, tối ưu hashtag và nội dung hấp dẫn.
- **Đăng bài lên Instagram** một cách tự động qua Postiz, tiết kiệm thời gian quản lý tài khoản.
- **Lưu trữ ảnh** trên Google Drive để quản lý và sử dụng lại.
- **Hoạt động liên tục** mà không cần can thiệp, tiết kiệm thời gian cho các sếp.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản RunPod** (để sử dụng Nano Banana Pro Edit API):
   - [Đăng ký RunPod](https://get.runpod.io/) và lấy **API Key Bearer Auth**.
2. **Tài khoản Google Cloud** (để sử dụng Google Gemini API):
   - [Cài đặt Google Gemini API](https://makersuite.google.com/app/apikey) và lấy **Google Palm API Key**.
3. **Tài khoản Google Drive** (để lưu trữ ảnh):
   - [Cấu hình OAuth2 cho Google Drive](https://developers.google.com/drive/api/v3/quickstart/python).
4. **Tài khoản Postiz** (để đăng bài lên Instagram):
   - [Đăng ký Postiz](https://postiz.com/?ref=n3witalia) và lấy **Channel ID** từ Dashboard.
5. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải workflow** từ [đây](https://n8n.io/workflows/12542) và chọn **Import**.
- **Hoặc copy/paste** JSON vào **n8n Editor** và chọn **Create Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
Các sếp cần cập nhật **credentials** cho các node quan trọng:

| **Node**               | **Credentials**               | **Hướng dẫn**                                                                 |
|------------------------|-------------------------------|-------------------------------------------------------------------------------|
| **Get status clip**    | `httpBearerAuth`              | Điền **API Key** từ RunPod vào **Credentials Manager** của n8n.              |
| **Generate selfie**    | `httpBearerAuth`              | Cùng với **API Key** từ RunPod.                                               |
| **Upload to Postiz**   | `httpHeaderAuth`              | Thêm **Header Auth** với `Authorization: Bearer <Postiz API Key>`.            |
| **Upload to Social**   | `postizApi`                   | Điền **Channel ID** từ Postiz vào **Credentials Manager**.                     |
| **SMC Agent**          | `googlePalmApi`              | Điền **API Key** từ Google Cloud vào **Credentials Manager**.                  |
| **Upload file**        | `googleDriveOAuth2Api`        | Cấu hình OAuth2 cho Google Drive (theo hướng dẫn [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python)). |

#### **B. Cấu hình Node Form Trigger**
- Thêm các **fields** sau vào **Form Trigger**:
  - `IMAGE_URL` (URL ảnh gốc).
  - `PROMPT` (mô tả selfie muốn tạo, ví dụ: *"Tôi với Taylor Swift ở Paris"*).
  - `FORMAT` (kiểu hình ảnh, ví dụ: `1:1` cho Instagram).

#### **C. Cập nhật Endpoint & Folder ID**
- Trong node **Upload file (Google Drive)**, cập nhật:
  - **Folder ID** (lấy từ liên kết Google Drive của bạn).
- Trong node **Upload to Postiz**, cập nhật:
  - **Endpoint** của Postiz (lấy từ Dashboard Postiz).

#### **D. Test Run & Kích hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhập một **URL ảnh**, **prompt** và **format**.
   - Chạy workflow và kiểm tra các bước:
     - **Generate selfie** (kiểm tra ảnh có được tạo không).
     - **SMC Agent** (kiểm tra caption có hợp lý không).
     - **Upload to Postiz** (kiểm tra bài đã đăng lên Instagram chưa).
2. **Bật Active** workflow khi tất cả các bước chạy thành công.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
2. **Lưu Log & Analytics**:
   - Sử dụng node **Google Sheets** để lưu trữ dữ liệu của từng bài post (URL, caption, lượt tương tác).
3. **Tự động Chọn Hashtag**:
   - Sử dụng **Google Gemini** để phân tích trend hashtag và tự động cập nhật.
4. **Tạo Bài Post cho TikTok/YouTube Shorts**:
   - Sử dụng node **Postiz** để đăng bài lên TikTok hoặc YouTube Shorts cùng một lúc.
5. **Tự động Xóa Ảnh Sau Một Thời Gian**:
   - Sử dụng node **Google Drive** để xóa ảnh sau 30 ngày nếu không cần thiết.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **content marketing** trên Instagram mà không cần viết code. Với **AI tạo ảnh, caption viral và đăng bài tự động**, các sếp sẽ tiết kiệm **80% thời gian** và tăng **tương tác hiệu quả**.

👉 **Bắt đầu ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS.
2. **Import workflow** và cấu hình credentials.
3. **Test Run** và kích hoạt workflow.
4. **Chia sẻ kết quả** với bạn bè và đồng nghiệp!

**Nếu có vấn đề, hãy liên hệ với Davide qua [LinkedIn](https://linkedin.com/in/davideboizza) hoặc email [info@n3w.it](mailto:info@n3w.it) để hỗ trợ!**

---
**🎁 Đăng ký VPS TinoHost với mã giảm giá VPSN8N để chạy workflow 24/7!**
👉 [Đăng ký ngay](https://tino.vn/vps-n8n?affid=388)