---
title: "🚀 Tự Động Hóa Email Outreach B2B Cá Nhân Hóa Siêu Tốc với Apollo, LinkedIn, GPT-4.1 & SendGrid (N8n)"
description: "Workflow tự động hóa email B2B siêu cá nhân hóa, tích hợp Apollo.io, LinkedIn, GPT-4.1 và SendGrid để tự động tìm kiếm, phân tích và gửi email outreach với tỷ lệ mở cao, tiết kiệm 80% thời gian so với thủ công. Phù hợp cho các doanh nghiệp bán hàng B2B, startup và team marketing."
slug: "tieu-dong-hoa-email-outreach-b2b-canh-nhac-gpt-4-1"
tags: [n8n, automation, lead-nurturing, gpt-4, sendgrid, apollo-io, linkedin, no-code, ai, b2b-marketing]
keywords: [n8n workflow email outreach, tự động hóa email B2B, gpt-4.1 cho outreach, apollo.io + linkedin + n8n, tự động hóa bán hàng B2B, sendgrid n8n, lead nurturing tự động]
---

# 🚀 **Tự Động Hóa Email Outreach B2B Cá Nhân Hóa Siêu Tốc với Apollo, LinkedIn, GPT-4.1 & SendGrid**

---

## **🔥 Bạn đang gặp vấn đề gì?**
- **Thủ công tìm kiếm leads** trên Apollo.io và LinkedIn mất hàng giờ mỗi ngày?
- **Email outreach không cá nhân hóa** dẫn đến tỷ lệ mở thấp (dưới 5%)?
- **Không biết cách kết hợp AI (GPT-4.1) để tự động viết email** phù hợp với từng lead?
- **Quá tải công việc** khi phải theo dõi hàng trăm leads mỗi tháng?

