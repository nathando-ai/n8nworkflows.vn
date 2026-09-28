---
title: "🚀 Tự Động Hóa Pipeline B2B Sales Tối Đa: Apollo Lead Gen + Mailgun Outreach + AI Trả Lời Tự Động (N8N)"
description: "Workflow này tự động hóa toàn bộ chuỗi từ tìm kiếm leads B2B trên Apollo, gửi email outreach qua Mailgun, đến quản lý trả lời tự động bằng AI (OpenAI/Anthropic) - giúp các sếp tiết kiệm 20-30 giờ/tháng và tăng tỷ lệ chuyển đổi lên 40%. Hoàn toàn không cần code!"
slug: "tieu-dong-hoa-pipeline-b2b-sales-apollo-mailgun-ai"
tags: [n8n, automation, b2b-sales, lead-generation, ai-outreach, mailgun, apollo, self-hosted]
keywords: [n8n workflow sales pipeline, tự động hóa outreach B2B, AI trả lời email tự động, Mailgun + Apollo + n8n, tự động hóa bán hàng không code]
---

# 🚀 **Tự Động Hóa Pipeline B2B Sales: Từ Lead Gen Đến Trả Lời AI (Không Cần Code!)**

### **Nỗi Đau Của Các Sếp Trong Bán Hàng B2B**
Các sếp đã từng phải:
- **Tìm kiếm leads** trên Apollo và copy-paste vào Excel hàng giờ mỗi ngày.
- **Gửi email outreach** thủ công qua Mailgun, chỉ để nhận **tỷ lệ mở thấp** và **trả lời chậm chạp**.
- **Phản hồi khách hàng** bằng cách viết lại email một cách lặp đi lặp lại, mất thời gian và dễ sai sót.
- **Không biết liệu email đã được gửi** hay đã được trả lời, dẫn đến **trùng lặp hoặc bỏ lỡ cơ hội**.

**Workflow này giải quyết tất cả!** Nó tự động hóa **tất cả chuỗi bán hàng B2B** từ tìm kiếm leads đến gửi email và quản lý trả lời bằng AI, giúp các sếp **tiết kiệm 20-30 giờ/tháng** và **tăng tỷ lệ chuyển đổi lên 40%**.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động tìm kiếm leads** từ Apollo và lọc ra email hợp lệ (không spam, domain chính thức).
- **Gửi email outreach** theo chuỗi tự động (cold email, follow-up) với **tỷ lệ mở cao** nhờ AI tối ưu nội dung.
- **Trả lời tự động** cho khách hàng bằng AI (OpenAI/Anthropic), **cá nhân hóa** và **chuyên nghiệp** như người.
- **Theo dõi trạng thái email** (đã gửi, đã mở, đã trả lời) và **cập nhật dữ liệu** vào Supabase/PostgreSQL.
- **Báo cáo tự động** qua Telegram, giúp các sếp **quản lý pipeline** một cách minh bạch.
- **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào thời gian làm việc.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ               | API Key / Credentials          | Ghi Chú                                  |
|-----------------------|--------------------------------|-------------------------------------------|
| **Apollo.io**         | API Key                       | Để tìm kiếm leads B2B.                   |
| **Mailgun**           | Domain + API Key              | Để gửi email outreach.                   |
| **OpenAI**            | API Key                       | Để sử dụng AI tạo nội dung email & trả lời. |
| **Anthropic (Claude)**| API Key                       | Lựa chọn thay thế OpenAI (nếu muốn).    |
| **Supabase/PostgreSQL**| URL, Database Name, Credentials | Lưu trữ leads và lịch sử email.         |
| **Telegram Bot**      | Token Bot                     | Gửi báo cáo tự động.                    |
| **Gmail**            | Email + OAuth 2.0 Credentials | Theo dõi email đã gửi và trả lời.         |
| **Apify**            | API Key                       | Nếu sử dụng scraper tự động.             |

