---
title: "🎬 Tự Động Hoàn Thành Video Podcast Thơ Nhịp Cho Bé Với AI - Từ Văn Bản Đến Video Chỉ Với 1 Clic!"
description: "Workflow này tự động chuyển đổi nội dung podcast về chủ đề thơ nhịp cho bé thành video động hình hoàn chỉnh, kết hợp AI tạo hình (DALL·E), giọng nói tự nhiên (ElevenLabs) và công cụ video (Hedra). Giúp các sếp tiết kiệm 10+ giờ công sức mỗi tháng, đồng thời tạo ra nội dung cá nhân hóa cho khán giả trẻ."
slug: "tieu-dong-hoan-thanh-video-podcast-tho-nhip-cho-be"
tags: [n8n, automation, ai, podcast, video-creation, dall-e, elevenlabs, hedra, no-code]
keywords: [tự động hóa video podcast cho bé, tạo video động hình với AI, n8n workflow podcast, tự động hóa nội dung giáo dục, công cụ tạo video từ văn bản, hedra n8n, dall-e elevenlabs n8n]
---

# 🎬 **Tự Động Hoàn Thành Video Podcast Thơ Nhịp Cho Bé - Từ Văn Bản Đến Video Chỉ Với 1 Clic!**

### **Nỗi Đau Của Các Sếp Trong Ngành Giáo Dục & Podcast**
Các sếp trong lĩnh vực giáo dục, podcast cho trẻ em hay các nhà sản xuất nội dung thường gặp phải những thách thức sau:
- **Tốn thời gian**: Viết kịch bản, tìm hình ảnh phù hợp, thu âm giọng nói và chỉnh sửa video là quá trình tốn nhiều giờ công sức.
- **Khó tìm hình ảnh phù hợp**: Các hình ảnh về thơ nhịp cho bé thường đòi hỏi sự sáng tạo cao, khó tìm được nguồn chất lượng cao.
- **Giọng nói không tự nhiên**: Giọng đọc podcast thường nghe máy móc, không thu hút trẻ em.
- **Chỉnh sửa video phức tạp**: Hoàn thiện video từ các tài nguyên rời rạc (ảnh + âm thanh) đòi hỏi kỹ năng chỉnh sửa chuyên nghiệp.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình từ **tạo kịch bản, sinh hình ảnh, tạo giọng nói tự nhiên đến biên tập video** chỉ với một cú nhấp chuột!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công sức mỗi tháng**: Không cần viết kịch bản, tìm hình ảnh hoặc chỉnh sửa video thủ công.
- **Video động hình chuyên nghiệp**: Hình ảnh sinh ra từ DALL·E và video biên tập bởi Hedra mang chất lượng cao.
- **Giọng nói tự nhiên**: ElevenLabs tạo giọng đọc podcast với âm thanh sống động, thu hút trẻ em.
- **Cá nhân hóa nội dung**: Thay đổi kịch bản hoặc chủ đề chỉ cần cập nhật input, workflow tự động xử lý.
- **Hoạt động 24/7**: Workflow có thể chạy tự động khi có dữ liệu mới, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - [OpenAI](https://platform.openai.com/) (DALL·E và GPT-3.5/4 cho tạo hình ảnh và kịch bản).
   - [ElevenLabs](https://elevenlabs.io/) (Tạo giọng nói tự nhiên).
   - [Hedra](https://hedra.ai/) (Tạo video từ hình ảnh + âm thanh).
   - [Google Drive](https://drive.google.com/) (Lưu trữ video cuối cùng).
2. **Credentials trong n8n**:
   - API Key của OpenAI, ElevenLabs, Hedra.
   - Thư mục Google Drive để lưu video kết quả.
3. **Dữ liệu đầu vào**:
   - Văn bản podcast về thơ nhịp cho bé (ví dụ: "Con chim nhỏ bay lên trời").
   - (Nếu không có, workflow có thể tự động tạo kịch bản từ prompt bằng GPT).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5308) hoặc copy toàn bộ mã JSON dưới đây vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Workflow Editor.
  2. Nhấn **"Import"** và chọn file JSON.
  3. Hoặc nhấn **"Create"** → **"Import"** và dán JSON.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **21 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình Credentials**
- **OpenAI**:
  - Đi đến **Credentials** → Tạo mới **OpenAI**.
  - Nhập `API Key` từ tài khoản OpenAI.
  - Chọn `DALL·E` và `GPT-3.5/4` trong các node liên quan (`Baby Image Generator`, `Script`).

- **ElevenLabs**:
  - Tạo **Credentials** mới với tên `ElevenLabs`.
  - Nhập `API Key` từ ElevenLabs.
  - Sử dụng trong node `Audio Creation`.

- **Hedra**:
  - Tạo **Credentials** mới với tên `Hedra`.
  - Nhập `API Key` từ Hedra.
  - Cấu hình trong các node `Create Image Asset For Hedra`, `Create Audio Asset For Hedra`, `Generate Video Asset Hedra`.

- **Google Drive**:
  - Tạo **Credentials** mới với tên `Google Drive`.
  - Nhập `Client ID` và `Client Secret` từ [Google Cloud Console](https://console.cloud.google.com/).
  - Chọn thư mục lưu video kết quả trong node `Upload Bin File To Conver In Google Drive`.

##### **B. Cấu Hình Node Quan Trọng**
1. **`Generate Baby Podcast` (FormTrigger)**:
   - Đây là **điểm khởi động** của workflow.
   - Cấu hình **form** để nhập văn bản podcast (ví dụ: "Con gấu trắng ngủ trong hang").
   - **Lưu ý**: Nếu không muốn sử dụng form, có thể thay thế bằng **Webhook** hoặc **Schedule Trigger**.

2. **`Baby Image Generator` (OpenAI)**:
   - Node này **tạo hình ảnh** từ văn bản bằng DALL·E.
   - **Prompt mẫu**:
     ```
     A cute animated baby character reading a rhyming poem about a little bird, hyper-detailed, 4K, cinematic lighting, soft colors, anime style, by Studio Ghibli
     ```
   - **Tham số cần chỉnh**:
     - `Model`: `dall-e-3`.
     - `Size`: `1024x1024`.

3. **`Audio Creation` (ElevenLabs)**:
   - Node này **tạo giọng nói** từ văn bản.
   - **Prompt mẫu**:
     ```
     A warm, friendly female voice reading a baby rhyming poem in a soothing tone, 24khz, high quality
     ```
   - **Tham số cần chỉnh**:
     - `Voice ID`: Chọn giọng phù hợp (ví dụ: `21m00Tcm4TlvDq8ikWAM`).
     - `Model`: `eleven_multilingual_v2`.

4. **`Generate Video Asset Hedra` (Hedra)**:
   - Node này **tạo video** từ hình ảnh + âm thanh.
   - **Tham số cần chỉnh**:
     - `Input Image URL`: Địa chỉ hình ảnh từ OpenAI.
     - `Input Audio URL`: Địa chỉ âm thanh từ ElevenLabs.
     - `Duration`: Thời lượng video (ví dụ: `30` giây).

5. **`Upload Bin File To Conver In Google Drive` (Google Drive)**:
   - Node này **lưu video kết quả** vào Google Drive.
   - **Tham số cần chỉnh**:
     - Chọn **folder** phù hợp.
     - Đặt tên file tự động (ví dụ: `BabyPodcast_[Date]_[Title].mp4`).

##### **C. Các Node Code (Code2, Extract And Combine Binary and Array)**
- Các node này **xử lý dữ liệu trung gian** (chuyển đổi binary, gộp array).
- **Không cần chỉnh** nếu import workflow từ file JSON đã cấu hình sẵn.
- **Nếu cần sửa**:
  - Mở node `Code2` và `Extract And Combine Binary and Array` trong **n8n Editor**.
  - Chỉnh sửa mã JavaScript nếu cần thay đổi logic xử lý dữ liệu.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập một **văn bản mẫu** vào form (ví dụ: "Con mèo xanh nhảy qua vạch").
   - Nhấn **"Run Workflow"** để kiểm tra từng node.
   - Kiểm tra **log** để đảm bảo không có lỗi.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.
   - **Lưu ý**: Nếu sử dụng **FormTrigger**, workflow sẽ hoạt động khi có người nhập dữ liệu.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Hoạt Động Hàng Ngày**:
   - Thay thế **FormTrigger** bằng **Schedule Trigger** để workflow chạy tự động mỗi sáng.
   - Ví dụ: Tạo podcast mới từ một **list văn bản** đã lưu trong Google Sheets.

2. **Gửi Video Đến Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `Download Video` để thông báo khi video hoàn thành.
   - **Cách làm**:
     - Tạo **Credentials** mới cho Slack/Telegram.
     - Thêm node `Slack` hoặc `Telegram Bot` và cấu hình message mẫu:
       ```
       🎉 Video podcast mới đã hoàn thành!
       Tiêu đề: {{ $node["Generate Baby Podcast"].json["title"] }}
       Link: {{ $node["Download Video"].json["url"] }}
       ```

3. **Lưu Log Hoạt Động**:
   - Thêm node **Google Sheets** sau node `Download Video` để ghi lại lịch sử tạo video.
   - **Cách làm**:
     - Tạo một **Google Sheet** mới.
     - Thêm node `Google Sheets` và cấu hình:
       - **Sheet Name**: `BabyPodcast_Logs`.
       - **Row Data**: `{{ $json }}` (để lưu tất cả dữ liệu).

4. **Tối Ưu Hình Ảnh**:
   - Nếu hình ảnh từ DALL·E không phù hợp, **cập nhật prompt** trong node `Baby Image Generator` để mô tả chi tiết hơn.
   - Ví dụ:
     ```
     A 3D animated baby character reading a rhyming poem about a rainbow, ultra-detailed, 8K, vibrant colors, cartoon style, by Pixar
     ```

5. **Sử Dụng GPT Tự Động Tạo Kịch Bản**:
   - Nếu không có kịch bản sẵn, thêm node **OpenAI (GPT)** trước node `Generate Baby Podcast` để tự động tạo văn bản.
   - **Prompt mẫu**:
     ```
     Tạo một bài thơ nhịp cho bé về chủ đề [topic], ngắn gọn, có nhịp điệu, phù hợp với trẻ 3-6 tuổi.
     Topic: "Con gấu trắng"
     ```

---

### 📌 **Kết Luận**
Workflow này **cứu rỗi thời gian và công sức** của các sếp trong việc tạo nội dung podcast cho bé, đồng thời mang lại **chất lượng chuyên nghiệp** với hình ảnh động và giọng nói tự nhiên. Bằng cách tự động hóa toàn bộ quy trình từ **tạo kịch bản đến biên tập video**, các sếp có thể tập trung vào **nội dung sáng tạo** thay vì công việc thủ công.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình credentials.
2. **Test với một bài thơ mẫu** để xem kết quả.
3. **Áp dụng cho dự án podcast** của mình!

---
**🚀 Cảm ơn các sếp đã quan tâm!** Nếu có bất kỳ câu hỏi hoặc gặp khó khăn trong quá trình setup, hãy để lại bình luận bên dưới. Chúng tôi sẵn sàng hỗ trợ! 😊