**Workflow này giải quyết tất cả!** Với **33 node n8n**, bạn sẽ tự động:
✅ **Scrape dữ liệu leads** từ Apollo.io và LinkedIn (bao gồm bài viết gần đây, thông tin cá nhân).
✅ **Phân tích và lọc leads không phù hợp** (tránh lãng phí thời gian).
✅ **Sử dụng GPT-4.1 tự động viết email outreach siêu cá nhân hóa** dựa trên hành vi, ngành nghề và sở thích của từng lead.
✅ **Gửi email qua SendGrid** với tỷ lệ mở **trên 20%** (so với 2-3% của email thông thường).
✅ **Cập nhật trạng thái outreach** trên Supabase để theo dõi hiệu quả.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và xử lý hàng trăm leads mỗi ngày, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Tỷ lệ mở email tăng gấp 5-10x** nhờ nội dung siêu cá nhân hóa.
- **Tự động lọc leads không phù hợp** (giảm chi phí quảng cáo).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dữ liệu leads được cập nhật liên tục** từ Apollo.io và LinkedIn.
- **Gửi email qua SendGrid** với tính năng anti-spam cao.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
| **Tài nguyên**               | **Chi tiết**                                                                 | **Lưu ý**                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Apollo.io**                | Tài khoản Apollo.io (đăng ký [tại đây](https://www.apollo.io/)).           | Cần **API Key** để scrape dữ liệu.                                        |
| **LinkedIn**                  | Tài khoản LinkedIn cá nhân (để scrape dữ liệu công khai).                  | Không cần API, nhưng **tránh bị chặn** bằng cách sử dụng proxy.          |
| **OpenAI (GPT-4.1)**          | API Key từ [OpenAI](https://platform.openai.com/) (đăng ký miễn phí).      | **Khuyến nghị**: Nạp tiền để tránh giới hạn token (7000-12000 token/run). |
| **SendGrid**                  | API Key từ [SendGrid](https://sendgrid.com/) (đăng ký miễn phí).             | Cần **SMTP hoặc API Key** để gửi email.                                  |
| **Supabase**                  | Database miễn phí từ [Supabase](https://supabase.com/) (để lưu leads).      | Cần **table** để lưu trữ dữ liệu leads và trạng thái outreach.            |
| **Twilio (SMTP - tùy chọn)**  | Nếu muốn sử dụng SMTP thay vì SendGrid.                                    | Khuyến nghị để **tránh bị chặn email**.                                  |
| **RapidAPI (tùy chọn)**       | Nếu muốn scrape LinkedIn với tốc độ cao hơn.                              | **Free tier chỉ cho phép 20-25 scrape**, sau đó cần trả phí.               |

---
:::note[Lưu ý quan trọng]
- **Không cần code**: Workflow hoàn toàn **no-code**, chỉ cần cấu hình các node.
- **Dữ liệu scrape từ Apollo.io và LinkedIn là công khai**, không vi phạm chính sách.
- **GPT-4.1 sẽ tự động viết email** dựa trên:
  - **Thông tin cá nhân** (tên, ngành nghề, vị trí công việc).
  - **Bài viết gần đây** trên LinkedIn (để cá nhân hóa nội dung).
  - **Sản phẩm/dịch vụ** của bạn (do bạn cung cấp trong workflow).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/6039) (ấn **Export**).
2. **Mở n8n Editor** trên máy chủ của bạn ([n8n.io](https://n8n.io/)).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải workflow** từ link trên và copy toàn bộ JSON.
2. Trong **n8n Editor**, nhấn **"+ New Workflow"**.
3. Chọn **Import from JSON** và dán JSON vào.
4. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **phức tạp** và cần cấu hình cẩn thận. Dưới đây là **các node quan trọng** cần chỉnh:

#### **🔹 Apollo Scraper (httpRequest)**
- **URL**: Copy **link filter** từ Apollo.io (ví dụ: `https://apollo.io/search?filters=...`).
  - Ví dụ:
    ```plaintext
    "https://apollo.io/search?filters=company_name:Google&limit=100"
    ```
- **Headers**:
  - `Authorization`: `Bearer YOUR_APOLLO_API_KEY`
  - `User-Agent`: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`
- **Method**: `GET`

#### **🔹 LinkedIn Data & Posts (httpRequest)**
- **URL**:
  - **LinkedIn Profile**: `https://api.linkedin.com/v2/people/~:(id,first-name,last-name,headline,profile-picture){?projection}` (sử dụng **RapidAPI** nếu cần).
  - **LinkedIn Posts**: `https://api.linkedin.com/v2/ugcPosts?q=author&author=urn:li:person:YOUR_LINKEDIN_ID&projection=(id,author,title,content,created)`.
- **Headers**:
  - `Authorization`: `Bearer YOUR_LINKEDIN_API_KEY` (nếu có).
  - `X-RapidAPI-Key`: `YOUR_RAPIDAPI_KEY` (nếu dùng RapidAPI).
- **Lưu ý**:
  - **Free tier của RapidAPI chỉ cho phép 20-25 scrape**, sau đó cần trả phí (~$20/tháng).
  - Nếu không muốn trả phí, **sử dụng scraping thủ công** (nhưng chậm hơn).

#### **🔹 OpenAI Chat Model (lmChatOpenAi)**
- **API Key**: Điền vào **n8n Credentials** (Settings → Credentials → Add → OpenAI).
- **Model**: Chọn **gpt-4.1** (hoặc gpt-4-turbo nếu có).
- **Prompt Template**:
  ```plaintext
  "Tôi là một chuyên gia bán hàng B2B. Hãy viết một email outreach siêu cá nhân hóa cho lead sau:
  - Tên: {{firstName}}
  - Vị trí: {{jobTitle}}
  - Công ty: {{companyName}}
  - Ngành nghề: {{industry}}
  - Bài viết gần đây trên LinkedIn: {{lastPost}}

  Email phải:
  1. Giới thiệu sản phẩm/dịch vụ của tôi một cách ngắn gọn.
  2. Nêu ra **1-2 điểm tương đồng** giữa lead và sản phẩm của tôi (dựa trên bài viết gần đây).
  3. Kết thúc bằng một câu hỏi hoặc CTA (Call-to-Action) rõ ràng.
  4. Không quá 200 từ.

  Đừng viết email generic, hãy làm nó **cá nhân hóa 100%**!"
  ```
- **Temperature**: 0.7 (để email không quá ngẫu nhiên).

#### **🔹 SendGrid (sendGrid)**
- **API Key**: Điền vào **n8n Credentials** (Settings → Credentials → Add → SendGrid).
- **From Email**: Điền email bạn muốn gửi (ví dụ: `no-reply@têncôngty.com`).
- **To Email**: `{{email}}` (được scrape từ Apollo.io).
- **Subject**: `{{firstName}}, một lời khuyên từ {{companyName}}` (cá nhân hóa).
- **HTML Content**: Nội dung email từ OpenAI (được xử lý bởi **HTML Modifier** node).

#### **🔹 Supabase (supabase)**
- **Table**: Tạo **bảng "leads"** với các trường:
  | Trường          | Loại dữ liệu | Mô tả                          |
  |-----------------|--------------|--------------------------------|
  | id              | UUID         | ID duy nhất                    |
  | first_name      | Text         | Tên của lead                   |
  | last_name       | Text         | Họ của lead                    |
  | email           | Text         | Email của lead                 |
  | company_name    | Text         | Tên công ty                    |
  | job_title       | Text         | Vị trí công việc               |
  | industry        | Text         | Ngành nghề                      |
  | linkedin_url    | Text         | Link LinkedIn                  |
  | last_post       | Text         | Bài viết gần đây trên LinkedIn |
  | outreach_status | Text         | `pending`, `sent`, `irrelevant` |
  | outreach_date   | Timestamp    | Ngày gửi email                 |

- **Operation**:
  - **Irrelevant Leads**: `UPDATE leads SET outreach_status = 'irrelevant' WHERE id = {{id}}`.
  - **Successful Outreach**: `UPDATE leads SET outreach_status = 'sent', outreach_date = NOW() WHERE id = {{id}}`.

#### **🔹 Merge & Aggregate Nodes**
- **Merge**: Kết hợp dữ liệu từ Apollo.io, LinkedIn và OpenAI.
- **Aggregate**: Tóm tắt dữ liệu trước khi gửi đến OpenAI (để giảm token usage).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Test Workflow** và nhập **1 lead mẫu** (ví dụ: `https://www.linkedin.com/in/tenlead/`).
   - Kiểm tra:
     - Dữ liệu scrape có chính xác không?
     - Email được viết có cá nhân hóa không?
     - Email có được gửi thành công không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tăng tốc độ scrape với RapidAPI**
- Nếu **free tier của RapidAPI không đủ**, mua **gói Pro** (~$20/tháng) để scrape **nghìn leads/ngày**.
- **Lưu ý**: Nếu không mua, workflow sẽ **chậm và ngừng hoạt động sau 20-25 scrape**.

### **2. Lưu log hoạt động**
- Thêm **node `set`** sau **SendGrid** để lưu:
  ```json
  {
    "email": "{{email}}",
    "status": "sent",
    "date": "{{$node["SendGrid"].json["sentAt"]}}"
  }
  ```
- **Gửi log đến Slack/Telegram** để theo dõi:
  ```plaintext
  "📧 Email sent to {{email}} | Status: {{status}} | Date: {{date}}"
  ```

### **3. Tự động gửi báo cáo hàng tuần**
- Sử dụng **node `httpRequest` + `sendGrid`** để gửi **báo cáo tổng hợp** (ví dụ: số lead được tiếp cận, tỷ lệ phản hồi).
- **Dữ liệu báo cáo** lấy từ Supabase:
  ```sql
  SELECT
    outreach_status,
    COUNT(*) as count
  FROM leads
  WHERE outreach_date > NOW() - INTERVAL '7 days'
  GROUP BY outreach_status
  ```

### **4. Kết hợp với Slack/Telegram**
- Thêm **node `webhook`** để nhận thông báo khi:
  - Email được gửi thành công.
  - Lead bị loại vì không phù hợp.
  - Có lỗi xảy ra trong workflow.

### **5. Optimize token usage**
- **GPT-4.1 tiêu tốn ~7000-12000 token/run**.
- **Mẹo tiết kiệm token**:
  - Sử dụng **gpt-3.5-turbo** (rẻ hơn) nếu nội dung email không quá phức tạp.
  - **Lọc leads** trước khi gửi đến OpenAI (ví dụ: chỉ gửi cho leads có bài viết gần đây).

---
## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc thủ công**