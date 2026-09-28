---
title: "🎬 Tự Động Hóa Sáng Tạo Video Viral Từ Hình Ảnh Tham Khảo Với Fal.ai VIDU + Upload Trực Tiếp TikTok & YouTube"
description: "Workflow tự động hóa 100% không code chuyển đổi **bộ ảnh tham khảo** thành video AI hấp dẫn, sau đó tự động upload lên TikTok và YouTube. Giúp các sếp tiết kiệm **10+ giờ/tháng** trong content creation mà không cần kỹ năng thiết kế hoặc video editing."
slug: "tieu-dong-hoa-tao-video-viral-tu-hinh-anh-tham-khao"
tags: [n8n, automation, content-creation, ai-multimodal, tiktok-youtube, fal-ai, openai, google-drive]
keywords: [n8n workflow tự động hóa video, tạo video từ ảnh tham khảo, Fal.ai VIDU, upload video TikTok YouTube tự động, AI content creation không code]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video Viral Từ Hình Ảnh Tham Khảo + Upload TikTok & YouTube**

### **Giải pháp cho các sếp:**
Bạn đã bao giờ **mệt mỏi** khi phải:
❌ Tốn **giờ đồng hồ** để chỉnh sửa video từ nhiều ảnh tham khảo?
❌ Lo lắng video không **hấp dẫn** như mong đợi?
❌ Phải **tìm kiếm công cụ** để upload video lên TikTok và YouTube một cách tự động?
❌ **Không có kỹ năng** thiết kế hoặc video editing?

