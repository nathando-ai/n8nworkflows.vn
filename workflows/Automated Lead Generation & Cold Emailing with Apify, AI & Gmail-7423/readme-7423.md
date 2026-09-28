---
title: "🚀 Tự Động Hóa Tìm Kiếm & Gửi Email Lạnh AI Cho Doanh Nghiệp - Khai Thác Lead Tiềm Năng 24/7"
description: "Workflow tự động hóa tìm kiếm lead doanh nghiệp từ website, trích xuất email chính xác bằng AI Gemini/OpenAI, và gửi email lạnh cá nhân hóa qua Gmail - tiết kiệm 80% thời gian marketing cho các sếp."
slug: "tieu-dong-hoa-tim-kiem-email-lanh-ai"
tags: [n8n, automation, lead-generation, ai-chatbot, gmail-integration, google-sheets, apify]
keywords: [n8n workflow tự động hóa, tìm kiếm lead doanh nghiệp, email lạnh AI, tự động hóa marketing, apify + n8n, gemini openai trong n8n]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Lead & Gửi Email Lạnh AI - Giải Pháp Marketing 100% Không Code**

## **Nỗi Đau Của Các Sếp Trong Marketing Bán Hàng**
Bạn đã bao giờ phải:
- **Tìm kiếm thủ công** thông tin liên hệ của khách hàng tiềm năng trên Google, LinkedIn hay website?
- **Gửi email lạnh** hàng chục, hàng trăm bản mà chỉ có tỷ lệ phản hồi thấp?
- **Phải update dữ liệu lead** vào Google Sheets mỗi ngày để theo dõi?
- **Mất thời gian** viết nội dung email cá nhân hóa cho từng lead?

