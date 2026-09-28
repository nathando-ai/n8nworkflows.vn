---
title: "🎬 **Tự Động Hóa Xây Dựng Video TikTok Siêu Nhanh với GPT-4o-mini & Sisif.ai - Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn tạo video TikTok từ ý tưởng đến xuất bản, giảm thời gian từ 2h xuống 5 phút với AI GPT-4o-mini và Sisif.ai. Phù hợp cho marketer, content creator và doanh nghiệp cần nội dung video nhanh chóng."
slug: "tu-dong-hoa-tao-video-tiktok-voi-gpt-4o-mini"
tags: [n8n, automation, tiktok, ai-marketing, gpt-4o-mini, sisif-ai]
keywords: [tự động hóa video tiktok, n8n workflow tiktok, tạo video tiktok bằng ai, gpt-4o-mini tự động hóa, sisif ai n8n]
---

# 🚀 **Tự Động Hóa Xây Dựng Video TikTok Siêu Nhanh với GPT-4o-mini & Sisif.ai**

## **💥 Nỗi Đau Của Các Sếp Trong Tạo Video TikTok**
Bạn đã bao giờ phải:
- **Tốn 2-3 tiếng** để viết kịch bản, chọn nhạc, chỉnh sửa và xuất video?
- **Chỉnh sửa lại và lại** vì nội dung không thu hút người xem?
- **Phải học kỹ năng chỉnh sửa** để tạo video chuyên nghiệp?
- **Không biết ý tưởng nào sẽ "fire"** và thu hút nhiều người xem?

