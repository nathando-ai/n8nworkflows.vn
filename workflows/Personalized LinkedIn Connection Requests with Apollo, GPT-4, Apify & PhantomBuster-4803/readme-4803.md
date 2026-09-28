---
title: "🚀 Tự Động Hóa Yêu Cầu Kết Nối LinkedIn Cá Nhân Hóa Với AI (Apollo + GPT-4 + Apify)"
description: "Workflow tự động hóa tìm kiếm và gửi yêu cầu kết nối LinkedIn cá nhân hóa 100% tự động, tiết kiệm thời gian lên đến 80% so với cách làm thủ công. Sử dụng AI để phân tích và tạo nội dung icebreaker độc đáo cho từng lead."
slug: "tieu-dong-hoa-yeu-cau-ket-noi-linkedin-canh-nhac-ai"
tags: [n8n, automation, marketing, ai, linkedin, apollo, gpt-4, apify]
keywords: [tự động hóa linkedin, n8n workflow, tìm kiếm lead linkedin, ai personalize outreach, apollo scraper, gpt-4 tự động hóa]
---

# 🚀 **Tự Động Hóa Yêu Cầu Kết Nối LinkedIn Cá Nhân Hóa Với AI (Apollo + GPT-4 + Apify)**

### **💡 Giải Pháp Cho Các Sếp Bận Rộn**
Bạn có bao giờ cảm thấy **mệt mỏi** khi phải:
- Tìm kiếm thủ công hàng trăm lead trên LinkedIn?
- Viết hàng chục tin nhắn kết nối giống nhau, không cá nhân hóa?
- Phải theo dõi kết quả và điều chỉnh chiến lược một cách thủ công?

