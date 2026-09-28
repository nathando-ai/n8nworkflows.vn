---
title: "🚀 Tự Động Hóa Tạo Bài Blog Từ Tin Tức Đến Xuất Bản Với Gemini, Ideogram & Slack"
description: "Workflow này tự động tra cứu xu hướng thị trường, tạo nội dung blog SEO-optimized bằng AI Gemini, sinh ảnh bìa bằng Ideogram, xuất bản lên CMS (Supabase) và thông báo trên Slack - hoàn toàn không cần code. Giúp các sếp tiết kiệm 8+ giờ/ngày viết blog và duy trì nội dung liên tục."
slug: "tieu-dong-hoa-tao-bai-blog-tu-tin-tuc-den-xuat-ban"
tags: [n8n, automation, no-code, ai-content, seo, supabase, slack, gemini, replicate, ideogram]
keywords: [n8n workflow tự động hóa blog, tạo bài viết blog bằng AI, tự động hóa nội dung marketing, SEO blog tự động, Gemini API, Ideogram AI, xuất bản blog tự động, Slack notification]
---

# **🚀 Tự Động Hóa Tạo Bài Blog Từ Tin Tức Đến Xuất Bản Với Gemini, Ideogram & Slack**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp**
Các sếp marketing, CEO hoặc content manager thường phải đối mặt với những thách thức sau khi viết blog thủ công:
- **Tốn thời gian**: Viết một bài blog chất lượng từ 0 mất **3-5 giờ**, còn viết hàng tuần thì **8+ giờ/ngày** chỉ dành cho nội dung.
- **Không đồng bộ xu hướng**: Nội dung dễ trở nên lỗi thời khi không cập nhật liên tục từ tin tức mới nhất.
- **Chất lượng không nhất quán**: AI có thể tạo nội dung nhanh, nhưng **sạch sẽ, SEO-optimized và chuyên nghiệp** vẫn là vấn đề.
- **Quá trình xuất bản phức tạp**: Sau khi viết xong, phải **chỉnh sửa, thêm ảnh, xuất bản và chia sẻ** trên nhiều kênh - tốn thêm thời gian.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Tra cứu xu hướng** từ tin tức mới nhất (NewsAPI)
✅ **Tạo đề tài blog trending** bằng Gemini AI
✅ **Viết bài blog SEO-optimized** (1200-1500 từ) với cấu trúc Markdown
✅ **Sinh ảnh bìa** bằng Ideogram (Replicate)
✅ **Xuất bản tự động** lên Supabase (hoặc CMS tùy chỉnh)
✅ **Thông báo trên Slack** khi bài viết hoàn tất

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và an toàn dữ liệu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/ngày**: Không cần viết blog thủ công, tự động hóa toàn bộ quy trình từ tra cứu đến xuất bản.
- **Nội dung SEO-optimized**: Bài viết được AI viết với **từ khóa, meta description, và cấu trúc Markdown** chuẩn.
- **Ảnh bìa tự động**: Sinh ảnh chuyên nghiệp từ mô tả bài viết bằng Ideogram.
- **Xuất bản liên tục**: Workflow chạy **hàng ngày tự động** (cài đặt thời gian tùy chọn).
- **Duy trì nội dung mới**: Luôn cập nhật từ tin tức mới nhất, tránh nội dung lỗi thời.
- **Thông báo tức thời**: Nhận tin nhắn Slack khi bài viết xuất bản, không cần kiểm tra thủ công.
- **Chỉnh sửa dễ dàng**: Thay đổi **ngành nghề, mô hình AI, hoặc CMS xuất bản** chỉ với vài cú click.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - [NewsAPI](https://newsapi.org/) (đăng ký miễn phí, free tier 100 requests/ngày)
   - [Google Gemini API](https://makersuite.google.com/) (API Key cho Gemini 2.5)
   - [Replicate](https://replicate.com/) (Bearer Token cho Ideogram v3 Turbo)
   - [Supabase](https://supabase.com/) (Header Auth cho endpoint `/functions/v1/blog-api`)
   - [Slack API Token](https://api.slack.com/apps) (đăng ký Slack App với quyền `chat:write`)

2. **CMS hoặc Backend**:
   - **Supabase** (đã có sẵn template endpoint) **hoặc** bất kỳ CMS nào hỗ trợ API (WordPress, Ghost, Webflow...).

3. **Thời gian**:
   - Workflow chạy **~1-2 phút/lần**, tùy vào thời gian sinh ảnh Ideogram (~10-20s).
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9658) hoặc copy/paste JSON từ trang này.
- Trong **n8n Editor**, chọn **"Import"** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Kích hoạt workflow** sau khi import xong.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình các node sau:

##### **🌐 Fetch Industry Trends (HTTP Request)**
- **Mục đích**: Tra cứu **10 tin tức mới nhất** về ngành nghề (mặc định là "AI automation SaaS").
- **Cấu hình**:
  - **Credentials**: Chọn `httpQueryAuth` (đã tạo từ NewsAPI Key).
  - **URL**: `https://newsapi.org/v2/everything`
  - **Query Parameters**:
    ```json
    {
      "q": "AI automation SaaS",  // Thay đổi thành ngành nghề của bạn (ví dụ: "finance AI", "healthcare automation")
      "pageSize": 10,
      "sortBy": "publishedAt",
      "apiKey": "{{$httpQueryAuth.apiKey}}"
    }
    ```
  - **Lưu ý**:
    - Free tier của NewsAPI chỉ cho phép **100 request/ngày**, nên không chạy quá nhiều lần/ngày.
    - Nếu muốn tra cứu ngành khác, thay đổi giá trị `q`.

##### **🤖 Message a model (Google Gemini) – Tạo Đề Tài Blog**
- **Mục đích**: Gemini phân tích tin tức và **tạo 1 đề tài blog trending** dưới dạng JSON.
- **Cấu hình**:
  - **Credentials**: Chọn `googlePalmApi` (API Key Gemini).
  - **Prompt mẫu** (có thể chỉnh sửa):
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "Analyze the latest news about 'AI automation SaaS' and suggest **one trending blog topic** in JSON format. The output should include:\n\n- title: A catchy, SEO-friendly title\n- description: A short summary (100-150 words)\n- keywords: 5-7 relevant keywords\n- image_prompt: A description for generating an image (1-2 sentences)\n\nExample format:\n```json\n{\n  \"title\": \"How AI Automation is Transforming SaaS in 2024\",\n  \"description\": \"Explore the latest trends in AI-driven automation for SaaS businesses...\",\n  \"keywords\": [\"AI automation\", \"SaaS trends\", \"machine learning\", \"no-code\"],\n  \"image_prompt\": \"A futuristic city with AI robots and SaaS dashboard\"\n}\n```\n\nUse the news articles provided as context."
            }
          ]
        }
      ],
      "model": "gemini-2.5-flash"  // Mô hình nhanh, phù hợp cho đề tài blog
    }
    ```
  - **Lưu ý**:
    - Thay đổi `q` trong prompt để phù hợp với ngành nghề của bạn.
    - Output phải là **JSON strict** để node tiếp theo xử lý dễ dàng.

##### **📝 Message a model1 (Google Gemini) – Viết Bài Blog**
- **Mục đích**: Gemini viết **bài blog SEO-optimized** (1200-1500 từ) với cấu trúc Markdown.
- **Cấu hình**:
  - **Credentials**: Giống node trước (`googlePalmApi`).
  - **Prompt mẫu** (chỉnh sửa theo ngành):
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "Write a **1200-1500 word blog post** in Markdown format about the topic:\n\nTitle: {{title}}\nDescription: {{description}}\n\nInstructions:\n1. Start with a **hook** (question, statistic, or bold statement).\n2. Include **subheadings (H2/H3)** for readability.\n3. Add **bullet points** for key takeaways.\n4. Use **internal/external links** where relevant.\n5. End with a **strong CTA** (e.g., \"Ready to automate your workflow? Try [Product Name] today!\").\n6. **SEO Optimization**:\n   - Meta title: \"{{title}}\" (max 60 chars)\n   - Meta description: \"{{description}}\" (max 160 chars)\n   - Excerpt: First 2-3 sentences of the blog\n   - Keywords: {{keywords}}\n\nOutput format (JSON):\n```json\n{\n  \"title\": \"{{title}}\",\n  \"slug\": \"{{slug}}\",  // Auto-generated from title\n  \"excerpt\": \"...\",\n  \"content\": \"\"\"Markdown content here\"\"\",\n  \"keywords\": {{keywords}},\n  \"image_prompt\": \"{{image_prompt}}\"\n}\n```\n\nUse the news articles and topic provided as context."
            }
          ]
        }
      ],
      "model": "gemini-2.5-pro"  // Mô hình chất lượng cao cho bài viết dài
    }
    ```
  - **Lưu ý**:
    - Output có thể chứa **Markdown hoặc text noise**, node **Code in JavaScript** sẽ xử lý sạch.

##### **🧹 Code in JavaScript – Xử Lý Output AI**
- **Mục đích**: **Làm sạch và chuẩn hóa** JSON từ Gemini (xóa Markdown thừa, sửa lỗi cú pháp).
- **Lưu ý**:
  - **Không cần chỉnh sửa** trừ khi thay đổi cấu trúc output của Gemini.
  - Code đã được tối ưu để **bảo vệ chống lỗi** (ví dụ: nếu Gemini trả về text thay vì JSON, node vẫn tạo fallback).

##### **🖼️ HTTP Request (Replicate – Generate Image)**
- **Mục đích**: Sinh **ảnh bìa blog** từ mô tả (`image_prompt`) bằng Ideogram (Replicate).
- **Cấu hình**:
  - **Credentials**: Chọn `httpBearerAuth` (Bearer Token Replicate).
  - **URL**:
    ```
    https://api.replicate.com/v1/predictions
    ```
  - **Headers**:
    ```json
    {
      "Authorization": "{{$httpBearerAuth.token}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "version": "337e484d856f45799e7e6f370509a8e88218e03b6061e013b87754f9f2522e9b",
      "input": {
        "prompt": "{{image_prompt}}",
        "width": 1024,
        "height": 1024,
        "model": "ideogram-ai/ideogram-v3-turbo"
      }
    }
    ```
  - **Lưu ý**:
    - Thay đổi `model` nếu muốn dùng mô hình khác (ví dụ: Stable Diffusion).
    - Kích thước ảnh mặc định là **1024x1024**, có thể điều chỉnh.

##### **⏱️ Wait & HTTP Request1 (Replicate Polling)**
- **Mục đích**: **Chờ ảnh sinh xong** và lấy URL download.
- **Cấu hình**:
  - **Wait**: 20s (thời gian sinh ảnh Ideogram ~10-20s).
  - **HTTP Request1**: Polling trạng thái sinh ảnh bằng `prediction ID`.
  - **URL**:
    ```
    https://api.replicate.com/v1/predictions/{{prediction_id}}
    ```
  - **Lưu ý**:
    - Nếu ảnh chưa sẵn sàng, workflow **loop lại** qua node `Wait` và `HTTP Request1`.

##### **✅ If – Kiểm Tra Trạng Thái Ảnh**
- **Mục đích**: **Xác nhận ảnh đã sinh xong** trước khi xuất bản.
- **Cấu hình**:
  - **Condition**: `status === "succeeded"`.
  - **Lưu ý**:
    - Nếu ảnh sinh thất bại, workflow **dừng lại** và không xuất bản bài viết.

##### **🧩 Edit Fields (Set Node)**
- **Mục đích**: **Kết hợp** tiêu đề, nội dung, và URL ảnh thành **JSON chuẩn** cho xuất bản.
- **Cấu hình**:
  - **Fields**:
    ```json
    {
      "title": "{{title}}",
      "slug": "{{slug}}",
      "excerpt": "{{excerpt}}",
      "content": "{{content}}",
      "image_url": "{{image_url}}",
      "published": true
    }
    ```
  - **Lưu ý**:
    - Thêm trường `category` hoặc `author` nếu cần.

##### **🚀 Publish to Supabase (HTTP Request)**
- **Mục đích**: **Xuất bản bài viết** lên Supabase (hoặc CMS tùy chỉnh).
- **Cấu hình**:
  - **Credentials**: Chọn `httpHeaderAuth` (Header Auth Supabase).
  - **URL**:
    ```
    https://your-project.supabase.co/functions/v1/blog-api
    ```
  - **Headers**:
    ```json
    {
      "Authorization": "{{$httpHeaderAuth.token}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "title": "{{title}}",
      "slug": "{{slug