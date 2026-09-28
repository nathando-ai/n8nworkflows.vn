---
title: "🚀 Tự Động Hóa Sáng Tạo Video Avatar AI Từ Đầu Đến Cuối Với Gemini, HeyGen & Google Sheets"
description: "Workflow tự động hóa 100% không code giúp các sếp tạo và phát hành video ngắn AI avatar từ ý tưởng viral đến công cụ phân tích, viết kịch bản, sinh video và đăng tải lên TikTok/Facebook chỉ trong vài phút. Giảm thời gian sáng tạo 90% và tối ưu hóa nội dung cho engagement cao."
slug: "tieu-dong-hoa-tao-tao-video-avatar-ai-gemini-google-sheets"
tags: [n8n, automation, content-creation, ai-avatar, google-sheets, gemini-ai, heygen, tiktok-automation, facebook-automation]
keywords: [n8n workflow tự động hóa video avatar, tạo video ngắn AI không code, tự động hóa content viral, gemini ai viết kịch bản, heygen sinh video avatar, đăng tải video tiktok facebook tự động]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video Avatar AI: Từ Ý Tưởng Viral Đến Video Hot Trên TikTok & Facebook**

## **🔥 Nỗi Đau Của Các Sếp Trong Sáng Tạo Video AI**
Hiện nay, việc tạo video ngắn AI avatar để thu hút người dùng trên TikTok, Facebook hay YouTube đang trở thành **trend không thể bỏ qua**. Tuy nhiên, quá trình này thường gặp phải những khó khăn như:
- **Tốn thời gian**: Tìm ý tưởng viral, viết kịch bản, sinh video và đăng tải thủ công mất hàng giờ/lần.
- **Chất lượng không đồng nhất**: Kịch bản viết tay dễ bị thiếu sáng tạo, video sinh ra không phù hợp với xu hướng.
- **Không tối ưu hóa**: Không biết cách phân tích video viral để tạo nội dung tương tự, dẫn đến tỷ lệ engagement thấp.
- **Không tự động hóa**: Phải làm lại từ đầu mỗi khi muốn thử ý tưởng mới.

**Workflow này giải quyết tất cả!** Với **Gemini AI** phân tích video viral, **HeyGen** sinh video avatar, và **Google Sheets** quản lý quy trình, các sếp sẽ **tự động hóa toàn bộ chuỗi giá trị sáng tạo** chỉ trong vài phút.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian**: Từ tìm ý tưởng đến đăng tải video chỉ mất **5-10 phút/lần**.
✅ **Nội dung viral tự động**: AI phân tích xu hướng và tạo kịch bản phù hợp với xu hướng hiện tại.
✅ **Chất lượng cao nhất**: Video avatar sinh ra từ kịch bản được tối ưu hóa bởi Gemini AI.
✅ **Đăng tải tự động**: Video được tự động chia sẻ lên **TikTok & Facebook** mà không cần can thiệp thủ công.
✅ **Theo dõi hiệu quả**: Google Sheets ghi lại tất cả quá trình (từ ý tưởng đến kết quả engagement).
✅ **Hoạt động 24/7**: Workflow chạy tự động theo lịch trình, không cần người quản lý.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets với **2 sheet**:
     - `Viral_Ideas` (để lưu ý tưởng viral và trạng thái).
     - `Video_Status` (để theo dõi quá trình sinh và đăng tải video).
   - **Cấu trúc sheet**:
     | Column          | Dữ liệu cần có                          |
     |-----------------|-----------------------------------------|
     | `Title`         | Tên ý tưởng viral (vd: "Trend 'AI Cooking'") |
     | `Video_URL`     | Link video viral (để Gemini phân tích) |
     | `Script`        | Kịch bản tự động sinh (nếu đã có)      |
     | `Status`        | `Pending` / `Processing` / `Published` |
     | `Video_Link`    | Link video avatar sau khi sinh thành   |

