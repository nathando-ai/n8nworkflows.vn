---
title: "🚀 Tự Động Hóa Xếp Loại Video YouTube & Tóm Tắt Email Bằng GPT-4 (Không Cần Code)"
description: "Workflow tự động theo dõi video mới từ các kênh YouTube, phân loại video viral (>=1000 like) và tự động gửi tóm tắt tuần bằng GPT-4 qua email. Giúp các sếp tiết kiệm 10+ giờ/tuần theo dõi thị trường."
slug: "tuy-dong-hoa-xep-loai-video-youtube-va-tom-tat-email"
tags: [n8n, automation, youtube-api, gpt-4, gmail, no-code, openai]
keywords: [n8n workflow youtube, tự động hóa video viral, gpt-4 tóm tắt email, phân loại video youtube, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Xếp Loại Video YouTube & Tóm Tắt Email Bằng GPT-4 (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
- **Thời gian rắc rối**: Phải thủ công theo dõi hàng chục kênh YouTube, đọc video mới, phân loại và tóm tắt nội dung.
- **Thiếu hiệu quả**: Nhiều video viral bị bỏ qua vì không theo dõi kịp thời, hoặc tóm tắt không khách quan.
- **Khó tự động hóa**: Cần code hoặc công cụ chuyên dụng để phân loại video và gửi báo cáo định kỳ.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ Theo dõi video mới từ nhiều kênh YouTube.
✅ Phân loại video viral (>=1000 like) và thông thường.
✅ Tóm tắt video bằng GPT-4 với **tone khác biệt** (urgent cho viral, chuyên nghiệp cho thông thường).
✅ Gửi **báo cáo tuần hoàn** qua email với định dạng HTML đẹp mắt.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần**: Không phải thủ công theo dõi video mới.
- **Phân loại chính xác**: Video viral (>=1000 like) được nhắc nhở ưu tiên.
- **Tóm tắt chuyên nghiệp**: GPT-4 tự động viết tóm tắt với **tone khác biệt** cho từng loại video.
- **Báo cáo tuần hoàn**: Email định kỳ với **định dạng HTML đẹp**, dễ chia sẻ trong team.
- **Kết nối đa nền tảng**: Hoạt động với Gmail, YouTube API, và OpenAI (GPT-4).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản YouTube API**:
   - [Mở khóa YouTube Data API v3](https://developers.google.com/youtube/v3/getting-started) và tạo **API Key**.
   - **Không hardcode API Key** vào workflow! Sử dụng **credential "YouTube_API_Key"** trong n8n.

✔ **Tài khoản Gmail (OAuth)**:
   - Cấu hình **Gmail OAuth** trong n8n để gửi email tự động.
   - **Không dùng mật khẩu thường**: Sử dụng **App Password** nếu kích hoạt 2FA.

✔ **Tài khoản OpenAI (GPT-4)**:
   - Tạo **API Key** tại [OpenAI Platform](https://platform.openai.com/account/api-keys).
   - Sử dụng **credential "OpenAiApi"** trong workflow.

✔ **Danh sách Channel IDs**:
   - Lấy **Channel ID** từ URL kênh (ví dụ: `UCx...` trong `https://www.youtube.com/@ChannelName`).
   - Điền vào **node "Set Channel IDs"** trong workflow.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9616](https://n8n.io/workflows/9616).
- Trong **n8n Editor**, chọn **Import Workflow** và chọn file JSON.
- **Hoặc copy/paste** JSON vào **Import Workflow** (tab bên phải).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Channel IDs**
- Mở **node "Set Channel IDs"** → Điền **Channel ID** vào trường `ChannelID`.
  - Ví dụ: `UCx...` (lấy từ URL kênh).
  - Nếu muốn theo dõi nhiều kênh, thêm vào dưới dạng mảng JSON:
    ```json
    [
      "UCx123...",
      "UCx456..."
    ]
    ```

##### **B. Cấu Hình YouTube API Key**
- **Không hardcode API Key!** Sử dụng **credential "YouTube_API_Key"**:
  1. Trong **n8n Credentials**, tạo mới **HTTP Query Auth**.
  2. Đặt tên: `YouTube_API_Key`.
  3. Điền **API Key** vào trường `apiKey`.
  4. Trong **node "Get Video Stats"**, chọn credential này.

##### **C. Cấu Hình Gmail OAuth**
- Trong **n8n Credentials**, tạo mới **Gmail OAuth2**:
  1. Đăng nhập tài khoản Gmail.
  2. Chọn **Tài khoản muốn gửi email**.
  3. Trong **node "Send Weekly Briefing"**, chọn credential `gmailOAuth2`.

##### **D. Cấu Hình OpenAI (GPT-4)**
- Trong **n8n Credentials**, tạo mới **OpenAI API**:
  1. Đặt tên: `OpenAiApi`.
  2. Điền **API Key** từ OpenAI.
  3. Trong **node "Write Post (Normal)"**, **"Write Post (Viral)"**, **"Generate Weekly Briefing"**, chọn credential này.

##### **E. Threshold Phân Loại Video Viral**
- Mặc định, video **>=1000 like** được xếp vào **viral**.
- Để thay đổi ngưỡng, mở **node "Classify by Likes (Code)"** và chỉnh giá trị `THRESHOLD` trong code:
  ```javascript
  const THRESHOLD = 1000; // Thay đổi giá trị này
  ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **node "Manual Run"** → Nhấn **Execute**.
   - Kiểm tra **log** để đảm bảo workflow hoạt động.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Kênh YouTube Mới**:
   - Mở **node "Set Channel IDs"** → Thêm Channel ID mới vào mảng JSON.

2. **Tùy Chỉnh Tone Tóm Tắt**:
   - Mở **node "Write Post (Normal)"** và **"Write Post (Viral)"** → Chỉnh **prompt** trong OpenAI để thay đổi tone:
     - Ví dụ: Thêm `Tone: Formal` cho video thông thường, `Tone: Urgent` cho viral.

3. **Lưu Log & Monitoring**:
   - Sử dụng **node "StickyNote"** để ghi chú lỗi hoặc kết quả.
   - Kết nối với **Prometheus/Grafana** (nếu self-host) để theo dõi workflow.

4. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node "Set"** để đặt lịch **cron job** (ví dụ: `0 0 * * 0` để gửi mỗi Chủ Nhật).

5. **Kết Nối Slack/Telegram**:
   - Thêm **node "Webhook"** để gửi thông báo khi có video viral mới.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì công việc thủ công. Với **GPT-4**, video được tóm tắt **chuyên nghiệp**, và **báo cáo tuần hoàn** giúp team theo dõi thị trường một cách **liên tục và chính xác**.

**Bắt đầu ngay!**
1. Import workflow.
2. Cấu hình Channel IDs và API Keys.
3. **Test Run** và bật Active.
4. **Xem email tóm tắt tuần đầu tiên** của mình!

👉 [Tải workflow nguyên bản](https://n8n.io/workflows/9616) và **cài đặt VPS** để chạy 24/7!