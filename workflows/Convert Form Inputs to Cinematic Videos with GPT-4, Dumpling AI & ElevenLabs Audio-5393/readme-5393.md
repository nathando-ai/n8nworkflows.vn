---
title: "🎬 **Tự Động Hoá Chuyển Đổi Input Form → Video Cinematic Siêu Đẹp Với AI (GPT-4 + Dumpling AI + ElevenLabs) - Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn chuyển đổi dữ liệu từ form (tên video, 4 loài động vật, phong cách nghệ thuật) thành video động hình siêu đẹp, âm thanh âm nhạc tự động, và tự động lưu trữ kết quả trên Google Drive + Google Sheets. Giúp các sếp tiết kiệm thời gian lên tới 80% trong việc tạo nội dung video AI!"
slug: "tieu-dong-hoa-chuyen-doi-form-ve-video-cinematic-ai"
tags: [n8n, automation, content-creation, ai-multimodal, google-drive, google-sheets, openai, dumpling-ai, elevenlabs, no-code]
keywords: [n8n workflow video ai, tự động hóa video động hình, tạo video từ form, gpt-4 + dumpling ai + elevenlabs, tự động hóa content creation, tự động hóa google drive, tự động hóa google sheets]
---

# 🚀 **Tự Động Hoá Chuyển Đổi Input Form → Video Cinematic Siêu Đẹp Với AI (GPT-4 + Dumpling AI + ElevenLabs)**

### **🔥 Giải Pháp Cho Nỗi Đau Của Các Sếp Trong Tạo Nội Dung Video AI**
Hiện nay, việc tạo nội dung video động hình, đặc biệt là video **cinematic** (phong cách nghệ thuật cao) thường đòi hỏi:
- **Thời gian dài**: Từ viết kịch bản, chọn hình ảnh, tạo âm thanh đến chỉnh sửa video.
- **Kỹ năng chuyên môn**: Cần hiểu về AI, âm nhạc, và kỹ thuật chỉnh sửa.
- **Chi phí cao**: Mua gói premium của các công cụ AI như MidJourney, Runway ML, hoặc thuê designer.

