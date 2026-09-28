---
title: "🚀 Tự Động Hóa Email Lạnh Cá Nhân Hóa Với AI Gemini, Supabase & Smartlead - Giảm 90% Thời Gian Tìm Lead"
description: "Workflow này tự động tạo email lạnh cá nhân hóa từ dữ liệu lead trong Supabase, sử dụng AI Gemini để phân tích và tối ưu hóa nội dung, sau đó tự động thêm vào chiến dịch Smartlead. Giúp các sếp tiết kiệm 10+ giờ/tuần và tăng tỷ lệ phản hồi lên 30%."
slug: "tieu-dong-hoa-email-lanh-canh-nhan-hoa-ai-gemini-supabase-smartlead"
tags: [n8n, automation, no-code, lead-nurturing, ai-gemini, smartlead, supabase, cold-email]
keywords: [n8n workflow tự động hóa email lạnh, AI Gemini tự động hóa marketing, tự động hóa lead nurturing, tối ưu email lạnh với AI, tự động thêm lead vào Smartlead]
---

# 🚀 **Tự Động Hóa Email Lạnh Cá Nhân Hóa Với AI Gemini, Supabase & Smartlead**

## **💡 Nỗi Đau Của Các Sếp Trong Tìm & Gửi Email Lạnh**
Gửi email lạnh vẫn là một trong những chiến thuật hiệu quả nhất trong marketing và bán hàng, nhưng làm thủ công lại tốn thời gian và dễ bị bỏ qua:
- **Tạo nội dung email cá nhân hóa** cho từng lead mất từ 15-30 phút/email.
- **Tìm kiếm thông tin lead** từ nhiều nguồn khác nhau (LinkedIn, website, CRM) là công việc mệt mỏi.
- **Quản lý chiến dịch** và theo dõi phản hồi thủ công dẫn đến sai sót và mất hiệu quả.

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Tạo email lạnh cá nhân hóa** từ dữ liệu lead trong Supabase.
✅ **Phân tích và tối ưu hóa nội dung** bằng AI Gemini.
✅ **Tự động thêm lead vào chiến dịch Smartlead** để theo dõi và gửi tự động.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** bằng việc tự động hóa toàn bộ quy trình từ tìm lead đến gửi email.
- **Tăng tỷ lệ phản hồi lên 30%** nhờ nội dung email cá nhân hóa và tối ưu hóa bởi AI.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Tích hợp hoàn hảo** với Smartlead để quản lý chiến dịch hiệu quả.
- **Dễ dàng mở rộng** cho nhiều lead và chiến dịch khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Supabase** (để lưu trữ và quản lý lead):
   - API Key (`supabaseApi`) và URL của dự án Supabase.
   - Bảng dữ liệu chứa thông tin lead (cần có các trường như `email`, `name`, `company`, `position`, `website`, `social_media`).
2. **Tài khoản Smartlead**:
   - API Key và URL của Smartlead.
   - Chiến dịch đã được tạo sẵn (hoặc workflow sẽ tự động tạo).
