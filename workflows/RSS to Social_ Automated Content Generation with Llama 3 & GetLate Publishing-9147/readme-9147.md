---
title: "🚀 Tự Động Hóa Sáng Tạo Nội Dung AI + Đăng Bài LinkedIn & Bluesky Miễn Chi Phí (RSS → AI → Social)"
description: "Workflow này tự động lấy bài viết từ RSS, sử dụng Llama 3.3-70B của Groq tạo nội dung cá nhân hóa cho LinkedIn & Bluesky, tự động sinh ảnh AI và đăng bài theo lịch trình. Giúp các sếp tiết kiệm 10+ giờ/tuần, tăng tần suất đăng bài 5x mà không cần viết thủ công."
slug: "tu-dong-hoa-sang-tao-noi-dung-ai-den-linkedin-bluesky"
tags: [n8n, automation, content-creation, ai, linkedin, bluesky, llm, groq, airtable, rss]
keywords: [n8n workflow tự động hóa nội dung, tự động đăng bài linkedin bluesky bằng ai, llm content generation, groq llama 3.3, tự động hóa marketing digital]
---

# 🚀 **Tự Động Hóa Sáng Tạo Nội Dung AI + Đăng Bài LinkedIn & Bluesky (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
- **"Tôi phải viết hàng chục bài đăng mỗi tuần, nhưng lại không có thời gian để nghiên cứu và cá nhân hóa nội dung."**
- **"LinkedIn và Bluesky yêu cầu nội dung độc đáo, nhưng viết thủ công lại tốn quá nhiều thời gian."**
- **"Không biết cách tự động hóa quá trình này mà vẫn giữ được chất lượng cao."**

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động lấy bài viết từ RSS** (Wallabag, Medium, Substack...)
✅ **Sử dụng Llama 3.3-70B (Groq) tạo nội dung cá nhân hóa** cho từng nền tảng
✅ **Tự động sinh ảnh AI** (nếu cần) và đăng bài theo lịch trình
✅ **Lưu trữ tất cả bài viết trong Airtable** để theo dõi và quản lý
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** viết và chỉnh sửa bài đăng.
- **Tăng tần suất đăng bài 5x** (từ 3 bài/tuần → 15 bài/tuần).
- **Nội dung cá nhân hóa** cho từng nền tảng (LinkedIn & Bluesky).
- **Tự động sinh ảnh AI** cho bài đăng (nếu cần).
- **Hoạt động liên tục** theo lịch trình đã thiết lập.
- **Lưu trữ toàn bộ bài viết** trong Airtable để theo dõi hiệu quả.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Link Đăng Ký**                          | **Ghi Chú**                                                                 |
|---------------------------|------------------------------------------|----------------------------------------------------------------------------|
| **Wallabag**              | [https://wallabag.it](https://wallabag.it) | Tạo RSS feed từ bài viết (ví dụ: `https://wallabag.example.com/feed/wallabag/token/tags/t:tag-name`) |
| **Airtable**              | [https://airtable.com](https://airtable.com) | API Key để lưu trữ bài viết và dữ liệu.                                      |
| **Groq (Llama 3.3-70B)**  | [https://console.groq.com](https://console.groq.com) | API Key cho mô hình AI.                                                     |
| **GetLate**               | [https://getlate.dev](https://getlate.dev) | API Key để đăng bài trên LinkedIn & Bluesky.                                |
| **Imgbb**                 | [https://api.imgbb.com](https://api.imgbb.com) | Upload ảnh AI cho bài đăng.                                                |
| **Hugging Face (AI Image)**| [https://huggingface.co](https://huggingface.co) | API Key để sinh ảnh AI (có thể thay thế bằng Fal.ai, Stability AI...).     |

### **2. Thiết Lập Wallabag (Nguồn RSS)**
- Tạo **tags** trong Wallabag để phân loại bài viết cần chia sẻ:
  - `#to-share-linkedin` (cho LinkedIn)
  - `#to-share-bluesky` (cho Bluesky)
- **Cấu trúc RSS feed**:
  ```
  https://wallabag.example.com/feed/wallabag/ACCESS_TOKEN/tags/t:tag-name
  ```
  Ví dụ:
  ```
  https://wallabag.example.com/feed/wallabag/abc123/tags/t:to-share-linkedin
  ```

### **3. Airtable (Lưu Trữ Bài Viết)**
- Tạo **bảng Airtable** để lưu trữ:
  - Tiêu đề bài viết
  - Nội dung Markdown
  - Thông tin đăng bài (draft/đã đăng)
  - Thông tin ảnh (nếu có)
- **Chuẩn hóa schema** để workflow có thể upsert dữ liệu.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/9147](https://n8n.io/workflows/9147) (chọn **Export as JSON**).
2. **Mở n8n Editor** → **Import** → Chọn file JSON vừa tải.
3. **Chọn "Create new workflow"** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** → **Create new workflow**.
2. **Nhấn "Import"** → Chọn **Paste JSON**.
3. **Dán JSON** từ file workflow và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và cần cấu hình cẩn thận. Dưới đây là **các node quan trọng** cần thiết lập:

#### **🔹 Node 1: RSS Feed Trigger (Lấy Bài Viết)**
- **Cấu hình**:
  - **URL Feed**:
    ```
    https://wallabag.example.com/feed/wallabag/ACCESS_TOKEN/tags/t:to-share-linkedin
    ```
    (Thay `ACCESS_TOKEN` và `tag-name` theo cấu hình Wallabag).
  - **Filter**: Chỉ lấy bài viết mới (cập nhật `lastUpdated`).
  - **Credentials**: Không cần (sử dụng `httpRequest` với `httpBearerAuth` nếu cần).

#### **🔹 Node 2: Groq Chat Model (Tạo Nội Dung AI)**
- **Cấu hình**:
  - **Credentials**: `groqApi` (đã thêm trong n8n).
  - **Model**: `llama-3.3-70b-versatile` (không thay đổi).
  - **Prompt**:
    ```json
    {
      "niche": "Tên ngành nghề của bạn (ví dụ: Marketing Digital)",
      "tone": "Professional & polished",
      "goal": "Drive traffic to the article",
      "target_audience": "Industry professionals",
      "custom_hashtags": "#DigitalMarketing,#n8n,#Automation",
      "is_draft": false,
      "generate_image_prompt": true,
      "platform_account_id": "LINKEDIN_ACCOUNT_ID"
    }
    ```
    (Thay `LINKEDIN_ACCOUNT_ID` bằng ID tài khoản GetLate của bạn).

#### **🔹 Node 3: Structured Output Parser (Xử Lý Kết Quả AI)**
- **Không cần chỉnh sửa** (n8n tự động phân tích output từ Groq).

#### **🔹 Node 4: Check For Image Generation Prompt (Bluesky/LinkedIn)**
- **Cấu hình**:
  - Nếu `generate_image_prompt: true`, workflow sẽ:
    1. **Gọi API sinh ảnh AI** (Hugging Face/Fal.ai).
    2. **Upload ảnh lên Imgbb**.
    3. **Đăng bài với ảnh**.
  - Nếu `false`, workflow chỉ **đăng bài văn bản**.

#### **🔹 Node 5: Post/Draft via GetLate API**
- **Cấu hình**:
  - **Credentials**: `httpBearerAuth` (API Key GetLate).
  - **Endpoint**:
    - **LinkedIn**: `https://api.getlate.dev/v1/post`
    - **Bluesky**: `https://api.getlate.dev/v1/bluesky/post`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_GETLATE_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "account_id": "YOUR_PLATFORM_ACCOUNT_ID",
      "content": "Nội dung bài đăng từ AI",
      "image_url": "https://i.imgur.com/IMAGE_ID.jpg" (nếu có)
    }
    ```

#### **🔹 Node 6: Airtable (Lưu Trữ Bài Viết)**
- **Cấu hình**:
  - **Credentials**: `airtableTokenApi`.
  - **Table Name**: Tên bảng Airtable bạn đã tạo.
  - **Operation**: `upsert` (cập nhật nếu tồn tại, tạo mới nếu không).
  - **Fields**:
    | Field          | Type    | Value Example                     |
    |----------------|---------|-----------------------------------|
    | `title`        | Text    | "Tên bài viết từ RSS"              |
    | `content`      | Long Text| `{{ $node["Markdown: Convert Article Content"].json }}` |
    | `platform`     | Text    | "LinkedIn" hoặc "Bluesky"         |
    | `status`       | Text    | "Draft" hoặc "Published"          |
    | `image_url`    | Text    | `https://i.imgur.com/IMAGE_ID.jpg` (nếu có) |

#### **🔹 Node 7: Schedule Trigger (Lịch Trình Đăng Bài)**
- **Cấu hình**:
  - **Frequency**: Chọn `hourly`, `daily`, hoặc `weekly`.
  - **Time**: Ví dụ: `9:00 AM UTC+7` (thời gian đăng bài).
  - **Active**: Bật `Active` để workflow chạy theo lịch.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow):
   - Nhấn **Run Workflow** với dữ liệu mẫu từ RSS.
   - Kiểm tra:
     - Nội dung AI có hợp lý không?
     - Ảnh AI có sinh thành công không?
     - Bài đăng có đăng lên LinkedIn/Bluesky không?
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa Prompt cho AI**
- **Thêm thông tin chi tiết** về:
  - **Tone**: Ví dụ: "Friendly & conversational" (thay vì "Professional").
  - **Hashtags**: Thêm hashtags phổ biến trong ngành.
  - **Call-to-Action (CTA)**: Ví dụ: "Like và chia sẻ nếu bạn thích nội dung này!"
- **Ví dụ Prompt nâng cao**:
  ```json
  {
    "niche": "Marketing Digital",
    "tone": "Friendly & conversational",
    "goal": "Engage audience & drive discussion",
    "target_audience": "Small business owners & freelancers",
    "custom_hashtags": "#DigitalMarketing,#SmallBusiness,#n8n,#Automation",
    "cta": "Like và chia sẻ nếu bạn muốn học cách tự động hóa công việc!",
    "is_draft": false,
    "generate_image_prompt": true,
    "platform_account_id": "LINKEDIN_ACCOUNT_ID"
  }
  ```

### **2. Sử Dụng Slack/Telegram để Thông Báo**
- **Thêm node `n8n-nodes-base.slack`** hoặc `n8n-nodes-base.telegram` sau node **Post/Draft** để:
  - Gửi thông báo khi bài đăng thành công.
  - Gửi lỗi nếu workflow bị lỗi.
- **Cấu hình**:
  - **Credentials**: `slackToken` hoặc `telegramBotToken`.
  - **Message**:
    ```
    🚀 Bài đăng thành công trên {{ $node["Check Platform"].json["platform"] }}!
    Tiêu đề: {{ $node["RSS Feed Trigger"].json["title"] }}
    Link: {{ $node["Post/Draft via GetLate API"].json["url"] }}
    ```

### **3. Lưu Log vào Airtable**
- **Thêm node `n8n-nodes-base.airtable`** sau node **Post/Draft** để:
  - Lưu **log hoạt động** (thành công/thất bại, thời gian đăng).
  - Dùng để **theo dõi hiệu quả** của workflow.
- **Cấu hình**:
  - **Table Name**: `Log_Posting`.
  - **Fields**:
    | Field          | Type    | Value Example                     |
    |----------------|---------|-----------------------------------|
    | `post_id`      | Text    | `{{ $node["Post/Draft via GetLate API"].json["id"] }}` |
    | `platform`     | Text    | `{{ $node["Check Platform"].json["platform"] }}` |
    | `status`       | Text    | `Success` hoặc `Failed`           |
    | `timestamp`    | DateTime| `{{ $node["Schedule Trigger"].json["date"] }}` |
    | `error`        | Long Text| `{{ $node["Post/Draft via GetLate API"].error }}` (nếu có) |

### **4. Tự Động Xóa Bài Draft Sau Thời Gian**
- **Thêm node `n8n-nodes-base.scheduleTrigger`** để:
  - Xóa bài **draft** sau 7 ngày nếu chưa đăng.
  - Cấu hình **frequency**: `daily`.
  - **Query Airtable** để lấy bài draft cũ:
    ```json
    {
      "filterByFormula": "OR({status} = 'Draft', {status} = 'Pending' AND DATE_DIFF(NOW(), {createdTime}) > 7)"
    }
    ```
  - **Xóa bằng GetLate API**:
    ```json
    {
      "method": "DELETE",
      "url": "https://api.getlate.dev/v1/post/{{ $node["Airtable"].json["post_id"] }}",
      "headers": {
        "Authorization": "Bearer YOUR_GETLATE_API_KEY"
      }
    }
    ```

### **5. Kết Hợp với Notion/Google Sheets**
- **Thay thế Airtable bằng Notion/Google Sheets**:
  - **Node `n8n-n