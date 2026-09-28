---
title: "🚀 Tự Động Hóa Tìm Kiếm & Gửi Email Lạnh LinkedIn Siêu Cá Nhân Hóa Với AI (GPT-4.1 Mini) - Không Cần Code"
description: "Workflow tự động hóa tìm kiếm leads CEO tại New York trên LinkedIn, enrich dữ liệu, lọc email chất lượng cao và tạo draft email lạnh cá nhân hóa bằng GPT-4.1 Mini. Giúp các sếp tiết kiệm 10+ giờ/tháng và tăng tỷ lệ phản hồi lên 30%."
slug: "tieu-dong-hoa-tim-kiem-linkedin-email-lanh-ai"
tags: [n8n, automation, no-code, ai-automation, linkedin-lead-generation, gpt-4.1-mini, cold-email]
keywords: [n8n workflow linkedin, tự động hóa tìm kiếm leads, email lạnh cá nhân hóa, AI GPT-4.1 Mini, CRM tự động, lead generation]
---

# 🚀 **Tự Động Hóa Tìm Kiếm CEO LinkedIn + Email Lạnh Cá Nhân Hóa Với AI (Không Cần Code)**

### **🔥 Nỗi Đau Của Các Sếp Trong Bán Hàng & Marketing**
- **Tìm kiếm leads thủ công** trên LinkedIn mất **3-5 giờ/ngày**, nhưng lại chỉ thu được **5-10 lead chất lượng**.
- **Email lạnh không cá nhân hóa** dẫn đến **tỷ lệ mở thấp (5-10%)** và **tỷ lệ phản hồi gần như 0%**.
- **Dữ liệu leads không đầy đủ** (email, company info) khiến nội dung email trở nên **khô khan và không chuyên nghiệp**.
- **Phải review từng email** trước khi gửi, tốn thêm **thời gian và công sức**.

