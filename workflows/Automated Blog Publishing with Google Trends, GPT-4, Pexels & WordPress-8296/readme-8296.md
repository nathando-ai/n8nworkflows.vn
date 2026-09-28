---
title: "🚀 Tự Động Hóa Viết Blog & Đăng Bài Trên WordPress Với Google Trends, GPT-4 & Pexels – Không Cần Code!"
description: "Workflow tự động hóa viết bài blog từ khóa hot trên Google Trends, tạo nội dung AI với GPT-4, tìm ảnh miễn phí từ Pexels và đăng bài tự động lên WordPress – tiết kiệm 80% thời gian so với viết thủ công!"
slug: "tu-dong-hoa-viet-blog-google-trends-gpt-4-wordpress"
tags: [n8n, automation, content-creation, ai-gpt-4, wordpress, google-trends, no-code]
keywords: [tự động hóa viết blog, n8n workflow blog, tự động hóa content marketing, viết bài AI GPT-4, đăng bài WordPress tự động, tìm từ khóa Google Trends]
---

# 🚀 **Tự Động Hóa Viết Blog & Đăng Bài Trên WordPress – Giải Pháp AI + No-Code Cho Người Sáng Tạo Nội Dung**

### **Nỗi Đau Của Các Sếp Trong Viết Blog**
Viết blog là một trong những công việc tốn thời gian nhất cho các marketer, blogger và doanh nghiệp. Các sếp phải:
- **Tìm kiếm từ khóa** thủ công trên Google Trends, mất hàng giờ để lọc ra những keyword có tiềm năng.
- **Viết nội dung** từ đầu đến cuối, đôi khi phải chỉnh sửa nhiều lần để phù hợp với SEO.
- **Tìm ảnh đẹp** miễn phí hoặc mua license, mất thời gian tải và chỉnh sửa.
- **Đăng bài lên WordPress** và quản lý metadata, dẫn đến sai sót thường xuyên.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lọc từ khóa hot** từ Google Trends.
✅ **Viết bài blog** với GPT-4 (giống như có một nhà văn AI 24/7).
✅ **Tìm ảnh miễn phí** từ Pexels và xử lý metadata.
✅ **Đăng bài tự động** lên WordPress với tiêu đề, nội dung và hình ảnh hoàn chỉnh.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với viết blog thủ công.
- **Nội dung SEO tối ưu** từ từ khóa hot trên Google Trends.
- **Hình ảnh chuyên nghiệp** tự động tìm và xử lý metadata.
- **Đăng bài tự động** lên WordPress, không cần can thiệp.
- **Hoạt động 24/7** với lịch trình tự động (dùng `scheduleTrigger`).
- **Cá nhân hóa** nội dung theo từng từ khóa.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys**:
   - **Google Sheets**: Tạo một sheet để lưu trữ từ khóa và bài viết (cần **Google Sheets OAuth 2.0 API**).
   - **OpenAI API**: [Đăng ký API Key](https://platform.openai.com/account/api-keys) để sử dụng GPT-4.
   - **WordPress**: Tài khoản admin WordPress và **WordPress REST API Key**.
   - **Pexels API**: [Đăng ký API Key](https://www.pexels.com/api/) (nếu muốn tìm ảnh tự động).
   - **VPS n8n**: Đã cài đặt và chạy n8n (self-hosted).

2. **File Google Sheets**:
   - Tạo một sheet với **2 cột**:
     - `Keyword` (từ khóa tìm kiếm).
     - `Status` (trạng thái: `pending`, `in_progress`, `done`).
   - **Link sheet** phải được chia sẻ với n8n (quyền chỉnh sửa).

3. **WordPress**:
   - Cài đặt plugin **WP REST API** (nếu chưa có).
   - Tạo một **category** mới (ví dụ: "AI-Generated") để bài viết tự động được phân loại.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON**: [Tải workflow từ n8n.io](https://n8n.io/workflows/8296) (ấn "Export").
- **Import vào n8n**:
  - Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
  - **Hoặc** copy toàn bộ JSON và paste vào **"Import"** → **"Paste JSON"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow có **20 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Credentials (Tài Khoản)**
| Node | Credentials Cần Thiết | Hướng Dẫn Cấu Hình |
|------|----------------------|----------------------|
| **Google Sheets** | `googleSheetsOAuth2Api` | - Tạo OAuth 2.0 Client ID trên [Google Cloud Console](https://console.cloud.google.com/). <br> - Chọn **Google Sheets API** và cấp quyền. <br> - Thêm vào n8n dưới **Credentials → Add Credential → Google Sheets OAuth 2.0**. |
| **OpenAI (GPT-4)** | `openAiApi` | - Đăng ký API Key trên [OpenAI](https://platform.openai.com/account/api-keys). <br> - Thêm vào n8n dưới **Credentials → Add Credential → OpenAI API**. |
| **WordPress** | `wordpressApi` | - Tạo **REST API Key** trong WordPress (Settings → General → API Keys). <br> - Thêm vào n8n dưới **Credentials → Add Credential → WordPress**. |
| **Pexels (nếu dùng)** | `httpHeaderAuth` | - Sử dụng API Key từ Pexels trong **Headers** của node `Search Pexels Image`. |

##### **B. Cấu Hình Node Quan Trọng**
1. **`Main Config` (Set)**
   - Điền **Google Sheets URL** (link chia sẻ của sheet).
   - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1:B`).

2. **`GoogleTrends` (HTTP Request)**
   - **URL**: `https://trends.google.com/trends/api/explore?hl=en-US&q={keyword}&geo=US`.
   - **Headers**:
     ```json
     {
       "Accept": "application/json",
       "Referer": "https://trends.google.com/"
     }
     ```
   - **Query Parameters**:
     - `q`: `$node["Grab one random keyword"].json()["keyword"]` (sẽ lấy từ node sau).

3. **`AI Agent` (LangChain Agent)**
   - **Prompt Template**: Cần chỉnh sửa để phù hợp với yêu cầu viết blog.
     Ví dụ:
     ```plaintext
     Tôi là một nhà viết blog chuyên nghiệp. Viết một bài blog dài 1000-1200 từ về chủ đề "{keyword}" với cấu trúc:
     1. Tiêu đề SEO (có từ khóa).
     2. Mở đầu hấp dẫn.
     3. 3-5 phần nội dung chi tiết.
     4. Kết luận + CTA (Call to Action).
     Đảm bảo bài viết có từ khóa "{keyword}" xuất hiện tự nhiên 3-5 lần.
     ```
   - **Model**: Đã cấu hình là `gpt-4.1-mini` (tiết kiệm chi phí).

4. **`Create posts on WordPress`**
   - **Endpoint**: `https://{domain}.com/wp-json/wp/v2/posts`.
   - **Headers**:
     ```json
     {
       "Authorization": "Basic {wordpress_api_key}",
       "Content-Type": "application/json"
     }
     ```
   - **Body**:
     ```json
     {
       "title": "$node["Structured Output Parser"].json()["title"]",
       "content": "$node["Structured Output Parser"].json()["content"]",
       "status": "publish",
       "categories": [123] // ID category "AI-Generated"
     }
     ```

5. **`Search Pexels Image` (HTTP Request)**
   - **URL**: `https://api.pexels.com/videos/search?query={keyword}&per_page=1`.
   - **Headers**:
     ```json
     {
       "Authorization": "YourPexelsApiKey"
     }
     ```
   - **Query Parameters**:
     - `query`: `$node["Grab one random keyword"].json()["keyword"]`.

6. **`Upload media` (WordPress)**
   - **Endpoint**: `https://{domain}.com/wp-json/wp/v2/media`.
   - **Body**:
     ```json
     {
       "source": "$node["Search Pexels Image"].json()["src.large2x"]",
       "title": "{keyword} Image"
     }
     ```

7. **`Set image ID for the post` (HTTP Request)**
   - **Endpoint**: `https://{domain}.com/wp-json/wp/v2/posts/{post_id}`.
   - **Body**:
     ```json
     {
       "featured_media": "$node["Upload media"].json()["id"]
     }
     ```

##### **C. Node `Schedule Trigger`**
- **Cấu hình lịch trình**:
  - **Frequency**: `Daily` (hoặc `Weekly`).
  - **Time**: Ví dụ: `09:00 AM` (thời gian tự động lấy từ khóa mới).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** với một từ khóa mẫu (ví dụ: `"tự động hóa no-code"`).
   - Kiểm tra:
     - Bài viết có được tạo trên Google Sheets không?
     - GPT-4 có viết bài thành công không?
     - Ảnh có được tải và gắn lên WordPress không?

2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và **bật `scheduleTrigger`**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu từ khóa**:
   - Thêm node **`Filter Scraped Keywords`** (Code) để lọc từ khóa có **trend > 50** và **search volume > 1000**.

2. **Xử lý lỗi tự động**:
   - Thêm node **`Set Error Handling`** (Code) để nếu GPT-4 trả về lỗi, workflow sẽ **skip** và tiếp tục với từ khóa khác.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **`Slack/Email`** để báo cáo số lượng bài viết được tạo mỗi ngày.

4. **Cập nhật ảnh định kỳ**:
   - Thêm node **`Schedule Trigger`** để **cập nhật ảnh mới** cho bài viết cũ (ví dụ: 1 lần/tháng).

5. **Dùng Telegram Bot**:
   - Thêm node **`Telegram Bot`** để nhận thông báo khi bài viết được đăng thành công.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa toàn bộ quy trình viết blog, từ tìm từ khóa đến đăng bài. Với **n8n + GPT-4 + WordPress**, các sếp có thể:
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược nội dung.
✔ **Nâng cao hiệu suất SEO** với từ khóa hot.
✔ **Cải thiện chất lượng hình ảnh** với Pexels.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình credentials** theo hướng dẫn.
3. **Bật schedule** và để AI làm việc cho bạn!

**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ với team để được tư vấn chi tiết! 🚀