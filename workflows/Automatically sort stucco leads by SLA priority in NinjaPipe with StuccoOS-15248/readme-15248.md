---
title: "🚀 Tự Động Hóa Xếp Loại Lead Email Theo SLA Nhờ AI + NinjaPipe & StuccoOS (Không Cần Code)"
description: "Workflow này tự động phân loại, nhắc nhở và xử lý lead từ email theo độ ưu tiên SLA (Service Level Agreement), giảm thiểu thời gian phản hồi và tối ưu hóa quản lý CRM. Giúp các sếp tự động hóa triệt để quy trình triage email, kết hợp AI phân loại và CRM quản lý."
slug: "tu-dong-hoa-xep-loai-lead-email-theo-sla-ai-ninjapipe-stuccoos"
tags: [n8n, automation, no-code, ticket-management, ai-summarization, crm-automation, stuccoos, ninjapipe]
keywords: [n8n workflow tự động hóa email, phân loại lead theo SLA, AI triage email, CRM automation, StuccoOS + NinjaPipe, tự động hóa quản lý lead]
---

# 🚀 **Tự Động Hóa Xếp Loại Lead Email Theo SLA Nhờ AI + NinjaPipe & StuccoOS**

### **Giải pháp cho các sếp:**
Bạn có bao giờ cảm thấy **mất thời gian quét hàng chục email hàng ngày** để phân loại lead, nhớ nhắc nhở SLA, hoặc lo lắng về việc **trễ hạn xử lý**? Workflow này sẽ **tự động hóa toàn bộ quy trình triage email**, sử dụng **AI phân loại thông minh** và **CRM quản lý**, giúp bạn:
✅ **Tiết kiệm 8+ giờ/tuần** cho việc phân loại và nhắc nhở lead.
✅ **Giảm thiểu lỗi nhân sự** với quy trình tự động hóa 100% chính xác.
✅ **Tối ưu hóa SLA** bằng cách tự động nhắc nhở và phân loại lead theo độ ưu tiên.
✅ **Kết nối CRM** (NinjaPipe) với **AI phân loại** (Groq) để xử lý lead một cách cá nhân hóa.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
### **Lợi ích cốt lõi:**
1. **Tự động phân loại email** theo độ ưu tiên SLA (Urgent, Standard, Low Priority).
2. **Nhắc nhở tự động** cho chủ nhiệm lead khi email mới đến (trong vòng 30 giây).
3. **Tạo task CRM tự động** với nhãn SLA phù hợp (Urgent → xử lý ngay, Standard → trong 48h).
4. **Tránh trễ hạn SLA** nhờ hệ thống nhắc nhở và phân loại tự động.
5. **Kết nối CRM (NinjaPipe) với AI** để xử lý lead một cách thông minh.

