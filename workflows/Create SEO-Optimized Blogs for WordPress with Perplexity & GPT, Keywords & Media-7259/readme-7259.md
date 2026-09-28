---
title: "🚀 Tự Động Hóa Viết Blog SEO Tối Ưu Hóa WordPress Với AI (Perplexity, GPT, Keywords & Ảnh Bìa) - N8N Workflow"
description: "Workflow này tự động tạo nội dung blog SEO tối ưu cho WordPress, bao gồm viết bài, tìm kiếm từ khóa, tạo ảnh bìa, và quản lý nội dung thông minh bằng AI (Perplexity, OpenAI, LangChain). Giúp các sếp tiết kiệm 80% thời gian viết blog và cải thiện xếp hạng Google."
slug: "tieu-dong-hoa-viet-blog-seo-wordpress-ai-n8n"
tags: [n8n, automation, content-creation, ai, seo, wordpress, perplexity, openai, langchain, no-code]
keywords: [n8n workflow blog seo, tự động hóa viết blog, ai viết bài cho wordpress, seo content automation, perplexity ai, openai chatbot tự động hóa]
---

# 🚀 **Tự Động Hóa Viết Blog SEO Tối Ưu Hóa WordPress Với AI (Perplexity, GPT, Keywords & Ảnh Bìa)**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 80% thời gian viết blog** mà không cần viết một dòng code.
- **Tạo nội dung SEO tối ưu** tự động, từ khóa chính xác, và cấu trúc bài viết chuyên nghiệp.
- **Tạo ảnh bìa đẹp** bằng AI và tích hợp vào bài viết.
- **Quản lý nội dung thông minh** với cơ sở dữ liệu PostgreSQL và WordPress.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không gián đoạn, các sếp nên **self-host n8n** trên một VPS ổn định. Dưới đây là một số gợi ý:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Viết blog chỉ trong vài phút thay vì nhiều giờ.
- **Nội dung SEO tối ưu**: Từ khóa chính xác, cấu trúc bài viết chuyên nghiệp, và nội dung độc đáo.
- **Ảnh bìa tự động**: Sử dụng AI tạo ảnh bìa đẹp và phù hợp với nội dung.
- **Quản lý nội dung thông minh**: Lưu trữ và quản lý bài viết trong PostgreSQL và WordPress.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình hoặc khi có yêu cầu mới.
- **Cải thiện xếp hạng Google**: Nội dung được tối ưu SEO, giúp trang web của các sếp lên top nhanh hơn.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị các tài khoản và thông tin sau:

