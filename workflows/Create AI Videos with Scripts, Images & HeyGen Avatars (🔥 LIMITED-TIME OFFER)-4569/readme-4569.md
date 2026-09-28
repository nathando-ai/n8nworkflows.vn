---
title: "🎬 Tự Động Hoà Video AI Từ Script, Ảnh & Avatar HeyGen - Giảm 90% Thời Gian Chỉnh Sửa Video 🚀"
description: "Workflow này tự động tạo video AI chuyên nghiệp từ script, hình ảnh và avatar HeyGen, giúp các sếp tiết kiệm thời gian, nâng cao chất lượng nội dung marketing và tự động hóa quy trình sản xuất video 24/7. Kết hợp OpenAI, Runway ML và Baserow để tối ưu hóa quy trình."
slug: "tieu-dong-hoa-video-ai-HeyGen"
tags: [n8n, automation, AI, video-editing, marketing-automation, HeyGen, OpenAI, RunwayML]
keywords: [tự động hóa video AI, HeyGen n8n, tạo video từ script, tự động hóa marketing, workflow n8n video, AI video generator]
---

# 🎬 **Tự Động Hoà Video AI Từ Script, Ảnh & Avatar HeyGen - Giải Pháp Tiết Kiệm 90% Thời Gian**

## **🔥 Nỗi Đau Của Các Sếp Trong Sản Xuất Video**
Bạn có bao giờ phải:
- **Chỉnh sửa video thủ công** trong giờ phút cuối cùng, khiến nội dung không kịp thời?
- **Tìm kiếm hình ảnh phù hợp** cho mỗi đoạn script, mất thời gian và công sức?
- **Đặt avatar AI** (như HeyGen) cho từng video, nhưng lại phải làm lại từ đầu nếu có thay đổi?
- **Không có cách nào tự động hóa** quy trình từ script đến video hoàn chỉnh?

Workflow này **giải quyết tất cả** những vấn đề trên bằng cách **tự động hóa toàn bộ quy trình tạo video AI** từ script, hình ảnh và avatar HeyGen, giúp các sếp **tiết kiệm thời gian, nâng cao chất lượng và tự động hóa 100%**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian** so với cách làm thủ công.
✅ **Video chuyên nghiệp** với avatar AI (HeyGen) và hiệu ứng động (Runway ML).
✅ **Tự động cập nhật** khi có thay đổi script hoặc hình ảnh.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Kết hợp AI (OpenAI, HeyGen, Runway ML)** để tối ưu hóa chất lượng.
✅ **Lưu trữ và quản lý** video trong Baserow (hoặc cơ sở dữ liệu khác).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản API** của các dịch vụ sau:
   - **OpenAI** (API Key cho ChatGPT/GPT-4).
   - **HeyGen** (API Key để tạo avatar AI).
   - **Runway ML** (API Key để tạo video từ hình ảnh).
   - **Leo AI** (API Key để tạo hình ảnh từ mô tả).
   - **CaptionsAI** (API Key để tự động thêm phụ đề).
   - **Baserow** (hoặc cơ sở dữ liệu khác) để lưu trữ script và video.
2. **Script mẫu** (được viết sẵn trong Baserow hoặc file JSON).
3. **Hình ảnh tham khảo** (nếu sử dụng Leo AI tạo hình ảnh mới).
4. **VPS n8n** (để chạy workflow 24/7).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4569) hoặc copy toàn bộ JSON từ đây.
- Mở **n8n Editor** và chọn **"Import Workflow"** → Dán JSON hoặc tải file `.json`.
- **Không cần chỉnh sửa** nếu chỉ muốn test cơ bản.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **phức tạp** vì kết hợp nhiều API và logic điều kiện. Dưới đây là **các node quan trọng cần cấu hình**:

