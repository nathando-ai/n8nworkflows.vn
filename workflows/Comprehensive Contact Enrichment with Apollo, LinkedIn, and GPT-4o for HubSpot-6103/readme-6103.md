---
title: "🚀 Tự Động Hóa Nâng Cao Thông Tin Liên Lạc với Apollo, LinkedIn & GPT-4o cho HubSpot - Giải Pháp Lead Gen AI Toàn Diện"
description: "Workflow tự động hóa 100% không code giúp các sếp enrich thông tin liên lạc từ HubSpot bằng Apollo.io, phân tích bài viết LinkedIn mới nhất, và tổng hợp thông tin chi tiết bằng GPT-4o - tiết kiệm thời gian lên tới 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-enrich-contact-apollo-linkedin-gpt4o-hubspot"
tags: [n8n, automation, lead-generation, ai-summarization, hubspot, apollo-io, linkedin, gpt-4o]
keywords: [n8n workflow enrich contact, tự động hóa lead generation, enrich thông tin liên lạc, Apollo.io + HubSpot, phân tích bài viết LinkedIn, GPT-4o tự động hóa CRM]
---

# 🚀 **Tự Động Hóa Nâng Cao Thông Tin Liên Lạc với Apollo, LinkedIn & GPT-4o cho HubSpot**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tìm kiếm và enrich** thông tin liên lạc của lead từ HubSpot bằng cách tra cứu trên Apollo.io (hoặc các công cụ khác) → **Tốn thời gian, dễ sai sót**.
- **Phân tích bài viết LinkedIn** mới nhất của lead để hiểu xu hướng, sở thích, và hành vi gần đây → **Không thể làm được hàng loạt**.
- **Tổng hợp thông tin** từ nhiều nguồn (Apollo, LinkedIn, GPT-4o) thành một bản tóm tắt chuyên nghiệp để cập nhật vào HubSpot → **Lặp đi lặp lại, mất hiệu quả**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Tra cứu và enrich** thông tin liên lạc từ Apollo.io.
✅ **Lấy và phân tích** 3 bài viết LinkedIn mới nhất của lead.
✅ **Tổng hợp thông tin** bằng GPT-4o thành một bản tóm tắt AI, sẵn sàng để cập nhật vào HubSpot.
✅ **Cập nhật tự động** vào CRM, giúp các sếp **tiết kiệm 80% thời gian** và **tăng chất lượng lead** lên 30%.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động enrich và phân tích lead trong vài giây thay vì nhiều giờ.
- **Thông tin chính xác**: Dữ liệu từ Apollo.io + LinkedIn + AI tổng hợp, giảm sai sót.
- **Tóm tắt chuyên nghiệp**: GPT-4o tự động tạo bản tóm tắt lead, sẵn sàng để cập nhật vào HubSpot.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.
- **Tăng chất lượng lead**: Hiểu rõ hơn về lead thông qua bài viết LinkedIn và thông tin enrich.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HubSpot** (và **OAuth2 API Key** của HubSpot).
✔ **Tài khoản Apollo.io** (và **API Key** để tra cứu thông tin liên lạc).
✔ **Tài khoản OpenAI** (và **API Key** để sử dụng GPT-4o-mini và GPT-o3).
✔ **Tài khoản LinkedIn** (để lấy bài viết mới nhất của lead).
✔ **Workflow cha** (nếu muốn kích hoạt từ một workflow khác).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import Workflow** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/6103)).
3. Chọn **Create Workflow** và đặt tên (ví dụ: **"Enrich Contact with Apollo & LinkedIn"**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **19 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **🔹 Node "Enrich with Apollo" (HTTP Request)**
- **Mục đích**: Tra cứu thông tin liên lạc của lead trên Apollo.io.
- **Cấu hình**:
  - **URL**: `https://api.apollo.io/v1/search`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_APOLLO_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "query": "email:{{$node["Get Contact from HubSpot"].json["email"]}}",
      "limit": 1
    }
    ```
  - **Lưu ý**: Thay thế `YOUR_APOLLO_API_KEY` bằng API Key của Apollo.io.

##### **🔹 Node "OpenAI Chat Model5 & Model6" (LM Chat OpenAI)**
- **Mục đích**: Sử dụng GPT-4o-mini và GPT-o3 để tổng hợp thông tin.
- **Cấu hình**:
  - **API Key**: Điền vào **OpenAI API Key** trong credentials.
  - **Model**:
    - Node 5: `gpt-4o-mini` (dùng để tóm tắt thông tin enrich).
    - Node 6: `o3` (dùng để phân tích bài viết LinkedIn).
  - **Prompt**:
    - Các sếp có thể chỉnh sửa prompt trong **keyParameters** để phù hợp với nhu cầu (ví dụ: yêu cầu AI tập trung vào những điểm cụ thể trong lead).

##### **🔹 Node "Get recent posts" (HTTP Request)**
- **Mục đích**: Lấy bài viết LinkedIn mới nhất của lead.
- **Cấu hình**:
  - **URL**: `https://api.linkedin.com/v2/people/~:(posts{limit:3,sortBy:createdTime,sortDirection:DESC})`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_LINKEDIN_ACCESS_TOKEN",
      "X-Restli-Protocol-Version": "2.0.0"
    }
    ```
  - **Lưu ý**:
    - Các sếp cần **API Access Token** của LinkedIn (có thể lấy từ [LinkedIn Developer Portal](https://www.linkedin.com/developers/)).
    - Nếu không muốn lấy từ LinkedIn API, có thể thay thế bằng **Scraper API** (ví dụ: Apify, ParseHub).

##### **🔹 Node "Enrich in HubSpot1" (HubSpot)**
- **Mục đích**: Cập nhật thông tin enrich vào HubSpot.
- **Cấu hình**:
  - **Credentials**: Chọn `hubspotOAuth2Api` (đã cấu hình trước).
  - **Endpoint**: `contacts` (hoặc `properties` nếu muốn cập nhật thuộc tính cụ thể).
  - **Lưu ý**: Đảm bảo **email** của lead trong HubSpot khớp với email tra cứu trên Apollo.io.

##### **🔹 Node "Auto-fixing Output Parser2" & "Structured Output Parser2" (LangChain)**
- **Mục đích**: Chuyển đổi output của GPT-4o thành định dạng cấu trúc.
- **Cấu hình**:
  - **Schema**: Các sếp có thể chỉnh sửa schema trong **keyParameters** để phù hợp với dữ liệu output mong muốn (ví dụ: `{ "name": "string", "summary": "string" }`).

##### **🔹 Node "Loop Over Items" (Split In Batches)**
- **Mục đích**: Xử lý lead một cách batch để tránh giới hạn API.
- **Cấu hình**:
  - **Batch Size**: Đặt từ **5-10 lead/lần** để tránh bị chặn API.

##### **🔹 Node "clean" (Code)**
- **Mục đích**: Làm sạch dữ liệu trước khi gửi vào HubSpot.
- **Cấu hình**:
  - Các sếp có thể chỉnh sửa mã JavaScript trong **Code Node** để loại bỏ dữ liệu không cần thiết (ví dụ: `null`, `undefined`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một lead mẫu:
   - Chọn **Execute Workflow** và nhập **email của lead** vào node **"When Executed by Another Workflow"**.
   - Kiểm tra output để đảm bảo workflow hoạt động đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** để nhận thông báo khi enrich thành công.
   - Ví dụ:
     ```json
     {
       "text": "Lead {{$node["Get Contact from HubSpot"].json["email"]}} đã được enrich thành công!"
     }
     ```

2. **Lưu Log**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử enrich.
   - Cấu hình:
     ```json
     {
       "sheetName": "Enrichment Log",
       "appendRow": true,
       "data": [
         {"email": "{{$node["Get Contact from HubSpot"].json["email"]}}"},
         {"status": "success"},
         {"timestamp": "{{$node["Date/Time"].json}}"}
       ]
     }
     ```

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày/tuần.
   - Ví dụ: **Chạy vào 8h sáng hàng ngày** để enrich tất cả lead mới.

4. **Tối Ưu Hóa Prompt GPT-4o**:
   - Nếu muốn AI tập trung vào những điểm cụ thể (ví dụ: **sở thích, ngành nghề, dự án mới nhất**), chỉnh sửa prompt trong node **Enrichment summary agent**:
     ```json
     {
       "prompt": "Tóm tắt thông tin của lead {{name}} từ Apollo.io và bài viết LinkedIn mới nhất. Đặc biệt chú trọng đến:
       - Ngành nghề và vị trí hiện tại.
       - Dự án mới nhất (nếu có).
       - Sở thích và xu hướng công nghệ.
       Trả về định dạng JSON: { 'name': '{{name}}', 'summary': '{{summary}}' }"
     }
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động enrich** thông tin lead từ HubSpot bằng Apollo.io.
✔ **Phân tích bài viết LinkedIn** mới nhất để hiểu lead sâu hơn.
✔ **Tổng hợp thông tin** bằng GPT-4o thành bản tóm tắt chuyên nghiệp.
✔ **Cập nhật tự động** vào HubSpot, tiết kiệm **80% thời gian** và **tăng chất lượng lead**.

**Hành động ngay!**
1. **Import workflow** và cấu hình API keys.
2. **Test với 1-2 lead** để đảm bảo hoạt động.
3. **Bật Active** và để workflow làm việc 24/7!

**🚀 Còn chần chừ gì nữa?** Hãy tự động hóa lead generation của mình ngay hôm nay! 🚀