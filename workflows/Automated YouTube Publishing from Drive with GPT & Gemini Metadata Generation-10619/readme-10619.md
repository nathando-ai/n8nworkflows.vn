---
title: "🚀 Tự Động Hóa Tạo & Đăng Video YouTube Từ Google Drive Với AI GPT & Gemini (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tự động tải video từ Google Drive, tự động tạo tiêu đề, mô tả, thẻ SEO bằng AI, sau đó đăng lên YouTube và chia sẻ trên Instagram/Facebook chỉ trong vài giây. Giảm thời gian tạo nội dung xuống 0%!"
slug: "tu-dong-hoa-tao-dang-video-youtube-tu-google-drive-voi-ai"
tags: [n8n, automation, content-creation, ai-gpt, youtube-automation, google-drive, gemini-ai]
keywords: [n8n workflow youtube, tự động hóa video youtube, ai tạo mô tả video, gemini tự động thẻ youtube, tự động đăng video instagram facebook]
---

# 🚀 **Tự Động Hóa Tạo & Đăng Video YouTube Từ Google Drive Với AI GPT & Gemini**

## **🔥 Bỏ Qua Giai Đoạn "Tạo Nội Dung" Mệt Mỏi!**
Hãy tưởng tượng: Bạn chỉ cần **đăng video lên Google Drive**, workflow sẽ tự động:
✅ **Tải video** từ thư mục chỉ định
✅ **Tạo tiêu đề, mô tả, thẻ SEO** bằng AI (OpenAI GPT + Google Gemini)
✅ **Đăng video lên YouTube** với metadata tối ưu
✅ **Xóa video khỏi Drive** sau khi đăng thành công
✅ **Chia sẻ tự động** lên Instagram và Facebook (nếu cần)