---
## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản StuccoOS** (để nhận webhook email).
✔ **API Key CRM (NinjaPipe)** (để tạo/ cập nhật contact và task).
✔ **API Key Groq** (để sử dụng mô hình AI `openai/gpt-oss-120b`).
✔ **Credentials cho HTTP Request** (để kết nối với CRM).
✔ **Mã webhook** (để StuccoOS gửi email đến n8n).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15248](https://n8n.io/workflows/15248).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name** là **"StuccoOS Email Triage"** → Nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** → Dán toàn bộ JSON từ [n8n.io/workflows/15248](https://n8n.io/workflows/15248).
3. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Webhook (Triggers)**
- **Node:** `When Email Arrives` (Webhook)
  - **Path:** `agentmail-webhook` (không đổi).
  - **HTTP Method:** `POST`.
  - **Lưu ý:** Đảm bảo **StuccoOS** đã cấu hình webhook gửi email đến URL này.

#### **B. Cấu hình AI Classifier (Groq)**
- **Node:** `Chat Model Integration` (lmChatGroq)
  - **Credentials:** Chọn `groqApi` (đã tạo trước).
  - **Model:** `openai/gpt-oss-120b` (không đổi).
  - **Prompt:** Cần chỉnh sửa để phù hợp với **ngôn ngữ và quy trình SLA** của công ty.
    *Ví dụ:*
    ```json
    "prompt": "Analyze this email and classify it into one of these SLA categories: Urgent, Standard, Low Priority. Return the result in JSON format: { 'sla_category': 'Urgent|Standard|Low Priority', 'confidence': number }"
    ```

#### **C. Cấu hình CRM (NinjaPipe)**
- **Node:** `Search CRM for Contact` (HTTP Request)
  - **Credentials:** Chọn `httpBearerAuth` (API Key NinjaPipe).
  - **URL:** `https://api.ninjapipe.com/v1/contacts/search` (hoặc URL của CRM).
  - **Headers:** Thêm `Authorization: Bearer {API_KEY}`.

- **Node:** `Add New CRM Contact` (HTTP Request)
  - **Credentials:** `httpBearerAuth`.
  - **URL:** `https://api.ninjapipe.com/v1/contacts` (hoặc URL tương ứng).
  - **Body:** Cấu hình payload để tạo contact mới từ email.

- **Node:** `Add Contact to SLA List` (HTTP Request)
  - **Credentials:** `httpBearerAuth`.
  - **URL:** `https://api.ninjapipe.com/v1/lists/{LIST_ID}/contacts` (thay `{LIST_ID}` bằng ID danh sách SLA trong CRM).

#### **D. Cấu hình Filter & Routing**
- **Node:** `Filter Spam Emails` (Filter)
  - **Condition:** Chỉ giữ email **không phải spam** (cần chỉnh sửa logic phù hợp).
- **Node:** `Route by SLA Category` (Switch)
  - **Cases:** Cần map **Urgent → Task Urgent**, **Standard → Task Standard**, **Low Priority → Task Low Priority**.
  - **Lưu ý:** Đảm bảo **task được tạo trong CRM** với nhãn SLA tương ứng.

#### **E. Cấu hình Wait & Rate Limiting**
- **Node:** `Wait 30 Seconds` (Wait)
  - **Thời gian:** 30 giây (để tránh quá tải API).
- **Node:** `Log Email and Wait 48h` (Code)
  - **Lưu ý:** Nếu email là **Standard**, workflow sẽ chờ **48h** trước khi nhắc nhở lại.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với 1 email mẫu:
   - Gửi email test đến webhook (`https://{YOUR_N8N_URL}/agentmail-webhook`).
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active** workflow sau khi test thành công.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa AI Classifier**
- **Chỉnh sửa Prompt** để phù hợp với **ngôn ngữ và quy trình SLA** của công ty.
- **Thêm logic lọc spam** bằng regex hoặc từ khóa cụ thể (ví dụ: "unsubscribe", "promotion").

### **2. Kết nối với Slack/Telegram**
- **Thêm Node Slack/Telegram** để nhắc nhở chủ nhiệm lead khi email mới đến.
- **Ví dụ:**
  ```json
  {
    "name": "Notify Slack",
    "type": "slackWebhook",
    "credentials": ["slackWebhook"],
    "keyParameters": {
      "text": "New Urgent Lead: {{ $node["Route by SLA Category"].json["sla_category"] }} - {{ $node["Extract Email Content"].json["subject"] }}"
    }
  }
  ```

### **3. Lưu Log & Báo cáo**
- **Thêm Node Database (PostgreSQL/MySQL)** để lưu lịch sử email và SLA.
- **Tạo báo cáo định kỳ** (hàng tuần) về số lead được xử lý, trễ hạn, và độ chính xác của AI.

### **4. Xử lý lỗi & Rate Limiting**
- **Thêm Node Error Handling** để log lỗi và gửi cảnh báo Slack/Email.
- **Cài đặt Rate Limiting** cho API CRM (ví dụ: chờ 1 giây giữa các request).

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **quét email, phân loại lead thủ công**, và **nhớ nhắc nhở SLA**. Với **AI phân loại thông minh** và **CRM tự động hóa**, bạn sẽ:
✔ **Tăng hiệu suất** 3-5 lần so với cách làm thủ công.
✔ **Giảm thiểu lỗi** nhờ quy trình tự động hóa.
✔ **Tối ưu hóa SLA** bằng cách nhắc nhở kịp thời.

**Hành động ngay:**
1. **Import workflow** vào n8n.
2. **Cấu hình API Keys** (Groq, NinjaPipe).
3. **Test với email mẫu** và bật **Active**.
4. **Tối ưu hóa Prompt AI** để phù hợp với công ty.

**🚀 Cùng tự động hóa ngay hôm nay!** 🚀