### **2. Cấu Hình Hệ Thống**
- **n8n Self-hosted** (không dùng phiên bản cloud) để **hoạt động 24/7** và tránh giới hạn.
- **VPS 4GB RAM** (để chạy AI và nhiều node đồng thời).
- **Node.js v18+** (để chạy n8n và các node LangChain).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7410](https://n8n.io/workflows/7410) (ấn nút **Export**).
2. **Mở n8n Editor** trên VPS của mình.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** và workflow sẽ xuất hiện trong danh sách.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải workflow** từ link trên và copy toàn bộ JSON.
2. **Mở n8n Editor** → **Tạo workflow mới** → **Nhấn "Import"** → **Chọn "Paste JSON"**.
3. **Xác nhận** và workflow sẽ được tạo.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Node Apollo (Tìm kiếm Leads)**
- **Node:** `Run an Actor` (Apify)
  - **Cấu hình:**
    - **Actor:** `apollo-io-scraper` (hoặc tương tự).
    - **Input:**
      ```json
      {
        "startUrls": ["https://www.apollo.io/search?query=tech+startup"],
        "maxItems": 1000,
        "selectors": {
          "email": ".email-link::attr(href)",
          "name": ".company-name::text",
          "company": ".company-link::text"
        }
      }
      ```
  - **Lưu ý:** Thay đổi `query` để tìm kiếm ngành nghề phù hợp.

#### **B. Lọc Email Hợp Lệ (Tránh Spam)**
- **Node:** `Only Keep Verified Emails` (Filter)
  - **Cấu hình:**
    - **Condition:**
      ```js
      $email.includes("@") && !$email.includes("gmail") && !$email.includes("yahoo")
      ```
  - **Lưu ý:** Cần **cập nhật domain blacklist** nếu cần.

#### **C. Tạo Email Outreach Bằng AI**
- **Node:** `create email sequence` (Agent)
  - **Cấu hình:**
    - **Prompt:**
      ```plaintext
      Tôi là [Tên Bạn], từ [Công Ty]. Hãy viết một chuỗi email outreach 3 bước cho lead [Tên Lead] ở [Công Ty Lead], với tiêu đề:
      1. Email Cold: "Cách [Công Ty Bạn] Tiết Kiệm 30% Chi Phí [Dịch Vụ]"
      2. Follow-up: "Lời Mời Tham Gia Webinar Miễn Phí"
      3. Last Follow-up: "Câu Hỏi Cuối Cùng Trước Khi Kết Thúc"
      ```
    - **Model:** `gpt-4` (hoặc `claude-2`).
  - **Lưu ý:** **Thay đổi prompt** để phù hợp với ngành nghề.

#### **D. Gửi Email qua Mailgun**
- **Node:** `Mailgun` / `Mailgun1` / `Mailgun6` / `Mailgun7` / `Mailgun8` / `Mailgun9`
  - **Cấu hình chung:**
    - **Domain:** `your-domain.mx.mailgun.org`
    - **API Key:** `your-mailgun-api-key`
    - **From:** `noreply@yourdomain.com`
    - **To:** `$json["email"]`
    - **Subject:** `$json["subject"]`
    - **Text:** `$json["body"]`
  - **Lưu ý:**
    - **Kiểm tra SPF/DKIM** để tránh email bị đánh dấu là spam.
    - **Thêm delay** giữa các email (ví dụ: 1 email/ngày/lead) để tránh bị chặn.

#### **E. Quản Lý Trả Lời Email Bằng AI**
- **Node:** `Professional Email Response Agent` (Agent)
  - **Cấu hình:**
    - **Prompt:**
      ```plaintext
      Tôi là [Tên Bạn], từ [Công Ty]. Hãy trả lời email của khách hàng [Tên Lead] với nội dung:
      - Nếu khách hàng hỏi về [Dịch Vụ X], hãy cung cấp giải pháp cụ thể.
      - Nếu khách hàng không trả lời, hãy gửi follow-up sau 3 ngày.
      - Trả lời phải **chuyên nghiệp, cá nhân hóa** và **không spam**.
      ```
    - **Model:** `gpt-4` (hoặc `claude-2`).
  - **Lưu ý:**
    - **Kết hợp với `Gmail Trigger`** để theo dõi email đã trả lời.
    - **Cập nhật trạng thái** (`replied = Yes`) vào PostgreSQL/Supabase.

#### **F. Lưu Trữ Dữ Liệu vào Supabase/PostgreSQL**
- **Node:** `Supabase1` / `Supabase2` / `Supabase3` / `Supabase4` / `Supabase11` / `Supabase12` / `Supabase13` / `Supabase14` / `Supabase15` / `Supabase16`
  - **Cấu hình chung:**
    - **URL:** `your-supabase-url`
    - **Database:** `your-database-name`
    - **Table:** `leads` / `email_campaigns` / `responses`
    - **Insert/Update Query:**
      ```sql
      INSERT INTO leads (email, name, company, status, last_contact)
      VALUES ($email, $name, $company, 'pending', NOW())
      ON CONFLICT (email) DO UPDATE SET status = 'pending', last_contact = NOW()
      ```
  - **Lưu ý:**
    - **Tạo schema** trước khi chạy workflow.
    - **Backup dữ liệu** định kỳ.

#### **G. Báo Cáo Tự Động qua Telegram**
- **Node:** `Confirmation message` / `Set Telegram message`
  - **Cấu hình:**
    - **Bot Token:** `your-telegram-bot-token`
    - **Chat ID:** `@your-telegram-username` (hoặc ID chat)
    - **Message:**
      ```plaintext
      🚀 **Báo cáo Pipeline Sales:**
      - Leads mới: {{ $json["new_leads"] }}
      - Email đã gửi: {{ $json["emails_sent"] }}
      - Email đã mở: {{ $json["emails_opened"] }}
      - Email đã trả lời: {{ $json["emails_replied"] }}
      ```
  - **Lưu ý:**
    - **Kết hợp với `Schedule Trigger`** để báo cáo hàng ngày.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - **Tạo 1 lead mẫu** trong Apollo và kiểm tra workflow.
   - **Kiểm tra email** đã được gửi và trả lời AI có hợp lý không.
   - **Xem báo cáo Telegram** có xuất hiện không.

2. **Bật Active workflow:**
   - **Nhấn "Active"** trên n8n Editor.
   - **Kiểm tra log** để đảm bảo không có lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Tỷ Lệ Mở Email**
- **Sử dụng AI tối ưu tiêu đề:**
  - Thay vì viết tiêu đề thủ công, **sử dụng node `General analysis` (OpenAI)** để AI đề xuất tiêu đề có tỷ lệ mở cao nhất.
  - **Prompt:**
    ```plaintext
    Tôi có danh sách 10 tiêu đề email. Hãy chọn 3 tiêu đề có tỷ lệ mở cao nhất cho lead [Tên Lead] ở [Công Ty Lead].
    ```

### **2. Theo Dõi Tỷ Lệ Trả Lời & Cập Nhật Pipeline**
- **Thêm node `Sort`** để sắp xếp leads theo:
  - **Trạng thái:** `pending` → `contacted` → `interested` → `closed`.
  - **Thời gian cuối cùng liên lạc.**
- **Sử dụng `Schedule Trigger`** để **cập nhật trạng thái hàng tuần.**

### **3. Kết Hợp với Slack/Telegram cho Nhóm Sales**
- **Thay thế Telegram bằng Slack:**
  - Sử dụng node **`slack`** (n8n-nodes-slack) để gửi báo cáo vào channel Sales.
- **Gửi thông báo khi có lead mới:**
  - **Node `User message` (Telegram Trigger)** → **Kết nối với Slack.**

### **4. Lưu Log Tất Cả Hoạt Động**
- **Sử dụng node `stickyNote`** để ghi lại:
  - **Lịch sử email đã gửi.**
  - **Lỗi xảy ra** (ví dụ: email bị reject).
- **Export log định kỳ** vào Excel để phân tích.

### **5. Tự Động Chuyển Leads Sang CRM**
- **Kết nối với HubSpot/Zoho CRM:**
  - Sử dụng node **`hubspot`** hoặc **`zoho`** để tự động chuyển leads từ Supabase sang CRM.
  - **Cấu hình:**
    ```json
    {
      "action": "createContact",
      "data": {
        "email": $email,
        "firstName": $firstName,
        "lastName": $lastName,
        "company": $company,
        "status": "lead"
      }
    }
    ```

---

## 📌 **Kết Luận**
Workflow này **tự động hóa toàn bộ pipeline B2B sales** từ tìm kiếm leads đến gửi email và quản lý trả lời bằng AI, giúp các sếp:
✅ **Tiết kiệm 20-30 giờ/tháng** (không cần copy-paste, gửi email thủ công).
✅ **Tăng tỷ lệ chuyển đổi lên 40%** nhờ email outreach tự động và AI trả