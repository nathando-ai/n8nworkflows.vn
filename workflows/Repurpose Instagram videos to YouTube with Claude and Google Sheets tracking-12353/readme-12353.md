---
title: "🚀 Tự Động Hóa Chuyển Đổi Video Instagram Sang YouTube Với AI Claude + Theo Dõi Google Sheets"
description: "Workflow tự động hóa hoàn toàn chuyển đổi video từ Instagram sang YouTube với AI Claude tạo metadata thông minh, đồng thời theo dõi hiệu suất và gửi thông báo tự động qua WhatsApp. Giúp các sếp tiết kiệm 2-3 giờ/ngày và duy trì lịch trình đăng bài nhất quán."
slug: "tieu-dong-hoa-chuyen-doi-video-instagram-sang-youtube"
tags: [n8n, automation, ai, youtube, instagram, google-sheets, ai-chatbot, no-code]
keywords: [tự động hóa n8n, chuyển đổi video instagram youtube, ai claude, google sheets theo dõi, tự động hóa content marketing, workflow ai]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Video Instagram → YouTube Với AI Claude + Theo Dõi Google Sheets**

### **Nỗi Đau Của Các Sếp Trong Content Marketing**
Các sếp quản lý nội dung, nhà marketing hay các công ty media thường phải mất **2-3 giờ/ngày** để:
- **Tải video từ Instagram** sang YouTube thủ công
- **Tạo tiêu đề, mô tả, thẻ** phù hợp cho YouTube (mà vẫn giữ được tính sáng tạo)
- **Theo dõi hiệu suất** của video trên YouTube (views, like, engagement)
- **Gửi thông báo** khi video đã được đăng thành công

