---
title: "🎙️ Tự Động Hóa Tóm Tắt Podcast Hàng Ngày - Giảm Thời Gian Làm Việc Gấp 10 Lần"
description: "Workflow tự động hóa lấy danh sách podcast top trên Taddy, tải audio, chuyển âm thanh thành văn bản, tóm tắt nội dung bằng AI (GPT-4o-mini), và gửi email tổng hợp hàng ngày. Giúp các sếp tiết kiệm 5-10 giờ/tuần cho công việc nghiên cứu thị trường hoặc content curation."
slug: "tieu-dong-hoa-tom-tat-podcast-hang-ngay"
tags: [n8n, automation, ai, marketing, content-curation]
keywords: [tự động hóa podcast, tóm tắt podcast bằng AI, workflow n8n podcast, tự động hóa content marketing, taddy api]
---

# 🚀 **Tự Động Hóa Tóm Tắt Podcast Hàng Ngày - Giúp Các Sếp Tiết Kiệm 5-10 Giờ/Tuần**

### **Nỗi Đau Của Các Sếp Trong Công Việc Nghiên Cứu Podcast**
Các sếp thường phải:
- **Tìm kiếm thủ công** danh sách podcast top hàng ngày từ nhiều nguồn (Apple Charts, Spotify, Taddy...).
- **Tải và nghe** từng tập podcast (thời gian trung bình 30-60 phút/tập).
- **Ghi chú hoặc tóm tắt** nội dung bằng tay (rất mất thời gian và dễ bỏ sót).
- **So sánh và lựa chọn** nội dung phù hợp cho chiến dịch marketing hoặc content strategy.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động lấy** danh sách podcast top theo thể loại (Tech, News, Arts...) từ Taddy API.
✅ **Tải và cắt** audio để phù hợp với AI.
✅ **Chuyển âm thanh thành văn bản** bằng Whisper (OpenAI).
✅ **Tóm tắt nội dung** bằng GPT-4o-mini (chất lượng cao, cá nhân hóa).
✅ **Gửi email tổng hợp** hàng ngày với liên kết và tóm tắt chi tiết.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** so với cách làm thủ công.
- **Nội dung chính xác và toàn diện** do AI tóm tắt từ âm thanh nguyên bản.
- **Cá nhân hóa thể loại** (Tech, News, Arts...) theo nhu cầu marketing.
- **Hoạt động tự động** hàng ngày, không cần can thiệp.
- **Dữ liệu sẵn sàng** để phân tích xu hướng thị trường hoặc content strategy.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Taddy API** (miễn phí):
   - Đăng ký tại [https://taddy.org/signup/developers](https://taddy.org/signup/developers).
   - Lấy **User ID** và **API Key** từ dashboard.
2. **Tài khoản Gmail** (để nhận email tổng hợp):
   - Cấu hình **OAuth 2.0 Credentials** theo hướng dẫn [Google Workspace](https://developers.google.com/workspace/guides/create-credentials).
   - Tải file `client_secret.json` và sử dụng trong node Gmail.
3. **API Key OpenAI** (để sử dụng Whisper và GPT-4o-mini):
   - Đăng ký tại [https://platform.openai.com/account/api-keys](https://platform.openai.com/account/api-keys).
4. **Email nhận kết quả** (điền vào node Gmail).
5. **Thể loại podcast** (ví dụ: `TECHNOLOGY`, `NEWS`, `ARTS`).
   - Danh sách thể loại đầy đủ tại [api.taddy.org](https://api.taddy.org).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/2433](https://n8n.io/workflows/2433) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/2433) và dán vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Node `TaddyTopDaily` (HTTP Request)**
- **Header Parameters:**
  - `X-USER-ID`: Điền **User ID** từ Taddy.
  - `X-API-KEY`: Điền **API Key** từ Taddy.
- **Method:** `GET`
- **URL:** `https://api.taddy.org/podcasts/top`

##### **B. Cấu Hình Node `Genre` (Set)**
- **Value:** Chọn thể loại podcast (ví dụ: `PODCASTSERIES_TECHNOLOGY`).
  - Danh sách thể loại đầy đủ:
    - `TECHNOLOGY` → `PODCASTSERIES_TECHNOLOGY`
    - `NEWS` → `PODCASTSERIES_NEWS`
    - `ARTS` → `PODCASTSERIES_ARTS`
    - `COMEDY` → `PODCASTSERIES_COMEDY`
    - `SPORTS` → `PODCASTSERIES_SPORTS`
    - `FICTION` → `PODCASTSERIES_FICTION`

##### **C. Cấu Hình Node `Gmail` (Send Email)**
- **Credentials:** Chọn `gmailOAuth2` (đã cấu hình trước).
- **To:** Điền email nhận kết quả.
- **Subject:** `Daily Podcast Summary - [Thể Loại]` (ví dụ: `Daily Podcast Summary - Technology`).
- **Body:** Sử dụng **HTML Template** từ node `HTML` (sẽ được tự động tạo).

##### **D. Cấu Hình Node `Whisper Transcribe Audio` (HTTP Request)**
- **URL:** `https://api.openai.com/v1/audio/transcriptions`
- **Headers:**
  - `Authorization: Bearer {openAiApi}`
  - `Content-Type: multipart/form-data`
- **Body:**
  ```json
  {
    "model": "whisper-1",
    "file": "<base64_encoded_audio>"
  }
  ```

##### **E. Cấu Hình Node `Summarize Podcast` (OpenAI)**
- **Model:** `gpt-4o-mini` (đã mặc định).
- **Prompt:** Sử dụng template mặc định (có thể tùy chỉnh):
  ```
  Tóm tắt nội dung podcast này trong 3 đoạn ngắn (mỗi đoạn < 100 từ), nhấn mạnh:
  - Điểm chính (main takeaway)
  - Thông tin mới nhất (latest updates)
  - Ý kiến của tác giả (author's perspective)
  ```

##### **F. Cấu Hình Node `Schedule` (Schedule Trigger)**
- **Time:** Đặt thời gian gửi email hàng ngày (ví dụ: `09:00 AM`).
- **Time Zone:** Chọn múi giờ phù hợp.

#### **3. Kích Hoạt ⚡️**
- **Test Run:**
  - Thay thế node `Schedule` bằng node `Test Workflow` (tạm thời).
  - Nhấn **Test Workflow** và kiểm tra email.
- **Bật Workflow:**
  - Sau khi kiểm tra thành công, xóa node `Test Workflow` và bật `Schedule`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs cho Debugging:**
   - Sử dụng node `StickyNote` để ghi lại trạng thái của từng podcast (ví dụ: "Đã tải", "Đã tóm tắt", "Gửi email").
2. **Kết Nối Slack/Telegram:**
   - Thêm node `Slack` hoặc `Telegram Bot` để thông báo khi workflow hoàn thành.
3. **Lưu Lịch Sử Podcast:**
   - Sử dụng node `Google Sheets` hoặc `Airtable` để lưu tất cả podcast đã tóm tắt (dễ dàng theo dõi xu hướng).
4. **Tùy Chỉnh Prompt AI:**
   - Cải thiện prompt trong node `Summarize Podcast` để phù hợp với mục đích cụ thể (ví dụ: marketing, nghiên cứu thị trường).
5. **Bộ Lọc Podcast:**
   - Thêm node `If` để chỉ lấy podcast mới (so sánh ngày phát hành với ngày trước đó).

---
### 📌 **Kết Luận**
Workflow **Daily Podcast Summary** là giải pháp **tự động hóa hoàn chỉnh** cho việc nghiên cứu podcast hàng ngày, giúp các sếp:
✔ **Tiết kiệm thời gian** (5-10 giờ/tuần).
✔ **Nắm bắt xu hướng thị trường** nhanh chóng.
✔ **Cung cấp nội dung chất lượng** cho content marketing.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Schedule** và bắt đầu nhận email tổng hợp hàng ngày!

---
**💡 Chia sẻ ý kiến:**
Các sếp có thể tùy chỉnh workflow này để phù hợp với nhu cầu riêng. Nếu cần hỗ trợ, hãy để lại comment dưới đây! 🚀