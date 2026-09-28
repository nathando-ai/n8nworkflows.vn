---
title: "🚀 Tự Động Hoạt Động Tạo Bài Blog Tự Động Từ Video YouTube Với AI Mistral & Gemini (Không Cần Code)"
description: "Workflow này tự động chuyển đổi video YouTube thành bài blog SEO-friendly với nội dung chi tiết, hình ảnh AI sinh, và metadata tối ưu. Giúp các sếp tiết kiệm 80% thời gian viết blog mà vẫn giữ chất lượng cao."
slug: "tu-dong-hoat-dong-tao-blog-tu-video-youtube-voi-ai"
tags: [n8n, automation, content-creation, ai-generative, wordpress, seo, mistral-ai, gemini]
keywords: [n8n workflow blog từ video, tự động hóa nội dung AI, tạo bài blog SEO, Mistral AI cho blogger, Gemini image generation, tự động hóa YouTube thành bài viết]
---

# 🚀 **Tự Động Hoạt Động Tạo Bài Blog SEO-Friendly Từ Video YouTube (Với AI Mistral & Gemini)**

### **Giải pháp cho các sếp blogger, marketer, hoặc team nội dung:**
Bạn đã từng phải **quét video YouTube, viết script, tìm kiếm từ khóa, tạo hình ảnh, và xuất bản bài blog** trong vòng 3-5 tiếng? Workflow này sẽ **tự động hóa toàn bộ quy trình** chỉ trong vài phút, với nội dung **SEO-optimized**, hình ảnh **AI sinh** và metadata **cá nhân hóa** cho từng video.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** viết blog (từ 5 tiếng xuống còn 10 phút).
✅ **Nội dung SEO-optimized** với từ khóa, cấu trúc bài viết, và metadata tự động.
✅ **Hình ảnh AI sinh** (Gemini/Mistral) phù hợp với nội dung bài viết.
✅ **Cập nhật tự động** khi có video mới trên kênh YouTube.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✅ **Duy trì chất lượng cao** với AI có khả năng hiểu ngữ cảnh.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| Dịch vụ/API | Mô tả | Làm thế nào để lấy? |
|-------------|--------|----------------------|
| **WordPress** | Để xuất bản bài blog tự động | Tạo API Key từ **Settings → Network → API** (hoặc dùng plugin **WP REST API**) |
| **Google Sheets** | Lưu trữ danh sách video đã xử lý | Tạo **API Key** từ [Google Cloud Console](https://console.cloud.google.com/) |
| **Ollama** | Model AI Mistral/Llama3 (cài đặt local) | Cài đặt từ [ollama.ai](https://ollama.ai/) và chạy `ollama pull mistral` |
| **Tavily** | Tìm kiếm từ khóa & thông tin liên quan | Đăng ký miễn phí tại [Tavily](https://tavily.com/) và lấy API Key |
| **YouTube RSS Feed** | Theo dõi video mới trên kênh | URL RSS của kênh (ví dụ: `https://www.youtube.com/feeds/videos.xml?channel_id=CHANNEL_ID`) |

### **2. Cấu hình WordPress**
- **Plugin yêu cầu**: `WP REST API` (nếu chưa có).
- **Cấu hình CORS** (nếu xuất hiện lỗi `CORS blocked`):
  ```bash
  # Thêm vào file wp-config.php
  define('WP_JSON_PRETTY_PRINT', true);
  define('WP_JSON_FORCE_PRETTY_PRINT', true);
  ```

### **3. Cài đặt Ollama (Local AI)**
Các sếp cần cài **Ollama** và tải model Mistral/Llama3:
```bash
# Cài Ollama (Linux/macOS)
curl -fsSL https://ollama.ai/install.sh | sh

# Tải model Mistral
ollama pull mistral
```

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8190](https://n8n.io/workflows/8190) (chọn **Export JSON**).
2. Trong **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name** (ví dụ: `YouTube-to-Blog-AI`) và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** và dán toàn bộ mã JSON từ [n8n.io/workflows/8190](https://n8n.io/workflows/8190).

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Trigger (Bắt đầu workflow)**
- **Node `Check Youtube Channel` (RSS Feed Trigger)**:
  - Điền **URL RSS** của kênh YouTube (ví dụ: `https://www.youtube.com/feeds/videos.xml?channel_id=UCXXXXXXXXXX`).
  - **Lọc video mới**: Chọn `published > 1 day ago` để chỉ lấy video mới nhất.

- **Node `Schedule Trigger` (Nếu muốn chạy định kỳ)**:
  - Thiết lập **thời gian chạy** (ví dụ: 09:00 AM hàng ngày).
  - **Lưu ý**: Nếu dùng trigger RSS, **không cần kích hoạt Schedule Trigger**.

#### **B. Cấu hình WordPress**
- **Node `Create a post` & `Update a post`**:
  - **Authentication**: Chọn **OAuth 2.0** và điền:
    - **Client ID** & **Client Secret** từ WordPress REST API.
    - **Base URL**: `https://domain.com/wp-json/wp/v2/posts`.
  - **Headers**:
    - `Content-Type: application/json`
    - `Authorization: Bearer YOUR_API_KEY` (nếu dùng API Key thay OAuth).

#### **C. Cấu hình Google Sheets**
- **Node `Get row(s) in sheet`**:
  - Chọn **Google Sheets** → Tạo **API Key** từ [Google Cloud Console](https://console.cloud.google.com/).
  - **Spreadsheet ID**: Lấy từ URL Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Tên sheet chứa danh sách video đã xử lý (ví dụ: `Processed_Videos`).

#### **D. Cấu hình Ollama (AI Model)**
- **Tất cả node `Ollama Chat Model*`**:
  - **Model**: Chọn `mistral` (hoặc `llama3`).
  - **Prompt Template**: Các sếp **không cần chỉnh sửa** (workflow đã tối ưu sẵn).
  - **Parameters**:
    - `temperature`: 0.7 (để kết quả logic hơn).
    - `top_p`: 0.9 (đảm bảo đa dạng).

#### **E. Cấu hình Tavily (Tìm kiếm từ khóa)**
- **Node `Search in Tavily` & `Extract in Tavily`**:
  - Điền **API Key** từ Tavily.
  - **Query**: Workflow sẽ tự động lấy từ tiêu đề video.

#### **F. Cấu hình Gemini Image Generation (Nếu dùng)**
- **Node `Resize Image` & `Upload Image To WP`**:
  - **Lưu ý**: Workflow hiện không tích hợp trực tiếp Gemini, nhưng các sếp có thể **thêm node `editImage`** với API của **Gemini API** hoặc **DALL·E** (OpenAI).
  - **Alternative**: Sử dụng **Nano 🍌** (node `httpRequest`) để gọi API hình ảnh từ bên thứ ba.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với video mẫu:
   - Chọn **Run Workflow** và nhập **URL video YouTube** vào node `Check Youtube Channel`.
   - Kiểm tra **log** để đảm bảo không có lỗi.

2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Lưu ý**: Nếu dùng **RSS Trigger**, workflow sẽ chạy tự động khi có video mới.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu SEO thêm**
- **Thêm node `SEO Analysis`** (ví dụ: sử dụng **Ahrefs API** hoặc **SurferSEO**) để kiểm tra từ khóa.
- **Cập nhật metadata** sau khi bài viết được tạo:
  ```javascript
  // Thêm vào node `Code` (nếu cần)
  $json["meta"]["description"] = "Tóm tắt bài viết từ video YouTube...";
  ```

### **2. Gửi thông báo khi bài viết hoàn thành**
- **Thêm node `Slack` hoặc `Email`** để thông báo khi bài viết được xuất bản:
  ```json
  {
    "operation": "sendMessage",
    "text": "🚀 Bài blog mới đã xuất bản: {{ $json.title }}",
    "channel": "#content-updates"
  }
  ```

### **3. Lưu log vào Google Sheets**
- **Thêm node `googleSheets`** để ghi lịch sử:
  - **Action**: `Create Row`.
  - **Values**:
    ```json
    {
      "video_url": "{{ $json.video_url }}",
      "post_url": "{{ $json.post_url }}",
      "status": "Published",
      "date": "{{ $json.date }}"
    }
    ```

### **4. Chỉnh sửa hình ảnh tự động**
- **Thêm node `editImage`** với API **Canva API** hoặc **Remove.bg** để:
  - Cắt nền hình ảnh.
  - Thêm watermark.
  - Đổi kích thước phù hợp với WordPress.

### **5. Chạy workflow cho nhiều kênh YouTube**
- **Sử dụng node `Set`** để lưu danh sách kênh:
  ```json
  {
    "channels": [
      "UCXXXXXXXXXX", // Kênh 1
      "UCYYYYYYYYYY"  // Kênh 2
    ]
  }
  ```
- **Loop qua từng kênh** bằng node `Loop` (nếu cần).

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp blogger, marketer, và team nội dung để tập trung vào **strategy** thay vì **quét video và viết blog**. Với **AI Mistral & Gemini**, nội dung sẽ **ngôn ngữ tự nhiên, SEO-friendly**, và **hình ảnh đẹp mắt** mà không cần kỹ năng code.

**Bắt đầu ngay hôm nay!**
1. Import workflow.
2. Cấu hình API và trigger.
3. **Bật Active** và để AI làm việc cho bạn.

🔗 **Tải workflow nguyên bản**: [n8n.io/workflows/8190](https://n8n.io/workflows/8190)
💡 **Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy ổn định 24/7!

---
**#TựĐộngHóaBlog #AIContentCreation #N8NWorkflow #SEOAutomation**