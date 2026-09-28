---
title: "🚀 Tự Động Hóa Tạo & Đăng Reels Instagram AI 100% Auto (Heygen + Submagic + Blotato) - Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh từ viết kịch bản, tạo video AI avatar, thêm caption động, đến đăng Reels Instagram tự động - tiết kiệm 8h/ngày cho các sếp content creator. Đáp ứng nhu cầu tạo nội dung ngắn hàng ngày cho cá nhân, agency hay brand."
slug: "tieu-dong-hoa-tao-dang-reels-instagram-ai"
tags: [n8n, automation, content-creation, multimodal-ai, instagram-automation]
keywords: [n8n workflow instagram, tự động hóa reels instagram, ai clone video, heygen submagic blotato, content automation]
---

# 🚀 **Tự Động Hóa Tạo & Đăng Reels Instagram AI - Từ Khái Niệm Đến Đăng Tự Động (Heygen + Submagic + Blotato)**

### **Nỗi Đau Của Các Sếp Content Creator**
Các sếp đang mệt mỏi với quá trình tạo Reels Instagram thủ công:
- **Viết kịch bản** mất 30-60 phút/Reel.
- **Tạo video AI avatar** (Heygen) cần thời gian chờ và cấu hình.
- **Thêm caption động** (Submagic) phức tạp, mất thời gian chỉnh sửa.
- **Đăng lên Instagram** thủ công, dễ quên hoặc sai thời điểm.
- **Không có thời gian** để tạo nội dung hàng ngày cho chiến dịch marketing.

**Workflow này giải quyết tất cả!** Từ một **khái niệm đơn giản** (ví dụ: *"3 thói quen tài chính cho năm 2025"*), hệ thống sẽ tự động:
✅ **Viết kịch bản** tối ưu (hook + body + CTA).
✅ **Tạo video AI avatar** với Heygen (giọng nói + cử chỉ tự nhiên).
✅ **Thêm caption động** với Submagic (chọn template theo phong cách).
✅ **Upload & đăng Reels** tự động lên Instagram qua Blotato.
✅ **Tự động viết caption** + hashtag phù hợp với nội dung.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8-10 giờ/ngày** so với làm thủ công.
- **Nội dung chuyên nghiệp** với kịch bản, video và caption AI tối ưu hóa engagement.
- **Hoạt động 24/7** - không cần phải ngồi trước máy.
- **Tăng reach** với Reels được đăng tự động vào thời điểm tối ưu.
- **Dễ dàng mở rộng** cho TikTok, YouTube Shorts hoặc Facebook Reels.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản & API Key**:
   - **OpenAI** (hoặc mô hình tương thích như Mistral, Groq) - để viết kịch bản và caption.
   - **Heygen** - API Key (Header Auth) để tạo video AI avatar.
   - **Submagic** - API Key (Header Auth) để thêm caption động.
   - **Blotato** - Token và Account ID để đăng lên Instagram.
   - *(Tùy chọn)* **KodeKey/Base URL** nếu sử dụng mô hình OpenAI qua gateway riêng.

2. **Cấu hình trước trên Heygen & Submagic**:
   - **Heygen**: Chọn `avatar_id` và `voice_id` phù hợp với brand.
   - **Submagic**: Chọn `templateName` (ví dụ: *"Hormozi 2"*) và ngôn ngữ.