##### **🔹 Node Webhook (Bắt đầu workflow)**
- **Kiểu:** `webhook`
- **Lưu ý:**
  - Cần **bật Webhook** và chọn **HTTP POST**.
  - **Payload Format:** `JSON`.
  - **Credentials:** Đăng ký một **API Key** trong n8n để bảo mật.

##### **🔹 Node OpenAI (Tạo Script & Improve Prompt)**
- **Kiểu:** `lmChatOpenAi` (2 node: `OpenAI Chat Model` và `OpenAI Chat Model1`)
- **Cấu hình:**
  - **Model:** Chọn `gpt-4` hoặc `gpt-3.5-turbo` (tuỳ budget).
  - **API Key:** Điền **API Key OpenAI** từ tài khoản.
  - **Prompt:** Cần **cấu trúc rõ ràng** để AI sinh script hoặc cải thiện prompt.
  - **Lưu ý:**
    - Nếu script không phù hợp, **node `Leo - Improve Prompt`** sẽ tự động sửa lại.
    - **Test run** với một script mẫu trước khi chạy toàn bộ.

##### **🔹 Node HeyGen (Tạo Avatar AI)**
- **Kiểu:** `httpRequest` (node `HeyGen`)
- **Cấu hình:**
  - **URL:** `https://api.heygen.com/v1/avatar/videos`
  - **Headers:**
    - `Authorization: Bearer {API_KEY_HEYGEN}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "script": "{{$json["script"]}}",
      "avatar_id": "{{$json["avatar_id"]}}",
      "voice_id": "default",
      "background_type": "solid"
    }
    ```
  - **Lưu ý:**
    - **Cần có `avatar_id`** (đăng ký trên HeyGen).
    - **Test với script ngắn** trước để tránh phí không cần thiết.

##### **🔹 Node Runway ML (Tạo Video từ Hình Ảnh)**
- **Kiểu:** `httpRequest` (node `Runway - Create Video`)
- **Cấu hình:**
  - **URL:** `https://api.runwayml.com/v1/video/generate`
  - **Headers:**
    - `Authorization: Bearer {API_KEY_RUNWAY}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "prompt": "{{$json["prompt"]}}",
      "negative_prompt": "",
      "width": 1920,
      "height": 1080,
      "steps": 50
    }
    ```
  - **Lưu ý:**
    - **Hình ảnh đầu vào** phải được tạo bởi **Leo AI** (node `Leo - Generate Image`).
    - **Chờ node `Wait2`** để video hoàn thành trước khi lấy kết quả.

##### **🔹 Node Leo AI (Tạo Hình Ảnh từ Mô Tả)**
- **Kiểu:** `httpRequest` (node `Leo - Generate Image`)
- **Cấu hình:**
  - **URL:** `https://api.leo.ai/v1/images/generate`
  - **Headers:**
    - `Authorization: Bearer {API_KEY_LEO}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "prompt": "{{$json["prompt"]}}",
      "negative_prompt": "",
      "width": 1024,
      "height": 1024
    }
    ```
  - **Lưu ý:**
    - **Test với prompt đơn giản** trước (ví dụ: "A person wearing a suit in a modern office").

##### **🔹 Node Baserow (Lưu Trữ Script & Video)**
- **Kiểu:** `baserow`
- **Cấu hình:**
  - **URL:** `https://your-baserow-instance.com/api/v1/`
  - **Headers:**
    - `Authorization: Token {API_KEY_BASEROW}`
  - **Table:** Chọn **bảng script** hoặc **bảng video**.
  - **Lưu ý:**
    - **Cần tạo 2 bảng:**
      1. **Script Table** (để lưu script và hình ảnh tham khảo).
      2. **Video Table** (để lưu link video hoàn thành).

##### **🔹 Node Switch & If (Logic Điều Kiện)**
- **Node `Switch ScriptType`** và **node `If`** quyết định **cách xử lý script**:
  - Nếu script **không phù hợp**, workflow sẽ **sử dụng LLM để cải thiện** (`Leo - Improve Prompt`).
  - Nếu **avatar HeyGen thất bại**, workflow sẽ **quay lại node `Basic LLM Chain`** để sửa script.
