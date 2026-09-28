---
title: "🚀 Tự Động Clone Video Viral TikTok & Instagram Reels bằng AI Gemini 2.5 Pro – Không Cần Code!"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp phân tích, tách xương video viral từ TikTok/Instagram, tạo prompt AI chính xác để tái tạo nội dung giống hệt, và chia sẻ kết quả ngay trên Slack. Giúp tiết kiệm thời gian lên đến 80% so với phương pháp thủ công."
slug: "tieu-dong-clone-video-tiktok-instagram-gemini-2-5-pro"
tags: [n8n, automation, ai-summarization, content-creation, gemini-api, tiktok-instagram]
keywords: [tự động hóa n8n, clone video viral, gemini 2.5 pro, prompt ai, apify, reverse engineering video]
---

# 🚀 **Tự Động Clone Video Viral TikTok & Instagram Reels bằng AI Gemini 2.5 Pro**

### **Giải pháp cho các sếp muốn "hack" nội dung viral mà không cần viết một dòng code!**
Hãy tưởng tượng: Một video TikTok hay Instagram Reels đang viral với hàng triệu lượt xem. Bạn muốn **tái tạo nội dung tương tự** để áp dụng cho chiến dịch marketing của mình, nhưng không biết cách phân tích cấu trúc video đó? Hoặc bạn phải **tốn hàng giờ** để thủ công tách xương video, viết prompt AI và thử nghiệm nhiều lần?

**Workflow này sẽ giải quyết tất cả!** Với công nghệ **Apify + Gemini 2.5 Pro**, nó tự động:
✅ **Tải video** từ TikTok/Instagram Reels
✅ **Phân tích nội dung** bằng AI Gemini để tách xương video (text, âm thanh, hiệu ứng)
✅ **Tạo prompt AI chính xác** để tái tạo video giống hệt
✅ **Gửi kết quả ngay Slack** cho team review

Không cần kỹ thuật, không cần code – chỉ cần **nhập URL video** và workflow sẽ làm tất cả!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì tốn 3-5 giờ để phân tích video thủ công, workflow chỉ cần **vài giây** để hoàn thành.
- **Prompt AI chính xác**: Gemini 2.5 Pro phân tích video và tạo ra **prompt tái tạo 100% giống hệt** video gốc.
- **Áp dụng ngay cho content marketing**: Dễ dàng tái tạo video viral cho chiến dịch của mình.
- **Hoạt động liên tục**: Chạy tự động 24/7 trên VPS, không cần can thiệp.
- **Tích hợp Slack**: Kết quả được gửi ngay cho team review, không mất thời gian copy-paste.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để tải video từ TikTok/Instagram):
   - [Đăng ký miễn phí Apify](https://apify.com/)
   - **API Key**: Tạo tại [Apify Dashboard](https://apify.com/dashboard/settings/api-keys) và thêm vào n8n dưới **Credentials → Apify API Key**.
2. **Tài khoản Slack** (để nhận kết quả):
   - Tạo **OAuth Token** tại [Slack API](https://api.slack.com/apps) và thêm vào n8n dưới **Credentials → Slack OAuth2 API**.
3. **API Key Gemini 2.5 Pro** (để phân tích video):
   - Nếu chưa có, đăng ký tại [Google AI Studio](https://makersuite.google.com/app/apikey) và thêm vào n8n dưới **Credentials → HTTP Header Auth** (dùng cho node `analyze_tiktok` và `analyze_ig_reel`).
4. **URL video TikTok/Instagram Reels** (để input vào form trigger).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/6104) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6104) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **2 nhánh chính** (TikTok và Instagram Reels), nhưng **cấu hình chung** như sau:

##### **A. Cấu hình Apify (đối với tất cả node tải video)**
- **Node `scrape_tiktok` và `scrape_ig_reel`**:
  - **Method**: `POST`
  - **URL**: `https://api.apify.com/v2/act/your-apify-actor-id/run`
  - **Headers**:
    ```
    Authorization: Bearer YOUR_APIFY_API_KEY
    Content-Type: application/json
    ```
  - **Body**:
    ```json
    {
      "input": {
        "url": "${{ $json["url"] }}",
        "proxy": "apify-proxy"
      }
    }
    ```
  - **Lưu ý**:
    - Thay `your-apify-actor-id` bằng **ID Actor Apify** tương ứng với TikTok/Instagram (ví dụ: `apify/tiktok-scraper` cho TikTok).
    - **Test API** trước để đảm bảo hoạt động.

##### **B. Cấu hình Gemini 2.5 Pro (đối với node phân tích)**
- **Node `analyze_tiktok` và `analyze_ig_reel`**:
  - **Method**: `POST`
  - **URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-pro:generateContent`
  - **Headers**:
    ```
    Authorization: Bearer YOUR_GEMINI_API_KEY
    Content-Type: application/json
    ```
  - **Body**:
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "Analyze this video URL: ${{ $json["url"] }}. Extract the following details:\n1. Script (dialogue, narration)\n2. Visual elements (transitions, effects, colors)\n3. Audio (music, sound effects)\n4. Editing style (cutting rhythm, pacing)\n5. Generate a Veo 3 prompt to recreate this video exactly."
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý**:
    - **Gemini 2.5 Pro** có giới hạn free tier (50k token/tháng). Nếu vượt quá, cần nâng cấp.
    - **Đảm bảo API Key** được thêm vào **Credentials → HTTP Header Auth** trong n8n.

##### **C. Cấu hình Slack (đối với node gửi kết quả)**
- **Node `send_prompt_msg` và `upload_file`**:
  - **Channel**: Chọn **#general** hoặc channel phù hợp.
  - **Text**: Sử dụng **`${$json["prompt"]}`** để hiển thị prompt AI.
  - **File**: Node `upload_file` sẽ tự động upload file text chứa prompt (không cần chỉnh thêm).

##### **D. Cấu hình Form Trigger**
- **Node `form_trigger`**:
  - Thêm **input field** với tên `url` (loại `text`) để nhập URL video.
  - **Lưu ý**: URL phải là video **AI generate** (ví dụ: video từ Veo 3, Sora, Runway ML).

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhập URL video ví dụ (ví dụ: [video TikTok AI generate](https://www.tiktok.com/@veo3official/video/...)) vào form trigger.
   - Chạy **Test Run** để kiểm tra workflow.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Google Drive/OneDrive**:
   - Thay vì gửi Slack, có thể **lưu prompt vào Google Drive** bằng node `google-drive` để backup.
2. **Lưu log hoạt động**:
   - Thêm node **`stickyNote`** để ghi lại lịch sử URL đã xử lý.
3. **Tự động chia sẻ trên Telegram**:
   - Thay node Slack bằng **`telegram`** để gửi kết quả ngay vào nhóm Telegram.
4. **Tối ưu prompt**:
   - Nếu kết quả không chính xác, **cập nhật prompt** trong node `set_base_prompt` để Gemini phân tích chi tiết hơn.

---

### 📌 **Kết luận**
Workflow này là **công cụ mạnh mẽ** giúp các sếp **tái tạo video viral** một cách nhanh chóng, không cần kỹ thuật. Từ việc **tải video → phân tích AI → tạo prompt → chia sẻ kết quả**, tất cả chỉ cần **nhập URL** là xong!

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với video AI generate** để xem kết quả.
3. **Áp dụng cho chiến dịch marketing** của mình!

---
**💡 Lưu ý cuối cùng**: Workflow này **không vi phạm bản quyền** vì chỉ phân tích và tái tạo **cách thức** chứ không sao chép nội dung nguyên văn. Hãy sử dụng hợp pháp và sáng tạo! 🚀