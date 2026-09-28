---
title: "🎬 **Tự Động Hóa Sáng Tạo Video UGC (User-Generated Content) với Gemini Images + SORA 2 – Không Cần Code!**"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo video quảng cáo sản phẩm chất lượng cao từ mô tả văn bản, sử dụng AI Gemini (hình ảnh) + SORA 2 (video), lưu trữ trên Google Drive và theo dõi trên Google Sheets. Giúp tiết kiệm thời gian lên đến 90% so với cách làm thủ công!"
slug: "tieu-dong-hoa-sang-tao-video-ugc-gemini-sora-2"
tags: [n8n, automation, content-creation, ai-multimodal, google-drive, google-sheets, sorasai, gemini-ai]
keywords: [tự động hóa video quảng cáo, gemini images sorasai, tạo video từ mô tả, n8n workflow ai, lưu trữ video google drive, theo dõi video google sheets]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video UGC Chất Lượng Cao với Gemini + SORA 2**

### **🔥 Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Hiện nay, việc tạo video quảng cáo (UGC) cho sản phẩm thủ công là một công việc **mệt mỏi, tốn thời gian và đòi hỏi kỹ năng chuyên môn cao**. Các sếp thường phải:
- **Tìm kiếm và chọn hình ảnh phù hợp** từ nhiều nguồn khác nhau.
- **Chỉnh sửa video** với phần mềm phức tạp như Premiere Pro hoặc CapCut.
- **Đợi lâu** khi chờ AI tạo video hoàn chỉnh.
- **Quên theo dõi tiến trình** và không biết video đã hoàn tất chưa.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tạo video từ mô tả văn bản** (không cần kỹ năng thiết kế).
✅ **Sử dụng AI Gemini (Google) để tạo hình ảnh sản phẩm** và **SORA 2 (OpenAI) để tạo video động**.
✅ **Lưu video tự động lên Google Drive** và **ghi log vào Google Sheets** để theo dõi.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
- **Video chất lượng cao, chuyên nghiệp** như do nhà thiết kế tạo ra.
- **Theo dõi toàn bộ quá trình** trên Google Sheets (tên sản phẩm, URL video, trạng thái, thời gian hoàn thành).
- **Lưu trữ an toàn** tất cả video trên Google Drive, dễ dàng chia sẻ cho team.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
- **Google Sheets OAuth 2.0** (để ghi log video).
- **Google Drive OAuth 2.0** (để lưu video MP4).
- **Gemini API Key** (để tạo hình ảnh sản phẩm).
- **OpenAI API Key** (để sử dụng SORA 2 tạo video).

#### **2. Google Sheets & Google Drive**
- **Tạo một bảng Google Sheets** để lưu log video (cấu trúc mẫu sẽ được hướng dẫn).
- **Tạo một folder Google Drive** để lưu video MP4 (cấu trúc: `UGC_Videos/[Tên sản phẩm]`).

