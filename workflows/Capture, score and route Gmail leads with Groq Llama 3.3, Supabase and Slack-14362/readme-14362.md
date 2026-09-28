---
title: "🚀 Tự Động Hóa Chuyển Đổi Lead Gmail: AI Đánh Giá, Lọc & Gửi Đến Đội Ngũ Phù Hợp (Groq + Supabase + Slack)"
description: "Workflow này tự động chụp, đánh giá điểm số và phân loại lead từ Gmail bằng AI Groq Llama 3.3, lưu vào Supabase, rồi gửi đến Slack với phân loại Sales/Support/Billing. Giúp doanh nghiệp giảm 80% thời gian xử lý lead thủ công."
slug: "tieu-dong-hoa-chuyen-doi-lead-gmail-ai-groq-supabase-slack"
tags: [n8n, automation, lead-generation, ai-summarization, groq, supabase, slack, no-code]
keywords: [n8n workflow lead generation, tự động hóa chuyển đổi lead, AI đánh giá lead, Groq Llama 3.3, Supabase tự động hóa, Slack tự động hóa, tự động hóa Gmail]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Lead Gmail: AI Đánh Giá, Lọc & Gửi Đến Đội Ngũ Phù Hợp**

## **💡 Nỗi Đau Của Các Sếp: Lead "Chìm" Trong Inbox Gmail**
Hàng ngày, các sếp và đội ngũ marketing phải:
- **Làm thủ công**: Lọc hàng trăm email lead từ Gmail, đánh giá chất lượng, phân loại và chuyển giao cho các bộ phận khác (Sales, Support, Billing).
- **Mất thời gian**: Tốn trung bình **30-60 phút/ngày** để xử lý lead, trong khi chỉ có **10-20%** lead thực sự chất lượng.
- **Rủi ro sai phân loại**: Lead "hot" bị bỏ qua hoặc lead "lạnh" chiếm chỗ trong ưu tiên của Sales.
- **Không theo dõi được**: Không biết lead nào đã được xử lý, nào đang chờ, dẫn đến trải nghiệm khách hàng kém.

