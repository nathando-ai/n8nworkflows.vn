---
title: "🎵 Tự Động Hóa Sáng Tạo Nhạc Độc Đáo Từ Chat AI: Gemini + Suno (Kie.ai) + Google Drive"
description: "Workflow này biến n8n thành một **công cụ sản xuất nhạc AI toàn diện**, cho phép các sếp tạo nhạc tùy chỉnh từ cuộc trò chuyện với AI, sau đó tự động tải lên Google Drive. Khắc phục hoàn toàn công việc thủ công, tiết kiệm thời gian lên đến 80% và mở ra vô số khả năng sáng tạo cho content marketing, podcast, hoặc dự án âm nhạc cá nhân."
slug: "tieu-dong-hoa-san-tao-nhac-tu-chat-ai-gemini-suno"
tags: [n8n, automation, ai-chatbot, content-creation, google-drive, kie-ai, suno, google-gemini]
keywords: [tự động hóa sáng tạo nhạc AI, workflow n8n tạo nhạc từ chat, gemini + suno + google drive, sản xuất nhạc tự động, chatbot sáng tạo âm nhạc, n8n no-code]
---

# 🎵 **Tự Động Hóa Sáng Tạo Nhạc Độc Đáo Từ Trò Chuyện AI: Từ Chat → Nhạc → Google Drive**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm ý tưởng nhạc** từ nhiều nguồn khác nhau (Google, Spotify, hoặc thậm chí là chat với bạn bè).
- **Viết lời bài hát** hoặc chỉnh sửa nhạc theo yêu cầu cụ thể (thể loại, cảm xúc, chủ đề).
- **Tải nhạc lên cloud** để chia sẻ với team hoặc khách hàng, nhưng lại phải làm thủ công, dễ bị lỗi hoặc mất thời gian.

**Workflow này giải quyết tất cả đó!** Với **AI Gemini + API Suno (Kie.ai)**, các sếp chỉ cần **gửi yêu cầu qua chat**, hệ thống sẽ tự động:
✅ **Tạo nhạc tùy chỉnh** theo yêu cầu (tựa đề, thể loại, nguồn lời, hoặc thậm chí là từ một đoạn văn bản).
✅ **Tải nhạc lên Google Drive** với tên file logic và sẵn sàng chia sẻ.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Nhạc 100% tùy chỉnh** theo yêu cầu cụ thể (ví dụ: nhạc cho podcast, jingle quảng cáo, hoặc nhạc nền video).
- **Tự động hóa hoàn toàn** từ sáng tạo đến lưu trữ, giảm thiểu lỗi và tăng hiệu suất.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Gemini API** (để sử dụng chatbot và tìm kiếm nhạc).
   - **Gemini Search API** (tìm kiếm nhạc hoặc nguồn lời).
   - **Bearer Token Kie.ai** (để tạo nhạc qua API Suno).
   - **Google Drive OAuth2** (để tải nhạc lên cloud).
2. **Dịch vụ**:
   - **n8n Self-hosted** (để chạy workflow 24/7).
   - **Kie.ai** (API tạo nhạc Suno).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Editor** trên dashboard.