Không cần viết code, không cần kiến thức kỹ thuật – chỉ cần **cài đặt 1 lần** và workflow sẽ hoạt động **24/7** như một "nhân viên tự động" của bạn!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và an toàn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** cho việc tạo metadata và đăng video thủ công.
- **Tối ưu SEO YouTube** với tiêu đề, mô tả và thẻ tự động sinh bởi AI.
- **Hoạt động liên tục** (không cần can thiệp người dùng).
- **Chia sẻ tự động** trên Instagram/Facebook (nếu cấu hình).
- **Giảm rủi ro lỗi** so với cách làm thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để lưu video và kích hoạt trigger).
✔ **API Key OpenAI** (để sử dụng GPT-4 cho mô tả và tiêu đề).
✔ **API Key Google Gemini** (để sinh thẻ YouTube).
✔ **Tài khoản YouTube** (đã kết nối OAuth2).
✔ **Tài khoản Telegram** (để nhận thông báo khi video đăng thành công).
✔ **Tài khoản Facebook Business** (nếu muốn chia sẻ trên Instagram/Facebook):
   - **Đã xác thực doanh nghiệp** (xem hướng dẫn bên dưới).
   - **Token System User** (không hết hạn).

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/10619](https://n8n.io/workflows/10619) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Workflow sẽ xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/10619](https://n8n.io/workflows/10619).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Workflow sẽ tự động được tạo.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: "New Video?" (Google Drive Trigger)**
- **Cấu hình**:
  - Chọn **Google Drive OAuth2Api** (đã cấu hình trước).
  - **Folder ID**: Đặt vào thư mục Google Drive chứa video cần tự động hóa.
  - **File Type**: Chọn **Video** (`.mp4`, `.mov`, `.avi`...).
  - **Operation**: Chọn **Create** (để kích hoạt khi có file mới).

#### **🔹 Node 2: "Download New Video" (Google Drive)**
- **Cấu hình**:
  - Sử dụng **Google Drive OAuth2Api** cùng với node trước.
  - **File ID**: Lấy từ trigger (hoặc sử dụng `{{$node["New Video?"].json["files"][0].id}}`).
  - **Destination**: Chọn **Download to local** (n8n sẽ tải video vào máy chủ).

#### **🔹 Node 3 & 4: Tạo Metadata với AI (OpenAI + Gemini)**
- **"YT Title" (OpenAI)**:
  - **Model**: Chọn **GPT-4** (hoặc GPT-3.5).
  - **Prompt**: Sử dụng template mặc định (hoặc tự viết):
     ```
     Tạo tiêu đề YouTube hấp dẫn cho video có tên: {{$node["Download New Video"].json["fileName"]}}.
     Tiêu đề phải ngắn gọn (50-60 ký tự), có từ khóa chính và thu hút người xem.
     ```
  - **API Key**: Điền **OpenAI API Key** (đã cấu hình trước).

- **"2.5FlashPrev" (Google Gemini)**:
  - **Model**: Chọn **Gemini Pro**.
  - **Prompt**: Sử dụng template mặc định (hoặc tự viết):
     ```
     Tạo 10 thẻ YouTube phù hợp cho video có tên: {{$node["Download New Video"].json["fileName"]}}.
     Thẻ phải liên quan đến nội dung video và có từ khóa có traffic cao.
     ```
  - **API Key**: Điền **Google Palm API Key** (đã cấu hình trước).

- **"Create Description" (OpenAI)**:
  - **Model**: Chọn **GPT-4**.
  - **Prompt**: Sử dụng template:
     ```
     Tạo mô tả YouTube chi tiết (150-200 từ) cho video có tên: {{$node["Download New Video"].json["fileName"]}}.
     Mô tả phải bao gồm:
     1. Giới thiệu ngắn về video.
     2. Cách sử dụng/điểm nổi bật.
     3. Call-to-action (vd: "Like, Share, Subscribe").
     ```
  - **API Key**: Điền **OpenAI API Key**.

#### **🔹 Node 5: "Upload to YouTube"**
- **Cấu hình**:
  - **YouTube OAuth2Api**: Chọn tài khoản đã kết nối.
  - **Video File**: Chọn file từ node **Download New Video**.
  - **Title**: Lấy từ node **YT Title** (`{{$node["YT Title"].json["content"]}}`).
  - **Description**: Lấy từ node **Create Description**.
  - **Tags**: Lấy từ node **2.5FlashPrev** (`{{$json["tags"].join(", ")}}`).
  - **Privacy Status**: Chọn **Public** (hoặc Private nếu cần).

#### **🔹 Node 6: "Delete video from Upload Folder" (Google Drive)**
- **Cấu hình**:
  - **File ID**: Lấy từ node **Download New Video**.
  - **Operation**: Chọn **Delete File**.

#### **🔹 Node 7-14: Chia sẻ trên Telegram/Instagram/Facebook**
- **"Send a text message" (Telegram)**:
  - **Message**: Tự viết thông báo thành công (vd: `🎉 Video "{{$node["Download New Video"].json["fileName"]}}" đã đăng lên YouTube thành công!`).
- **"Post to Instagram" & "Post to Facebook" (HTTP Request)**:
  - **Token**: Sử dụng **System User Token Facebook** (xem hướng dẫn bên dưới).
  - **Link Video**: Lấy từ YouTube (`{{$node["Upload to youtube"].json["videoId"]}}`).
  - **Caption**: Lấy từ mô tả YouTube (`{{$node["Create Description"].json["content"]}}`).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Đăng một video mẫu lên Google Drive.
   - Chạy **Manual Test** trên node **New Video?** để kiểm tra workflow.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi ý Nâng Cao**

### **1. Cấu hình Facebook System User Token (Không Hết Hạn)**
Facebook yêu cầu **xác thực doanh nghiệp** trước khi tạo token không hết hạn. Hướng dẫn chi tiết:
1. **Xác thực doanh nghiệp**:
   - Đăng nhập [Facebook Business Settings](https://business.facebook.com/settings/info).
   - Điền thông tin doanh nghiệp và **nộp giấy tờ xác thực** (EIN/Tax-ID).
   - Đợi **1-5 ngày** để được phê duyệt.
2. **Tạo System User**:
   - Đi đến **System Users** → **Add**.
   - Chọn **Admin** và đặt tên (vd: `n8n-bot`).
3. **Gán quyền**:
   - Chọn **Page** (Full Control), **Instagram Account**, và **App**.
4. **Tạo Token**:
   - Nhấn **Generate Token** → Chọn **Never Expire**.
   - Cấp quyền:
     - `pages_show_list`
     - `pages_read_engagement`
     - `pages_manage_posts`
     - `instagram_basic`
     - `instagram_content_publish` (nếu cần).

### **2. Tối ưu Workflow**
- **Thêm node "Wait"** giữa các bước để tránh overloading API.
- **Lưu log** bằng node **StickyNote** để theo dõi lỗi.
- **Gửi báo cáo định kỳ** qua Telegram/Email khi có video mới đăng.

### **3. Kết hợp với Slack**
- Thêm node **Slack** để thông báo khi video đăng thành công.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc mệt mỏi là **tạo metadata và đăng video thủ công**. Với **AI GPT & Gemini**, video của bạn sẽ có **tiêu đề hấp dẫn, mô tả SEO tốt** và **được đăng tự động** lên YouTube, Instagram, Facebook.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Cấu hình các API Key** (Google Drive, OpenAI, Gemini, YouTube, Facebook).
3. **Import workflow** và **bật Active**.

**🚀 Còn chờ gì nữa?** Hãy tự động hóa nội dung của mình ngay hôm nay! 🚀