**Workflow này giải quyết tất cả!** Với sự kết hợp giữa **GPT-4o-mini** (AI tạo nội dung sáng tạo) và **Sisif.ai** (tạo video tự động), bạn chỉ cần **nhập một ý tưởng**, workflow sẽ:
✅ **Tự động viết kịch bản** phù hợp với xu hướng TikTok.
✅ **Chọn nhạc và hiệu ứng** phù hợp.
✅ **Chỉnh sửa và xuất video** trong vòng **5 phút**.
✅ **Cập nhật trạng thái** cho bạn biết video đã sẵn sàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **2h thành 5 phút** cho mỗi video.
- **Nội dung chuyên nghiệp**: AI GPT-4o-mini viết kịch bản **phù hợp với xu hướng TikTok**.
- **Chỉnh sửa tự động**: Sisif.ai **chọn nhạc, hiệu ứng và xuất video** một cách chuyên nghiệp.
- **Hoạt động liên tục**: Workflow **chạy tự động** theo lịch trình (ví dụ: tạo 1 video/ngày).
- **Tối ưu SEO**: Nội dung được **tối ưu hóa** cho thuật ngữ tìm kiếm TikTok.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Sisif.ai** (đăng ký tại [sisif.ai](https://sisif.ai/))
✔ **API Key Sisif.ai** (lấy từ **Settings > API Keys**)
✔ **Tài khoản OpenAI** (đăng ký tại [openai.com](https://openai.com/))
✔ **API Key OpenAI** (lấy từ **Settings > API Keys**)
✔ **Mã Bearer Auth Sisif.ai** (thường là `Bearer <API_KEY>`)
✔ **Tham số cấu hình Sisif.ai** (ví dụ: `video_type`, `template_id`)

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần kỹ năng code** để sử dụng workflow này.
- **Workflow chạy trên n8n self-hosted** để đảm bảo **tốc độ và ổn định**.
- **Nếu sử dụng n8n Cloud**, có thể gặp giới hạn về **tốc độ API và thời gian chạy**.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4969](https://n8n.io/workflows/4969) (chọn **Download JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n Cloud).
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/4969](https://n8n.io/workflows/4969).
2. **Mở n8n Editor** và nhấp vào **"Import"** → **"Paste JSON"**.
3. **Chọn "Import"** để workflow xuất hiện.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Schedule Trigger (Khởi động theo lịch)**
- **Cấu hình**:
  - **Schedule**: Chọn **Cron expression** phù hợp (ví dụ: `0 0 * * *` để chạy **mỗi ngày lẻ**).
  - **Timezone**: Chọn **Việt Nam (Asia/Ho Chi Minh)**.
- **Lưu ý**:
  - Nếu muốn **tạo video theo yêu cầu**, thay thế bằng **Webhook** (node `n8n-nodes-base.webhook`).

#### **🔹 Node 2 & 4: Create Sisif Video & Check Video Status (API Sisif.ai)**
- **Credentials**:
  - **httpBearerAuth**: Điền `Bearer <API_KEY_SISIF>`.
  - **httpHeaderAuth**: Điền `Authorization: Bearer <API_KEY_SISIF>`.
- **Parameters**:
  - **URL Sisif API**:
    - **Create Video**: `https://api.sisif.ai/v1/videos`
    - **Check Status**: `https://api.sisif.ai/v1/videos/{video_id}`
  - **Headers**:
    - `Content-Type: application/json`
    - `Authorization: Bearer <API_KEY_SISIF>`
  - **Body (Create Video)**:
    ```json
    {
      "template_id": "your_template_id",  // Lấy từ Sisif.ai
      "video_type": "short",              // Loại video (short, long)
      "script": "{{ $node["Idea creator"].json.output.text }}"  // Kịch bản từ AI
    }
    ```
  - **Body (Check Status)**:
    ```json
    {}
    ```

#### **🔹 Node 3: Wait 10s (Đợi video xử lý)**
- **Thời gian đợi**: **10 giây** (có thể điều chỉnh lên **30s** nếu Sisif.ai chậm).

#### **🔹 Node 5: Video Ready? (Kiểm tra trạng thái video)**
- **Cấu hình If Node**:
  - **If**: `{{ $json["status"] === "completed" }}`
  - **Else**: `{{ $json["status"] !== "completed" }}`

#### **🔹 Node 6: Prepare Final Data (Chuẩn bị dữ liệu cuối cùng)**
- **Function Code (JavaScript)**:
  ```javascript
  // Kiểm tra video đã hoàn thành và trả về dữ liệu cuối cùng
  return {
    video_url: $node["Check Video Status"].json.output.data.url,
    video_id: $node["Check Video Status"].json.output.data.id,
    status: $node["Check Video Status"].json.output.data.status,
    created_at: $node["Check Video Status"].json.output.data.created_at
  };
  ```

#### **🔹 Node 7: Structured Output Parser (Định dạng dữ liệu)**
- **Cấu hình**:
  - **Schema**:
    ```json
    {
      "type": "object",
      "properties": {
        "video_url": { "type": "string" },
        "video_id": { "type": "string" },
        "status": { "type": "string" },
        "created_at": { "type": "string" }
      },
      "required": ["video_url", "video_id"]
    }
    ```

#### **🔹 Node 8 & 9: Idea Creator & OpenAI Chat Model (Tạo ý tưởng video)**
- **Credentials**:
  - **openAiApi**: Điền **API Key OpenAI**.
- **Prompt (Idea Creator)**:
  ```plaintext
  Tôi muốn tạo một video TikTok về "{{ $input["topic"] }}". Hãy viết một kịch bản ngắn (5-10 dòng) với:
  1. Mở đầu hấp dẫn (hook).
  2. Nội dung chính (giải quyết vấn đề của người xem).
  3. Kết thúc với CTA (call-to-action).
  Đảm bảo kịch bản phù hợp với xu hướng TikTok hiện tại.
  ```
- **Model**: **gpt-4o-mini** (nhanh và hiệu quả).
- **Parameters**:
  - **Temperature**: `0.7` (để kết quả sáng tạo).
  - **Max Tokens**: `200`.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Điền **topic** vào **Schedule Trigger** (ví dụ: `"Cách học tiếng Anh hiệu quả"`).
   - Chạy **Test Execution** để kiểm tra workflow.
2. **Bật Active**:
   - Nhấp vào **Active** trên canvas để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram để thông báo**
- **Thêm node Slack/Telegram** sau **Prepare Final Data** để gửi thông báo khi video hoàn thành.
- **Dữ liệu gửi**:
  ```json
  {
    "text": `🎬 Video đã hoàn thành!\nURL: {{ $node["Prepare Final Data"].json.output.video_url }}`,
    "blocks": [
      {
        "type": "section",
        "text": { "type": "mrkdwn", "text": `Video TikTok mới:\n🔗 <{{ $node["Prepare Final Data"].json.output.video_url }}|Xem video>` }
      }
    ]
  }
  ```

### **🔹 Lưu log vào Google Sheets/Notion**
- **Thêm node Google Sheets** sau **Prepare Final Data** để lưu lịch sử video.
- **Dữ liệu lưu**:
  ```json
  {
    "topic": "{{ $input["topic"] }}",
    "video_url": "{{ $node["Prepare Final Data"].json.output.video_url }}",
    "status": "{{ $node["Prepare Final Data"].json.output.status }}",
    "created_at": "{{ $node["Prepare Final Data"].json.output.created_at }}"
  }
  ```

### **🔹 Tối ưu hóa với nhiều ý tưởng**
- **Thêm node `n8n-nodes-base.set`** trước **Idea Creator** để truyền **nhiều topic** vào một lần.
- **Ví dụ**:
  ```json
  [
    "Cách học tiếng Anh hiệu quả",
    "Top 5 app học tiếng Anh miễn phí",
    "Lỗi thường gặp khi học tiếng Anh"
  ]
  ```

### **🔹 Sử dụng Webhook thay cho Schedule**
- Nếu muốn **tạo video theo yêu cầu**, thay thế **Schedule Trigger** bằng **Webhook**.
- **Cấu hình Webhook**:
  - **Method**: `POST`
  - **URL**: `https://your-n8n-url/webhook/your-webhook-name`
  - **Body**:
    ```json
    {
      "topic": "Nhập chủ đề video ở đây"
    }
    ```

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì **chỉnh sửa video thủ công**. Với **GPT-4o-mini** và **Sisif.ai**, bạn có thể:
✅ **Tạo video TikTok chuyên nghiệp** trong **5 phút**.
✅ **Tối ưu hóa nội dung** theo xu hướng.
✅ **Hoạt động tự động** theo lịch trình.

**Hãy thử ngay và xem kết quả!** 🚀
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với **Vlad Temian** (tác giả workflow) qua [n8n.io](https://n8n.io/).

---
**💡 BẮN CHƯA CÓ VPS CHO N8N?**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với **mã giảm giá VPSN8N** (giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao).