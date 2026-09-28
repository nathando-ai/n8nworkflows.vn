---
title: "🤖 Tự Động Hóa Trích Xuất & Đăng Tin Việc Làm Từ URL Sang WordPress Với AI (N8N + OpenAI + Supabase)"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp HR trích xuất thông tin tuyển dụng từ URL, xử lý bằng AI, lưu trữ vector, và đăng bài lên WordPress chỉ trong vài giây. Giảm thời gian thủ công từ 30 phút xuống 0!"
slug: "tieu-dong-hoa-trich-xuat-dang-tin-viec-lam"
tags: [n8n, automation, hr, ai-multimodal, openai, wordpress, telegram-notification]
keywords: [n8n workflow tuyển dụng, tự động hóa tin việc làm, trích xuất dữ liệu từ URL, AI OpenAI cho HR, đăng bài WordPress tự động, Supabase vector database]
---

# 🚀 **Tự Động Hóa Trích Xuất & Đăng Tin Việc Làm Từ URL Sang WordPress (AI + N8N)**

### **Nỗi Đau Của Các Sếp HR**
Hàng ngày, các sếp HR phải:
- **Tìm kiếm và sao chép** thông tin tuyển dụng từ email, Telegram, hoặc website.
- **Chỉnh sửa thủ công** định dạng, loại bỏ thông tin không cần thiết (logo, footer).
- **Đăng bài lên WordPress** một cách mệt mỏi, dễ bị lỗi.
- **Lo lắng về độ chính xác** của dữ liệu, mất thời gian kiểm tra lại.