- **Lưu ý:**
  - **Không chỉnh sửa** logic này nếu không hiểu rõ, để tránh lỗi.

##### **🔹 Node Wait (Đợi Video Hoàn Thành)**
- **Node `Wait1`, `Wait2`, `Wait4`, `Wait6`** là **thời gian chờ** để:
  - HeyGen hoàn thành avatar.
  - Runway ML hoàn thành video.
  - Leo AI hoàn thành hình ảnh.
- **Cấu hình:**
  - **Thời gian chờ:** Đặt từ **30s đến 5 phút** (tuỳ thuộc vào API).

##### **🔹 Node Execute Workflow (Chạy Workflow Con)**
- **Node `Execute Workflow2`, `Execute Workflow3`, `Execute Workflow4`** chạy **workflow con** để:
  - **Xử lý lỗi** (ví dụ: nếu HeyGen thất bại).
  - **Cập nhật Baserow** khi video hoàn thành.
- **Lưu ý:**
  - **Cần tạo workflow con** tương ứng (nếu chưa có, workflow gốc sẽ **ngừng**).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ liệu Mẫu**
   - Tạo **một script mẫu** trong Baserow.
   - Gửi **request Webhook** (ví dụ: từ Postman hoặc Slack).
   - **Kiểm tra log** để xem workflow có chạy đúng không.

2. **Bật Active Workflow**
   - Sau khi test thành công, **bật chế độ Active**.
   - **Monitor** trong **n8n Dashboard** để theo dõi lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối với Slack/Telegram**
   - Thêm **node Slack/Telegram** vào cuối workflow để **báo cáo kết quả** (thành công/thất bại).
   - Ví dụ:
     ```json
     {
       "text": "🎬 Video đã tạo thành công! Link: {{$json["video_url"]}}"
     }
     ```

2. **Lưu Log Lỗi**
   - Thêm **node `Set`** sau mỗi **Execute Workflow Error** để **lưu lỗi** vào Baserow.
   - Cấu trúc log:
     ```json
     {
       "error_type": "{{$json["error_type"]}}",
       "error_message": "{{$json["error_message"]}}",
       "script_id": "{{$json["script_id"]}}",
       "timestamp": "{{$now}}"
     }
     ```

3. **Tự Động Cập Nhật Script**
   - Sử dụng **node `Execute Workflow Trigger`** để **chạy lại workflow** khi có **thay đổi script** trong Baserow.
   - Cấu hình:
     - **Trigger:** `Baserow` (khi record trong bảng script được cập nhật).

4. **Tối Ưu Hóa Chi Phí API**
   - **Limit số lần gọi API** (ví dụ: chỉ chạy HeyGen nếu script dài > 100 từ).
   - Sử dụng **node `If`** để kiểm tra điều kiện trước khi gọi API.

5. **Tạo Video Chuyển Scenes**
   - Nếu script có **nhiều scene**, sử dụng **node `Split In Batches`** để **chia nhỏ** và xử lý từng scene riêng.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy marketing** thay vì **chỉnh sửa video thủ công**. Với **AI + tự động hóa**, các sếp có thể:
✔ **Tạo video chuyên nghiệp** chỉ trong vài phút.
✔ **Cập nhật nội dung** một cách nhanh chóng.
✔ **Tiết kiệm chi phí** so với việc thuê nhà sản xuất video.

**🚀 Hãy áp dụng ngay workflow này và xem sự khác biệt!**
Nếu có vấn đề, **hãy để lại comment** dưới đây hoặc liên hệ với cộng đồng n8n để hỗ trợ.

---
**🔥 LIMITED-TIME OFFER:** Nếu bạn muốn **tối ưu hóa workflow này**, hãy liên hệ với **Adam Crafts** (tác giả) để có **các tips nâng cao**! 🚀