### **1. Tài khoản và API Keys**
| Dịch vụ/API | Mô tả | Yêu cầu |
|-------------|--------|----------|
| **WordPress** | Để đăng bài viết tự động | API Key từ plugin **WP REST API** hoặc **JWT Authentication** |
| **Perplexity AI** | Dùng để tìm kiếm và phân tích từ khóa | [API Key Perplexity](https://www.perplexity.ai/api) |
| **OpenAI (GPT-4, GPT-3.5)** | Dùng để viết nội dung, tối ưu SEO, và tạo FAQ | [API Key OpenAI](https://platform.openai.com/account/api-keys) |
| **PostgreSQL** | Cơ sở dữ liệu lưu trữ từ khóa, bài viết và dữ liệu SEO | Thông tin kết nối (Host, Port, Database, Username, Password) |
| **GitHub** | Lưu trữ sitemap và bài viết | Token Personal Access (đảm bảo quyền `repo` và `admin:repo_hook`) |
| **Slack** (nếu sử dụng) | Gửi thông báo khi bài viết được tạo hoặc cần phê duyệt | Token Slack và Channel ID |

### **2. Thiết lập cơ sở dữ liệu PostgreSQL**
Workflow sử dụng PostgreSQL để lưu trữ:
- Danh sách từ khóa (primary và secondary keywords).
- Bài viết đã tạo và chưa tạo.
- Dữ liệu SEO (score, intent, size, quality).
- Log bài viết cho liên kết nội bộ.

Các sếp cần tạo các bảng sau (hoặc sử dụng script SQL trong workflow):
```sql
-- Bảng lưu trữ từ khóa
CREATE TABLE keywords (
    id SERIAL PRIMARY KEY,
    keyword TEXT NOT NULL,
    intent TEXT,
    size INT,
    quality INT,
    used BOOLEAN DEFAULT FALSE
);

-- Bảng lưu trữ bài viết
CREATE TABLE blogs (
    id SERIAL PRIMARY KEY,
    title TEXT NOT NULL,
    slug TEXT,
    status TEXT DEFAULT 'draft',
    url TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Bảng lưu trữ bài viết chi tiết
CREATE TABLE blog_details (
    id SERIAL PRIMARY KEY,
    blog_id INT REFERENCES blogs(id),
    intro TEXT,
    content TEXT,
    conclusion TEXT,
    faq TEXT,
    image_url TEXT,
    plan TEXT,
    approval_status TEXT DEFAULT 'pending'
);
```

### **3. Thiết lập WordPress**
- Cài đặt plugin **WP REST API** hoặc **JWT Authentication** để n8n có thể đăng bài tự động.
- Thiết lập **API Key** trong n8n (node **WordPress**).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**.

#### **Bước 1: Tải file JSON**
- Tải workflow từ [n8n.io/workflows/7259](https://n8n.io/workflows/7259) (chọn **Export as JSON**).
- Hoặc copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7259) (nếu link không hoạt động, liên hệ tác giả Paul để lấy file).

#### **Bước 2: Import vào n8n**
1. Mở **n8n Editor** trên trang web hoặc self-hosted.
2. Nhấn **Import** và chọn file JSON.
3. Hoặc nhấn **Create Workflow** → **Import** → Paste JSON.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình các node quan trọng**
Workflow này phức tạp với **100+ nodes**, nhưng các sếp chỉ cần chú ý đến các node sau:

##### **1. Node `Schedule Trigger` (Đặt lịch chạy)**
- **Mục đích**: Chạy workflow định kỳ (ví dụ: hàng ngày hoặc hàng tuần).
- **Cấu hình**:
  - Chọn **Cron** hoặc **Time-based** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - Đặt **Time Zone** phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

##### **2. Node `WordPress` (Đăng bài tự động)**
- **Mô tả**: Node này đăng bài viết lên WordPress.
- **Cấu hình**:
  - **Authentication**: Chọn **JWT** hoặc **Basic Auth**.
  - **API Key**: Điền API Key từ plugin WordPress.
  - **Endpoint**: Chọn `wp/v2/posts` (đăng bài mới) hoặc `wp/v2/posts/{id}` (cập nhật).
  - **Headers**: Thêm `Content-Type: application/json`.

##### **3. Node `Perplexity` (Tìm kiếm từ khóa)**
- **Mô tả**: Sử dụng Perplexity để tìm kiếm từ khóa và phân tích intent.
- **Cấu hình**:
  - **API Key**: Điền vào `Perplexity API Key`.
  - **Prompt**: Cấu hình trong node `Message a model` (ví dụ: `"Tìm kiếm từ khóa SEO cho chủ đề [topic] và trả về intent, size, quality"`).

##### **4. Node `OpenAI` (Viết nội dung)**
- **Mô tả**: Sử dụng GPT-4 hoặc GPT-3.5 để viết:
  - **Intro**, **Content**, **Conclusion**, **FAQ**.
  - **Plan** cho bài viết.
- **Cấu hình**:
  - **Model**: Chọn `gpt-4` hoặc `gpt-3.5-turbo`.
  - **Temperature**: Đặt từ `0.7` đến `1.0` (để nội dung sáng tạo).
  - **Prompt**: Cấu hình trong node `Preliminary Plan` và các node `chainLlm` liên quan.
  - **API Key**: Điền vào `OpenAI API Key`.

##### **5. Node `PostgreSQL` (Lưu trữ dữ liệu)**
- **Mô tả**: Lưu trữ từ khóa, bài viết và dữ liệu SEO.
- **Cấu hình**:
  - **Connection**: Thiết lập kết nối với PostgreSQL.
  - **Query**: Các node như `Insert rows in a table`, `Select rows from a table` cần cấu hình chính xác bảng và cột.
  - **Example**:
    ```json
    {
      "database": "your_database",
      "table": "keywords",
      "values": {
        "keyword": "{{ $json.keyword }}",
        "intent": "{{ $json.intent }}",
        "size": "{{ $json.size }}",
        "quality": "{{ $json.quality }}"
      }
    }
    ```

##### **6. Node `Image Covers2` (Tạo ảnh bìa)**
- **Mô tả**: Sử dụng **HTTP Request** để gọi API tạo ảnh bìa (ví dụ: DALL·E, MidJourney, hoặc API tạo ảnh AI khác).
- **Cấu hình**:
  - **URL**: Điền vào `https://api.example.com/generate-image` (thay thế bằng API thực tế).
  - **Headers**: Thêm `Authorization: Bearer YOUR_API_KEY`.
  - **Body**: Gửi yêu cầu với `prompt` từ nội dung bài viết.
  - **Output**: Lưu URL ảnh vào `image_url` trong PostgreSQL.

##### **7. Node `Slack` (Gửi thông báo)**
- **Mô tả**: Gửi thông báo khi bài viết được tạo hoặc cần phê duyệt.
- **Cấu hình**:
  - **Token**: Điền `xoxb-your-token`.
  - **Channel**: Chọn `#your-channel`.
  - **Message**: Cấu hình tin nhắn như:
    ```json
    {
      "text": "📝 Bài viết mới đã được tạo: {{ $node["Create a post1"].json.title }}",
      "attachments": [
        {
          "title": "Chi tiết",
          "text": "URL: {{ $node["Create a post1"].json.url }}",
          "fields": [
            { "title": "Trạng thái", "value": "{{ $node["wait approval"].json.status }}", "short": true }
          ]
        }
      ]
    }
    ```

##### **8. Node `Agent` (Chọn từ khóa và intent)**
- **Mô tả**: Sử dụng **LangChain Agent** để chọn từ khóa phù hợp và intent.
- **Cấu hình**:
  - **Tools**: Đảm bảo các tool như `Primary keywords`, `Used secondary` được kết nối.
  - **Prompt**: Cấu hình trong node `Choose keywords, Intent, etc`:
    ```json
    {
      "input": "{{ $json.topic }}",
      "tools": [
        {
          "type": "function",
          "function": {
            "name": "get_primary_keywords",
            "description": "Lấy từ khóa chính cho chủ đề."
          }
        }
      ]
    }
    ```

##### **9. Node `GitHub` (Lưu sitemap và bài viết)**
- **Mô tả**: Lưu sitemap và bài viết vào repository GitHub.
- **Cấu hình**:
  - **Token**: Điền `ghp-your-token`.
  - **Repository**: Chọn repo và branch (ví dụ: `main`).
  - **File**: Cấu hình trong node `Edit a file`:
    ```json
    {
      "path": "sitemap.xml",
      "content": "{{ $json.sitemap_content }}",
      "commit_message": "Update sitemap"
    }
    ```

---

### **3. Kích hoạt ⚡️**
#### **Bước 1: Test Run**
1. Chọn **Test Tab** trong n8n Editor.
2. Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
3. Kiểm tra các node quan trọng như:
   - `Preliminary Plan` (AI viết plan).
   - `OpenAI Chat Model` (viết intro, content, conclusion).
   - `WordPress` (đăng bài).
   - `Slack` (thông báo).

#### **Bước 2: Bật Active**
- Sau khi test thành công, chuyển workflow sang **Active**.
- Đặt lịch chạy trong node `Schedule Trigger` (ví dụ: hàng ngày).

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa từ khóa SEO**
- **Sử dụng Perplexity + OpenAI** để phân tích từ khóa chi tiết:
  - Intent: Mục đích của người dùng (ví dụ: mua hàng, tìm hiểu, so sánh).
  - Size: Độ dài bài viết (ví dụ: 1000-1500 từ).
  - Quality: Đánh giá nội dung (A, B, C).
- **Lưu trữ trong PostgreSQL** để theo dõi và cập nhật định kỳ.

### **2. Tích hợp Slack/Telegram cho thông báo**
- **Slack**: Gửi thông báo khi bài viết được tạo hoặc cần phê duyệt.
- **Telegram**: Sử dụng node `httpRequest` để gửi tin nhắn qua Bot Telegram.
  ```json
  {
    "url": "https://api.telegram.org/botYOUR_BOT_TOKEN/sendMessage",
    "method": "POST",
    "body": {
      "chat_id": "YOUR_CHAT_ID",
      "text": "📝 Bài viết mới: {{ $node["Create a post1"].json.title }}"
    }
  }
  ```

### **3. Lưu log hoạt động**
- Sử dụng node `Postgres` để lưu log:
  ```sql
  CREATE TABLE blog_logs (
      id SERIAL PRIMARY KEY,
      blog_id INT REFERENCES blogs(id),
      action TEXT NOT NULL, -- "created", "updated", "failed"
      timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
      details TEXT
  );
  ```
- Cập nhật log trong node `Log blog link for future internal links`.

### **4. T