**Workflow này giúp bạn:**
✅ **Tạo video AI từ 1-7 ảnh tham khảo** chỉ trong **vài giây** (không cần skill thiết kế).
✅ **Tự động upload** video lên **TikTok và YouTube** (miễn phí hoặc trả phí).
✅ **Tiết kiệm 10+ giờ/tháng** cho việc content creation.
✅ **Cập nhật tự động** khi có hình ảnh mới (không cần can thiệp thủ công).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo video từ ảnh tham khảo **tự động**, không cần chỉnh sửa thủ công.
- **Chất lượng cao**: Video AI **mượt mà, chuyên nghiệp** với hiệu ứng chuyển cảnh tự động.
- **Upload tự động**: Video được **tải lên TikTok và YouTube** ngay sau khi tạo.
- **Dễ dàng mở rộng**: Kết hợp với **Slack/Telegram** để thông báo khi video hoàn thành.
- **Hoạt động liên tục**: Workflow chạy **24/7** trên VPS, không phụ thuộc vào máy tính cá nhân.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Fal.ai** (để tạo video từ ảnh tham khảo):
   - [Đăng ký tại đây](https://fal.ai/) và lấy **API Key**.
   - **Lưu ý**: API Key này sẽ được sử dụng trong node **"Create Video"**.

2. **Tài khoản Upload-Post** (để upload video lên TikTok và YouTube):
   - [Đăng ký tại đây](https://www.upload-post.com/) và lấy **API Key**.
   - **Lưu ý**:
     - **Miễn phí**: 10 upload/tháng (không bao gồm TikTok).
     - **Nâng cấp plan trả phí** để sử dụng TikTok (từ **$9.99/tháng**).

3. **Tài khoản Google Drive** (để lưu video tạm thời):
   - Cài đặt **OAuth 2.0** trong n8n để workflow có quyền truy cập.

4. **Tài khoản OpenAI** (để tạo tiêu đề video AI):
   - [Đăng ký tại đây](https://platform.openai.com/) và lấy **API Key**.

5. **Mô hình hình ảnh tham khảo**:
   - Các sếp cần **7 ảnh tham khảo tối đa** (được chia sẻ qua URL hoặc upload trực tiếp).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/8709) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8709) và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **13 node** chính, các sếp cần cấu hình **cẩn thận** các node sau:

##### **A. Cấu hình API Key**
- **Node "Get status"**, **"Create Video"**, **"Get Url Video"**, **"Upload on TikTok"**, **"Upload to Youtube"**:
  - **Credentials**: Chọn **"httpHeaderAuth"**.
  - **Header Auth**:
    - **Name**: `Authorization`
    - **Value**: `Key YOUR_FAL_AI_API_KEY` (đối với Fal.ai) hoặc `Apikey YOUR_UPLOAD_POST_API_KEY` (đối với Upload-Post).

- **Node "Generate title"**:
  - **Credentials**: Chọn **"openAiApi"**.
  - **API Key**: Điền **API Key OpenAI** của các sếp.

- **Node "Upload Video"**:
  - **Credentials**: Chọn **"googleDriveOAuth2Api"**.
  - **Cấu hình OAuth 2.0** trong n8n để workflow có quyền truy cập Google Drive.

##### **B. Cấu hình Form Trigger (Bắt đầu workflow)**
- **Node "On form submission"**:
  - Các sếp cần **cấu hình form** để người dùng có thể:
    - **Nhập prompt** (ví dụ: *"The girl is showing a pair of shoes to the monkey in the forest"*).
    - **Chọn ảnh tham khảo** (7 ảnh tối đa, chia sẻ qua URL hoặc upload).
  - **Lưu ý**: Workflow sẽ **chạy tự động** khi form được submit.

##### **C. Cấu hình Wait & Check Status**
- **Node "Wait 60 sec."**: Đảm bảo video được tạo hoàn toàn trước khi upload.
- **Node "Completed?" (If node)**: Kiểm tra trạng thái video trước khi upload.

##### **D. Cấu hình Upload Video**
- **Node "Upload Video" (Google Drive)**:
  - Chọn **folder** trong Google Drive để lưu video tạm thời.
- **Node "Upload on TikTok" & "Upload to Youtube"**:
  - Điền **YOUR_USERNAME** (tên profile TikTok/YouTube) vào **Auth Header**.

##### **E. Cấu hình OpenAI (Tạo tiêu đề)**
- **Node "Generate title"**:
  - **Model**: Chọn **gpt-3.5-turbo** (mặc định).
  - **Prompt**: Sử dụng mẫu:
    ```
    Generate a catchy title for a viral video based on the following prompt and images:
    Prompt: [USER_INPUT_PROMPT]
    Images: [USER_INPUT_IMAGES]
    Title must be under 60 characters for TikTok and under 100 for YouTube.
    ```

#### **3. Kích hoạt ⚡️**
- **Test run** với **dữ liệu mẫu**:
  - Nhập **prompt** và **7 ảnh tham khảo** vào form.
  - Chạy workflow và kiểm tra:
    - Video có được tạo không?
    - Video có upload lên TikTok/YouTube không?
    - Tiêu đề có được sinh ra không?
- **Bật Active workflow** khi test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để **thông báo** khi video hoàn thành.
   - Ví dụ: *"Video đã tạo thành công! Link: [LINK]"*.

2. **Lưu log video**:
   - Thêm node **Google Sheets** để **ghi lại lịch sử** video đã tạo (tiêu đề, link, ngày upload).

3. **Chạy định kỳ**:
   - Sử dụng **Schedule Trigger** để chạy workflow **tự động** mỗi **5 phút** (để cập nhật video mới).

4. **Tối ưu API Key**:
   - Nếu sử dụng **Fal.ai**, các sếp có thể **cài đặt rate limit** để tránh bị chặn.

5. **Tạo video từ video cũ**:
   - Nếu muốn **chỉnh sửa video cũ**, các sếp có thể **upload video lên Google Drive** và sử dụng **node "Set data"** để truyền vào workflow.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tạo video viral từ ảnh tham khảo một cách tự động**, sau đó **upload lên TikTok và YouTube** mà không cần kỹ năng thiết kế. **Chỉ cần 3 bước**:
1. **Chuẩn bị API Key** (Fal.ai, Upload-Post, OpenAI).
2. **Import và cấu hình workflow**.
3. **Chạy và xem video được tạo tự động!**

**🚀 Hãy áp dụng ngay và tiết kiệm **10+ giờ/tháng** cho công việc content creation!**

---
**💬 Cần hỗ trợ?** Liên hệ tác giả Davide qua:
- Email: [info@n3w.it](mailto:info@n3w.it)
- LinkedIn: [@davideboizza](https://www.linkedin.com/in/davideboizza/)