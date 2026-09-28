---
title: "🚀 Tự Động Hóa Xử Lý Email Leads Gmail Với AI Groq + Sync SLA Cases Sang Supabase (Không Cần Code)"
description: "Workflow tự động phân loại, phân loại email leads từ Gmail bằng AI Groq, đồng bộ hóa vụ việc SLA sang Supabase qua Redis, giúp các sếp tiết kiệm 8+ giờ/ngày xử lý thủ công. Giảm thiểu rủi ro lỗi và tối ưu hóa quy trình phản hồi khách hàng theo SLA."
slug: "tieu-dong-hoa-email-leads-gmail-ai-groq-supabase"
tags: [n8n, automation, no-code, ai-summarization, ticket-management, groq-ai, supabase, redis, gmail-automation]
keywords: [n8n workflow tự động hóa email, phân loại email leads bằng AI, đồng bộ SLA sang Supabase, tự động hóa Gmail với Groq, xử lý email theo SLA, tự động hóa không cần code]
---

# 🚀 **Tự Động Hóa Xử Lý Email Leads Gmail Với AI Groq + Sync SLA Cases Sang Supabase**

### **Giải pháp cho các sếp:**
Bạn đang phải **quét hàng chục email leads mỗi ngày**, phân loại thủ công, sau đó đồng bộ hóa vụ việc vào hệ thống quản lý SLA? **Thời gian và chính xác là vấn đề?** Workflow này sẽ **tự động hóa toàn bộ quy trình** bằng AI Groq, đồng thời **đồng bộ hóa vụ việc vào Supabase** để theo dõi và quản lý hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/ngày** xử lý email thủ công.
- **Phân loại email leads chính xác** bằng AI Groq (không cần code).
- **Đồng bộ hóa tự động** vụ việc SLA sang Supabase qua Redis.
- **Phân loại email theo SLA** (urgent, standard, delayed) và thông báo ngay cho người quản lý.
- **Lưu trữ và theo dõi lịch sử** vụ việc trong Supabase.
- **Không cần viết code** – chỉ cần cấu hình và chạy.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (cần cấp quyền OAuth 2.0 cho n8n).
2. **Redis Server** (để trigger và đồng bộ hóa giữa workflows).
3. **Supabase Database** (để lưu trữ và quản lý vụ việc SLA).
4. **Groq API Key** (để sử dụng AI Groq phân loại email).
5. **Mem0 API Key** (nếu muốn lưu trữ nội dung email).
6. **PostgreSQL Credentials** (để thiết lập bảng SLA trong Supabase).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15432](https://n8n.io/workflows/15432) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15432) và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Gmail Trigger**
- **Node:** `When Gmail Received` (gmailTrigger)
  - Chọn **credentials:** `gmailOAuth2`.
  - Cấu hình **labels** để chỉ lấy email có nhãn cụ thể (ví dụ: `leads`, `potential`).
  - **Lưu ý:** Nếu không có nhãn, email sẽ không được xử lý.

#### **B. Cấu hình Redis**
- **Node:** `Gmail Redis Trigger` (redisTrigger)
  - Chọn **credentials:** `redis`.
  - Đảm bảo Redis đang hoạt động và có thể kết nối từ n8n.
- **Node:** `Trigger Secondary Workflow` (redis)
  - Chọn **credentials:** `redis`.
  - Điền **channel** và **message** để trigger workflow phụ.

#### **C. Cấu hình Groq AI**
- **Node:** `Integrate Chat Model` (lmChatGroq)
  - Chọn **credentials:** `groqApi`.
  - Đặt **model:** `openai/gpt-oss-120b` (hoặc model khác nếu muốn).
  - **Prompt mẫu:**
    ```json
    "Analyze the email content and classify it as:
    - Urgent (needs immediate response)
    - Standard (needs response within 24h)
    - Delayed (can be responded later)
    Also extract key details like customer name, email, and request."
    ```

#### **D. Cấu hình Supabase (PostgreSQL)**
- **Node:** `Log to Supabase` (postgres)
  - Chọn **credentials:** `postgres`.
  - Điền **query SQL** để tạo bảng `slacases` (nếu chưa có):
    ```sql
    CREATE TABLE IF NOT EXISTS slacases (
      id SERIAL PRIMARY KEY,
      email_id TEXT,
      subject TEXT,
      body TEXT,
      classification TEXT,
      status TEXT,
      created_at TIMESTAMP DEFAULT NOW()
    );
    ```
- **Node:** `Setup SLA Database` (postgres)
  - Chạy query để thiết lập **triggers** và **functions** cho SLA.

#### **E. Cấu hình Mem0 API (nếu cần)**
- **Node:** `Post to Mem0 API` (httpRequest)
  - Chọn **credentials:** `httpHeaderAuth`.
  - Điền **URL API** và **headers** của Mem0.
  - **Payload mẫu:**
    ```json
    {
      "email_id": "{{$node["Retrieve Gmail Email"].json["id"]}}",
      "content": "{{$node["Retrieve Gmail Email"].json["body"]}}"
    }
    ```

#### **F. Cấu hình Switch (Phân loại theo SLA)**
- **Node:** `Direct Emails by SLA Status` (switch)
  - Cấu hình **conditions** để phân loại email:
    - `Urgent` → Gửi thông báo ngay cho người quản lý.
    - `Standard` → Tạo task tiêu chuẩn.
    - `Delayed` → Đặt lịch xử lý sau 48h.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với 1-2 email mẫu để kiểm tra logic.
2. **Bật Active** workflow sau khi xác nhận tất cả node hoạt động.
3. **Monitor** trong **n8n Dashboard** để theo dõi lỗi (nếu có).

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node `slack` hoặc `telegram` để thông báo kết quả phân loại email ngay khi nhận được.
2. **Lưu log chi tiết**
   - Sử dụng node `stickyNote` để ghi lại thông tin debug (ví dụ: email bị lỗi phân loại).
3. **Báo cáo định kỳ**
   - Tạo workflow phụ để gửi **báo cáo tổng hợp SLA** hàng tuần sang email.
4. **Tối ưu Groq API**
   - Nếu Groq API chậm, thử **batching emails** để giảm số lượng API calls.
5. **Cập nhật nhãn email tự động**
   - Sử dụng node `code` để **tự động thêm nhãn** cho email sau khi phân loại (ví dụ: `urgent`, `standard`).

---

## 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công** trong việc xử lý email leads, đồng thời **tự động hóa toàn bộ quy trình SLA** bằng AI Groq và Supabase. **Không cần viết code**, chỉ cần cấu hình và chạy – **tiết kiệm thời gian, tăng hiệu suất, và giảm thiểu lỗi**.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa ngay hôm nay!** 🚀

---
**💡 Gợi ý thêm:**
- Nếu cần **tùy chỉnh SLA criteria**, hãy chỉnh sửa node `Route Emails Based on SLA`.
- Để **tăng tốc độ**, các sếp có thể **upgrade Groq API** sang plan cao cấp.