3. **API Key Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://makersuite.google.com/app/apikey) để lấy `googlePalmApi`.
4. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - Để workflow hoạt động liên tục 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7713](https://n8n.io/workflows/7713) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
- Chọn **Create Workflow** và đặt tên (ví dụ: `Personalized Cold Email Generator`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **3 phần chính**:
- **Phần 1: Lấy dữ liệu lead từ Supabase** (`Get many rows`).
- **Phần 2: Xử lý và tạo email cá nhân hóa bằng AI Gemini** (`Google Gemini Chat Model1-6`, `Basic LLM Chain`, `Information Extractor`).
- **Phần 3: Tạo và thêm lead vào chiến dịch Smartlead** (`smatlead-create-campaign`, `smartlead-add-leads-to-campaign`).

##### **A. Cấu Hình Supabase**
- **Node `Get many rows`**:
  - Chọn `supabaseApi` trong **Credentials**.
  - Điền `Table Name` là tên bảng chứa lead (ví dụ: `leads`).
  - Thêm `Select` các trường cần lấy (ví dụ: `email`, `name`, `company`, `position`).
  - **Lưu ý**: Nếu bảng chưa có dữ liệu, cần thêm lead thủ công trước.

- **Node `Update a row` (3 lần)**:
  - Sử dụng cùng `supabaseApi`.
  - Cấu hình `Table Name` và `Column Name` để cập nhật trạng thái lead (ví dụ: `status = "processed"`).

##### **B. Cấu Hình Google Gemini AI**
- **Tất cả node `Google Gemini Chat Model1-6`**:
  - Chọn `googlePalmApi` trong **Credentials**.
  - **Prompt mẫu** (cần tùy chỉnh theo mục tiêu):
    ```json
    "You are a cold email expert. Generate a personalized cold email for {name} at {company} who works as {position}.
    Key points to include:
    - Mention their company's recent achievements (if available).
    - Reference their LinkedIn profile or website if provided.
    - Keep it concise (under 150 words).
    - End with a clear call-to-action (CTA).
    Email subject: [Suggest a subject line].
    Email body: [Write the email body]."
    ```
  - **Lưu ý**: Các `Basic LLM Chain` và `Information Extractor` sẽ tự động xử lý kết quả từ Gemini.

##### **C. Cấu Hình Smartlead**
- **Node `smatlead-create-campaign`**:
  - Chọn `httpRequest` và cấu hình:
    - **Method**: `POST`
    - **URL**: `https://api.smartlead.com/v1/campaigns` (tham khảo docs Smartlead).
    - **Headers**:
      ```json
      {
        "Authorization": "Bearer YOUR_SMARTLEAD_API_KEY",
        "Content-Type": "application/json"
      }
      ```
    - **Body**:
      ```json
      {
        "name": "Automated Cold Email Campaign",
        "type": "email",
        "settings": {
          "from_email": "your-email@example.com",
          "reply_to_email": "your-email@example.com",
          "subject": "Personalized Email from [Your Company]"
        }
      }
      ```
  - **Node `smartlead-add-leads-to-campaign`**:
    - **Method**: `POST`
    - **URL**: `https://api.smartlead.com/v1/campaigns/{campaign_id}/leads` (thay `{campaign_id}` bằng ID chiến dịch vừa tạo).
    - **Body**:
      ```json
      {
        "email": "{{$node["Get many rows"].json["email"]}}",
        "first_name": "{{$node["Get many rows"].json["name"]}}",
        "custom_fields": {
          "company": "{{$node["Get many rows"].json["company"]}}",
          "position": "{{$node["Get many rows"].json["position"]}}"
        }
      }
      ```

##### **D. Cấu Hình Schedule Trigger**
- **Node `Schedule Trigger`**:
  - Chọn **Cron Expression** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - **Lưu ý**: Nếu muốn chạy thủ công, có thể bỏ qua và kích hoạt bằng **Webhook** hoặc **Manual Trigger**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Execute Workflow** và kiểm tra kết quả:
    - Dữ liệu lead từ Supabase có được lấy đúng không?
    - Email cá nhân hóa có hợp lý không?
    - Lead có được thêm vào Smartlead thành công không?
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển **Status** từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram để báo cáo**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau `Update a row` để thông báo khi email đã được gửi thành công.
   - **Ví dụ**:
     ```json
     {
       "text": "✅ Email cá nhân hóa đã được gửi cho {{$node["Get many rows"].json["name"]}} tại {{$node["Get many rows"].json["company"]}}!"
     }
     ```

2. **Lưu Log vào Supabase**:
   - Thêm node `Update a row` để ghi lại thời gian gửi và trạng thái phản hồi (ví dụ: `last_sent_at`, `response_status`).

3. **Tối Ưu Hóa Prompt cho Gemini**:
   - Nếu tỷ lệ email không hiệu quả, thử cập nhật prompt để:
     - Thêm **ví dụ cụ thể** về email thành công.
     - Yêu cầu AI **tránh spam** và **tối ưu hóa CTA**.
   - **Prompt nâng cao**:
     ```json
     "You are a cold email expert. Generate a high-converting cold email for {name} at {company}.
     Rules:
     1. Keep it under 150 words.
     2. Start with a personal touch (mention their recent achievement if available).
     3. End with a strong CTA that encourages reply.
     4. Avoid sounding like a robot.
     Example:
     'Hi [Name],
     I noticed [Company] recently raised $X million in funding. Congrats!
     At [Your Company], we help [solve a specific problem they face].
     Would you be open to a quick chat next week to explore how we can help?
     Best,
     [Your Name]'
     Email subject: [Suggest a subject line].
     Email body: [Write the email body]."
     ```

4. **Kết Hợp với CRM khác**:
   - Nếu sử dụng HubSpot, Salesforce hoặc CRM khác, có thể thay thế Supabase bằng node tương ứng (ví dụ: `n8n-nodes-base.hubspot`).

5. **Duyệt Email Trước Gửi**:
   - Thêm node `n8n-nodes-base.code` để lọc email có nội dung không phù hợp hoặc trùng lặp.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược marketing và bán hàng cao cấp, trong khi AI và tự động hóa làm việc 24/7. **Tiết kiệm 10+ giờ/tuần** và **tăng tỷ lệ phản hồi lên 30%** chỉ với một workflow đơn giản!

👉 **Bắt đầu ngay**:
1. **Chuẩn bị tài khoản** Supabase, Smartlead và API Key Gemini.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và theo dõi kết quả!

**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ với tác giả [Rahi](https://www.linkedin.com/in/rahi/) để được hỗ trợ chi tiết! 🚀