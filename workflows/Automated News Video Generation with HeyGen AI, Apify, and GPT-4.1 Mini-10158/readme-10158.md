---
title: "🎬 Tự Động Hóa Sáng Tạo Video Tin Tức AI với HeyGen, Apify & GPT-4.1 Mini – Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo video tin tức chuyên nghiệp từ đầu vào văn bản, với giọng nói và avatar AI cá nhân hóa, tiết kiệm 80% thời gian so với thủ công. Áp dụng ngay cho blog, kênh YouTube, hoặc báo cáo doanh nghiệp."
slug: "tieu-dong-hoa-sang-tao-video-tin-tuc-ai-heygen-apify-gpt"
tags: [n8n, automation, content-creation, multimodal-ai, heygen, apify, gpt-4]
keywords: [tự động hóa video tin tức, heygen api n8n, apify news scraping, gpt-4 tạo video, workflow n8n content creation]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video Tin Tức AI – Từ Văn Bản Đến Video Chuyên Nghiệp**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải mất **giờ đồng hồ** để:
❌ Tìm kiếm và tổng hợp tin tức từ nhiều nguồn (Apify, RSS, hoặc thủ công).
❌ Viết kịch bản, chọn giọng nói và avatar phù hợp cho mỗi video.
❌ Chỉnh sửa và xuất bản video trên YouTube, TikTok, hoặc trang web.
❌ **Kết quả:** Video thiếu cá nhân hóa, mất thời gian, và không đồng bộ với nội dung mới nhất.

