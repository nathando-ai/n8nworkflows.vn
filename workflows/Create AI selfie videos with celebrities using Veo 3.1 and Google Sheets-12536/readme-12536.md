---
title: "🎥 Tự Động Hóa Sáng Tạo Video Selfie AI Với Nghệ Sĩ Nổi Tiếng - Dùng Veo 3.1 + Google Sheets"
description: "Workflow này tự động hóa quá trình tạo video selfie AI với các nhân vật nổi tiếng, giúp các sếp tiết kiệm thời gian và tạo nội dung viral trên TikTok, Instagram, YouTube chỉ với 1 cú nhấp chuột. Kết quả: Video chất lượng cao, phân phối tự động, không cần code."
slug: "tieu-dong-hoa-tao-video-selfie-ai-veo-3-1-google-sheets"
tags: [n8n, automation, content-creation, multimodal-ai, video-editing, google-sheets, veo-3-1, tiktok-automation, youtube-automation]
keywords: [n8n workflow tự động hóa video, tạo video selfie AI, Veo 3.1 API, tự động hóa TikTok, tự động hóa Instagram, tự động hóa YouTube, Google Sheets tự động, nội dung viral tự động]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video Selfie AI Với Nghệ Sĩ Nổi Tiếng - Dùng Veo 3.1 + Google Sheets**

### **Giải Pháp Cho Các Sếp Muốn Tạo Nội Dung Viral Miễn Phải Lo Lắng**
Hiện nay, việc tạo video selfie AI với các nhân vật nổi tiếng đang là xu hướng hot trên TikTok, Instagram và YouTube. Tuy nhiên, quá trình này thường tốn thời gian, yêu cầu kỹ năng chỉnh sửa video cao và phải phụ thuộc vào các nền tảng độc quyền. **Workflow này giúp các sếp tự động hóa toàn bộ quá trình từ đầu đến cuối, chỉ với một cú nhấp chuột!**