#### **3. Hệ Thống n8n Self-Hosted**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```bash
# Cách 1: Import từ file JSON
1. Tải workflow từ [n8n.io/workflows/10053](https://n8n.io/workflows/10053).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON tải xuống.

# Cách 2: Copy/Paste JSON
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/10053](https://n8n.io/workflows/10053).
2. Trên n8n Editor, nhấn **Import** > **Paste JSON**.
```

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **10 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Webhook (Nhận yêu cầu tạo video)**
- **Path:** `create-ugc-video` (không thay đổi).
- **HTTP Method:** `POST`.
- **Credentials:** Không cần (sẽ nhận dữ liệu từ API key truyền vào body request).

##### **🔹 Node 2 & 3: Nano Banana + Extract Image (Tạo hình ảnh với Gemini)**
- **Nano Banana (HTTP Request):**
  - **URL:** `https://generativelab.cloud.google.com/api/gemini/v1beta/models/gemini-pro-vision:generateContent`
  - **Headers:**
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer {{ $json["gemini_api_key"] }}"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "{{ $json["product_description"] }}"
            }
          ]
        }
      ]
    }
    ```
- **Extract Image (Code Node):**
  - **JavaScript:**
    ```javascript
    // Lấy dữ liệu base64 từ response Gemini
    const base64Image = $input.all()[0].json.content[0].parts[0].inlineData.data;
    return { imageBase64: base64Image };
    ```

##### **🔹 Node 4 & 5: SORA 2 + Get Video (Tạo video động)**
- **SORA 2 (HTTP Request):**
  - **URL:** `https://api.sorasai.com/v1/video/generate`
  - **Headers:**
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer {{ $json["openai_api_key"] }}"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "prompt": "{{ $json["video_prompt"] }}",
      "image": "{{ $previousOutput.imageBase64 }}"
    }
    ```
- **Get Video (HTTP Request):**
  - **URL:** `https://api.sorasai.com/v1/video/status/{{ $json["video_id"] }}`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer {{ $json["openai_api_key"] }}"
    }
    ```

##### **🔹 Node 6: Video Complete? (Kiểm tra trạng thái)**
- **Condition:**
  - **If:** `{{ $json.status }} === "completed"`
  - **Else:** `{{ $json.status }} !== "completed"`

##### **🔹 Node 7: Wait & Retry (Đợi video hoàn tất)**
- **Thời gian chờ:** `60000` (1 phút).
- **Lặp lại** cho đến khi video hoàn tất.

##### **🔹 Node 8: Add to Google Sheets (Ghi log)**
- **Sheet Name:** `UGC_Video_Logs` (các sếp tạo trước).
- **Range:** `A1` (đầu tiên).
- **Dữ liệu ghi:**
  ```json
  {
    "product": "{{ $json["product_name"] }}",
    "video_url": "{{ $json["video_url"] }}",
    "status": "{{ $json.status }}",
    "timestamp": "{{ $json.timestamp }}"
  }
  ```

##### **🔹 Node 9: Download Video File (Tải video từ SORA)**
- **URL:** `https://api.sorasai.com/v1/video/download/{{ $json["video_id"] }}`
- **Headers:**
  ```json
  {
    "Authorization": "Bearer {{ $json["openai_api_key"] }}"
  }
  ```

##### **🔹 Node 10: Upload file (Lưu video lên Google Drive)**
- **File:** `{{ $json["video_file"] }}`
- **Folder:** `UGC_Videos/{{ $json["product_name"] }}`
- **Tên file:** `{{ $json["product_name"] }}_video.mp4`

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Gửi một request POST đến `https://[your-n8n-domain]/create-ugc-video` với body:
     ```json
     {
       "product_name": "Sản phẩm mới của tôi",
       "product_description": "Một sản phẩm đẹp mắt, chất lượng cao, phù hợp với thị trường Việt Nam",
       "video_prompt": "Một video quảng cáo sản phẩm 15 giây, hiệu ứng động mạnh, âm nhạc background nhẹ nhàng",
       "gemini_api_key": "your-gemini-api-key",
       "openai_api_key": "your-openai-api-key"
     }
     ```
2. **Chờ workflow hoàn tất** (thường từ 2-5 phút).
3. **Kiểm tra Google Drive** để xem video đã được lưu chưa.
4. **Kiểm tra Google Sheets** để xem log video.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**3 Ý Tưởng Mở Rộng**]
1. **Kết nối với Slack/Telegram:**
   - Thêm node **Slack/Telegram** để thông báo khi video hoàn tất.
   - Ví dụ: `Video {{ $json["product_name"] }} đã hoàn tất! Link: {{ $json["video_url"] }}`

2. **Lưu log vào Firebase/Database:**
   - Thay vì Google Sheets, các sếp có thể lưu log vào **Firebase** hoặc **MongoDB** để dễ dàng truy xuất.

3. **Tự động chia sẻ video lên YouTube/TikTok:**
   - Sử dụng node **YouTube API** hoặc **TikTok API** để tự động upload video sau khi hoàn tất.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing muốn **tạo video UGC chất lượng cao mà không cần kỹ năng thiết kế**. Với chỉ **một request POST**, workflow sẽ tự động:
✔ Tạo hình ảnh sản phẩm với **Gemini AI**.
✔ Tạo video động với **SORA 2**.
✔ Lưu video lên **Google Drive**.
✔ Ghi log vào **Google Sheets**.

**Hãy áp dụng ngay và tiết kiệm thời gian cho team của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản từ n8n.io](https://n8n.io/workflows/10053)**
**💬 Có thắc mắc? Hãy để lại comment bên dưới!**