Kết quả? **Tốn thời gian, dễ sai sót, và không tối ưu hóa nội dung** cho từng nền tảng. **Workflow này giải quyết tất cả!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 2-3 giờ/ngày** – Không cần tải video thủ công
✅ **Metadata thông minh** – AI Claude tự động tạo **tiêu đề, mô tả, thẻ** tối ưu cho YouTube
✅ **Theo dõi hiệu suất** – Dữ liệu video được ghi vào **Google Sheets** (views, like, thời gian xem)
✅ **Thông báo tự động** – Khi video được đăng thành công, hệ thống sẽ **gửi tin nhắn WhatsApp**
✅ **Lịch trình đăng bài nhất quán** – Workflow chạy theo **schedule**, không phụ thuộc vào thời gian làm việc
✅ **AI kép tăng cường** – Sử dụng **Claude Sonnet 4.5** (Anthropic) để tối ưu hóa nội dung
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
📌 **Tài khoản Instagram Business/Creator** (có API access)
📌 **API Key của Anthropic** (để sử dụng AI Claude)
📌 **Tài khoản YouTube** (để upload video)
📌 **Google Sheets** (để lưu log hiệu suất video)
📌 **WhatsApp Business API** (để gửi thông báo tự động)

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12353](https://n8n.io/workflows/12353) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Lưu workflow** với tên **"Instagram → YouTube Auto-Upload"** (hoặc tên phù hợp).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **14 node**, các sếp cần **cấu hình kỹ** các phần sau:

##### **🔹 Node "Get Instagram Media" (HTTP Request)**
- **URL**: Sử dụng **Instagram Graph API** để lấy video từ tài khoản.
  - Ví dụ: `https://graph.instagram.com/[USER_ID]/media?fields=id,caption,media_type,media_url&access_token=[ACCESS_TOKEN]`
- **Headers**:
  - `Authorization: Bearer [YOUR_INSTAGRAM_ACCESS_TOKEN]`
  - `Content-Type: application/json`

##### **🔹 Node "Download Instagram Video" (HTTP Request)**
- **URL**: Lấy đường link video từ Instagram (đã được lấy ở node trước).
- **Headers**:
  - `Authorization: Bearer [YOUR_INSTAGRAM_ACCESS_TOKEN]`

##### **🔹 Node "Anthropic Chat Model" (AI Claude)**
- **API Key**: Điền vào **credentials "anthropicApi"** trong n8n.
- **Prompt mẫu** (có thể chỉnh sửa):
  ```
  Tôi có một video từ Instagram với tiêu đề: "[TITLE]". Hãy tạo một mô tả YouTube tối ưu hóa SEO với:
  - Từ khóa chính: "[KEYWORD]"
  - Cách gọi người xem: "Hãy like và subscribe nếu bạn thích nội dung này!"
  - Thêm 3 thẻ liên quan: [TAG1], [TAG2], [TAG3]
  ```
- **Model**: Chọn **"claude-sonnet-4-5-20250929"** (đã được cài sẵn).

##### **🔹 Node "Upload to YouTube"**
- **Credentials**: Chọn **YouTube OAuth2** (cấu hình trước trong n8n).
- **File video**: Lấy từ node **"Download Instagram Video"**.
- **Metadata**: Sử dụng kết quả từ AI Claude (tiêu đề, mô tả, thẻ).

##### **🔹 Node "Log to Google Sheets"**
- **Credentials**: Chọn **"googleSheetsOAuth2Api"**.
- **Sheet Name**: Điền tên sheet (ví dụ: **"YouTube Video Log"**).
- **Range**: `A1` (để ghi dữ liệu từ dòng 1).
- **Dữ liệu ghi**: Lấy từ node **"Upload to YouTube"** (ID video, tiêu đề, lượt xem, thời gian đăng).

##### **🔹 Node "Send WhatsApp Notification"**
- **Credentials**: Chọn **"whatsAppApi"**.
- **Message mẫu**:
  ```
  🚀 Video mới đã được đăng lên YouTube thành công!
  - Tiêu đề: [TITLE]
  - Link: [YOUTUBE_URL]
  - Thời gian đăng: [TIMESTAMP]
  ```

##### **🔹 Node "Schedule Trigger"**
- **Cài đặt lịch**: Chọn **thời gian và tần suất** (ví dụ: **mỗi ngày 8h sáng**).
- **Time Zone**: Chọn **múi giờ phù hợp** (Việt Nam: `Asia/Ho_Chi_Minh`).

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy thử với **1 video mẫu** để kiểm tra:
  - Video có được tải xuống từ Instagram không?
  - AI Claude có tạo metadata không?
  - Video có được upload lên YouTube không?
  - Dữ liệu có được ghi vào Google Sheets không?
  - Thông báo WhatsApp có được gửi không?
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa AI Prompt**:
   - Thay đổi **tone của mô tả** theo brand (ví dụ: chuyên nghiệp, thân thiện, hài hước).
   - Thêm **các từ khóa SEO** cụ thể cho ngành nghề của các sếp.

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** để gửi thông báo khi video được đăng thành công.

3. **Lưu Log Chi Tiết**:
   - Sử dụng **Google Sheets** để lưu **tất cả log** (thành công/thất bại) và **thống kê hiệu suất**.

4. **Tự động Chỉnh Sửa Video**:
   - Sử dụng **FFmpeg** (hoặc node **FFmpeg** trong n8n) để **cắt video** trước khi upload.

5. **Báo Cáo Hiệu Suất Định Kỳ**:
   - Sử dụng **Google Apps Script** hoặc **n8n + Email Node** để gửi **báo cáo tuần/month** về hiệu suất video.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì công việc lặp lại. Với **AI Claude tạo metadata thông minh**, **upload tự động**, và **theo dõi hiệu suất**, các sếp có thể:
✔ **Tăng engagement** trên YouTube
✔ **Tiết kiệm thời gian** lên đến 300% so với cách làm thủ công
✔ **Duy trì lịch trình đăng bài** một cách nhất quán

**🚀 Hãy áp dụng ngay và tự động hóa content marketing của mình!**
Nếu có vấn đề, liên hệ với **Dr. Cheng Siong CHIN** qua [mcschin1@yahoo.com](mailto:mcschin1@yahoo.com) để hỗ trợ tối ưu hóa workflow.

---
**💡 Lưu ý cuối cùng**: Nếu các sếp muốn **cải tiến thêm**, có thể thêm **node AI khác** (ví dụ: **MidJourney** để tạo thumbnail) hoặc **kết hợp với TikTok/Reels** để tối ưu hóa cross-platform.