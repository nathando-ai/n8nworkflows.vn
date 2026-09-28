---
title: "🚀 **Tự Động Hóa Thông Tin Doanh Nghiệp Mới Nhất: Theo Dõi Crunchbase Với Tóm Tắt AI & Email Cảnh Báo**"
description: "Workflow tự động hóa 100% không code giúp các sếp startup theo dõi cập nhật mới nhất từ Crunchbase, tóm tắt thông tin bằng AI, và gửi email cảnh báo hàng ngày. Tiết kiệm thời gian nghiên cứu, cập nhật nhanh chóng về đối thủ và xu hướng thị trường."
slug: "tieu-dong-thong-tin-doanh-nghiep-crunchbase-ai-email"
tags: [n8n, automation, no-code, startup, crunchbase, ai-summarization, email-alerts]
keywords: [n8n workflow crunchbase, tự động hóa startup, tóm tắt thông tin doanh nghiệp bằng AI, email cảnh báo cập nhật công ty, theo dõi đối thủ cạnh tranh]
---

# 🚀 **Tự Động Hóa Thông Tin Doanh Nghiệp Mới Nhất: Theo Dõi Crunchbase Với Tóm Tắt AI & Email Cảnh Báo**

## **🔍 Nỗi Đau Của Các Sếp Startup**
Các sếp startup và nhà đầu tư thường phải mất **giờ đồng hồ** mỗi ngày để:
- **Lọc và theo dõi** các công ty mới ra mắt, vốn mới, hoặc thay đổi chiến lược từ Crunchbase.
- **Đọc và phân tích** mô tả chi tiết của hàng trăm công ty để tìm ra xu hướng thị trường.
- **Báo cáo** cho đội ngũ hoặc đầu tư về những thay đổi quan trọng.

**Workflow này giải quyết tất cả vấn đề đó bằng cách:**
✅ **Tự động lấy dữ liệu** từ Crunchbase về các công ty mới cập nhật trong 24h.
✅ **Tóm tắt bằng AI** (GPT-4) thành văn bản dễ đọc, với tiêu đề và nội dung email chuẩn.
✅ **Gửi email cảnh báo** hàng ngày (hoặc theo lịch) để các sếp **không bỏ lỡ bất kỳ thông tin quan trọng nào**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** so với cách làm thủ công.
- **Cập nhật tức thời** về đối thủ, đối tác tiềm năng, và xu hướng ngành.
- **Tóm tắt chuyên nghiệp** bằng AI, không cần viết tay.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa** được email theo nhu cầu (đầu tư, marketing, nghiên cứu).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Crunchbase API**:
   - Đăng ký API key tại [Crunchbase Developer Portal](https://data.crunchbase.com/docs).
   - **Lưu ý**: Crunchbase có giới hạn API call (miễn phí 1000 call/tháng). Nếu cần nhiều hơn, mua gói premium.
2. **Tài khoản Gmail OAuth 2.0**:
   - Cấu hình OAuth 2.0 cho Gmail trong n8n để gửi email tự động.
   - **Lưu ý**: Không sử dụng tài khoản Gmail cá nhân (dễ bị block). Sử dụng tài khoản doanh nghiệp.
3. **API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và tạo API key.
   - **Model khuyến nghị**: `gpt-4o-mini` (rẻ và hiệu quả).
4. **n8n Self-hosted** (không dùng phiên bản cloud):
   - Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4792) hoặc copy toàn bộ mã JSON dưới đây vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Editor → Nhấn `+` → Chọn `Import Workflow`.
  2. Dán mã JSON hoặc tải file `.json` đã download.
  3. Chọn **credentials** tương ứng cho mỗi node (xem chi tiết dưới đây).

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **7 node** chính. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **🔹 Node 1: `Trigger Manual Test` (Giao diện)**
- **Mục đích**: Dùng để **test thủ công** trước khi chạy tự động.
- **Lưu ý**:
  - Trong **sản xuất**, thay thế bằng **Cron Node** để chạy hàng ngày.
  - **Cách thêm Cron Node**:
    ```markdown
    - Thêm node `Cron` vào đầu workflow.
    - Cấu hình schedule: `0 8 * * *` (8h sáng hàng ngày).
    - Kết nối node này với `Fetch Crunchbase Updates`.
    ```

#### **🔹 Node 2: `Fetch Crunchbase Updates` (HTTP Request)**
- **Mục đích**: Lấy dữ liệu từ Crunchbase về các công ty mới cập nhật trong 24h.
- **Cấu hình cần chỉnh**:
  - **URL**: `https://api.crunchbase.com/api/v4/entities/organizations`
  - **Headers**:
    ```
    Authorization: Bearer <CRUNCHBASE_API_KEY>
    ```
  - **Query Parameters**:
    ```
    updated_since: <YESTERDAY_DATE>  # Ngày hôm qua (format: YYYY-MM-DD)
    limit: 100  # Lấy tối đa 100 công ty (để tránh quá tải API)
    ```
  - **Lưu ý**:
    - Thay `<CRUNCHBASE_API_KEY>` bằng API key của mình.
    - Thay `<YESTERDAY_DATE>` bằng ngày hôm qua (ví dụ: `2024-05-20`).