2. Nhấn **Import Workflow** và chọn file JSON đã tải xuống từ [n8n.io/workflows/13542](https://n8n.io/workflows/13542).
   *Hoặc* copy toàn bộ JSON và paste vào **Import Workflow** → **Paste JSON**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **19 node** quan trọng, các sếp cần chú ý cấu hình sau:

#### **A. Cấu Hình API & Credentials**
| **Node**               | **Tham Số Cần Điền**               | **Lưu Ý**                                                                 |
|------------------------|------------------------------------|----------------------------------------------------------------------------|
| **Google Gemini Chat**  | `googlePalmApi` (credentials)      | Đăng ký API tại [Google AI Studio](https://makersuite.google.com/) và thêm vào n8n. |
| **Gemini Search**      | `geminiSearchApi` (credentials)    | Cung cấp API Key từ [Google Vertex AI](https://console.cloud.google.com/). |
| **Kie.ai (Suno API)**  | `httpBearerAuth` (Bearer Token)    | Lấy token từ [Kie.ai](https://kie.ai) và thêm vào n8n.                     |
| **Google Drive**       | `googleDriveOAuth2Api` (credentials)| Cấu hình OAuth2 cho Google Drive và chỉ định **folder mục tiêu**.          |

#### **B. Cấu Hình Node Quá Trình**
1. **`When chat message received` (chatTrigger)**
   - **Expose as Webhook**: Bật để nhận tin nhắn từ người dùng.
   - **Webhook URL**: Sử dụng URL của node **Wait** (sau này sẽ cấu hình callback cho Kie.ai).

2. **`Music Producer Agent` (agent)**
   - **Prompt**: Đảm bảo prompt đã được tối ưu hóa để thu thập thông tin như:
     - Tựa đề bài hát.
     - Thể loại (ví dụ: EDM, Pop, Jazz).
     - Nguồn lời (nếu có).
     - Các **negative tags** (những gì không muốn trong nhạc).

3. **`Create song` (httpRequest)**
   - **URL**: `https://kie.ai/api/v1/generate` (API của Kie.ai).
   - **Headers**: Thêm `Authorization: Bearer {token}`.
   - **Body**: JSON với tham số như:
     ```json
     {
       "styleWeight": 0.8,
       "weirdnessConstraint": 0.5,
       "vocal": "female",
       "text": "Lời bài hát từ người dùng"
     }
     ```

4. **`Upload song` (googleDrive)**
   - **Folder ID**: Chỉ định folder Google Drive muốn tải nhạc.
   - **File Name**: Sử dụng `{{ $node["Get response"].json["title"] }}.mp3` để tự động đặt tên.

#### **C. Cấu Hình Callback URL**
- Trong **Kie.ai Dashboard**, đi đến **Settings → Webhook Callback** và nhập **URL của node Wait** (node đầu tiên trong workflow).
- **Node Wait** phải có **HTTP Method = POST** và **Expose as Webhook = ON**.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một **tin nhắn mẫu** qua Webhook (ví dụ: `"Tạo một bài hát EDM về chủ đề 'mùa xuân' với lời từ đoạn văn này: 'Mùa xuân đến, cây cối non nảy...'"`).
   - Kiểm tra **Output** của node `Get response` để đảm bảo API trả về dữ liệu JSON hợp lệ.

2. **Bật Active Workflow**:
   - Nhấn **Active** trên tab workflow.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa Prompt cho Agent**:
   - Thêm các **constraint** cụ thể để AI trả về kết quả chính xác hơn (ví dụ: yêu cầu nhạc phải có **beat 128 BPM** hoặc **vocal female**).

2. **Lưu Log & Monitoring**:
   - Sử dụng **node StickyNote** để ghi chú lỗi hoặc kết quả.
   - Kết hợp với **Google Sheets** để lưu lịch sử tạo nhạc.

3. **Gửi Kết Quả qua Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau `Upload song` để thông báo khi nhạc đã tải lên Drive.

4. **Tạo Nhiều Bài Hát Tùy Chỉnh**:
   - Sử dụng **node `Split In Batches`** để tạo nhiều phiên bản nhạc từ một yêu cầu duy nhất.

---
## 📌 **Kết Luận**
Workflow này không chỉ **tự động hóa sáng tạo nhạc** mà còn **giải phóng thời gian** cho các sếp để tập trung vào nội dung chất lượng cao hơn. Từ **chat AI → nhạc tùy chỉnh → Google Drive**, tất cả đều được thực hiện **một cách hoàn toàn tự động**, không cần code!

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình API.
2. **Test với một yêu cầu nhạc mẫu**.
3. **Chia sẻ kết quả** với team hoặc khách hàng!

👉 **Xem video hướng dẫn chi tiết** từ tác giả Davide trên [YouTube @n3witalia](https://youtube.com/@n3witalia).

---