**Workflow này giải quyết tất cả!** Chỉ với **một form đơn giản**, các sếp có thể tự động:
✅ **Tạo video động hình siêu đẹp** từ 4 loài động vật được chọn (ví dụ: "Gấu trúc trong rừng mây với phong cách anime").
✅ **Tạo âm thanh âm nhạc tự động** phù hợp với phong cách video.
✅ **Tự động lưu video + âm thanh** lên Google Drive và ghi log vào Google Sheets.
✅ **Không cần code** – hoàn toàn tự động hóa với n8n!

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian lên tới 80%**: Không cần viết kịch bản, chọn hình ảnh, hoặc chỉnh sửa video thủ công.
- **Chất lượng chuyên nghiệp**: Video động hình được tạo bởi **Dumpling AI** (tương đương MidJourney) và **Leonardo AI**, âm thanh bởi **ElevenLabs** (tương đương Eleven Multimodal).
- **Cá nhân hóa hoàn toàn**: Mỗi video được tạo dựa trên **phong cách nghệ thuật** và **4 loài động vật** do người dùng chọn.
- **Hoạt động 24/7**: Workflow tự động chạy khi có form submission, không cần can thiệp thủ công.
- **Dễ dàng quản lý**: Tất cả video và âm thanh được lưu trên **Google Drive**, link được ghi vào **Google Sheets** để theo dõi.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **API Key / Credentials**                          | **Liên Hệ Đăng Ký**                          |
|---------------------------|--------------------------------------------------|---------------------------------------------|
| **OpenAI (GPT-4)**        | API Key (trong `n8n Credentials` với tên `openAiApi`) | [openai.com](https://platform.openai.com/)   |
| **Dumpling AI**           | API Key (trong `n8n Credentials` với tên `httpHeaderAuth`) | [dumpling.ai](https://dumpling.ai/)         |
| **Leonardo AI**           | API Key (trong `n8n Credentials` với tên `httpHeaderAuth`) | [leonardo.ai](https://leonardo.ai/)         |
| **ElevenLabs**           | API Key (trong `n8n Credentials` với tên `httpHeaderAuth`) | [elevenlabs.io](https://elevenlabs.io/)     |
| **Creatomate**            | API Key (trong `n8n Credentials` với tên `httpHeaderAuth`) | [creatomate.com](https://creatomate.com/)   |
| **Google Drive**          | OAuth 2.0 Credentials (tên `googleDriveOAuth2Api`) | [Google Cloud Console](https://console.cloud.google.com/) |
| **Google Sheets**         | OAuth 2.0 Credentials (tên `googleSheetsOAuth2Api`) | [Google Cloud Console](https://console.cloud.google.com/) |

### **2. File & Folder Trên Google Drive**
- **Folder "AI Generated Videos"**: Để lưu video cuối cùng.
- **Folder "AI Generated Audio"**: Để lưu âm thanh tự động tạo.

### **3. Google Sheet (Để Ghi Log)**
- **Cột cần có**: `Video Title`, `Video Link`, `Created At` (auto-fill).
- **Lưu ý**: Sheet phải có **header** trùng với tên cột trong workflow.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/5393](https://n8n.io/workflows/5393) (chọn **Export JSON**).
2. **Mở n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải.
4. **Xác nhận import** và workflow sẽ hiện lên canvas.

#### **Phương Pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/5393](https://n8n.io/workflows/5393) (chọn **Export JSON**).
2. **Mở n8n Editor** → Nhấp vào **"Import"** → Chọn **"Paste JSON"**.
3. **Xác nhận** và workflow sẽ được tạo.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **22 node**, nhưng chỉ **5 node quan trọng** cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Form Trigger (n8n-nodes-base.formTrigger)**
- **Cấu hình form** với các trường:
  - `title` (text): Tên video (ví dụ: "Câu chuyện của gấu trúc").
  - `animals` (multi-select): Chọn 4 loài động vật (ví dụ: Gấu trúc, Hươu, Khỉ, Rùa).
  - `style` (select): Phong cách nghệ thuật (ví dụ: Anime, Watercolor, Cyberpunk).
- **Lưu ý**:
  - **Enable "Active"** để form hoạt động.
  - **Test form** bằng cách submit dữ liệu mẫu trước khi cấu hình tiếp.

#### **🔹 Node 2: OpenAI Credentials (n8n-nodes-langchain.openAi)**
- **Tạo credentials mới**:
  1. Trong n8n Editor, nhấp **"Credentials"** → **"Add"** → Chọn **"OpenAI"**.
  2. Đặt tên: `openAiApi`.
  3. Nhập **API Key** từ OpenAI (tạo tại [platform.openai.com](https://platform.openai.com/)).
  4. **Chọn model**: `gpt-4` (hoặc `gpt-4-1106-preview` nếu có).
  5. **Lưu**.

#### **🔹 Node 3: Dumpling AI & Leonardo AI (n8n-nodes-base.httpRequest)**
- **Tạo credentials HTTP Header Auth**:
  1. Nhấp **"Credentials"** → **"Add"** → Chọn **"HTTP Header Auth"**.
  2. Đặt tên: `httpHeaderAuth`.
  3. Nhập **API Key** từ Dumpling AI/Leonardo AI.
  4. **Lưu**.
- **Cấu hình trong node**:
  - **URL**: `https://api.dumpling.ai/v1/images/generations` (Dumpling AI) hoặc `https://api.leonardo.ai/v1/endpoints/{endpoint_id}/outputs` (Leonardo AI).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "prompt": "{{ $node["GPT-4: Create Cinematic Prompt"].json["prompt"] }}",
      "width": 1024,
      "height": 1024,
      "negative_prompt": "blurry, low quality"
    }
    ```

#### **🔹 Node 4: ElevenLabs (n8n-nodes-base.httpRequest)**
- **Cấu hình tương tự Dumpling AI**, nhưng:
  - **URL**: `https://api.elevenlabs.io/v1/text-to-speech/{voice_id}`.
  - **Headers**:
    ```json
    {
      "xi-api-key": "YOUR_ELEVENLABS_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "text": "{{ $node["GPT-4: Generate Audio Prompt"].json["prompt"] }}",
      "model_id": "eleven_multimodal",
      "voice_settings": {
        "stability": 0.5,
        "similarity_boost": 0.5
      }
    }
    ```

#### **🔹 Node 5: Google Drive & Sheets (n8n-nodes-base.googleDrive/googleSheets)**
- **Tạo credentials OAuth 2.0**:
  1. Trong n8n Editor, nhấp **"Credentials"** → **"Add"** → Chọn **"Google Drive OAuth 2.0"** (và tương tự cho Sheets).
  2. Đặt tên: `googleDriveOAuth2Api` (và `googleSheetsOAuth2Api`).
  3. **Quản lý OAuth**:
     - Mở [Google Cloud Console](https://console.cloud.google.com/).
     - Tạo **OAuth Client ID** với scope:
       - `https://www.googleapis.com/auth/drive.file` (Drive).
       - `https://www.googleapis.com/auth/spreadsheets` (Sheets).
     - **Lưu file credentials JSON** và upload lên n8n.
  4. **Chọn folder** trong Google Drive:
     - Trong node **"Upload: Save Final Video to Drive"**, chọn folder **"AI Generated Videos"**.
  5. **Cấu hình Google Sheets**:
     - Trong node **"Log: Add Video Title & Link to Sheet"**, chọn sheet và **append data** vào cột `Video Title`, `Video Link`.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu**:
   - Nhấp **"Run Workflow"** và submit form với dữ liệu mẫu:
     - `title`: "Câu chuyện của gấu trúc".
     - `animals`: Gấu trúc, Hươu, Khỉ, Rùa.
     - `style`: Anime.
   - **Kiểm tra**:
     - Video động hình có được tạo không?
     - Âm thanh có được sinh ra không?
     - File có được upload lên Google Drive không?
     - Link video có được ghi vào Google Sheets không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấp **"Active"** để workflow chạy tự động khi có form submission.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM ĐẸP HƠN**]
- **Tạo Form Đẹp Hơn**:
  - Sử dụng **n8n Form Builder** hoặc **Google Forms** kết nối với workflow.
  - Thêm **hình ảnh mẫu** và **gợi ý phong cách** (ví dụ: "Chọn phong cách Anime để video có vẻ như anime").

- **Tự Động Gửi Video Đến Slack/Telegram**:
  - Thêm node **Slack/Telegram Webhook** sau node **"Upload: Save Final Video to Drive"** để thông báo khi video hoàn thành.
  - **Cấu hình**:
    ```json
    {
      "text": "🎬 Video mới được tạo: {{ $node["Log: Add Video Title & Link to Sheet"].json["title"] }}",
      "attachments": [
        {
          "title": "Xem video",
          "text": "{{ $node["Log: Add Video Title & Link to Sheet"].json["link"] }}",
          "callback_id": "video_link"
        }
      ]
    }
    ```

- **Lưu Log Chi Tiết**:
  - Thêm node **n8n-nodes-base.googleDrive** để lưu **tất cả file tạm** (ảnh, âm thanh, video trung gian) vào folder **"AI Generated Assets"** để debug.

- **Tự Động Xóa File Tạm**:
  - Sử dụng **n8n-nodes-base.googleDrive** với **operation: "delete"** để xóa file tạm sau khi video hoàn thành.

- **Tạo Báo Cáo Thống Kê**:
  - Sử dụng **Google Sheets** để tính toán số lượng video tạo ra mỗi tháng và chia sẻ với team.
  - **Công thức Google Sheets**:
    ```excel
    =COUNTIF(Sheet1!B:B, "=DONE")
    ```

- **Kết Hợp Với Notion**:
  - Thay vì Google Sheets, sử dụng **Notion API** để ghi log vào database Notion.
  - **Cài đặt**:
    - Tạo credentials Notion trong n8n.
    - Sử dụng node **n8n-nodes-base.httpRequest** với URL:
      ```
      https://api.notion.com/v1/pages
      ```
    - **Headers**:
      ```json
      {
        "Authorization": "Bearer YOUR_NOTION_API_KEY",
        "Notion-Version": "2022-06-28",
        "Content-Type": "application/json"
      }
      ```

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tạo nội dung video AI** mà không cần code. Với **GPT-4, Dumpling AI, ElevenLabs, và Creatomate**, mỗi form submission sẽ tự động trở thành một **video động hình siêu đẹp** với âm nhạc tự động, được lưu trữ và quản lý một cách chuyên nghiệp.

### **🎯 Bước Tiếp Theo**
1. **Lên đồ workflow