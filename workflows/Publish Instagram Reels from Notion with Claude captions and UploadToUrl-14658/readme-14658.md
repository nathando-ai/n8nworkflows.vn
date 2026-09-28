---
title: "🚀 Tự Động Hóa Đăng Instagram Reels Từ Notion Với Caption AI Claude & Upload CDN - Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo, kiểm duyệt và đăng Reels Instagram từ Notion với caption AI thông minh, quản lý chất lượng và báo cáo tự động. Giảm thời gian 90% so với làm thủ công!"
slug: "tieu-dong-hoa-dang-instagram-reels-tu-notion"
tags: [n8n, automation, social-media, ai-caption, instagram-reels, notion-integration, self-hosted, no-code]
keywords: [n8n workflow instagram reels, tự động hóa content instagram, caption ai cho reels, upload video instagram tự động, quản lý content social media, workflow approval gate]
---

# 🚀 **Tự Động Hóa Đăng Instagram Reels Từ Notion Với AI Claude & CDN - Không Cần Code**

### **Giải pháp hoàn chỉnh cho các sếp quản lý content Instagram**
Hãy tưởng tượng một ngày không cần phải:
- **Chuyển video từ Notion sang Instagram** một cách thủ công?
- **Viết caption** mất nhiều giờ mà vẫn không đảm bảo chất lượng?
- **Chờ đợi kiểm duyệt** và quên mất là đã đăng hay chưa?
- **Quản lý trạng thái** của từng Reels trong Notion?

Workflow này **tự động hóa toàn bộ quy trình** từ khi bạn submit yêu cầu đến khi Reels được đăng và báo cáo lên Discord. **Không cần viết một dòng code nào!**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với làm thủ công: Từ submit yêu cầu đến khi Reels live chỉ mất vài phút.
- **Caption AI thông minh**: Claude tạo caption phù hợp với tone (hype, minimal, storytelling) và tự động thêm hashtag, CTA.
- **Kiểm duyệt tự động hóa**: Email preview + button approve/reject, không quên đăng hay đăng sai.
- **Quản lý chất lượng**: Tất cả trạng thái (Chờ, Đang xử lý, Thất bại, Đã đăng) được cập nhật tự động trên Notion.
- **Báo cáo toàn diện**: Permalink, timestamp và thông tin đăng được gửi lên Discord ngay khi Reels live.
- **Hoạt động 24/7**: Workflow chạy tự động trên VPS, không phụ thuộc vào thời gian làm việc của bạn.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Instagram Business** (để sử dụng Graph API):
   - `IG_USER_ID` (ID người dùng Instagram)
   - `IG_ACCESS_TOKEN` (Token API Instagram, có thời hạn 60 ngày, cần renew)
2. **Notion Database**:
   - `NOTION_API_KEY` (API Key từ Notion)
   - `NOTION_DATABASE_ID` (ID của database chứa video)
   - Các trang Notion phải có các trường: **Title, Video URL, Cover URL, Description, Tags, Status**.
