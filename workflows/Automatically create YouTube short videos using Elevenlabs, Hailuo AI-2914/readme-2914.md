---
title: "🎥 Tự Động Hoá Sáng Tạo Video Shorts YouTube Với ElevenLabs & Hailuo AI - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn chuyển văn bản thành video Shorts YouTube với giọng nói AI tự nhiên (ElevenLabs) và hiệu ứng video chuyên nghiệp (Hailuo AI), tiết kiệm 80% thời gian so với làm thủ công."
slug: "tieu-dong-hoa-tao-video-shorts-you-tube"
tags: [n8n, automation, ai-marketing, elevenlabs, hailuo-ai, youtube-automation]
keywords: [tự động hóa video shorts youtube, elevenlabs n8n, tạo video ai tự động, workflow youtube automation, tự động hóa marketing ai]
---

# 🚀 **Tự Động Hoá Sáng Tạo Video Shorts YouTube Với AI - Không Cần Code**

### **Giải pháp hoàn toàn tự động hóa từ văn bản đến video Shorts YouTube**
Các sếp đã bao giờ phải mất **3-5 tiếng** để chuyển một bài viết blog hay một đoạn văn bản thành video Shorts YouTube? Hay phải **đợi đợi** giọng nói AI tạo ra âm thanh không tự nhiên? Hoặc **chỉnh sửa video** để phù hợp với định dạng Shorts? **Workflow này sẽ giải quyết tất cả những vấn đề đó trong vòng 10 phút!**