**Workflow này giúp bạn:**
✅ **Tự động tìm kiếm lead** phù hợp từ Apollo với chỉ cần mô tả bằng tiếng Việt.
✅ **Tạo tin nhắn kết nối cá nhân hóa** bằng GPT-4, phù hợp với từng lead.
✅ **Gửi yêu cầu kết nối** qua PhantomBuster, tối ưu hóa tỷ lệ chấp nhận.
✅ **Lưu toàn bộ dữ liệu** vào Google Sheets để theo dõi và phân tích.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 80% công việc tìm kiếm và viết tin nhắn.
- **Tỷ lệ chấp nhận cao**: Tin nhắn cá nhân hóa tăng tỷ lệ phản hồi lên **3-5 lần** so với tin nhắn chung.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy tự động.
- **Dữ liệu chi tiết**: Lấy thông tin lead (email, công ty, vị trí) để phân tích tiếp thị.
- **Tuân thủ LinkedIn**: Không vi phạm chính sách của LinkedIn bằng cách gửi quá nhiều yêu cầu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Apollo** (để tìm kiếm lead) + **API Key** (nếu sử dụng API Apollo).
2. **Tài khoản OpenAI** (để sử dụng GPT-4) + **API Key**.
3. **Tài khoản Apify** (để chạy actor scraper) + **API Key**.
4. **Tài khoản PhantomBuster** (để gửi yêu cầu kết nối) + **API Key**.
5. **Google Sheets** (để lưu lead và tin nhắn cá nhân hóa) + **OAuth 2.0 Credentials**.
6. **VPS n8n** (để chạy workflow 24/7) – 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4803](https://n8n.io/workflows/4803) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: On Form Submission (formTrigger)**
- **Mục đích**: Nhận input từ form mô tả lead mục tiêu (ví dụ: *"Nhân viên marketing tại Việt Nam, làm việc tại startup"*).
- **Lưu ý**:
  - Cấu hình **HTTP Basic Auth** để bảo mật form.
  - Test form bằng cách gửi yêu cầu POST từ Postman hoặc cURL.

##### **🔹 Node 2 & 3: Generate Search URL (openAi) + Run Apify Actor (httpRequest)**
- **Mục đích**: Chuyển mô tả tiếng Việt thành URL tìm kiếm Apollo, sau đó lấy lead từ Apify.
- **Cấu hình chi tiết**:
  - **Node `Generate Search URL`**:
    - **Credentials**: Chọn `openAiApi`.
    - **Prompt**: Điền template:
      ```json
      "Tôi muốn tìm kiếm lead trên Apollo với mô tả: '{input}'. Hãy chuyển mô tả này thành URL tìm kiếm Apollo với các tham số chính xác, bao gồm:
      - Kiểu công ty (startup, agency, corporation)
      - Địa điểm (nước, thành phố)
      - Vị trí công việc (CEO, Founder, Marketing Manager)
      - Kích thước công ty (số nhân viên)
      - Nền tảng công nghệ (nếu có)
      Trả về URL Apollo dưới dạng JSON với cấu trúc:
      {
        "url": "https://api.apollo.io/search?query=...",
        "params": { ... }
      }"
      ```
  - **Node `Run Apify Actor`**:
    - **URL**: `https://api.apify.com/v2/actors/{actor-id}/runs` (thay `{actor-id}` bằng ID actor Apollo của bạn).
    - **Headers**:
      ```json
      {
        "Authorization": "Bearer {apify-api-key}",
        "Content-Type": "application/json"
      }
      ```
    - **Body**:
      ```json
      {
        "input": {
          "url": "$node[Generate Search URL].json()"
        }
      }
      ```

##### **🔹 Node 4: Limit (limit)**
- **Mục đích**: Giảm số lượng lead để test trước khi chạy full.
- **Lưu ý**: Đặt giá trị `limit` = **5-10** để test, sau đó tăng lên **500** cho sản xuất.

##### **🔹 Node 5: Trigger PhantomBuster Agent (httpRequest)**
- **Mục đích**: Gửi yêu cầu kết nối LinkedIn với tin nhắn cá nhân hóa.
- **Cấu hình**:
  - **URL**: `https://api.phantombuster.com/v1/agents/{agent-id}/runs` (thay `{agent-id}` bằng ID agent của bạn).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {phantombuster-api-key}",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "input": {
        "leads": "$node[Aggregate].json()",
        "messages": "$node[Personalize Outreach].json()"
      }
    }
    ```

##### **🔹 Node 6 & 7: Add to Google Sheet (googleSheets) + Personalize Outreach (openAi)**
- **Node `Personalize Outreach`**:
  - **Prompt**: Điền template để GPT-4 tạo tin nhắn cá nhân hóa:
    ```json
    "Tôi có thông tin lead sau:
    - Tên: {name}
    - Công ty: {company}
    - Vị trí: {jobTitle}
    - Công việc hiện tại: {currentJob}
    - Kinh nghiệm: {experience}

    Hãy tạo một tin nhắn kết nối LinkedIn cá nhân hóa, dài khoảng 3-5 câu, với:
    1. Một điểm chung (nền tảng công nghệ, sở thích, công ty).
    2. Một câu hỏi mở để kích thích phản hồi.
    3. Không trích dẫn trực tiếp thông tin từ LinkedIn (để tránh bị flag).

    Kết quả phải trả về dưới dạng JSON:
    {
      "message": "Tin nhắn cá nhân hóa",
      "leadId": "{lead-id}"
    }"
    ```
- **Node `Add to Google Sheet`**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đặt tên sheet (ví dụ: "LinkedIn Leads").
  - **Range**: `A1` (để ghi dữ liệu từ đầu sheet).

##### **🔹 Node 8: Aggregate (aggregate)**
- **Mục đích**: Kết hợp lead và tin nhắn cá nhân hóa thành một JSON duy nhất.
- **Lưu ý**: Chọn `jsonPath` = `$.json()` để kết hợp dữ liệu từ node trước.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một request mẫu qua form (ví dụ: *"Nhân viên kỹ thuật AI tại Việt Nam"*).
   - Kiểm tra output từ mỗi node để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[TIẾP CẬN THÊM]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `webhook` để nhận thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn Slack khi có lead mới:
     ```json
     {
       "text": "🚀 Lead mới được tìm thấy: {{ $node["Add to Google Sheet"].json()["name"] }} ({{ $node["Add to Google Sheet"].json()["company"] }})",
       "channel": "#linkedin-leads"
     }
     ```
2. **Lưu Log Dữ Liệu**:
   - Sử dụng node `stickyNote` để ghi lại lỗi hoặc thông tin debug.
3. **Báo Cáo Định Kỳ**:
   - Thêm node `googleSheets` để tạo báo cáo hàng tuần về số lead, tỷ lệ phản hồi.
4. **Optimize Apollo Search**:
   - Nếu Apollo có API, thay vì Apify, các sếp có thể gọi API trực tiếp để tiết kiệm chi phí.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược marketing thay vì công việc thủ công. Với **AI cá nhân hóa**, tỷ lệ kết nối thành công sẽ tăng đáng kể, đồng thời **tự động hóa toàn bộ quy trình** từ tìm kiếm đến gửi tin nhắn.

**👉 Bắt đầu ngay!**
1. **Cài đặt VPS n8n** (👉 [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với 5-10 lead** trước khi chạy full scale.

**Chúc các sếp thành công!** 🚀