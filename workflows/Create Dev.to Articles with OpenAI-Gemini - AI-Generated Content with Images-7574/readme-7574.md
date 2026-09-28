---
title: "🚀 Tự Động Hóa Tạo Bài Viết Dev.to Với AI Gemini + OpenAI - Nội Dung AI Chất Lượng, Có Ảnh, Không Cần Code"
description: "Workflow này tự động tạo bài viết chuyên nghiệp cho Dev.to với nội dung AI sinh, hình ảnh tự động tạo bằng Gemini/OpenAI, và đăng tải tự động - tiết kiệm 80% thời gian viết bài cho các sếp Content Creator."
slug: "tieu-dong-hoa-tao-bai-viet-dev-to-ai-gemini-openai"
tags: [n8n, automation, content-creation, ai-gemini, openai, dev-to, no-code]
keywords: [tự động hóa viết bài dev.to, ai tạo nội dung dev.to, gemini openai dev.to, tự động hóa content marketing, workflow n8n cho content creator]
---

# 🚀 **Tự Động Hóa Tạo Bài Viết Dev.to Với AI Gemini + OpenAI: Nội Dung AI Chất Lượng, Có Ảnh, Không Cần Code**

### **Giải Phóng Thời Gian Cho Các Sếp Content Creator**
Hãy tưởng tượng một ngày không phải ngồi ghép ghép từ khóa, viết bài từ đầu đến cuối, hoặc tìm ảnh phù hợp cho bài viết. **Workflow này tự động hóa toàn bộ quy trình** từ **tạo ý tưởng** → **viết bài** → **tạo ảnh minh họa** → **đăng tải lên Dev.to** chỉ với một cú nhấp chuột. Dùng AI Gemini và OpenAI, các sếp có thể **nâng cấp nội dung từ 0 đến 100 điểm chỉ trong vài phút**, đồng thời **tăng tốc độ xuất bản lên 5-10 bài/ngày** mà không cần viết một chữ nào.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) với tài nguyên tối thiểu:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý AI nhanh)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian viết bài**: AI tự động viết nội dung chuyên nghiệp, phù hợp với SEO và độc giả Dev.to.
- **Hình ảnh tự động tạo**: Sử dụng Gemini/OpenAI để sinh ảnh minh họa chất lượng cao, phù hợp với bài viết.
- **Đăng tải tự động**: Bài viết được tự động đăng lên Dev.to với tiêu đề, nội dung và ảnh hoàn chỉnh.
- **Tối ưu SEO**: Nội dung được AI tối ưu từ khóa và cấu trúc logic, giúp bài viết xếp hạng cao hơn.
- **Hoạt động 24/7**: Cấu hình **Schedule Trigger** để workflow chạy tự động hàng ngày (ví dụ: sáng 7h).
- **Cá nhân hóa nội dung**: Dùng dữ liệu từ Google Sheets để tạo bài viết phù hợp với chủ đề hoặc khách hàng mục tiêu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Dev.to**:
   - API Key hoặc OAuth Token của Dev.to (để đăng bài tự động).
   - [Hướng dẫn lấy API Key Dev.to](https://dev.to/api/docs#authentication) (nếu không có, cần tạo tài khoản mới và kích hoạt API).

2. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets chứa **dữ liệu đầu vào** cho workflow (ví dụ: danh sách chủ đề, từ khóa, hoặc mô tả bài viết).
   - **Cấu trúc bảng**:
     | Chủ đề          | Từ khóa chính       | Mô tả ngắn (optional) |
     |------------------|---------------------|-----------------------|
     | Tự động hóa n8n | AI + no-code         | Bài viết về cách tự động hóa với n8n |
     | Gemini AI         | Multimodal AI        | So sánh Gemini và OpenAI |

3. **API Keys cho AI**:
   - **OpenAI API Key** (để sử dụng OpenAI Chat/GPT-4).
   - **Google Gemini API Key** (để sinh ảnh và xử lý multimodal).
   - [Hướng dẫn lấy API Key OpenAI](https://platform.openai.com/account/api-keys)
   - [Hướng dẫn lấy API Key Gemini](https://ai.google.dev/gemini-api/docs/quickstart)

4. **Tài khoản Cloudinary (optional)**:
   - Nếu muốn lưu ảnh sinh ra trên Cloudinary thay vì Dev.to, cần API Key của Cloudinary.
   - [Hướng dẫn lấy API Key Cloudinary](https://cloudinary.com/documentation/cloudinary_api_reference#authentication)

5. **Tài khoản n8n Self-hosted**:
   - Workflow này yêu cầu **n8n phiên bản Community hoặc Enterprise** (cài đặt trên VPS).
   - Các node **LangChain** (OpenAI, Gemini) cần được cài đặt thêm:
     ```bash
     n8n install @n8n/nodes-langchain
     ```
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON**:
   - Tải workflow từ [link gốc](https://n8n.io/workflows/7574) hoặc sử dụng file JSON đã cung cấp.
2. **Import vào n8n**:
   - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON → Nhấn **Import**.
   - Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **22 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
1. **Google Sheets**:
   - Node: **"Get data from sheet"**
   - **Cấu hình**:
     - Chọn **Google Sheets** trong **Credentials**.
     - Điền **Sheet ID** và **Sheet Name** (tên trang tính trong Google Sheets).
     - Chọn **Range** (ví dụ: `Sheet1!A1:B10`).
     - **Lưu ý**: Dữ liệu trong Google Sheets phải có **cột "Chủ đề"** và **cột "Từ khóa"** (hoặc tên khác, cần điều chỉnh trong node **Split In Batches**).

2. **Dev.to API**:
   - Node: **"Post article on dev.to"**
   - **Cấu hình**:
     - Chọn **HTTP Request** → **Basic Auth** (nếu Dev.to yêu cầu).
     - Điền **Username** (email Dev.to) và **Password** (API Key hoặc OAuth Token).
     - **Endpoint**: `https://dev.to/api/articles/`
     - **Headers**:
       ```json
       {
         "Content-Type": "application/json",
         "Authorization": "Bearer YOUR_DEV_TO_API_KEY"
       }
       ```
     - **Body (JSON)**:
       ```json
       {
         "title": "{{ $node["Set Input Image"].json["title"] }}",
         "body": "{{ $node["Article writer"].json["content"] }}",
         "tag_list": ["ai", "automation", "n8n"],
         "cover_image": "{{ $node["Set Output Image"].json["image_url"] }}"
       }
       ```

3. **OpenAI & Gemini API**:
   - Node: **"OpenAI Chat Model"**, **"Generate an image"**, **"Google Gemini"**
   - **Cấu hình chung**:
     - Điền **API Key** tương ứng vào **Credentials** của node.
     - **Prompt cho AI**:
       - **Viết bài**: Sử dụng template như:
         ```
         Tôi là một tác giả chuyên nghiệp viết cho Dev.to. Viết một bài viết dài 1000 từ về chủ đề "{{ $node["Get data form sheet"].json["chủ đề"] }}" với từ khóa chính là "{{ $node["Get data form sheet"].json["từ_khóa"] }}". Nội dung phải:
         1. Có tiêu đề hấp dẫn.
         2. Cấu trúc rõ ràng (mở đầu, nội dung, kết luận).
         3. Được tối ưu SEO với từ khóa "{{ $node["Get data form sheet"].json["từ_khóa"] }}" xuất hiện tự nhiên.
         4. Có ví dụ thực tế và liên kết đến các nguồn đáng tin cậy.
         5. Kết thúc bằng một câu hỏi hoặc call-to-action.
         ```
       - **Tạo ảnh**: Sử dụng prompt như:
         ```
         Tạo một hình ảnh minh họa cho bài viết về "{{ $node["Get data form sheet"].json["chủ đề"] }}" với phong cách hiện đại, chuyên nghiệp. Hình ảnh phải:
         - Có màu sắc sống động.
         - Được thiết kế theo phong cách flat design.
         - Chứa các biểu tượng liên quan đến chủ đề (ví dụ: AI, code, robot).
         - Phù hợp với kích thước cover image của Dev.to (1200x630 pixels).
         ```

##### **B. Cấu Hình Node Quan Trọng**
1. **Schedule Trigger**:
   - Node: **"Schedule Trigger"**
   - **Cấu hình**:
     - Chọn **Cron expression** để chạy workflow định kỳ (ví dụ: `0 7 * * *` để chạy sáng 7h hàng ngày).
     - **Lưu ý**: Nếu không muốn chạy tự động, có thể bỏ qua và sử dụng **Manual Trigger**.

2. **Agent & Chain LLM**:
   - Node: **"AI Agent"**, **"Article writer"**
   - **Cấu hình**:
     - Chọn **Model** (ví dụ: `gpt-4` hoặc `gemini-pro`).
     - Đảm bảo **Prompt** được truyền từ node **Set Input Data** (xem phần sau).

3. **Generate Image**:
   - Node: **"Generate an image"** (OpenAI DALL·E) và **"Generate an image1"** (Gemini)
   - **Cấu hình**:
     - Chọn **Model** (DALL·E 3 hoặc Gemini Image).
     - **Prompt** phải rõ ràng (xem ví dụ trên).

4. **Set Input Data**:
   - Node: **"Set input data/credentials"**
   - **Cấu hình**:
     - Truyền dữ liệu từ **Google Sheets** vào các node sau (ví dụ: `{{ $node["Get data form sheet"].json }}`).
     - **Lưu ý**: Cần điều chỉnh **field names** phù hợp với cấu trúc Google Sheets của các sếp.

##### **C. Test Run Trước Khi Bật Active**
1. **Chạy Test Run**:
   - Nhấn **Execute Workflow** (Manual Trigger) với **1 dòng dữ liệu mẫu** từ Google Sheets.
   - Kiểm tra:
     - AI có viết bài không?
     - Ảnh có sinh ra không?
     - Dev.to có đăng bài thành công không?
2. **Sửa lỗi**:
   - Nếu AI viết bài không phù hợp, điều chỉnh **prompt** trong node **OpenAI Chat Model** hoặc **Gemini**.
   - Nếu ảnh không sinh ra, kiểm tra **prompt** và **API Key**.

#### **3. Kích Hoạt Workflow ⚡️**
- Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.
- Nếu dùng **Schedule Trigger**, workflow sẽ chạy tự động theo lịch đã đặt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tối ưu Prompt cho AI**:
   - Thêm **các yêu cầu cụ thể** vào prompt để AI viết bài chuyên nghiệp hơn:
     - Ví dụ: `"Nội dung phải có ít nhất 3 ví dụ thực tế từ ngành công nghiệp tech."`
     - `"Sử dụng từ khóa 'n8n automation' 3 lần trong bài viết."`

2. **Lưu Log & Monitoring**:
   - Thêm node **Slack/Telegram** để nhận thông báo khi workflow chạy thành công/thất bại.
   - Sử dụng node **Google Sheets** để lưu **lịch sử bài viết** (tiêu đề, ngày đăng, link).

3. **Tạo Bài Viết Cho Nhiều Chủ Đề**:
   - Nếu Google Sheets có **nhiều hàng dữ liệu**, sử dụng node **Limit** để chỉ lấy **5-10 chủ đề** mỗi lần chạy (tránh quá tải API).

4. **Tích Hợp với Canva (Optional)**:
   - Thay vì sử dụng DALL·E/Gemini, các sếp có thể **tạo ảnh bằng Canva API** và gắn vào bài viết.

5. **Tối ưu SEO với All-in-One SEO (Optional)**:
   - Sau khi đăng bài, sử dụng node **HTTP Request** để gửi bài viết lên **All-in-One SEO** để tối ưu hóa thêm.

6. **Dùng Gemini cho Multimodal**:
   - Nếu muốn **ảnh và bài viết được tạo từ một prompt duy nhất**, sử dụng node **Google Gemini** với **multimodal prompt**:
     ```
     Tôi muốn một bài viết về "Tự động hóa với n8n" và một hình ảnh minh họa. Bài viết phải dài 1000 từ, có cấu trúc rõ ràng, và hình ảnh phải phù hợp với nội dung.
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp **Content Creator, Blogger, hoặc Marketing Specialist** muốn **tăng tốc độ xuất bản nội dung** mà không cần viết một chữ nào. Với **AI Gemini và OpenAI**, các sếp có thể:
✅ **Tạo bài viết chất lượng cao** chỉ trong vài phút.
✅ **Tự động tạo ảnh minh họa** phù hợp với nội dung.
✅ **Đăng tải tự động lên Dev.to** (hoặc Medium, WordPress...).
✅ **Hoạt động 24/7** với Schedule Trigger.

**Hành động ngay hôm nay**:
1. Chuẩn bị **Google Sheets** với dữ liệu đầu vào.
2. Cài đặt **n8n Self-hosted** trên VPS.
3. Import workflow và **cấu hình credentials**.
4. **Test Run** và **bật Active** để bắt đầu tự động hóa!

**Nếu cần hỗ trợ**, các sếp có thể liên hệ với tác giả LukaszB qua email: **kontakt@lumizone.pl**.

---
**#TựĐộngHóa #AIContent #Dev.to #n8n #OpenAI #Gemini**