Với công nghệ **ElevenLabs** (giọng nói AI siêu tự nhiên) và **Hailuo AI** (tạo video từ văn bản), workflow này sẽ tự động:
✅ **Chuyển văn bản → giọng nói AI** (không bị lặp lại, tự nhiên như người)
✅ **Tạo video từ văn bản** (hiệu ứng động, text overlay, background chuyên nghiệp)
✅ **Tích hợp captions tự động** (phù hợp với người dùng không nghe được)
✅ **Lưu tất cả tài nguyên** (audio, video, hình ảnh) lên **Google Cloud Storage**
✅ **Ghi lại lịch sử** trên **Google Sheets** để theo dõi và phân tích

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với làm thủ công (không cần cắt video, thêm hiệu ứng, hoặc tìm giọng nói AI).
- **Chất lượng video chuyên nghiệp** (hiệu ứng động, text overlay, âm thanh tự nhiên).
- **Hoạt động 24/7** (không cần can thiệp người dùng, chỉ cần kích hoạt workflow).
- **Dữ liệu theo dõi chi tiết** (tất cả video được lưu trên Google Sheets và Cloud Storage).
- **Cá nhân hóa hoàn toàn** (thay đổi prompt, giọng nói, hoặc hiệu ứng video theo nhu cầu).
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản ElevenLabs** (để tạo giọng nói AI):
   - [Đăng ký ElevenLabs](https://elevenlabs.io/) (mã giảm giá: **ELEVENLABS** - giảm 20%).
   - **API Key** của ElevenLabs (cần cấp phép cho API).
2. **Tài khoản Hailuo AI** (để tạo video từ văn bản):
   - [Đăng ký Hailuo AI](https://www.hailuoai.com/) (mã giảm giá: **HAILOU** - giảm 15%).
   - **API Key** của Hailuo AI.
3. **Tài khoản Google Cloud Storage** (để lưu audio, video, hình ảnh):
   - [Tạo tài khoản Google Cloud](https://cloud.google.com/) (miễn phí 300$ đầu tiên).
   - **Service Account JSON Key** (cấp quyền `Storage Admin`).
4. **Tài khoản Google Sheets** (để lưu lịch sử video):
   - [Tạo Google Sheets](https://sheets.google.com/) (nếu chưa có).
   - **Sheet Name** (ví dụ: `YouTube_Shorts_Logs`).
5. **Tài khoản YouTube** (để upload video sau khi hoàn tất).
6. **Văn bản nguồn** (có thể lấy từ blog, bài viết, hoặc file Excel trên Google Sheets).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/2914) (nút "Export").
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy JSON** từ file → Paste vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không cần chỉnh sửa workflow** nếu đã import đúng file.
- **Kích hoạt chế độ "Active"** sau khi import.
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **3 phần quan trọng** cần cấu hình cẩn thận:

##### **A. Cấu hình API Keys**
- **ElevenLabs**:
  - Node: **"Fetch Elevenlabs"**, **"Download Audio"**
  - Điền **API Key** vào trường `Authorization` (dạng `Bearer YOUR_API_KEY`).
- **Hailuo AI**:
  - Node: **"Hailuo AI"**, **"Get Hailuo Download Link"**, **"Get Hailuo Status"**
  - Điền **API Key** vào trường `Authorization` (dạng `Bearer YOUR_API_KEY`).
- **Google Cloud Storage**:
  - Node: **"Save Audio"**, **"Save Image"**, **"Save Video"**
  - Chọn **Service Account JSON Key** trong `Credentials`.
  - Điền **Bucket Name** (ví dụ: `youtube-shorts-media`).

##### **B. Cấu hình Google Sheets**
- Node: **"Google Sheets"**
  - Chọn **Sheet Name** (ví dụ: `YouTube_Shorts_Logs`).
  - Chọn **Range** (ví dụ: `A1:D100`).
  - **Cột cần điền**:
    - `Video Title` (tiêu đề video).
    - `Video URL` (link video sau khi tạo).
    - `Audio URL` (link audio ElevenLabs).
    - `Image URL` (link hình ảnh tạo bởi Hailuo AI).

##### **C. Cấu hình Input (Văn bản nguồn)**
- Node: **"Manual Trigger"** (nút "Test workflow")
  - **Input JSON** (ví dụ):
    ```json
    {
      "text": "Chào mọi người! Đây là video Shorts tự động tạo bằng n8n và AI. Hôm nay tôi sẽ giới thiệu cách tự động hóa marketing với AI.",
      "video_category": "Marketing",
      "output_format": "mp4"
    }
    ```
  - **Lưu ý**:
    - `text` là nội dung văn bản cần chuyển thành video.
    - `video_category` là danh mục video (ví dụ: `Marketing`, `Tech`, `Education`).
    - `output_format` là định dạng video (cần phù hợp với Hailuo AI).

##### **D. Cấu hình Wait Nodes**
- Node: **"Wait Hailuo done process"**, **"Wait1 andynocode combine video"**
  - Thời gian chờ mặc định là **30 giây** (có thể điều chỉnh nếu Hailuo AI xử lý chậm).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Test workflow"** và điền input JSON như trên.
   - Kiểm tra các node quan trọng:
     - **"Hailuo AI"** → **"Get Hailuo Download Link"** (video có được tạo không?).
     - **"ElevenLabs"** → **"Download Audio"** (audio có được tải xuống không?).
     - **"Create Video"** → **"Get Video Progress"** (video có được kết hợp không?).
2. **Bật Active workflow** sau khi kiểm tra thành công.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM NÂNG CAO]
1. **Tích hợp Slack/Telegram để báo cáo kết quả**
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **"Set Final Video URL"** để thông báo khi video hoàn tất.
   - Ví dụ:
     ```json
     {
       "text": `🎉 Video "${data.video_title}" đã hoàn tất!\n🔗 Link: ${data.final_video_url}`
     }
     ```
2. **Lưu log chi tiết vào Google Sheets**
   - Thêm node **Google Sheets** sau node **"Set Final Video URL"** để ghi thêm thông tin như:
     - Thời gian tạo video.
     - Thời gian xử lý của Hailuo AI.
     - Trạng thái thành công/thất bại.
3. **Tự động upload lên YouTube**
   - Thêm node **YouTube API** sau node **"Set Final Video URL"** để tự động upload video.
   - Cần cấu hình:
     - **YouTube API Key**.
     - **Channel ID**.
     - **Tiêu đề, mô tả, thẻ** tự động từ input.
4. **Tạo nhiều video từ một file Excel**
   - Sử dụng node **Google Sheets** để lấy dữ liệu từ nhiều hàng (ví dụ: cột `A` là tiêu đề, cột `B` là nội dung).
   - Thêm node **SplitOut** để xử lý từng hàng riêng biệt.
5. **Tối ưu hóa prompt cho Hailuo AI**
   - Nếu video tạo ra không phù hợp, thử thay đổi prompt trong node **"Hailuo AI"**:
     ```json
     {
       "prompt": "Chỉnh sửa video này thành phong cách hiện đại, với text overlay đậm màu đỏ, hiệu ứng zoom-in khi nói về phần quan trọng, và nền động cho phần giới thiệu.",
       "style": "cinematic"
     }
     ```
6. **Sử dụng ElevenLabs Voice Cloning**
   - Nếu muốn giọng nói giống một người cụ thể, kích hoạt **Voice Cloning** trong ElevenLabs và cập nhật API Key mới.
---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình tạo video Shorts YouTube** mà không cần kỹ năng code. Với **ElevenLabs** và **Hailuo AI**, video của các sếp sẽ **chuyên nghiệp, tự nhiên, và thu hút người xem** hơn bao giờ hết.

**Bắt đầu ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình API Keys.
3. **Test Run** với dữ liệu mẫu.
4. **Bật Active** và để AI làm việc cho các sếp!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và phản hồi!** Nếu các sếp có bất kỳ câu hỏi hoặc cần hỗ trợ, hãy để lại comment bên dưới. Chúc các sếp thành công với chiến dịch marketing AI! 🚀