#### **🔹 Node 3: `Extract Company Details` (Set)**
- **Mục đích**: Lọc và chuẩn hóa dữ liệu từ Crunchbase thành định dạng dễ đọc.
- **Cấu hình**:
  - **Expression** (để lấy các trường cần thiết):
    ```json
    {
      "name": $json.data.items[0].name,
      "description": $json.data.items[0].description,
      "location": $json.data.items[0].location.city,
      "industry": $json.data.items[0].industry,
      "updated_at": $json.data.items[0].updated_at
    }
    ```
  - **Lưu ý**:
    - Nếu Crunchbase trả về nhiều công ty, cần **loop** qua danh sách bằng node `Loop`.
    - Ví dụ cấu hình loop:
      ```json
      $json.data.items
      ```

#### **🔹 Node 4: `Summarizer Agent` (AI Agent)**
- **Mục đích**: Sử dụng AI (GPT-4) để tóm tắt thông tin công ty thành văn bản ngắn gọn.
- **Cấu hình cần chỉnh**:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
  - **Model**: `gpt-4o-mini` (hoặc `gpt-3.5-turbo` nếu muốn tiết kiệm chi phí).
  - **Prompt** (đã được định sẵn trong workflow):
    ```txt
    You are a helpful assistant that summarizes Crunchbase company updates.

    Output your response strictly as valid JSON with two properties:
    - "subject": a string for the email subject line.
    - "body": a string for the email content formatted in plain text. Use "\n" for new lines inside the string.

    Do NOT output anything other than the JSON object.
    Ensure the JSON is well-formed with no trailing commas or syntax errors.
    ```
  - **Input Data**:
    - Điền vào `input` của node `agent`:
      ```json
      {
        "company_name": "{{$node["Extract Company Details"].json.name}}",
        "description": "{{$node["Extract Company Details"].json.description}}",
        "location": "{{$node["Extract Company Details"].json.location}}",
        "industry": "{{$node["Extract Company Details"].json.industry}}",
        "updated_at": "{{$node["Extract Company Details"].json.updated_at}}"
      }
      ```

#### **🔹 Node 5: `Structured Output Parser`**
- **Mục đích**: Đảm bảo AI trả về định dạng JSON chuẩn để n8n xử lý.
- **Lưu ý**:
  - Node này **bắt buộc** để trích xuất `subject` và `body` từ JSON.
  - Không cần chỉnh gì thêm, chỉ cần kết nối sau node `agent`.

#### **🔹 Node 6: `Send Email with Summary` (Gmail)**
- **Mục đích**: Gửi email cảnh báo với tóm tắt AI.
- **Cấu hình cần chỉnh**:
  - **Credentials**: Chọn `gmailOAuth2` (đã cấu hình OAuth 2.0).
  - **Email To**: Điền địa chỉ email nhận (ví dụ: `team@doanhnghiep.com`).
  - **Subject**: `{{$json.subject}}` (trích xuất từ AI).
  - **Body**: `{{$json.body}}` (nội dung email từ AI).
  - **Lưu ý**:
    - **Không dùng tài khoản Gmail cá nhân** (dễ bị block).
    - **Test email** trước khi chạy sản xuất.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy node `Trigger Manual Test` để kiểm tra workflow.
   - Kiểm tra email nhận được có đúng định dạng không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.
   - Nếu dùng **Cron Node**, đảm bảo nó được kết nối đúng với node `Fetch Crunchbase Updates`.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Gửi email cho nhiều người**:
   - Thay `Email To` trong node Gmail bằng danh sách email (ví dụ: `team1@doanhnghiep.com, team2@doanhnghiep.com`).
2. **Lưu log vào Google Sheets**:
   - Thêm node `Google Sheets` sau node `Send Email` để ghi lại lịch sử cập nhật.
   - Cấu hình:
     ```json
     {
       "sheet_name": "Crunchbase_Updates",
       "data": {
         "Company": "{{$node["Extract Company Details"].json.name}}",
         "Subject": "{{$json.subject}}",
         "Date": "{{$node["Fetch Crunchbase Updates"].json.data.items[0].updated_at}}"
       }
     }
     ```
3. **Kết nối với Slack/Telegram**:
   - Thêm node `Slack` hoặc `Telegram Bot` để thông báo tức thời khi có cập nhật mới.
4. **Lọc công ty theo ngành**:
   - Thêm node `Filter` trước node `Summarizer Agent` để chỉ lấy công ty thuộc ngành cần theo dõi.
   - Ví dụ:
     ```json
     {{$node["Extract Company Details"].json.industry}} === "AI" || {{$node["Extract Company Details"].json.industry}} === "Fintech"
     ```
5. **Tự động cập nhật API key**:
   - Sử dụng node `Set` để thay đổi API key nếu hết hạn.
   - Ví dụ:
     ```json
     {
       "crunchbase_api_key": "NEW_API_KEY_HERE"
     }
     ```
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp startup muốn:
✔ **Tự động hóa theo dõi đối thủ** mà không cần viết code.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược.
✔ **Cập nhật tức thời** về xu hướng thị trường.

**Hành động ngay**:
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Cấu hình API keys** (Crunchbase, OpenAI, Gmail).
3. **Import workflow** và **bật chạy**!

**Nếu gặp vấn đề**, liên hệ với tác giả qua:
- **LinkedIn**: [Yaron Been](https://www.linkedin.com/in/yaronbeen/)
- **YouTube**: [Yaron Been](https://www.youtube.com/@YaronBeen/videos)

---
**🚀 Chúc các sếp thành công với việc tự động hóa thông tin doanh nghiệp!**