3. **API Key Claude (Anthropic)**:
   - `ANTHROPIC_API_KEY` (Đăng ký tại [Anthropic](https://www.anthropic.com/))
4. **Email cho người kiểm duyệt**:
   - `APPROVER_EMAIL` (Email của người có quyền approve/reject)
5. **Webhook Discord** (tùy chọn):
   - `DISCORD_WEBHOOK_URL` (Để nhận thông báo khi Reels đăng thành công/thất bại)
6. **CDN Public** (để upload video và cover):
   - Workflow sử dụng `UploadToUrl` để push video lên CDN công khai (Instagram yêu cầu URL HTTPS công khai).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14658](https://n8n.io/workflows/14658) hoặc copy toàn bộ JSON từ canvas.
- **Import vào n8n Editor**:
  - Mở n8n Workflow Editor → Nhấn **Import** → Dán JSON hoặc chọn file JSON.
  - **Không cần chỉnh sửa gì** nếu đã có tất cả credentials (env vars) sẵn.

:::note[LƯU Ý]
- Workflow **không chạy được** nếu thiếu bất kỳ env var nào. Đảm bảo đã điền đầy đủ:
  ```env
  IG_USER_ID=your_ig_user_id
  IG_ACCESS_TOKEN=your_ig_access_token
  NOTION_API_KEY=your_notion_api_key
  NOTION_DATABASE_ID=your_notion_db_id
  ANTHROPIC_API_KEY=your_claude_api_key
  APPROVER_EMAIL=approver@example.com
  DISCORD_WEBHOOK_URL=your_discord_webhook_url
  ```
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Node `n8n Form Submit Reel Request` (Form Trigger)**
- **Cấu hình form**:
  - **Fields**:
    - `Notion Page ID` (Text): ID của trang Notion chứa video (ví dụ: `abc123`).
    - `Caption Tone` (Dropdown): Chọn tone caption (hype, minimal, storytelling).
  - **URL form**: Sẽ được tạo tự động sau khi import. **Chia sẻ URL này** với team để họ submit yêu cầu.
  - **Không cần đăng ký tài khoản n8n**: Ai cũng có thể submit yêu cầu chỉ bằng form này.

#### **B. Node `HTTP Read Notion Page` (Read Notion API)**
- **Configuration**:
  - **Method**: `GET`
  - **URL**: `https://api.notion.com/v1/pages/{page_id}`
  - **Headers**:
    - `Authorization`: `Bearer {{ $node["Credentials"]["notion"]["apiKey"] }}`
    - `Notion-Version`: `2022-06-28`
  - **Query Parameters**:
    - `page_id`: `$node["n8n Form Submit Reel Request"]["json"]["Notion Page ID"]`
  - **Lưu ý**:
    - API Key Notion phải có **quyền đọc** database.
    - Nếu Notion API bị rate limit, thêm delay bằng node `Wait`.

#### **C. Node `Code Claude AI Caption` (AI Caption Generation)**
- **Logic**:
  - Gửi request đến Claude API với:
    - `Title`, `Description`, `Tags` từ Notion.
    - `Tone` được chọn từ form.
  - **Fallback**: Nếu Claude API lỗi, workflow sẽ sử dụng template caption mặc định.
- **Code mẫu** (nếu cần chỉnh sửa):
  ```javascript
  // Gọi Claude API
  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "x-api-key": $node["Credentials"]["anthropic"]["apiKey"],
      "anthropic-version": "2023-10-01"
    },
    body: JSON.stringify({
      model: "claude-haiku-3-5",
      max_tokens_to_sample: 200,
      messages: [
        { role: "user", content: `Tone: ${$json["Caption Tone"]}\nTitle: ${$json["Title"]}\nDescription: ${$json["Description"]}\nTags: ${$json["Tags"]}\n\nGenerate a caption for Instagram Reels under 2200 characters with a CTA and hashtag block.` }
      ]
    })
  });
  ```

#### **D. Node `Upload to URL Video CDN` (Upload Video)**
- **Configuration**:
  - **URL**: URL CDN công khai (ví dụ: `https://cdn.yourdomain.com/upload`).
  - **Headers**:
    - `Authorization`: `Bearer {{ $node["Credentials"]["uploadToUrl"]["apiKey"] }}` (nếu cần).
  - **Body**: Binary video từ `$node["HTTP Download Video Binary"]["binary"]`.
  - **Lưu ý**:
    - Instagram **không chấp nhận** binary upload trực tiếp. Workflow **phải** push video lên CDN trước.
    - Nếu CDN không hỗ trợ, thay thế bằng **Google Drive** hoặc **AWS S3**.

#### **E. Node `Wait for Approval` (Approval Gate)**
- **Configuration**:
  - **Resume URL**: Sẽ được tạo tự động. **Không cần chỉnh**.
  - **Email Preview**:
    - **Người nhận**: `$node["Credentials"]["approver"]["email"]`.
    - **Nội dung**: Gồm caption AI, video preview, và 2 button **Approve**/**Reject**.
  - **Lưu ý**:
    - **Không có timeout**: Workflow sẽ chờ mãi cho đến khi người approve click button.
    - **URL approve/reject** sẽ được gửi trong email.

#### **F. Node `HTTP Poll Container Status` (Check Encoding Status)**
- **Configuration**:
  - **URL**: `https://graph.instagram.com/{container_id}?fields=status_code`
  - **Headers**:
    - `Authorization`: `Bearer {{ $node["Credentials"]["ig"]["accessToken"] }}`
  - **Wait Time**: 20 giây giữa mỗi poll (để Instagram có thời gian xử lý).
  - **Max Retry**: 15 lần (nếu quá 15 lần `IN_PROGRESS`, workflow sẽ đánh dấu **Failed**).

#### **G. Node `IF Approved` (Decision Gate)**
- **Logic**:
  - Nếu `action=approve` → Tiến hành đăng Reels.
  - Nếu `action=reject` → Cập nhật Notion thành **Rejected** và thông báo Discord.

#### **H. Node `IG Publish Reel` (Publish to Instagram)**
- **Configuration**:
  - **URL**: `https://graph.instagram.com/v19.0/{ig_user_id}/media_publish`
  - **Body**:
    ```json
    {
      "creation_id": "{{$json["container_id"]}}",
      "caption": "{{$json["caption"]}}",
      "share_to_feed": true
    }
    ```
  - **Lưu ý**:
    - Instagram **không cho phép** đăng lại nếu container đã bị xóa. Đảm bảo `container_id` hợp lệ.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Submit một yêu cầu từ form → Kiểm tra email preview → Click **Approve**.
   - Theo dõi log trong n8n để xác nhận Reels đã đăng thành công.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì Discord, sử dụng **Slack Webhook** để thông báo nhanh hơn.
   - Ví dụ: `https://hooks.slack.com/services/XXX` với payload:
     ```json
     {
       "text": "🎥 Reel mới đăng: {{$json["permalink"]}}",
       "attachments": [{
         "title": "{{$json["Title"]}}",
         "title_link": "{{$json["permalink"]}}",
         "image_url": "{{$json["cover_url"]}}"
       }]
     }
     ```

2. **Lưu log tất cả hoạt động**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại:
     - Thời gian submit.
     - Trạng thái (Chờ, Đang xử lý, Thất bại, Đã đăng).
     - Người approve/reject.

3. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **n8n Scheduler** để chạy workflow định kỳ (ví dụ: Chủ Nhật sáng) và gửi email tổng hợp:
     - Số Reels đăng thành công/thất bại.
     - Link top 3 Reels có engagement cao nhất.

4. **Tối ưu CDN**:
   - Sử dụng **Cloudflare Stream** hoặc **Mux** để giảm thời gian upload và tăng tốc độ loading.

5. **Xử lý lỗi Claude API**:
   - Nếu Claude API down, thay thế bằng **GPT-4** (OpenAI) hoặc **Bard** (Google).
   - Thêm node **Retry** với delay 5 phút trước khi fallback.

6. **Quản lý token Instagram tự động**:
   - Sử dụng **n8n Cron** để renew token Instagram trước khi hết hạn (60 ngày).
   - Ví dụ: Workflow nhỏ để check token và refresh nếu `expires_in < 24h`.
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý content Instagram, đồng thời **đảm bảo chất lượng** với:
✅ **Caption AI thông minh** (Claude).
✅ **Kiểm duyệt tự động** (email + button approve).
✅ **Quản lý trạng thái** trên Notion.
✅ **Báo cáo tự động** lên Discord/Slack.

**Hành động ngay**:
1. **Chuẩn bị credentials** (env vars) và **CDN công khai**.
2. **Import workflow** và **test với video mẫu**.
3. **Chia sẻ form submit** với team để bắt đầu tự động hóa!

:::success[💡 **LƯU Ý CUỐI CUNG**]
- **Instagram Graph API có giới hạn**: Nếu đăng nhiều Reels, cần **upgrade plan** hoặc chia nhỏ batch.
- **Claude API có rate limit**: Nếu submit nhiều yêu cầu, thêm delay giữa các request.
- **VPS Self-hosted** là lựa chọn tốt nhất để workflow hoạt động 24/7. 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N** (giảm tới 39%).
:::

---
**Bạn đã sẵn sàng tự động hóa content Instagram chưa?** 🚀