**Kết quả?** Thời gian làm việc tăng gấp 3-5 lần, chất lượng bài đăng không đồng nhất, và AI chưa được tận dụng.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Chính xác 100%** nhờ AI OpenAI trích xuất thông tin chính xác từ URL.
- **Cá nhân hóa logo** cho mỗi bài đăng (tự động tải từ URL và upload lên WordPress).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Lưu trữ dữ liệu** trong Supabase Vector Store để tra cứu nhanh chóng.
- **Thông báo tự động** trên Telegram khi có lỗi hoặc thành công.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ file mẫu và dữ liệu đầu vào).
2. **API Key OpenAI** (để sử dụng AI trích xuất dữ liệu).
3. **Supabase Project** (để lưu trữ vector embeddings).
4. **Tài khoản WordPress** (để đăng bài tự động).
5. **Bot Telegram** (để nhận thông báo lỗi/thành công).
6. **File mẫu tin việc làm** (để workflow biết định dạng đầu vào).
7. **Danh sách loại việc làm và danh mục** (để AI phân loại chính xác).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [n8n.io](https://n8n.io/workflows/6518).
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Chọn file JSON vừa tải.
- **Bước 3:** Chọn **"Import"** để hoàn tất.

:::note[LƯU Ý]
- **Không copy/paste JSON trực tiếp** từ trang web, vì có thể mất cấu trúc. **Tải file JSON** là cách an toàn nhất.
- Nếu workflow quá lớn, có thể **tách thành nhiều phần** và import từng phần.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials (Tài Khoản API)**
Các sếp cần **đăng ký và điền thông tin** cho các credentials sau trong **n8n Credentials Manager**:
| **Credentials**       | **Cách Đăng Ký**                                                                 | **Tham Số Cần Điền**                          |
|-----------------------|---------------------------------------------------------------------------------|-----------------------------------------------|
| `googleDriveOAuth2Api` | [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) | Client ID, Client Secret, Refresh Token       |
| `openAiApi`           | [OpenAI API](https://platform.openai.com/account/api-keys)                     | API Key                                       |
| `supabaseApi`         | [Supabase Project](https://supabase.com/dashboard)                            | URL Project, Service Role Key                 |
| `wordpressApi`        | [WordPress REST API](https://developer.wordpress.org/rest-api/)                 | Username, Password, Site URL                   |
| `telegramApi`         | [BotFather Telegram](https://core.telegram.org/bots/api)                       | Token Bot                                      |

#### **B. Cấu Hình Node Quan Trọng**
##### **1. Node `📥 New Job Link via Telegram` (Trigger)**
- **Chức năng:** Nhận URL tin việc làm từ Telegram.
- **Cách cấu hình:**
  - Mở node này → Chọn **"Add"** → Điền **Chat ID** của bot Telegram.
  - **Lưu ý:** Nếu không có bot Telegram, các sếp cần tạo một bot mới từ [BotFather](https://t.me/BotFather).

##### **2. Node `🧮 Map Job Type & Category IDs` (Code)**
- **Chức năng:** AI phân loại loại việc làm và danh mục.
- **Cách chỉnh sửa:**
  - **Double click** vào node → Sửa code để phù hợp với danh sách loại việc làm của công ty.
  - **Dữ liệu mẫu:**
    ```json
    {
      "jobTypes": {
        "Full-time": 1,
        "Part-time": 2,
        "Internship": 3
      },
      "categories": {
        "Software Engineer": 101,
        "Marketing": 102,
        "HR": 103
      }
    }
    ```

##### **3. Node `📚 Load Valid Job Types & Categories` (Set)**
- **Chức năng:** Đưa danh sách loại việc làm và danh mục vào workflow.
- **Cách điền:**
  - **Tham số `data`:** Điền JSON tương tự như trên (dùng dữ liệu của công ty).

##### **4. Node `📥 Download Company Logo` & `☁️ Upload Logo to WordPress` (HTTP Request)**
- **Chức năng:** Tải logo từ URL và upload lên WordPress.
- **Cách cấu hình:**
  - **Node `Download Company Logo`:**
    - Tham số `url`: `{{$node["🔧 Prepare URL for Extraction"].json()["logoUrl"]}}`
  - **Node `Upload Logo to WordPress`:**
    - **Endpoint:** `{{$node["🚀 Publish to Your web"].json()["url"]}}/wp-json/wp/v2/media`
    - **Headers:**
      ```json
      {
        "Authorization": "Basic {{$credentials.wordpressApi.base64Auth}}",
        "Content-Type": "multipart/form-data"
      }
      ```

##### **5. Node `📦 Format Final Job Post Data` (Set)**
- **Chức năng:** Chuẩn hóa dữ liệu trước khi đăng bài.
- **Cách chỉnh sửa:**
  - **Tham số `data`:** Đảm bảo tất cả trường (`title`, `content`, `logo`, `jobType`, `category`) đều có giá trị.
  - **Dữ liệu mẫu:**
    ```json
    {
      "title": "{{$node["🧮 Map Job Type & Category IDs"].json()["title"]}}",
      "content": "{{$node["📥 Download Company Logo"].json()["content"]}}",
      "logo": "{{$node["☁️ Upload Logo to WordPress"].json()["id"]}}",
      "jobType": "{{$node["🧮 Map Job Type & Category IDs"].json()["jobType"]}}",
      "category": "{{$node["🧮 Map Job Type & Category IDs"].json()["category"]}}"
    }
    ```

##### **6. Node `✅ All Fields Available?` (If)**
- **Chức năng:** Kiểm tra xem tất cả trường dữ liệu có đầy đủ không.
- **Cách cấu hình:**
  - **Condition:** `{{$node["📦 Format Final Job Post Data"].json()["title"] !== null && ...}}` (kiểm tra tất cả trường).

##### **7. Node `🚀 Publish to Your web` (HTTP Request)**
- **Chức năng:** Đăng bài lên WordPress.
- **Cách cấu hình:**
  - **Endpoint:** `{{$node["🚀 Publish to Your web"].json()["url"]}}/wp-json/wp/v2/posts`
  - **Headers:**
    ```json
    {
      "Authorization": "Basic {{$credentials.wordpressApi.base64Auth}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body:**
    ```json
    {
      "title": "{{$node["📦 Format Final Job Post Data"].json()["title"]}}",
      "content": "{{$node["📦 Format Final Job Post Data"].json()["content"]}}",
      "featured_media": "{{$node["📦 Format Final Job Post Data"].json()["logo"]}}",
      "categories": ["{{$node["📦 Format Final Job Post Data"].json()["category"]}}"]
    }
    ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run Dữ Liệu Mẫu:**
   - Gửi URL tin việc làm từ Telegram vào bot.
   - Kiểm tra **Telegram Notification** để xem workflow có chạy đúng không.
2. **Bật Active Workflow:**
   - Chọn **"Active"** ở góc trên bên phải của canvas.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp với Slack thay vì Telegram**
- Thay node `telegram` bằng `slack` (n8n-nodes-base.slack).
- **Cách cấu hình:**
  - Đăng ký bot Slack tại [API Slack](https://api.slack.com/apps).
  - Thêm credentials `slackApi` trong n8n.

### **2. Lưu Log Lỗi vào Google Sheets**
- Thêm node `googleSheets` để ghi log lỗi.
- **Cách cấu hình:**
  - Tạo sheet mới trong Google Drive.
  - Thêm node `googleSheets` sau node `Error Trigger` để ghi dữ liệu lỗi.

### **3. Gửi Báo Cáo Định Kỳ về Số Lượng Tin Việc Làm Đăng**
- Sử dụng node `set` + `googleSheets` để cập nhật thống kê hàng ngày.
- **Cách thực hiện:**
  - Tạo node `set` với dữ liệu:
    ```json
    {
      "date": "{{$node["Wait"].date}}",
      "totalPosts": "{{$node["📊 Did Publish Succeed?1"].json()["count"]}}"
    }
    ```
  - Sau đó append vào Google Sheets.

### **4. Sử Dụng AI ChatGPT để Chỉnh Sửa Nội Dung**
- Thêm node `openAi` để AI tự động chỉnh sửa nội dung bài đăng.
- **Prompt mẫu:**
  ```json
  {
    "prompt": "Rewrite this job post to be more engaging and professional:\n{{$node["📦 Format Final Job Post Data"].json()["content"]}}",
    "model": "gpt-3.5-turbo"
  }
  ```

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR để tập trung vào công việc chiến lược hơn. Bằng cách tự động hóa trích xuất, xử lý AI, và đăng bài lên WordPress, công ty của các sếp sẽ:
✅ **Tiết kiệm 90% thời gian** so với cách làm thủ công.
✅ **Đảm bảo chất lượng cao** nhờ AI OpenAI.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** theo hướng dẫn.
3. **Test với URL mẫu** và bắt đầu tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và đánh giá nếu bài hướng dẫn hữu ích!** 🚀