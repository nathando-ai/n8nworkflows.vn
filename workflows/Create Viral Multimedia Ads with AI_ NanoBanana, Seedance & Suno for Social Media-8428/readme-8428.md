---
title: "🚀 Tự Động Hóa Sáng Tạo Quảng Cáo Viral AI: NanoBanana + Seedance + Suno Cho Mạng Xã Hội"
description: "Workflow tự động hóa hoàn toàn bằng n8n giúp các sếp tạo quảng cáo đa phương tiện AI (ảnh, video, nhạc) từ ý tưởng Telegram, tự động đăng lên Instagram, TikTok, YouTube và theo dõi hiệu quả qua Google Sheets. Tiết kiệm 80% thời gian so với làm thủ công!"
slug: "tự-dộng-hoa-quang-cao-viral-ai-nanobanana-seedance-suno"
tags: [n8n, automation, no-code, ai-multimodal, social-media, upload-post, google-sheets, openai]
keywords: [n8n workflow quảng cáo AI, tự động hóa tạo video TikTok, nano banana seedance suno n8n, đăng quảng cáo tự động instagram tiktok youtube, google sheets theo dõi quảng cáo]
---

# 🚀 **Tự Động Hóa Sáng Tạo Quảng Cáo Viral AI: NanoBanana + Seedance + Suno Cho Mạng Xã Hội**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, việc tạo quảng cáo hiệu quả cho mạng xã hội thường tốn thời gian và chi phí cao:
- **Sáng tạo thủ công**: Tốn nhiều giờ để viết script, thiết kế ảnh/video, chọn nhạc phù hợp.
- **Chất lượng không đồng nhất**: Mỗi quảng cáo phải được chỉnh sửa lại nhiều lần để phù hợp với từng nền tảng.
- **Đăng tải phức tạp**: Cần đăng lên nhiều nền tảng khác nhau (Instagram, TikTok, YouTube) với định dạng khác nhau.
- **Không theo dõi hiệu quả**: Không biết quảng cáo nào hiệu quả, không có báo cáo tự động.