**Workflow này giải quyết tất cả!** Với **HeyGen AI**, **Apify** (scraping tin tức), và **GPT-4.1 Mini**, các sếp chỉ cần **nhấn một nút**, hệ thống sẽ tự động:
✅ **Tìm tin tức mới nhất** từ Apify.
✅ **Viết kịch bản** bằng GPT-4.1 Mini.
✅ **Chọn avatar và giọng nói AI** từ HeyGen.
✅ **Tạo video hoàn chỉnh** trong vòng **30 giây**.
✅ **Xuất video** sẵn sàng chia sẻ trên mọi nền tảng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** – Đảm bảo tốc độ tối ưu cho AI.
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với thủ công: Từ viết kịch bản đến xuất video chỉ **30 giây**.
- **Video chuyên nghiệp** với avatar và giọng nói AI cá nhân hóa (thậm chí là giọng của chính các sếp).
- **Tự động cập nhật tin tức** từ Apify, không cần theo dõi thủ công.
- **Hoạt động 24/7**: Workflow chạy tự động mỗi khi có tin tức mới.
- **Dễ dàng mở rộng**: Thêm các nguồn tin tức khác (RSS, Twitter API) hoặc tích hợp với Slack/Telegram.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản HeyGen** ([Đăng ký miễn phí](https://app.heygen.com/)) và **API Key**.
✔ **Avatar AI** (có thể import giọng nói từ ElevenLabs hoặc HeyGen tự động clone giọng các sếp).
✔ **Tài khoản OpenRouter** ([Đăng ký](https://openrouter.ai/)) để sử dụng GPT-4.1 Mini.
✔ **Token Apify** ([Đăng ký](https://apify.com/)) để lấy tin tức tự động.
✔ **Credentials trong n8n**:
   - HeyGen API Key (để `Generate Video`, `Get Avatars`, `Get Voices`).
   - OpenRouter API Key (để `GPT 4.1 Mini`).
   - Apify Token (để `News`).

---
:::note[LƯU Ý AN TOÀN]
- **Không lưu API Key trong plain text** trong workflow. Sử dụng **Credentials Store** của n8n để bảo mật.
- Nếu muốn **test trước khi chạy live**, các sếp có thể sử dụng **mode "dry run"** trong node `If`.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/10158) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **13 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình HeyGen (3 Node Chính)**
| Node | Yêu Cầu Cấu Hình |
|------|------------------|
| **`Generate Video`** | - **Endpoint**: `https://api.heygen.com/v1/videos` (API HeyGen).<br>- **Headers**: `Authorization: Bearer {HEYGEN_API_KEY}`.<br>- **Body**: JSON cấu hình video (avatar ID, voice ID, kịch bản từ GPT). |
| **`Get Avatars`** | - **Endpoint**: `https://api.heygen.com/v1/avatars`.<br>- **Headers**: `Authorization: Bearer {HEYGEN_API_KEY}`.<br>- **Lọc avatar** theo tên hoặc ID. |
| **`Get Voices`** | - **Endpoint**: `https://api.heygen.com/v1/voices`.<br>- **Headers**: `Authorization: Bearer {HEYGEN_API_KEY}`.<br>- **Chọn giọng nói** phù hợp (có thể là giọng của các sếp). |

##### **B. Cấu Hình GPT-4.1 Mini (Node `Script Writer`)**
- **Node `GPT 4.1 Mini`** sử dụng **LangChain Agent** kết hợp với OpenRouter.
- **Cấu hình Prompt**:
  ```json
  {
    "prompt": "Tôi là một nhà báo AI. Viết một kịch bản video 30 giây về tin tức sau: '{news_content}'. Kịch bản phải bao gồm:\n1. Dòng mở đầu hấp dẫn.\n2. Thông tin chính (3 điểm nổi bật).\n3. Kết thúc với call-to-action (ví dụ: 'Like và chia sẻ nếu bạn thích!').\nGiọng văn: chuyên nghiệp, ngắn gọn, phù hợp với video YouTube.",
    "model": "openrouter/gpt-4.1-mini",
    "temperature": 0.7
  }
  ```
- **Lưu ý**: Đảm bảo **API Key OpenRouter** được điền vào **Credentials Store** của n8n.

##### **C. Cấu Hình Apify (Node `News`)**
- **Node `News`** sử dụng **Apify SDK** để lấy tin tức.
- **Cấu hình**:
  - **Endpoint**: `https://api.apify.com/v2/act/{ACT_ID}/runs` (thay `{ACT_ID}` bằng ID của **Actor Apify** lấy tin tức).
  - **Headers**: `Authorization: Bearer {APIFY_TOKEN}`.
  - **Body**: JSON cấu hình Actor (ví dụ: `{"input": {"startUrls": ["https://vnexpress.net"]}}`).

##### **D. Node `If` (Kiểm Tra Trạng Thái Video)**
- **Cấu hình điều kiện**:
  - Nếu `Get Video` trả về **status = "completed"**, chuyển sang **`Generate Video1`**.
  - Nếu chưa hoàn thành, **wait 30s** và **polling lại** (thiết lập trong node `Wait`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **`Test workflow`** và nhập **tin tức mẫu** vào node `News`.
   - Kiểm tra:
     - GPT-4.1 Mini có viết kịch bản không?
     - HeyGen có tạo avatar/voice không?
     - Video có xuất ra không?
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và kết nối với **Webhook** (nếu cần tự động hóa từ nguồn tin tức khác).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để thông báo khi video hoàn thành.
   - Ví dụ:
     ```json
     {
       "type": "slack",
       "method": "chat.postMessage",
       "url": "https://hooks.slack.com/services/...",
       "payload": {
         "text": "🎬 Video tin tức mới đã hoàn thành: {{ $json["video_url"] }}"
       }
     }
     ```

2. **Lưu Log & Báo Cáo**:
   - Sử dụng node **`n8n-nodes-base.googleSheets`** để lưu **tất cả video tạo ra** và **thời gian tạo**.
   - Cấu hình:
     ```json
     {
       "sheetName": "Video_Logs",
       "columns": [
         {"name": "Tin tức", "value": "{{ $json["news_title"] }}"},
         {"name": "Video URL", "value": "{{ $json["video_url"] }}"},
         {"name": "Thời gian", "value": "{{ $json["timestamp"] }}"
       ]
     }
     ```

3. **Tự Động Hóa Từ RSS**:
   - Thay thế node `News` bằng **`n8n-nodes-base.rss`** để lấy tin tức từ RSS feed.
   - Cấu hình:
     ```json
     {
       "url": "https://vnexpress.net/rss/tin-tuc.rss",
       "parse": "full"
     }
     ```

4. **Chọn Avatar/Voice Tự Động**:
   - Sử dụng **node `Set`** trước `Generate Video` để động态 chọn avatar/voice phù hợp với chủ đề tin tức.
   - Ví dụ:
     ```json
     {
       "path": "$json.avatar_id",
       "value": "{{ $json["news_category"] === 'tech' ? 'avatar_tech' : 'avatar_general' }}"
     }
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tiết kiệm thời gian** trong việc tạo video tin tức.
✅ **Cải thiện chất lượng nội dung** với AI.
✅ **Hoạt động tự động** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Self-host n8n** trên VPS để workflow chạy 24/7.
2. **Import workflow** và cấu hình API keys.
3. **Test với tin tức mẫu**, sau đó **bật tự động hóa**.

**🚀 CÓ THỂ ÁP DỤNG TRÊN:**
- Kênh YouTube cá nhân.
- Blog doanh nghiệp.
- Báo cáo định kỳ (ví dụ: tin tức thị trường).
- Nội dung marketing cho SMBs.

**Nếu có vấn đề**, các sếp có thể tham khảo [các video hướng dẫn của Jadai Kongolo](https://www.youtube.com/@jadaikongolo) hoặc để lại comment bên dưới! 👇

---
**Chúc các sếp thành công với tự động hóa video AI!** 🎥✨