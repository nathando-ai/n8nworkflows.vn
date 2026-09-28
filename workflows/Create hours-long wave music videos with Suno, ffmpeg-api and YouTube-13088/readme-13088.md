---
title: "🎵 Tự Động Hoà Âm & Chỉnh Sửa Video YouTube Dài Hơn 1 Giờ Với AI - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh từ tạo nhạc wave dài giờ bằng Suno, xử lý video với ffmpeg-api đến upload tự động lên YouTube. Giúp content creator tiết kiệm 10+ giờ công sức mỗi video!"
slug: "tieu-dong-hoa-tao-nhac-video-youTube-dai-hon-1-gio"
tags: [n8n, automation, content-creation, AI-music, YouTube-automation, ffmpeg-api]
keywords: [tự động hóa tạo nhạc video YouTube, Suno API n8n, ffmpeg-api tự động, upload YouTube tự động, AI tạo nhạc wave, workflow n8n content creator]
---

# 🚀 **Tự Động Hoà Âm Video YouTube Dài Hơn 1 Giờ Với AI - Không Cần Code!**

### **Giải pháp hoàn chỉnh cho content creator**
Bạn là một **content creator** hay **youtuber** muốn tạo **video dài giờ** (1-3 giờ) với nhạc wave ấn tượng nhưng lại **mệt mỏi** với quá trình:
- Tìm nhạc phù hợp?
- Chỉnh sửa âm thanh và video?
- Upload tự động lên YouTube?