**Workflow này giải quyết tất cả!** Với **AI + Automatization**, các sếp sẽ:
✅ **Tự động tìm kiếm** CEO tại New York (hoặc bất kỳ vị trí nào) trên LinkedIn.
✅ **Enrich dữ liệu** (email, company info, about section) để **cá nhân hóa hoàn toàn** email.
✅ **Lọc email chất lượng cao** (score ≥ 70) để **tránh bounce và spam**.
✅ **Tạo draft email lạnh** bằng **GPT-4.1 Mini** (rẻ hơn GPT-4, hiệu quả hơn GPT-3.5).
✅ **Lưu leads vào Google Sheets** như một **CRM mini**, dễ dàng theo dõi và phân tích.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/tháng** cho việc tìm kiếm và tạo email lạnh.
- **Tăng tỷ lệ phản hồi lên 30%** nhờ nội dung **cá nhân hóa 100%**.
- **Giảm chi phí** so với dịch vụ lead gen truyền thống (từ **$50/lead** xuống **$0.5/lead**).
- **An toàn & kiểm soát hoàn toàn** (email chỉ là draft, không tự động gửi).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI CHẠY WORKFLOW**]
Để workflow hoạt động, các sếp cần:
✔ **Tài khoản Google** (để kết nối **Google Sheets** và **Gmail**).
✔ **Tài khoản Apify** (để tìm kiếm và enrich leads trên LinkedIn).
✔ **API Key OpenAI** (để sử dụng **GPT-4.1 Mini** tạo email).
✔ **Google Sheet** đã tạo sẵn (để lưu leads).
✔ **Gmail OAuth2** (để tạo draft email).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/15624](https://n8n.io/workflows/15624) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy hoặc VPS).
3. Nhấn **Import** → **Paste JSON** → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/15624](https://n8n.io/workflows/15624).
2. **Mở n8n Editor** → **Create New Workflow** → **Paste JSON** → **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

#### **🔹 Node 1: Schedule Trigger (Điều khiển lịch chạy)**
- **Thời gian mặc định**: **11:06 AM hàng ngày**.
- **Lưu ý**:
  - Nếu muốn chạy **ngày khác**, chỉnh sửa **cron expression** ở **Schedule Trigger**.
  - Ví dụ: `0 6 * * *` (6:00 AM hàng ngày).
  - **Không cần manual trigger** sau khi bật workflow.

#### **🔹 Node 2 & 3: Apify - Tìm Kiếm & Enrich Leads**
- **Tìm kiếm CEO tại New York** (hoặc thay đổi theo nhu cầu).
- **Cấu hình Apify**:
  - **Actor**: `linkedin-lead-finder` (tìm kiếm) và `linkedin-lead-enricher` (enrich).
  - **Credentials**: Điền **Apify API Token** (mua tại [Apify](https://apify.com/)).
  - **Search Query**:
    - **Role**: `CEO` (có thể thay đổi: `CTO`, `Founder`, `Director`).
    - **Location**: `New York` (thay đổi theo khu vực mục tiêu).
    - **Max Results**: `5` (có thể tăng lên `10-20` nếu muốn nhiều leads).
  - **Enrich Settings**:
    - **Email Quality Score**: **≥ 70** (lọc email chất lượng cao).

#### **🔹 Node 4: Filter (Lọc Email Chất Lượng)**
- **Điều kiện mặc định**: `Email Score >= 70`.
- **Lưu ý**:
  - Nếu muốn **chặt chẽ hơn**, tăng lên `80`.
  - Nếu muốn **lỏng lẻo hơn**, giảm xuống `60`.

#### **🔹 Node 5: OpenAI - Tạo Email Cá Nhân Hóa**
- **Prompt mẫu** (có thể chỉnh sửa):
  ```plaintext
  You are an expert cold email writer. Create a personalized cold email for a CEO at a company.
  Use the following details:
  - First Name: {{$json["firstName"]}}
  - Last Name: {{$json["lastName"]}}
  - Job Title: {{$json["jobTitle"]}}
  - Company: {{$json["company"]}}
  - About Section: {{$json["aboutSection"]}}
  - Company Website: {{$json["companyWebsite"]}}

  Email should be:
  - Professional and concise (under 200 words).
  - Include a clear value proposition.
  - End with a strong CTA.
  - Subject line should be engaging and relevant.
  ```
- **Model**: `gpt-4-1106-preview` (GPT-4.1 Mini).
- **Credentials**: Điền **OpenAI API Key** (mua tại [OpenAI](https://openai.com/)).

#### **🔹 Node 6: Google Sheets - Lưu Leads**
- **Sheet Name**: Chọn **Google Sheet** đã tạo sẵn.
- **Range**: `Sheet1!A1` (hoặc tùy chỉnh).
- **Operation**: `Append` (thêm mới mỗi lần chạy).

#### **🔹 Node 7: Gmail - Tạo Draft Email**
- **Credentials**: Chọn **gmailOAuth2** (cấu hình OAuth2 trong n8n).
- **Recipient**: `{{$json["email"]}}` (email từ leads).
- **Subject**: `{{$json["subject"]}}` (từ OpenAI).
- **Body**: `{{$json["htmlBody"]}}` (HTML từ OpenAI).
- **Lưu ý**:
  - **Chỉ tạo draft**, không tự động gửi.
  - **Email sẽ được gửi đến inbox draft** của Gmail, các sếp **review và chỉnh sửa** trước khi gửi.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **dữ liệu mẫu** (nếu có).
2. **Bật Active** workflow.
3. **Kiểm tra Google Sheets** để xem leads đã được lưu chưa.
4. **Mở Gmail Drafts** để xem email đã được tạo chưa.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM NGOÀI THƯỜNG**]
- **Thay đổi vị trí & vai trò**:
  - Thay `CEO` thành `CTO`, `Founder`, `Director` để tìm leads khác.
  - Thay `New York` thành `Hà Nội`, `TP.HCM`, `Ho Chi Minh` (nếu làm việc tại Việt Nam).

- **Kết hợp với Slack/Telegram**:
  - Thêm **Slack Webhook** hoặc **Telegram Bot** để **báo cáo kết quả** mỗi khi workflow chạy.

- **Lưu log vào Google Sheets**:
  - Thêm **Google Sheets (Append)** sau **OpenAI** để **lưu lịch sử email** đã tạo.

- **Gửi email tự động sau review**:
  - Sau khi các sếp **review và chỉnh sửa draft**, có thể thêm **Gmail Send** để tự động gửi.

- **Tăng số lượng leads**:
  - Đổi **Max Results** từ `5` lên `20` để có nhiều leads hơn.

- **Sử dụng AI khác**:
  - Thay **GPT-4.1 Mini** bằng **Claude 3** (nếu có API key).
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **tìm kiếm leads thủ công và viết email lạnh không cá nhân hóa**. Với **AI + Automatization**, các sếp sẽ:
✔ **Tìm kiếm leads chất lượng** trong vài giây.
✔ **Tạo email cá nhân hóa** với nội dung chuyên nghiệp.
✔ **Lưu leads vào CRM mini** để theo dõi.
✔ **Review và gửi email** một cách an toàn.

**🚀 Hãy áp dụng ngay và tăng gấp đôi hiệu quả bán hàng của mình!**

---
:::note[**LƯU Ý CUỐI CUNG**]
- **Không tự động gửi email** (tránh bị block).
- **Kiểm tra email trước khi gửi** để đảm bảo chất lượng.
- **Nếu có vấn đề**, hãy **check log** trong n8n và **Google Sheets**.
:::