Thay vì phải sử dụng các công cụ đóng kín, workflow này kết hợp **API Veo 3.1 của fal.ai** (một trong những mô hình AI tiên tiến nhất hiện nay) với **Google Sheets** để:
✅ **Tạo video selfie AI** với các nhân vật nổi tiếng (nghệ sĩ, diễn viên, ca sĩ...)
✅ **Tự động kiểm tra trạng thái** và cập nhật kết quả vào Google Sheets
✅ **Gộp video** thành một đoạn clip hoàn chỉnh
✅ **Phân phối tự động** lên Google Drive, YouTube, TikTok, Instagram, Facebook và X (Twitter) thông qua **Postiz**
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ cần nhập prompt và hình ảnh, workflow tự động xử lý toàn bộ quá trình.
- **Nội dung chất lượng cao**: Sử dụng mô hình AI Veo 3.1 để tạo video tự nhiên, giống như thực tế.
- **Phân phối đa nền tảng**: Video được tự động upload lên YouTube, TikTok, Instagram, Facebook và X (Twitter) thông qua Postiz.
- **Dễ dàng theo dõi**: Tất cả trạng thái và kết quả được cập nhật trực tiếp vào Google Sheets.
- **Không phụ thuộc vào nền tảng**: Không cần sử dụng các công cụ độc quyền, toàn bộ quá trình được tự động hóa trên n8n.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản fal.ai** (để sử dụng API Veo 3.1):
   - [Đăng ký tài khoản](https://fal.ai/) và lấy **API Key**.
2. **Google Sheets** với cấu trúc cột như sau:
   - `START` (hình ảnh đầu tiên)
   - `LAST` (hình ảnh cuối cùng)
   - `PROMPT` (mô tả video)
   - `DURATION` (thời lượng video)
   - `VIDEO URL` (để lưu kết quả)
   - `MERGE` (đánh dấu để gộp video)
   - **Lưu ý**: Hình ảnh trong cột `LAST` của dòng này phải khớp với hình ảnh trong cột `START` của dòng tiếp theo!
   - [Mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1QLZmenUJ-vQAw2UzCe-zKTeWU9ybC1aVfi4ThVq3aUg/edit?usp=sharing)
3. **Google Drive OAuth 2.0** (để upload video).
4. **Postiz API Key** (để phân phối video lên TikTok, Instagram, Facebook, X, YouTube):
   - [Đăng ký Postiz](https://affiliate.postiz.com/n3witalia) và lấy **Channel ID**.
5. **(Tùy chọn)** Tài khoản YouTube và **API Key của Upload-Post** (để upload video lên YouTube):
   - [Đăng ký Upload-Post](https://www.upload-post.com/?linkId=lp_144414&sourceId=n3witalia&tenantId=upload-post-app) và lấy **Username** và **Title**.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấp vào **Import** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/12536)).
3. Hoặc copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12536) và paste vào **Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **23 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **A. Cấu Hình Credentials**
- **Google Sheets OAuth 2.0**:
  - Đăng nhập vào n8n và thêm **Google Sheets OAuth 2.0** credentials.
  - Chọn quyền: `Read/Write`.
  - Sau khi cấp quyền, chọn **Google Sheet** cần sử dụng (mẫu đã cung cấp).

- **Google Drive OAuth 2.0**:
  - Thêm **Google Drive OAuth 2.0** credentials.
  - Chọn quyền: `Read/Write`.

- **fal.ai API Key (HTTP Header Auth)**:
  - Trong các node `httpRequest` liên quan đến Veo 3.1, thêm **Header Auth**:
    - **Name**: `Authorization`
    - **Value**: `Key YOURAPIKEY` (thay `YOURAPIKEY` bằng API Key từ fal.ai).

- **Postiz API Key**:
  - Thêm **Postiz API Key** trong node `n8n-nodes-postiz.postiz`.
  - Điền **Channel ID** từ Postiz.

- **(Tùy chọn) Upload-Post API Key**:
  - Nếu muốn upload lên YouTube, thêm **HTTP Header Auth** trong node `httpRequest` (Upload to Youtube):
    - **Name**: `Authorization`
    - **Value**: `Bearer YOUR_UPLOAD_POST_API_KEY` (lấy từ Upload-Post).

##### **B. Cấu Hình Node Quan Trọng**
1. **Node `Get prompts` và `Get prompt` (Google Sheets)**:
   - Chọn **Google Sheets OAuth 2.0** credentials đã thiết lập.
   - Chọn **Sheet Name** là tên của Google Sheet mẫu.
   - Chọn **Range**: `Sheet1!A:F` (hoặc điều chỉnh theo cấu trúc cột của bạn).

2. **Node `Set params` (Set)**:
   - Đảm bảo các biến như `prompt`, `start_image`, `last_image`, `duration` được truyền từ Google Sheets vào node này.

3. **Node `Generate clip` (HTTP Request)**:
   - Chọn **HTTP Bearer Auth** và **HTTP Header Auth** (đã cấu hình API Key).
   - Điền **URL API** của Veo 3.1 (thường là `https://api.fal.ai/models/veo-3.1`).
   - Body JSON:
     ```json
     {
       "prompt": "${{ $json["prompt"] }}",
       "start_image": "${{ $json["start_image"] }}",
       "last_image": "${{ $json["last_image"] }}",
       "duration": ${{ $json["duration"] }}
     }
     ```

4. **Node `Merge Videos` (HTTP Request)**:
   - Chọn **HTTP Header Auth** (API Key fal.ai).
   - Điền **URL API** của FFmpeg (thường là `https://api.fal.ai/ffmpeg`).
   - Body JSON:
     ```json
     {
       "inputs": ${{ $json["video_urls"] }},
       "output": "merged.mp4"
     }
     ```

5. **Node `Upload to Youtube` (HTTP Request)**:
   - Chọn **HTTP Header Auth** (API Key Upload-Post).
   - Điền **URL API** của Upload-Post (thường là `https://api.upload-post.com/upload`).
   - Body JSON:
     ```json
     {
       "link": "${{ $json["final_video_url"] }}",
       "username": "YOUR_USERNAME",
       "title": "TITLE"
     }
     ```

6. **Node `Upload to Postiz` (Postiz)**:
   - Chọn **Postiz API Key** credentials.
   - Điền **Channel ID** và **Title** (ví dụ: `Selfie AI with [Tên Nghệ Sĩ]`).

##### **C. Cấu Hình Thời Gian Chờ (Wait)**
- Node `Wait 60 sec.` và `Wait 30 sec.`:
  - Thời gian chờ này giúp đảm bảo video được tạo và gộp hoàn chỉnh trước khi tiếp tục.
  - Các sếp có thể điều chỉnh thời gian này tùy thuộc vào tốc độ API (thường là 30-60 giây).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **Execute Workflow** và chọn **Test Run** với một dòng dữ liệu mẫu từ Google Sheets.
   - Kiểm tra các node quan trọng như `Generate clip`, `Merge Videos`, và `Upload to Youtube/Postiz` để đảm bảo không có lỗi.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Cập Nhật Google Sheets**:
   - Sử dụng **Google Apps Script** để tự động thêm dữ liệu mới vào Google Sheets khi có yêu cầu từ bên ngoài (ví dụ: qua form Google Form).

2. **Gửi Báo Cáo Định Kỳ**:
   - Thêm node **Email** (ví dụ: `n8n-nodes-base.email`) để gửi báo cáo kết quả video đã tạo mỗi ngày qua email.

3. **Kết Hợp Với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo trạng thái video khi hoàn thành.

4. **Lưu Log Kết Quả**:
   - Sử dụng node **Google Drive** để lưu log chi tiết của workflow (ví dụ: thời gian tạo, URL video, lỗi nếu có).

5. **Tối Ưu Hóa Prompt**:
   - Để video chất lượng cao, các sếp nên viết **prompt chi tiết** bao gồm:
     - Mô tả nhân vật (tuổi, tính cách, trang phục).
     - Cảnh quay (địa điểm, ánh sáng, cảm xúc).
     - Ví dụ: *"A selfie video of me with Taylor Swift at a concert, 25 years old, smiling, golden hour lighting, cinematic style."*

6. **Sử Dụng Mô Hình AI Khác**:
   - Nếu muốn thử nghiệm với các mô hình AI khác (ví dụ: Sora, Pika Labs), các sếp có thể thay thế node `Generate clip` bằng API của mô hình mới.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình tạo video selfie AI với các nhân vật nổi tiếng, tiết kiệm thời gian và tạo nội dung viral trên mạng xã hội. **Không cần code, không phụ thuộc vào nền tảng**, toàn bộ quá trình được tự động hóa trên n8n!

👉 **Bắt đầu ngay hôm nay**:
1. Chuẩn bị Google Sheets và API Key.
2. Import workflow và cấu hình credentials.
3. Nhấp **Execute Workflow** và xem video của mình ra đời!

**Nếu có bất kỳ câu hỏi nào, hãy để lại comment bên dưới hoặc liên hệ với tác giả Davide qua [LinkedIn](https://www.linkedin.com/in/davideboizza) hoặc email [info@n3w.it](mailto:info@n3w.it).**

🎬 **Chúc các sếp thành công với nội dung viral của mình!** 🚀