**Workflow này giải quyết tất cả đó!** Với **AI + n8n**, các sếp chỉ cần **gửi ý tưởng qua Telegram**, hệ thống sẽ tự động:
✅ **Tạo ảnh/video AI** (NanoBanana)
✅ **Chỉnh sửa video hiệu ứng** (Seedance)
✅ **Tạo nhạc nền tự động** (Suno)
✅ **Đăng tải lên Instagram, TikTok, YouTube** (Upload-Post)
✅ **Lưu dữ liệu vào Google Sheets** để theo dõi hiệu quả

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và an toàn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với làm thủ công (từ 5h/quảng cáo xuống còn 5 phút).
- **Chất lượng cao nhất** với AI tạo nội dung chuyên nghiệp (ảnh, video, nhạc).
- **Đăng tải tự động** lên tất cả nền tảng (Instagram, TikTok, YouTube) với định dạng phù hợp.
- **Theo dõi hiệu quả** qua Google Sheets (lượt xem, tương tác, chi phí).
- **Cá nhân hóa hoàn toàn** mỗi quảng cáo theo ý tưởng của các sếp.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Upload-Post** (gói Pro để sử dụng API):
   - [Tạo tài khoản Upload-Post](https://www.upload-post.com/)
   - [Tạo API Key](https://www.upload-post.com/settings/api-keys) (trong Dashboard > Settings > API Keys).
2. **API Key OpenAI** (để sử dụng GPT-4 và các mô hình AI khác).
3. **Tài khoản Google Drive & Google Sheets**:
   - [Cài đặt OAuth 2.0 cho Google Drive](https://developers.google.com/drive/api/v3/quickstart/python).
   - [Bảng mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1TCebBvfgvVJyxYXeOiFVpg0RJGP38CpLKNxcOiRwbfQ/edit) (được chia sẻ, các sếp copy và sử dụng).
4. **Tài khoản Telegram**:
   - Bot Telegram để nhận ý tưởng và gửi kết quả (cần tạo bot và lấy `API Token`).
5. **n8n đã cài đặt** (phiên bản mới nhất):
   - [Tải n8n](https://n8n.io/) (Self-hosted hoặc dùng phiên bản cloud).
6. **Node Upload-Post** đã cài đặt trong n8n:
   - [Hướng dẫn cài đặt node Upload-Post](https://n8n.io/integrations/upload-post/).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này có **37 node** và được chia thành **7 bước chính** (xem phần **Hướng Dẫn Chi Tiết** dưới đây). Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/8428](https://n8n.io/workflows/8428) và import vào n8n Editor.
- **Copy/paste JSON** từ file đã tải vào n8n Editor (đường dẫn: `https://<your-n8n-instance>/workflow/edit`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng** như sau:

##### **🔹 Node Trigger: Nhận Ý Tưởng qua Telegram**
- **Tên Node**: `Trigger: Receive Idea via Telegram`
- **Cấu hình**:
  - Chọn **credentials** là `telegramApi` (đã tạo trước).
  - **Message Content** phải chứa ý tưởng quảng cáo (ví dụ: *"Tạo quảng cáo cho sản phẩm nano banana mới với hiệu ứng chuyển động"*).
  - **Test**: Gửi tin nhắn từ Telegram Bot đến workflow để kích hoạt.

##### **🔹 Node NanoBanana: Tạo Ảnh AI**
- **Tên Node**: `NanoBanana: Create Image`
- **Cấu hình**:
  - **Headers Auth**: Điền `httpHeaderAuth` (tạo trong Credentials của n8n).
  - **Body Request**:
    ```json
    {
      "prompt": "{{ $node["Parse Idea Into Prompts"].json["image_prompt"] }}",
      "model": "nanoBanana-v1"
    }
    ```
  - **Lưu ý**: Node này sẽ trả về URL ảnh đã tạo.

##### **🔹 Node Seedance: Chỉnh Sửa Video**
- **Tên Node**: `Seedance: Generate Video from Image`
- **Cấu hình**:
  - **Headers Auth**: Điền `httpHeaderAuth` (tạo trong Credentials).
  - **Body Request**:
    ```json
    {
      "input": "{{ $node["Download Edited Image"].json["url"] }}",
      "effects": ["transition", "zoom", "textOverlay"]
    }
    ```
  - **Lưu ý**: Node này sẽ trả về URL video đã chỉnh sửa.

##### **🔹 Node Suno: Tạo Nhạc Nền**
- **Tên Node**: `Suno: Generate Music`
- **Cấu hình**:
  - **Headers Auth**: Điền `httpHeaderAuth`.
  - **Body Request**:
    ```json
    {
      "prompt": "{{ $node["Ads Copywriter Generator (AI)"].json["music_prompt"] }}",
      "duration": 15
    }
    ```
  - **Lưu ý**: Node này sẽ trả về URL nhạc đã tạo.

##### **🔹 Node Upload-Post: Đăng Quảng Cáo**
- **Tên Node**: `Post Video on Social Media (FB, TikTok, YT)`
- **Cấu hình**:
  - **Credentials**: Chọn `uploadPostApi` (đã tạo trước).
  - **Body Request**:
    ```json
    {
      "url": "{{ $node["Download Final Video"].json["url"] }}",
      "platforms": ["instagram", "tiktok", "youtube"],
      "caption": "{{ $node["Rewrite Caption (TikTok/Instagram)"].json["caption"] }}"
    }
    ```
  - **Lưu ý**:
    - Cần **đăng ký tài khoản** trên các nền tảng (Instagram, TikTok, YouTube) và liên kết với Upload-Post.
    - **Test trước** với video mẫu để đảm bảo định dạng đúng.

##### **🔹 Node Google Sheets: Lưu Dữ Liệu**
- **Tên Node**: `Save Ad Data to Google Sheets`
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Điền tên bảng đã copy từ [mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1TCebBvfgvVJyxYXeOiFVpg0RJGP38CpLKNxcOiRwbfQ/edit).
  - **Headers**:
    ```json
    {
      "ad_id": "{{ $node["Set: Video URL"].json["id"] }}",
      "platform": "instagram",
      "status": "published",
      "views": 0,
      "likes": 0
    }
    ```

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một **ý tưởng mẫu** từ Telegram Bot vào workflow.
  - Theo dõi quá trình từ **tạo ảnh** → **chỉnh sửa video** → **tạo nhạc** → **đăng tải**.
  - Kiểm tra **Google Sheets** để xem dữ liệu đã lưu chưa.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để chạy tự động khi nhận được yêu cầu.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Gửi Báo Cáo Hàng Tuần**:
   - Sử dụng **node `telegram`** để gửi báo cáo tổng hợp từ Google Sheets về Telegram mỗi thứ 7.
   - **Cách làm**:
     - Thêm node `telegram` mới sau `Save Publishing Status to Google Sheets`.
     - **Message**:
       ```json
       {
         "text": "📊 Báo cáo quảng cáo tuần này:\n- Tổng lượt đăng: {{ $node["Save Publishing Status to Google Sheets"].json["rowCount"] }}\n- Nền tảng phổ biến: {{ $node["Read Brand Settings"].json["preferred_platform"] }}"
       }
       ```

2. **Kết Hợp với Zapier/Integromat**:
   - Nếu cần **gửi quảng cáo lên nhiều nền tảng khác** (Facebook Ads, LinkedIn), các sếp có thể kết nối với **Zapier** hoặc **Integromat** thông qua API của Upload-Post.

3. **Tối Ưu Hóa Prompt AI**:
   - **Node `Parse Idea Into Prompts`** (Code Node) có thể được **cải tiến** để tạo ra prompt chi tiết hơn cho NanoBanana và Seedance.
   - **Ví dụ**:
     ```javascript
     // Thay thế nội dung hiện tại trong node Code
     return {
       image_prompt: `A vibrant advertisement for ${$input.all().idea} with a futuristic style, high contrast, and dynamic lighting. The product is in the center, with a modern font overlay saying "Discover ${$input.all().idea} Now!"`,
       video_prompt: `Add cinematic transitions, zoom effects, and text overlays to the image. Use a trending sound effect for engagement.`
     };
     ```

4. **Lưu Log Tất Cả Các Bước**:
   - Thêm **node `stickyNote`** để ghi lại trạng thái của workflow (ví dụ: "Đang tạo ảnh", "Đang upload video").
   - **Cách làm**:
     - Thêm node `stickyNote` sau mỗi bước quan trọng (ví dụ: sau `NanoBanana: Create Image`).
     - **Content**:
       ```json
       {
         "status": "Image created successfully",
         "image_url": "{{ $node["NanoBanana: Create Image"].json["url"] }}"
       }
       ```

5. **Sử Dụng Mô Hình AI Mới Nhất**:
   - **Node `LLM: OpenAI Chat`** hiện đang sử dụng `gpt-5-mini`. Các sếp có thể **thay thế bằng `gpt-4`** (nếu có API Key) để cải thiện chất lượng caption và prompt.
   - **Cách thay đổi**:
     - Trong node `LLM: OpenAI Chat`, thay `model: gpt-5-mini` thành `model: gpt-4`.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình sáng tạo và đăng tải quảng cáo AI** trên mạng xã hội. Với **n8n + AI**, các sếp không chỉ **tiết kiệm thời gian** mà còn **tăng chất lượng và hiệu quả** của quảng cáo.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với ý tưởng mẫu** để đảm bảo mọi thứ hoạt động.
3. **Bật workflow** và bắt đầu **tạo quảng cáo viral tự động**!

---
**💬 Cần hỗ trợ?**
- **Xem video tutorial** của Dr. Firas: [🎥 Full Tutorial](https://youtu.be/4ec9WDCz9CY).
- **Đọc tài liệu chi tiết** trên Notion: [📖 Documentation](https://automatisation.notion.site/Create-viral-Ads-with-NanoBanana-Seedance-publish-on-socials-via-upload-post-2683d6550fd980ffa23ee340fdb3285e).
- **Góp ý hoặc báo lỗi**: Mở issue trên [GitHub n8n](https://github.com/n8n-io/n8n/issues).