**Workflow này giải quyết tất cả!** Với sự kết hợp giữa **Apify (scraping website)**, **AI Gemini/OpenAI (trích xuất email & viết email)**, và **Gmail (gửi tự động)**, bạn sẽ:
✅ **Tìm kiếm lead** từ website doanh nghiệp chỉ trong vài giây
✅ **Trích xuất email chính xác** bằng AI (không cần nhập thủ công)
✅ **Gửi email lạnh cá nhân hóa** tự động, với tỷ lệ mở cao hơn 50%
✅ **Theo dõi tất cả lead** trên Google Sheets, sẵn sàng cho các bước tiếp theo

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công
- **Tỷ lệ chuyển đổi cao** nhờ email cá nhân hóa bằng AI
- **Hoạt động 24/7** mà không cần can thiệp
- **Dữ liệu lead sạch** được lưu trữ trên Google Sheets
- **Không cần kỹ năng code** - chỉ cần cấu hình API
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scraping website)
   - [Đăng ký miễn phí Apify](https://apify.com/)
   - Tạo **1 Actor** (công cụ scraping) và lấy **URL Endpoint** (sẽ dùng trong node `HTTP Request`).

2. **API Key Google Gemini** (trích xuất email)
   - [Đăng ký API Key Gemini](https://aistudio.google.com/apikey)
   - Thêm vào node `Google Gemini Chat Model`.

3. **API Key OpenAI** (viết email lạnh)
   - [Đăng ký API Key OpenAI](https://platform.openai.com/)
   - Chọn mô hình `gpt-4.1-mini` (đã được cấu hình sẵn trong workflow).

4. **Google Sheets** (lưu trữ lead)
   - Tạo 1 bảng Google Sheets với **cột sau** (để workflow append dữ liệu):
     - `Company Name`, `Website`, `Phone`, `Email`, `Address`, `Category`, `Cold Mail Status`, `Send Time`.
   - **Chia sẻ bảng** với quyền **Editor** cho n8n.

5. **Tài khoản Gmail** (gửi email tự động)
   - **Không dùng 2FA** (n8n không hỗ trợ 2FA hiện tại).
   - Cấu hình **App Password** nếu đã bật 2FA:
     - [Hướng dẫn tạo App Password](https://myaccount.google.com/apppasswords).

6. **n8n Self-hosted** (để workflow chạy 24/7)
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/7423](https://n8n.io/workflows/7423) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7423) và paste vào **Import Workflow** trên n8n.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import Workflow**.
2. Chọn **Paste JSON** và dán toàn bộ mã từ [n8n.io/workflows/7423](https://n8n.io/workflows/7423).
3. Nhấn **Import**.

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **🔹 Bước 1: Cấu Hình Form Trigger (Tìm kiếm Lead)**
- Node: **"On form submission"** (type: `formTrigger`)
- **Cấu hình các trường form** (để người dùng nhập yêu cầu tìm kiếm):
  - `Business Type` (Loại doanh nghiệp: Công ty TNHH, Cổ phần, Startup...)
  - `Location` (Địa chỉ: Hà Nội, TP.HCM, Quốc tế...)
  - `Lead Number` (Số lượng lead muốn tìm)
  - `Email Style` (Chọn kiểu email: Cá nhân hóa, Chuyên nghiệp, Giới thiệu sản phẩm...)
- **Lưu ý**: Các trường này sẽ được sử dụng để **lọc và gửi email** sau này.

#### **🔹 Bước 2: Kết Nối Apify (Scraping Website)**
- Node: **"HTTP Request"** (type: `httpRequest`)
- **Thay đổi URL Endpoint**:
  - Thay `Apify_Actor_Endpoint_URL` bằng **URL Actor** của bạn từ Apify.
  - Ví dụ:
    ```json
    "url": "https://api.apify.com/v2/actors/YOUR_ACTOR_ID/runs"
    ```
  - **Headers** cần thêm:
    ```json
    {
      "Authorization": "Bearer YOUR_APIFY_API_TOKEN",
      "Content-Type": "application/json"
    }
    ```
  - **Body** (gửi yêu cầu scraping):
    ```json
    {
      "input": {
        "startUrls": ["https://website-can-scrape.com"],
        "maxRequests": 100
      }
    }
    ```

#### **🔹 Bước 3: Trích Xuất Email Bằng AI (Gemini & OpenAI)**
- **Node 1: "Information Extractor"** (type: `informationExtractor`)
  - **API Key**: Điền `API_KEY_GOOGLE_GEMINI` (từ bước chuẩn bị).
  - **Prompt** (đã cấu hình sẵn):
    ```
    Extract the best email address from the business website.
    If no email found, return "No email found".
    ```
  - **Lưu ý**: Node này sẽ **lọc email chính xác** từ trang web scraped.

- **Node 2: "OpenAI Chat Model"** (type: `lmChatOpenAi`)
  - **API Key**: Điền `API_KEY_OPENAI`.
  - **Prompt** (viết email lạnh):
    ```
    Write a cold email for {company_name} with the following details:
    - Business type: {business_type}
    - Location: {location}
    - Subject: "Chào {company_name}, Tôi là {your_name} từ {your_company}"
    - Body: "Tôi đã nghiên cứu về {company_name} và thấy rằng {specific_value_proposition}. Tôi muốn giới thiệu {your_product} vì {reason}..."
    Keep it professional and under 200 words.
    ```

#### **🔹 Bước 4: Lọc & Lưu Lead Vào Google Sheets**
- Node: **"Filter"** (type: `filter`)
  - **Cấu hình**: Chỉ giữ lead có `Email` không trống.
- Node: **"Append row in sheet"** (type: `googleSheets`)
  - **Chọn Sheet**: Điền tên bảng Google Sheets đã tạo.
  - **Headers**: Đảm bảo trùng khớp với cột trong bảng (ví dụ: `Company Name`, `Email`, `Website`...).
- Node: **"Append or update row in sheet"** (type: `googleSheets`)
  - **Cấu hình tương tự**, nhưng dùng để **cập nhật trạng thái** của lead (ví dụ: `Cold Mail Status: "Sent"`).

#### **🔹 Bước 5: Gửi Email Lạnh Tự Động**
- Node: **"Send a message"** (type: `gmail`)
  - **Chọn tài khoản Gmail** đã cấu hình.
  - **Thiết lập template email**:
    - **Subject**: `$json["subject"]` (trích từ OpenAI).
    - **Body**: `$json["body"]` (trích từ OpenAI).
    - **Người nhận**: `$json["email"]`.
  - **Lưu ý**:
    - **Không dùng 2FA** (n8n không hỗ trợ).
    - Nếu Gmail yêu cầu **App Password**, điền vào **Password** thay vì mật khẩu chính.

#### **🔹 Bước 6: Loop Over Items (Gửi Batch Email)**
- Node: **"Loop Over Items"** (type: `splitInBatches`)
  - **Cấu hình**:
    - `Batch Size`: 5 (gửi 5 email/lần để tránh bị chặn).
    - `Wait Between Batches`: 60 giây (tránh bị đánh dấu spam).
  - **Node "Wait"** (type: `wait`):
    - Thời gian chờ giữa các batch: **60 giây**.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập vào **Form Trigger** (ví dụ: `Business Type: Công ty TNHH`, `Location: Hà Nội`, `Lead Number: 3`).
   - Nhấn **Run Workflow** để kiểm tra:
     - Email có được trích xuất không?
     - Email có được gửi thành công không?
     - Dữ liệu có được lưu vào Google Sheets không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ `Inactive` sang `Active`.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Kết Nối Slack/Telegram để Báo Lỗi**
- Thêm node **`slack`** hoặc **`telegram`** sau node **`gmail`** để nhận thông báo khi email gửi thành công/lỗi.
- **Cấu hình**:
  - **Slack**: Thêm node `slackNotification` và điền `Webhook URL`.
  - **Telegram**: Thêm node `telegramBot` và điền `Chat ID`.

### **🔹 2. Lưu Log Tất Cả Hoạt Động**
- Thêm node **`stickyNote`** sau node **`gmail`** để ghi log:
  ```json
  {
    "text": `Email sent to ${$json["email"]} at ${new Date().toLocaleString()}`,
    "color": "#4CAF50"
  }
  ```
- **Kết quả**: Tất cả email đã gửi sẽ được lưu trong **Sticky Notes** để theo dõi.

### **🔹 3. Gửi Báo Cáo Định Kỳ (Hàng Tuần)**
- Thêm node **`googleSheets`** mới để tạo **báo cáo tổng hợp**:
  - **Query**: Lấy tất cả lead trong tuần qua.
  - **Cột mới**: `Weekly Status` (ví dụ: "Active", "Inactive").
  - **Gửi báo cáo qua email** bằng node **`gmail`**.

### **🔹 4. Sử Dụng AI Gemini Pro (Nâng Cao)**
- Nếu muốn **trích xuất email chính xác hơn**, thay thế `gpt-4.1-mini` bằng **Gemini Pro** (tính phí cao hơn nhưng hiệu quả hơn).
- **Cấu hình**:
  ```json
  {
    "model": {
      "__rl": true,
      "mode": "list",
      "value": "gemini-pro"
    }
  }
  ```

### **🔹 5. Tối Ưu Hóa Tỷ Lệ Mở Email**
- **Thêm node `informationExtractor`** sau node `gmail` để:
  - **Trích xuất tên người nhận** từ email (nếu có).
  - **Cập nhật subject** thành: `"Chào {name}, Tôi là {your_name}..."`.
- **Kết quả**: Tỷ lệ mở email tăng **30-50%**.

---

## **📌 Kết Luận: Bắt Đầu Tự Động Hóa Marketing Ngay Hôm Nay!**

Workflow này không chỉ **giải phóng thời gian** cho các sếp mà còn **tăng tỷ lệ chuyển đổi** nhờ email cá nhân hóa và AI. **Không cần code**, chỉ cần **cấu hình API** và **n8n Self-hosted**, bạn đã có một **công cụ marketing tự động 24/7**.

### **🚀 Bước Tiếp Theo**
1. **Đăng ký VPS** để n8n chạy ổn định:
   - 👉 [TinoHost (39% giảm)](https://tino.vn/vps-n8n?affid=388)
   - 👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và **cấu hình API** theo hướng dẫn.
3. **Test run** với 1-2 lead mẫu.
4. **Bật Active** và **đợi AI làm việc cho bạn!**

**💡 Lời khuyên cuối cùng**: Đừng quên **theo dõi Google Sheets** và **cập nhật lead** định kỳ để tối ưu hóa hiệu quả!

---
**🔥 Cảm ơn các sếp đã đọc đến cuối!** Nếu có vấn đề, hãy để lại