**Workflow này giải quyết tất cả vấn đề trên bằng AI + tự động hóa 100% không code!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian**: AI tự động đánh giá và phân loại lead trong giây lát.
✅ **Chất lượng lead cao**: AI Groq Llama 3.3 đánh giá điểm số (scoring) và phân loại lead chính xác (Sales/Support/Billing).
✅ **Phân công tự động**: Lead được gửi ngay đến Slack của bộ phận phù hợp, không cần manual forwarding.
✅ **Theo dõi toàn diện**: Dữ liệu lead được lưu vào **Supabase** (database cloud) với trạng thái, điểm số và lịch sử.
✅ **Hoạt động 24/7**: Không cần người dùng trực tiếp, workflow chạy liên tục ngay cả khi các sếp nghỉ ngơi.
✅ **Cá nhân hóa thông báo**: Slack alert với thông tin chi tiết lead (tên, email, nội dung email, điểm số AI).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail**:
   - Email chính của doanh nghiệp (hoặc email chuyên dụng để nhận lead).
   - **API Key Gmail**: [Cài đặt OAuth 2.0 cho Gmail](https://developers.google.com/gmail/api/quickstart/python) và tạo **Service Account** (nếu cần).
   - **Thiết lập Filter Gmail**: Tạo một **label** (ví dụ: "Lead_Inbox") để workflow chỉ lấy email từ label này.

2. **Tài khoản Supabase** (Database):
   - [Đăng ký miễn phí Supabase](https://supabase.com/) và tạo **Project mới**.
   - **Table "leads"**: Workflow sẽ tự động tạo table này nếu chưa có. Các sếp cần đảm bảo có **permission** để write/read.
   - **API Key Supabase**: Tạo **anon key** hoặc **service role key** trong **Project Settings > API**.

3. **Tài khoản Slack**:
   - **Workspace Slack** của doanh nghiệp.
   - **OAuth Token Slack**: Tạo **Bot Token** với quyền `chat:write`, `channels:join`, `groups:join` (tham khảo [hướng dẫn Slack API](https://api.slack.com/apps)).
   - **Channel IDs**:
     - `#sales-leads` (để lead Sales)
     - `#support-leads` (để lead Support)
     - `#billing-leads` (để lead Billing)
     - `#new-lead-notifications` (để thông báo mới lead)

4. **Tài khoản Groq API** (AI Llama 3.3):
   - [Đăng ký Groq API](https://console.groq.com/) (miễn phí với giới hạn credit).
   - **API Key Groq**: Tạo tại **API Keys** trong dashboard Groq.

5. **N8n Self-Hosted** (không dùng n8n.cloud):
   - **Lý do**: Workflow này sử dụng **Groq API** và **Supabase**, nên cần **self-hosted** để tránh giới hạn của n8n.cloud.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ JSON**
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/14362) (ấn **Export**).
2. **Mở n8n Editor** trên VPS của mình.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/14362) và copy toàn bộ JSON.
2. **Mở n8n Editor** → **Create new workflow** → **Paste JSON** từ file.
3. **Nhấn "Create"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **5 bước chính**, các sếp cần cấu hình kỹ các node sau:

#### **🔹 Bước 1: Cấu Hình Gmail Trigger**
- **Node: "Gmail Trigger1"**
  - **Chọn Credential**: Tạo mới credential Gmail với **Service Account** (nếu dùng OAuth 2.0).
  - **Label**: Chỉnh thành **`Lead_Inbox`** (phù hợp với filter Gmail đã tạo).
  - **Test**: Nhấn **Execute Node** và kiểm tra email từ label `Lead_Inbox` có được chụp không.

#### **🔹 Bước 2: Cấu Hình Supabase**
- **Node: "Store Lead in Database1"**
  - **Chọn Credential Supabase**: Điền **URL Project** và **API Key** từ Supabase.
  - **Table Name**: Workflow sẽ tự động tạo table `leads`, không cần chỉnh.
  - **Columns**:
    - `id` (auto-increment)
    - `email` (text)
    - `name` (text)
    - `message` (text)
    - `thread_id` (text)
    - `score` (integer, từ AI)
    - `category` (text: "sales", "support", "billing")
    - `status` (text: "unscored", "scored", "routed")

#### **🔹 Bước 3: Cấu Hình Groq AI (Llama 3.3)**
- **Node: "LLM (Scoring)1" và "LLM (Classification)1"**
  - **Chọn Credential Groq**: Điền **API Key Groq** từ dashboard Groq.
  - **Model**: Chọn `llama-3.3-70b-versatile` (đã mặc định).
  - **Prompt Templates**:
    - **Scoring**: Workflow đã tự động cấu hình prompt đánh giá lead (ví dụ: "Đánh giá lead này từ 0-100 dựa trên độ hấp dẫn thương mại").
    - **Classification**: Prompt phân loại lead (Sales/Support/Billing).
    - **Lưu ý**: Nếu muốn thay đổi logic AI, chỉnh ở **`Structured Output Parser1`** (node sau).

#### **🔹 Bước 4: Cấu Hình Slack**
- **Node: "Notify New Lead (Slack)1"**, "Send to Sales Channel1"**, etc.**
  - **Chọn Credential Slack**: Điền **Bot Token** từ Slack.
  - **Channel IDs**:
    - `#sales-leads` → ID từ `https://slack.com/apps/A0F7XP6-ChannelName`
    - `#support-leads` → ID tương tự
    - `#billing-leads` → ID tương tự
  - **Message Template**: Workflow đã cấu hình sẵn, các sếp chỉ cần **test** để đảm bảo thông báo Slack hiển thị đúng.

#### **🔹 Bước 5: Cấu Hình AI Agent (Nếu Cần Tùy Chỉnh)**
- **Node: "AI Lead Scoring Engine1" và "AI Lead Classification Engine1"**
  - Nếu muốn **tùy chỉnh logic AI**, chỉnh ở:
    - **Prompt trong `lmChatGroq`** (node `LLM (Scoring)1` và `LLM (Classification)1`).
    - **Structured Output Parser** (node `Structured Output Parser1`) để định dạng đầu ra (ví dụ: `{ "score": 85, "category": "sales" }`).

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ liệu Mẫu**:
   - Gửi **1 email mẫu** vào Gmail với label `Lead_Inbox`.
   - Chạy workflow và kiểm tra:
     - Email có được chụp không?
     - Lead có được lưu vào Supabase không?
     - Slack có nhận được thông báo không?
     - AI có đánh giá điểm số và phân loại lead không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật toggle "Active"** ở góc trên bên phải.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Tích Hợp Email Marketing (Mailchimp/HubSpot)**
- **Cách làm**:
  - Sau khi lead được phân loại (Sales/Support/Billing), thêm **node `n8n-nodes-base.mailchimp`** để tự động thêm lead vào danh sách email marketing.
  - **Lợi ích**: Tự động follow-up với lead sau khi Sales xử lý.

### **🔹 2. Lưu Log & Báo Cáo Định Kỳ**
- **Cách làm**:
  - Thêm **node `n8n-nodes-base.googleSheets`** để lưu log hoạt động của workflow.
  - Sử dụng **node `n8n-nodes-base.cron`** để chạy báo cáo hàng tuần về:
    - Số lead mới.
    - Phân bố lead theo bộ phận (Sales/Support/Billing).
    - Trung bình điểm số lead.

### **🔹 3. Tích Hợp CRM (HubSpot/Zoho)**
- **Cách làm**:
  - Thay thế **Supabase** bằng **node `n8n-nodes-base.hubspot`** để tự động tạo lead trong HubSpot.
  - **Lợi ích**: Tích hợp hoàn toàn với hệ thống CRM hiện có.

### **🔹 4. Thêm AI Chatbot Trả Lời Lead**
- **Cách làm**:
  - Sau khi lead được phân loại, thêm **node `n8n-nodes-base.telegram`** hoặc **Slack** để tự động trả lời lead với tin nhắn cá nhân hóa (ví dụ: "Chúng tôi đã nhận được email của bạn và sẽ liên hệ trong 24h!").

### **🔹 5. Cảnh Báo Thông Qua Email**
- **Cách làm**:
  - Thêm **node `n8n-nodes-base.email`** để gửi email cảnh báo khi có lead mới (nếu Slack không được sử dụng).

---

## 📌 **Kết Luận: Tự Động Hóa Lead Bắt Đầu Từ Hôm Nay!**

Workflow này **giải phóng thời gian** cho các sếp và đội ngũ marketing để tập trung vào **strategy** thay vì **execution**. Bằng cách:
✔ **AI Groq Llama 3.3** đánh giá và phân loại lead chính xác.
✔ **Supabase** lưu trữ dữ liệu lead một cách an toàn và dễ truy cập.
✔ **Slack** tự động phân công lead đến bộ phận phù hợp.
✔ **Tự động hóa 24/7** mà không cần code.

**🚀 Hành động ngay:**
1. **Chuẩn bị tài khoản** (Gmail, Supabase, Slack, Groq).
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test với email mẫu** và bật workflow.
4. **Theo dõi kết quả** và mở rộng với các tính năng nâng cao!

**Nếu có vấn đề**, các sếp có thể:
- **Trả lời comment** dưới bài viết này.
- **Gửi tin nhắn** cho Avkash Kakdiya (tác giả workflow) qua [iTechNotion](https://itechnotion.com/).
- **Hỏi hỗ trợ** trên [Community n8n](https://community.n8n.io/).

**💡 Mẹo cuối**: Nếu muốn **tăng hiệu suất**, các sếp có thể **tùy chỉnh prompt AI** để phù hợp với ngành nghề cụ thể (tech, e-commerce, SaaS...). Ví dụ:
- **Tech**: AI đánh giá lead dựa trên kỹ năng kỹ thuật.
- **E-commerce**: AI phân loại lead theo sản phẩm quan tâm.

**Hãy tự động hóa lead của mình ngay hôm nay!** 🚀