3. **n8n Self-Hosted**:
   - Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS.
   :::info[Gợi ý hạ tầng cho n8n]
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8918](https://n8n.io/workflows/8918) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --credentials
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **16 node** với các bước quan trọng sau. Các sếp phải **cấu hình chính xác** các node này:

##### **A. Cấu Hình Credentials (API Keys)**
| Node | Loại | Tham Số Cần Điền | Ghi Chú |
|------|------|------------------|---------|
| **OpenAI Chat Model** | `lmChatOpenAi` | `model` (ví dụ: `gpt-4o`, `gpt-4-turbo`) | Chọn mô hình phù hợp với budget. |
| **Heygen** | `httpRequest` | `Authorization: Bearer {API_KEY}` | Đặt API Key trong **Credentials** của n8n. |
| **Submagic** | `httpRequest` | `Authorization: Bearer {API_KEY}` | Đặt API Key trong **Credentials** của n8n. |
| **Blotato** | `blotato` | `accountId`, `instagramMediaType: reel` | Kiểm tra `accountId` trong Blotato Dashboard. |

##### **B. Cấu Hình Node Quan Trọng**
1. **`When chat message received` (chatTrigger)**
   - **Input**: Nhập **topic/khái niệm** (ví dụ: *"5 cách tăng doanh thu online"*).
   - **Output**: Dữ liệu này sẽ truyền vào **Instagram Script Generator**.

2. **`Instagram Script Generator` (Agent)**
   - **System Prompt**: Để tối ưu hóa kịch bản, các sếp có thể chỉnh sửa **system prompt** trong node này để phù hợp với **tone voice** của brand (ví dụ: chuyên nghiệp, hài hước, giáo dục).
   - **Example Prompt**:
     ```
     Tôi là một chuyên gia tạo nội dung Instagram Reels. Viết một kịch bản 25-30 giây với:
     - Hook mạnh mẽ (dùng câu hỏi hoặc số liệu Shocking).
     - Body giải thích chi tiết (3-4 điểm chính).
     - CTA mềm (không bán hàng trực tiếp).
     ```

3. **`Post to Heygen` (httpRequest)**
   - **Headers**:
     ```json
     {
       "Authorization": "Bearer {HEYGEN_API_KEY}",
       "Content-Type": "application/json"
     }
     ```
   - **Body**:
     ```json
     {
       "avatar_id": "YOUR_AVATAR_ID",
       "voice_id": "YOUR_VOICE_ID",
       "script": "$json[script].content"
     }
     ```
   - **Lưu ý**: Thay `YOUR_AVATAR_ID` và `YOUR_VOICE_ID` từ Heygen Dashboard.

4. **`GET Result` (httpRequest)**
   - **Headers**:
     ```json
     {
       "Authorization": "Bearer {HEYGEN_API_KEY}"
     }
     ```
   - **Method**: `GET` với URL:
     ```
     https://api.heygen.com/v1/video/{video_id}/status
     ```
   - **Lưu ý**: Node này **polling** (kiểm tra trạng thái) cho đến khi video sẵn sàng.

5. **`Post to Submagic` (httpRequest)**
   - **Headers**:
     ```json
     {
       "Authorization": "Bearer {SUBMAGIC_API_KEY}",
       "Content-Type": "application/json"
     }
     ```
   - **Body**:
     ```json
     {
       "templateName": "Hormozi 2",
       "language": "en",
       "videoUrl": "$json[video_url].url"
     }
     ```
   - **Lưu ý**: Thay `templateName` theo phong cách muốn sử dụng (ví dụ: *"Hormozi 2"*, *"Minimalist"*).

6. **`Upload media` & `Create post` (Blotato)**
   - **Credentials**: Đặt `accountId` và `token` từ Blotato.
   - **Media Type**: Chọn `reel` trong `instagramMediaType`.
   - **Caption**: Dữ liệu từ node **`Instagram Caption Agent`** sẽ tự động điền.

7. **`Instagram Caption Agent` (openAi)**
   - **Prompt**: Sử dụng template như:
     ```
     Tôi là một chuyên gia viết caption Instagram. Từ kịch bản sau:
     "$json[script].content"
     Viết một caption:
     - 1-2 câu hook (dùng emoji).
     - Giải thích ngắn gọn (3-4 câu).
     - CTA mềm (ví dụ: "DM để biết chi tiết").
     - 5-10 hashtag liên quan (không quá 30 ký tự).
     ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập **topic** vào node `When chat message received`.
   - Kiểm tra từng bước:
     - Kịch bản có hợp lý không?
     - Video Heygen có tải xong không?
     - Caption Submagic có đúng template không?
     - Caption AI có phù hợp không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật Active** và lưu workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
1. **Tối ưu hóa Heygen**:
   - Chọn `avatar_id` và `voice_id` phù hợp với brand (ví dụ: avatar nam nữ, giọng nói trẻ trung).
   - Đặt kích thước video là **1080x1920** (Full HD) cho chất lượng tốt nhất.

2. **Chỉnh sửa Caption Agent**:
   - Nếu muốn **caption dài hơn**, chỉnh sửa system prompt để tăng số lượng câu.
   - Nếu muốn **CTA mạnh mẽ hơn**, thêm yêu cầu như:
     ```
     CTA phải là câu hỏi khuyến khích tương tác (ví dụ: "Bạn đã thử chưa? DM cho mình nhé!").
     ```

3. **Lưu Log & Alert**:
   - Thêm node **Slack/Email Alert** để nhận thông báo khi Reels đăng thành công hoặc lỗi xảy ra.
   - Sử dụng node **`n8n-nodes-base.set`** để lưu log vào **Google Sheets** hoặc **Airtable**.

4. **Cross-Posting**:
   - Sử dụng **Blotato** để đăng cùng lúc lên **TikTok/YouTube Shorts** bằng cách thêm node `blotato` mới với `mediaType: short`.

5. **Schedule Posting**:
   - Nếu không muốn đăng ngay lập tức, thêm node **`n8n-nodes-base.dateTime`** để **delay** trước khi đăng (ví dụ: đăng vào 8h sáng).

6. **Dùng Mô Hình OpenAI Tương Thích**:
   - Nếu OpenAI quá đắt, thử **Mistral AI** (gpt-4-turbo tương thích) hoặc **Groq** (mô hình nhanh hơn).
   - Cấu hình trong node `lmChatOpenAi`:
     ```json
     {
       "model": "mistral-tiny",
       "apiUrl": "https://api.mistral.ai/v1/chat/completions"
     }
     ```

7. **Tự động Xóa Video Lỗi**:
   - Thêm node **`If`** sau `GET Result` (Heygen) để xóa video nếu trạng thái là `failed`.
   - Ví dụ:
     ```json
     {
       "if": "$json[status] === 'failed'",
       "then": [
         {
           "resource": "httpRequest",
           "method": "DELETE",
           "url": "$json[video_url].url"
         }
       ]
     }
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp **tự động hóa toàn bộ quy trình tạo và đăng Reels Instagram** chỉ với một **khái niệm**. Không cần kỹ năng code, không cần phải ngồi trước máy, và **nội dung vẫn chuyên nghiệp, tối ưu hóa engagement**.

**Hành động ngay!**
1. **Import workflow** và cấu hình credentials.
2. **Test với 1-2 topic** để đảm bảo hoạt động.
3. **Bật Active** và bắt đầu **tạo Reels hàng ngày tự động**.

👉 **Xem video hướng dẫn chi tiết** của Automate With Marc: [YouTube - AI Clone Instagram Reel Builder](https://youtu.be/MmZxLuAkqig?si=DRfS89yQlSlbMbfZ)

**Chúc các sếp thành công với chiến dịch content tự động hóa!** 🚀