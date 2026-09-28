---
title: "🚀 Tự Động Hóa Lên Kế Hoạch & Đăng Bài Instagram 100% AI (OpenAI + Content Calendar) - Không Cần Code"
description: "Workflow này tự động hóa toàn bộ quy trình lên kế hoạch nội dung Instagram từ tháng, tuần đến bài đăng hàng ngày, sử dụng OpenAI để tạo hình ảnh và văn bản, đồng thời quản lý sự phê duyệt qua email. Giúp các sếp tiết kiệm 20+ giờ/tháng và đảm bảo nội dung chuyên nghiệp, đồng bộ."
slug: "tieu-dong-hoa-len-ke-hoach-dang-bai-instagram-ai"
tags: [n8n, automation, marketing, ai, instagram, openai, content-calendar, no-code, supabase, gmail]
keywords: [tự động hóa instagram, lên kế hoạch nội dung ai, đăng bài instagram tự động, openai cho marketing, workflow n8n marketing, quản lý nội dung instagram]
---

# 🚀 **Tự Động Hóa Lên Kế Hoạch & Đăng Bài Instagram Với AI (OpenAI + Content Calendar)**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 20+ giờ/tháng** lên kế hoạch nội dung Instagram.
- **Tạo hình ảnh & văn bản chuyên nghiệp** bằng AI (OpenAI).
- **Quản lý sự phê duyệt** qua email tự động.
- **Đăng bài đồng bộ** trên Instagram (Facebook Graph API).
- **Lưu trữ & theo dõi lịch sử** trên Supabase (không cần cơ sở dữ liệu phức tạp).

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: AI tự động lên kế hoạch từ tháng, tuần đến bài đăng hàng ngày.
✅ **Nội dung chuyên nghiệp**: OpenAI tạo văn bản và hình ảnh theo yêu cầu cụ thể.
✅ **Quản lý phê duyệt tự động**: Email tự động gửi yêu cầu phê duyệt và lưu kết quả.
✅ **Đăng bài đồng bộ**: Hỗ trợ đăng bài trên Instagram (Facebook Graph API).
✅ **Lưu trữ an toàn**: Dữ liệu kế hoạch và bài đăng được lưu trên Supabase.
✅ **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tài khoản n8n Self-hosted** (khuyến nghị cài trên VPS để ổn định 24/7).
- **Tài khoản Gmail** (để gửi yêu cầu phê duyệt kế hoạch).
- **API Key OpenAI** (để sử dụng AI tạo hình ảnh và văn bản).
- **Tài khoản Facebook Business Manager** (để đăng bài trên Instagram).
- **Tài khoản Supabase** (để lưu trữ kế hoạch và bài đăng).
- **Tài khoản Instagram Business** (để đăng bài tự động).
- **Email cá nhân** (để nhận thông báo phê duyệt).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4060](https://n8n.io/workflows/4060) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **45 node** và được chia thành **3 phần chính**:
- **Lên kế hoạch nội dung** (tháng, tuần, bài đăng).
- **Tạo hình ảnh & văn bản bằng AI** (OpenAI).
- **Quản lý phê duyệt & đăng bài** (Gmail + Facebook Graph API).

##### **A. Cấu hình cơ bản (Set)**
- **Node "Configure workflow"**: Điền thông tin chung như:
  - **Tên tài khoản Instagram**.
  - **Thời gian đăng bài mặc định** (ví dụ: 9h sáng).
  - **Ngôn ngữ mặc định** (Việt Nam/English).
  - **Tên email phê duyệt** (để gửi yêu cầu phê duyệt).

##### **B. Kết nối với Gmail (Quản lý phê duyệt)**
- **Node "Get instructions on the monthly plan"**, **"Weekly plan approval"**, **"Get approval for the post"**:
  - **Chọn credentials Gmail** trong n8n.
  - **Cấu hình email**:
    - **Người gửi**: Email cá nhân của bạn.
    - **Người nhận**: Email của người phê duyệt (ví dụ: `marketing@doanhnghiep.com`).
    - **Tiêu đề email**: `"Phê duyệt kế hoạch nội dung Instagram - [Thời gian]"`.
    - **Nội dung email**: Sử dụng **dữ liệu động** từ workflow (ví dụ: `{{ $json["monthly_plan"] }}`).

##### **C. Kết nối với OpenAI (Tạo hình ảnh & văn bản)**
- **Node "OpenAI Chat Model"**:
  - **Điền API Key OpenAI** (mua trên [openai.com](https://openai.com)).
  - **Cấu hình Prompt**:
    ```json
    {
      "role": "user",
      "content": "Tạo một bài viết Instagram về chủ đề {{ $json["topic"] }} với:
        - Văn bản: {{ $json["content_requirements"] }}
        - Hình ảnh: Một hình ảnh đẹp, chuyên nghiệp, phù hợp với chủ đề, kích thước 1080x1080px.
        - Kết cấu: 1 tiêu đề hấp dẫn, 2-3 đoạn văn bản, 1 call-to-action."
    }
    ```
  - **Node "Generate image with OpenAI"**:
    - Sử dụng **DALL·E** (nếu có API Key DALL·E) hoặc **Stable Diffusion** (nếu không).
    - **Cấu hình URL API**:
      ```
      https://api.openai.com/v1/images/generations
      ```
    - **Headers**:
      ```json
      {
        "Authorization": "Bearer {{ $json["openai_api_key"] }}",
        "Content-Type": "application/json"
      }
      ```

##### **D. Kết nối với Supabase (Lưu trữ kế hoạch)**
- **Node "Get monthly plan"**, **"Save monthly plan"**, **"Save weekly plan"**:
  - **Cấu hình Supabase**:
    - **URL**: `https://[your-project-ref].supabase.co`
    - **Key**: `your-supabase-key`
    - **Database**: Chọn bảng `content_plans`.
  - **Cấu trúc dữ liệu mẫu**:
    ```json
    {
      "id": "{{ $node["Generate unique id"].json() }}",
      "type": "monthly",
      "content": "{{ $json["monthly_plan"] }}",
      "status": "pending",
      "created_at": "{{ $node["Date/Time"].json() }}"
    }
    ```

##### **E. Kết nối với Facebook Graph API (Đăng bài)**
- **Node "Facebook Graph API"**:
  - **Cấu hình OAuth 2.0**:
    - **Client ID & Secret**: Mua trên [Facebook for Developers](https://developers.facebook.com/).
    - **Page ID**: ID của tài khoản Instagram Business.
  - **Cấu hình payload đăng bài**:
    ```json
    {
      "message": "{{ $json["post_content"] }}",
      "caption": "{{ $json["post_caption"] }}",
      "image_url": "{{ $json["image_url"] }}"
    }
    ```

##### **F. Kết nối với Instagram (Upload hình ảnh)**
- **Node "Upload image to Supabase"**:
  - **URL**: `https://[your-project-ref].supabase.co/storage/v1/object/public/instagram_posts/{{ $json["filename"] }}`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{ $json["supabase_key"] }}",
      "apikey": "{{ $json["supabase_key"] }}"
    }
    ```

---
#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **"Test workflow"** và điền thông tin mẫu (ví dụ: chủ đề "Cách tự động hóa marketing").
   - Kiểm tra các bước:
     - AI tạo văn bản và hình ảnh.
     - Email phê duyệt được gửi.
     - Bài đăng được lưu trên Supabase.
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển trạng thái từ **"Inactive"** sang **"Active"**.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết nối với Slack/Telegram**: Thông báo khi bài đăng được phê duyệt hoặc có yêu cầu chỉnh sửa.
  ```json
  // Ví dụ cấu hình Slack Webhook
  {
    "url": "https://hooks.slack.com/services/[YOUR_WEBHOOK_URL]",
    "payload": {
      "text": "📢 Bài đăng đã được phê duyệt: {{ $json["post_content"] }}",
      "attachments": [{
        "image_url": "{{ $json["image_url"] }}"
      }]
    }
  }
  ```
- **Lưu log hoạt động**: Sử dụng **Sticky Note** để ghi lại lịch sử phê duyệt và chỉnh sửa.
- **Báo cáo định kỳ**: Tạo một workflow riêng để gửi báo cáo tuần/month về số bài đăng, tương tác, và kế hoạch tiếp theo.
- **Tích hợp với Notion/Google Sheets**: Lưu kế hoạch nội dung vào Notion thay vì Supabase.
- **Sử dụng AI để phân tích sentiment**: Dùng **LangChain** để đánh giá phản hồi từ người dùng và điều chỉnh kế hoạch.
:::

---
### **📌 Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp trong việc lên kế hoạch và quản lý nội dung Instagram. Bằng cách kết hợp **AI (OpenAI)**, **quản lý phê duyệt tự động (Gmail)**, và **đăng bài đồng bộ (Facebook Graph API)**, các sếp có thể:
✔ **Tạo nội dung chuyên nghiệp** mà không cần thiết kế.
✔ **Quản lý quy trình phê duyệt** một cách minh bạch.
✔ **Đăng bài tự động** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Cài n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test và bật Active** để bắt đầu tự động hóa!

---
:::note[💡 LƯU Ý CUỐI CÙNG]
- **N8n Self-hosted là bắt buộc** để workflow hoạt động ổn định.
- **API Key OpenAI** cần có để AI tạo hình ảnh và văn bản.
- **Facebook Graph API** yêu cầu tài khoản Business Manager.
- **Supabase** miễn phí cho dự án nhỏ, nhưng các sếp nên mua gói Pro nếu lưu lượng lớn.
:::

---
👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow](https://n8n.io/workflows/4060) và cài đặt n8n trên VPS. 🚀