Workflow này **tự động hóa toàn bộ quy trình** từ **tạo nhạc wave AI** đến **xuất bản video lên YouTube** chỉ với **một cú nhấp chuột**! Không cần kỹ năng code, không cần chỉnh sửa thủ công – chỉ cần **cung cấp chủ đề nhạc và video nền**, workflow sẽ **xử lý tất cả**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ công sức** mỗi video – workflow tự động hóa **tất cả** từ tạo nhạc đến upload YouTube.
✅ **Nhạc wave dài giờ ấn tượng** – Suno AI tạo nhạc phù hợp với chủ đề, không cần tìm kiếm thủ công.
✅ **Chỉnh sửa video tự động** – ffmpeg-api xử lý âm thanh và video một cách chuyên nghiệp.
✅ **Upload YouTube tự động** – Video được xuất bản ngay sau khi hoàn thành, không cần can thiệp thủ công.
✅ **Dễ dàng mở rộng** – Thêm nhiều track nhạc, chỉnh sửa metadata tự động, hoặc tự động chia sẻ lên các nền tảng khác.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Suno API** (để tạo nhạc wave):
   - [Đăng ký Suno API](https://kie.ai?ref=f8cec88ea15f9ecbff52ccbafa41dd6e) (mã giới thiệu: `f8cec88ea15f9ecbff52ccbafa41dd6e`).
   - Lấy **API Key** từ tài khoản Suno.

2. **Tài khoản ffmpeg-api** (để xử lý video và âm thanh):
   - [Đăng ký ffmpeg-api](https://ffmpeg-api.com) và lấy **API Key**.

3. **Tài khoản YouTube (Blotato)**:
   - [Đăng ký Blotato](https://blotato.com/?ref=giang9s) (mã giới thiệu: `giang9s`) để upload tự động.
   - Cần **OAuth 2.0 Token** của YouTube.

4. **Tài khoản Google Sheets** (để lưu log nhạc và metadata):
   - Một bảng Google Sheets để lưu trữ thông tin nhạc và video.

5. **Tài khoản Gemini AI** (để tạo metadata SEO):
   - [Đăng ký Google AI Studio](https://aistudio.google.com/) và lấy **API Key**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13088](https://n8n.io/workflows/13088) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13088) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **27 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **A. Cấu hình API Keys**
- **Suno API**:
  - Node: `Create Song (Suno API)`
  - Điền **API Key** từ Suno vào `Authorization` header.

- **ffmpeg-api**:
  - Node: `Create Working Directory (ffmpeg-api)`, `Prepare Video Path (ffmpeg-api)`, `Merge Audio with Video (ffmpeg-api)`,...
  - Điền **API Key** từ ffmpeg-api vào `Authorization` header.

- **Blotato (YouTube Upload)**:
  - Node: `Publish YouTube Video`, `Upload Media On Blotato`
  - Chọn **credentials OAuth 2.0** từ tài khoản Blotato.

- **Google Sheets**:
  - Node: `Log Song Metadata`
  - Chọn **Google Sheets credentials** và chỉ định **Sheet Name** để lưu log.

- **Gemini AI**:
  - Node: `Gemini LLM`, `Gemini LLM1`
  - Điền **API Key** từ Google AI Studio.

##### **B. Cấu hình Input Form**
- Node: `Suno Wave Music Input Form`
  - Thêm các trường sau:
    - `Music Theme` (chủ đề nhạc, ví dụ: "Video game epic", "Chill study music").
    - `Background Video URL` (link video nền từ YouTube/Vimeo).
    - `Number of Tracks` (số track nhạc muốn tạo, ví dụ: 3 track).
    - `YouTube Title` (tên video trên YouTube, có thể để trống để AI tự động tạo).

##### **C. Cấu hình AI Agent (Music Prompt & SEO Metadata)**
- Node: `Generate Music Prompts (AI Agent)` và `Generate SEO Title & Description`
  - Các sếp có thể **tùy chỉnh prompt** để AI tạo nhạc và metadata phù hợp với phong cách của mình.

##### **D. Cấu hình ffmpeg-api Paths**
- Node: `Create Working Directory (ffmpeg-api)`, `Prepare Video Path (ffmpeg-api)`, `Prepare Audio Path (ffmpeg-api)`
  - Đảm bảo **path storage** trong ffmpeg-api là **rỗng** hoặc đã xóa trước khi chạy workflow.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập một **chủ đề nhạc**, **video nền**, và số **track**.
   - Chạy **Test Run** để kiểm tra workflow hoạt động như thế nào.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi có input.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tạo nhiều video cùng lúc**:
   - Sử dụng **Webhook** để nhận dữ liệu từ một form ngoài (ví dụ: Typeform, Google Form) và tự động kích hoạt workflow.

2. **Lưu log và báo cáo**:
   - Node `Log Song Metadata` sẽ ghi lại tất cả thông tin nhạc và video vào Google Sheets. Các sếp có thể **tạo báo cáo tự động** bằng Google Data Studio.

3. **Tự động chia sẻ lên Telegram/Slack**:
   - Thêm node **Telegram Bot** hoặc **Slack Webhook** sau node `Publish YouTube Video` để thông báo khi video được upload.

4. **Tối ưu hóa chất lượng video**:
   - Trong node `Merge Audio with Video (ffmpeg-api)`, các sếp có thể **tùy chỉnh bitrate** và **kích thước video** để phù hợp với YouTube.

5. **Sử dụng AI Agent nâng cao**:
   - Tùy chỉnh **prompt** trong node `Generate Music Prompts` và `Generate SEO Title & Description` để AI tạo nhạc và metadata **phù hợp với phong cách riêng** của các sếp.

---

### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn** công sức của các sếp trong việc tạo **video dài giờ với nhạc wave ấn tượng**! Từ **tạo nhạc AI** đến **upload YouTube tự động**, tất cả đều được xử lý **một cách chuyên nghiệp và không cần code**.

**Hãy thử ngay!**
1. **Import workflow** và cấu hình API keys.
2. **Nhập chủ đề nhạc và video nền**.
3. **Chạy workflow** và xem video của mình **xuất hiện trên YouTube chỉ trong vài phút!**

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/13088) và bắt đầu tự động hóa content của mình **hôm nay!** 🚀