2. **API Keys & Credentials**:
   - **Google Gemini API Key**: [Cài đặt tại đây](https://makersuite.google.com/app/apikey).
   - **HeyGen API Key**: [Đăng ký tại đây](https://www.heygen.com/).
   - **Blotato API Key** (để đăng tải TikTok/Facebook):
     - [Tạo tại đây](https://blotato.com/) (nên dùng **Blotato Pro** để hỗ trợ TikTok).
   - **Tài khoản TikTok & Facebook Business Manager**:
     - TikTok: [Tạo tài khoản Developer](https://developers.tiktok.com/).
     - Facebook: [Cài đặt Meta Business Suite](https://www.facebook.com/business/).

3. **Dịch vụ bổ sung**:
   - **Apify Actor** (để lấy dataset video viral):
     - Sử dụng [actor "Viral Videos"](https://apify.com/actor/your-actor-name) (nếu không có, có thể thay bằng API khác như YouTube Data API).
   - **n8n Self-Hosted** (để workflow chạy 24/7):
     - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
     - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13024](https://n8n.io/workflows/13024).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → **Create Workflow** → **Import from JSON**.
3. **Dán JSON** và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Cron – Fetch Viral Ideas (n8n-nodes-base.scheduleTrigger)**
- **Cấu hình lịch trình**:
  - Thời gian chạy: **Mỗi ngày 8h sáng** (để phân tích xu hướng mới nhất).
  - **Schedule Type**: `cron` → Điền `0 8 * * *` (8h00 UTC).

#### **🔹 Node 2: Get Viral Video Dataset (@apify/n8n-nodes-apify.apify)**
- **Cấu hình Apify Actor**:
  - **Actor Name**: Nhập tên actor lấy dataset viral (vd: `viral-videos-scraper`).
  - **Run Mode**: `Run actor and get dataset`.
  - **Credentials**: Điền **API Token** của Apify (nếu không có, có thể thay bằng API YouTube Data API).

#### **🔹 Node 3: Google Sheets (Save Viral Ideas)**
- **Chọn Credentials**:
  - **Google Sheets**: Chọn credential đã tạo trước (nếu chưa có, tạo tại **n8n Credentials** → **Add Credential** → **Google Sheets**).
- **Cấu hình Sheet**:
  - **Sheet Name**: `Viral_Ideas`.
  - **Range**: `A1` (để ghi dữ liệu từ hàng đầu tiên).
  - **Operation**: `append` (thêm dữ liệu mới vào cuối sheet).

#### **🔹 Node 4: Cron – Process Viral Row (n8n-nodes-base.scheduleTrigger)**
- **Cấu hình lịch trình**:
  - Thời gian chạy: **Mỗi 2 giờ** (để xử lý nhiều ý tưởng đồng thời).
  - **Schedule Type**: `cron` → Điền `0 */2 * * *` (mỗi 2 giờ).

#### **🔹 Node 5: Load Viral Idea from Sheet (n8n-nodes-base.googleSheets)**
- **Chọn Credentials**: Điền credential Google Sheets tương tự như Node 3.
- **Cấu hình Sheet**:
  - **Sheet Name**: `Viral_Ideas`.
  - **Range**: `A1:D1000` (đọc tất cả dữ liệu trong sheet).
  - **Filter**: `Status = "Pending"` (chỉ lấy ý tưởng chưa xử lý).

#### **🔹 Node 6: Analyze Viral Video (n8n-nodes-langchain.googleGemini)**
- **Cấu hình Gemini AI**:
  - **Model**: `gemini-pro` (hoặc `gemini-1.5-flash` nếu muốn tiết kiệm chi phí).
  - **Prompt**:
     ```plaintext
     Analyze this viral video at {video_url} and extract:
     1. Main topic (1-2 keywords).
     2. Emotional trigger (funny, inspirational, shocking, etc.).
     3. Key phrases used in the video.
     4. Suggest a short script (under 30 seconds) for an AI avatar video.
     Format response as JSON:
     {
       "topic": "string",
       "emotion": "string",
       "key_phrases": ["string", "string"],
       "script": "string"
     }
     ```
  - **API Key**: Điền **Google Gemini API Key** đã tạo trước.

#### **🔹 Node 7: Parse Script Structure (n8n-nodes-langchain.outputParserStructured)**
- **Cấu hình**:
  - **Schema**: Điền schema JSON tương ứng với output của Gemini (vd:
    ```json
    {
      "topic": "string",
      "emotion": "string",
      "key_phrases": ["string"],
      "script": "string"
    }
    ```
  - **Error Handling**: Bật **Retry failed items** (3 lần).

#### **🔹 Node 8: AI Agent – Script & Avatar Director (n8n-nodes-langchain.agent)**
- **Cấu hình Agent**:
  - **Role**: `AI Avatar Script Director`.
  - **Tools**:
    - `googleGemini` (đã cấu hình ở Node 6).
    - `heygen` (sẽ cấu hình sau).
  - **Prompt**:
     ```plaintext
     You are an AI director for creating short-form avatar videos.
     Given a viral video analysis, refine the script to:
     1. Be under 30 seconds.
     2. Match the emotional trigger.
     3. Include key phrases naturally.
     4. Optimize for engagement (hook in first 3 seconds).
     Use the following structure:
     - [Hook: 1-2 seconds]
     - [Story: 10-15 seconds]
     - [Call-to-Action: 3-5 seconds]
     Finalize the script and prepare for HeyGen avatar generation.
     ```

#### **🔹 Node 9: Create AI Avatar Video (n8n-nodes-base.httpRequest)**
- **Cấu hình HeyGen API**:
  - **URL**: `https://api.heygen.com/v1/video`.
  - **Headers**:
    - `Authorization`: `Bearer {heygen_api_key}`.
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "script": "{{$node["AI Agent – Script & Avatar Director"].json["script"]}}",
      "avatar_id": "your-avatar-id",  // Tải avatar từ HeyGen Dashboard
      "voice": "female_english_1",    // Chọn giọng nói phù hợp
      "language": "en",
      "style": "natural"
    }
    ```
  - **Lưu ý**:
    - **Trước tiên**, tạo **avatar** trên [HeyGen Dashboard](https://www.heygen.com/dashboard) và lấy `avatar_id`.
    - **Giọng nói**: Chọn giọng phù hợp với nội dung (vd: `male_english_1` cho nội dung nghiêm túc).

#### **🔹 Node 10: Wait for Video Rendering (n8n-nodes-base.wait)**
- **Thời gian chờ**: **300 giây (5 phút)** (HeyGen thường hoàn thành trong 3-5 phút).
- **Lưu ý**: Nếu video lớn, có thể tăng thời gian lên **600 giây**.

#### **🔹 Node 11: Get Rendered Video & Check Video Status (n8n-nodes-base.httpRequest + n8n-nodes-base.if)**
- **Get Rendered Video**:
  - **URL**: `https://api.heygen.com/v1/video/{video_id}` (lấy `video_id` từ response của Node 9).
  - **Headers**: `Authorization: Bearer {heygen_api_key}`.
- **Check Video Status**:
  - **Condition**: Kiểm tra `status` trong response:
    - Nếu `status = "completed"`, chuyển sang Node tiếp theo.
    - Nếu `status = "processing"`, **wait again** (sử dụng Node `Wait`).

#### **🔹 Node 12: Publish Video to TikTok & Facebook (@blotato/n8n-nodes-blotato.blotato)**
- **Cấu hình Blotato**:
  - **Credentials**: Chọn `blotatoApi` đã tạo trước.
  - **Platforms**:
    - **TikTok**:
      - **URL**: `https://api.blotato.com/v1/tiktok/videos`.
      - **Body**:
        ```json
        {
          "video_url": "{{$node["Get Rendered Video"].json["url"]}}",
          "caption": "{{$node["Finalize Avatar Script"].json["script"] | substr(0, 100)}}...",
          "hashtags": ["#AIAvatar", "#ViralContent"]
        }
        ```
    - **Facebook**:
      - **URL**: `https://api.blotato.com/v1/facebook/videos`.
      - **Body**:
        ```json
        {
          "video_url": "{{$node["Get Rendered Video"].json["url"]}}",
          "caption": "{{$node["Finalize Avatar Script"].json["script"]}}",
          "page_id": "your_page_id"  // Lấy từ Facebook Business Manager
        }
        ```
  - **Lưu ý**:
    - **TikTok**: Nếu không có tài khoản TikTok Business, tạo tại [TikTok Developer](https://developers.tiktok.com/).
    - **Facebook**: Chọn **Page ID** từ **Facebook Business Suite**.

#### **🔹 Node 13: Update Google Sheets (googleSheets)**
- **Cập nhật trạng thái**:
  - **Operation**: `update`.
  - **Range**: `D2` (cột `Status`).
  - **Value**: `Published`.
  - **Video_Link**: Điền link video từ HeyGen.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**: