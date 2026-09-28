---
title: "🤖 Tự Động Hóa Tạo Issue JIRA Từ Email Hỗ Trợ Outlook - Giảm 90% Thời Gian Triển Khởi Ticket"
description: "Workflow tự động hóa chuyển đổi email hỗ trợ từ Outlook thành issue JIRA với AI phân loại, gán nhãn và đánh giá ưu tiên tự động. Giúp đội ngũ kỹ thuật tiết kiệm 90% thời gian triệt để ticket và tập trung vào giải quyết vấn đề."
slug: "tieu-dong-hoa-tao-issue-jira-tu-email-outlook"
tags: [n8n, automation, jira, outlook, ai, no-code, support-ticket]
keywords: [n8n workflow jira, tự động hóa email jira, ai triaging ticket, tự động hóa hỗ trợ kỹ thuật, workflow n8n outlook]
---

# 🚀 **Tự Động Hóa Tạo Issue JIRA Từ Email Hỗ Trợ Outlook Với AI**

### **Giải pháp cho đội ngũ kỹ thuật bị ngập dưới email hỗ trợ**
Các sếp đã từng phải làm việc với hàng trăm email hỗ trợ hàng ngày chưa? Thời gian triệt để ticket, gán nhãn và đánh giá ưu tiên thường chiếm đến **80% thời gian** của kỹ sư, khiến họ không thể tập trung vào việc phát triển sản phẩm. **Workflow này tự động hóa toàn bộ quy trình đó chỉ với một dòng email!**

N8n kết hợp với **OpenAI (GPT-4o-mini)** sẽ:
✅ **Phân loại tự động** email hỗ trợ từ Outlook
✅ **Gán nhãn và đánh giá ưu tiên** dựa trên nội dung
✅ **Tạo issue JIRA** với tiêu đề và mô tả được tổng hợp từ AI
✅ **Tránh xử lý trùng lặp** với cơ chế "Mark as Seen"

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian triệt để ticket** – AI tự động xử lý email trong khi kỹ sư tập trung vào giải quyết vấn đề.
- **Chính xác và nhất quán** – Gán nhãn và đánh giá ưu tiên theo quy tắc logic của AI, không còn sai sót do con người gây ra.
- **Hoạt động 24/7** – Workflow chạy tự động theo lịch trình, không cần can thiệp thủ công.
- **Cá nhân hóa và mở rộng** – Dễ dàng tùy chỉnh hệ thống prompt của AI để phù hợp với quy trình công ty.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Microsoft Outlook** (đặc biệt là **inbox chia sẻ dành riêng cho hỗ trợ**).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)) để sử dụng mô hình **GPT-4o-mini**.
3. **Tài khoản JIRA Cloud** (cấu hình API trong n8n).
4. **VPS để self-host n8n** (để workflow chạy liên tục 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/3893](https://n8n.io/workflows/3893) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần cấu hình kỹ lưỡng các node sau:

##### **🔹 Node 1: Schedule Trigger (Động cơ kích hoạt theo lịch)**
- **Cấu hình:**
  - Chọn **Cron expression** phù hợp (ví dụ: `0 * * * *` để chạy mỗi giờ).
  - **Lưu ý:** Nếu inbox email quá lớn, nên điều chỉnh thời gian để tránh quá tải.

##### **🔹 Node 2: Get Recent Messages (Lấy email mới từ Outlook)**
- **Credentials:** Chọn `microsoftOutlookOAuth2Api` (đã cấu hình trước).
- **Key Parameters:**
  - `operation`: Đặt thành `getAll` (lấy tất cả email mới).
  - **Lưu ý:**
    - Chỉ sử dụng **inbox chia sẻ hỗ trợ** (không phải inbox cá nhân).
    - Nếu email không phải hỗ trợ, cần thêm **bước lọc** trước khi xử lý.

##### **🔹 Node 3 & 4: OpenAI Chat Model + Structured Output Parser (AI phân tích email)**
- **Credentials:** Chọn `openAiApi` (đã cấu hình API Key).
- **Key Parameters:**
  - `model`: Chọn `gpt-4o-mini` (mô hình hiệu quả và rẻ).
  - **System Prompt (cần tùy chỉnh):**
    ```json
    "You are an AI assistant that triages support tickets. For each email, extract:
    - Title (summary of the issue)
    - Description (detailed problem)
    - Priority (High/Medium/Low)
    - Labels (e.g., 'bug', 'feature-request', 'documentation')
    Return the output in JSON format."
    ```
  - **Lưu ý:**
    - **Tùy chỉnh hệ thống prompt** để phù hợp với quy trình công ty (ví dụ: thêm/loại bỏ nhãn).
    - **Structured Output Parser** sẽ chuyển kết quả AI thành định dạng JSON dễ xử lý.

##### **🔹 Node 5: Markdown (Chuyển HTML thành Markdown)**
- **Lưu ý:** N8n tự động chuyển đổi nội dung email từ HTML sang Markdown để AI dễ phân tích.

##### **🔹 Node 6: Create Issue (Tạo issue JIRA)**
- **Credentials:** Chọn `jiraSoftwareCloudApi` (đã cấu hình).
- **Key Parameters:**
  - `projectKey`: ID dự án JIRA (ví dụ: `SUPPORT`).
  - `summary`: Điền từ `{{ $node["Structured Output Parser"].json["title"] }}`.
  - `description`: Điền từ `{{ $node["Structured Output Parser"].json["description"] }}`.
  - `labels`: Điền từ `{{ $node["Structured Output Parser"].json["labels"] }}`.
  - `priority`: Điền từ `{{ $node["Structured Output Parser"].json["priority"] }}`.
  - **Lưu ý:**
    - Nếu cần thêm trường khác (ví dụ: `epicLink`, `assignee`), mở rộng ở đây.

##### **🔹 Node 7: Mark as Seen (Tránh xử lý trùng lặp)**
- **Key Parameters:**
  - `operation`: Đặt thành `removeItemsSeenInPreviousExecutions`.
  - **Lưu ý:** Node này đảm bảo **mỗi email chỉ được xử lý 1 lần**.

##### **🔹 Node 8: Generate Issue From Support Request (Chain LLM)**
- **Lưu ý:** Node này kết nối các bước AI và JIRA. **Không cần chỉnh sửa** nếu đã import từ template.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run:** Chạy workflow với **dữ liệu mẫu** (ví dụ: email hỗ trợ giả).
   - Kiểm tra:
     - AI có phân loại nhãn và ưu tiên chính xác không?
     - Issue JIRA có tạo thành công không?
2. **Bật Active:** Sau khi kiểm tra, **bật workflow** để chạy tự động.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram:**
   - Thêm node `webhook` để gửi thông báo khi issue JIRA được tạo thành công.
   ```json
   {
     "name": "Notify Slack",
     "type": "n8n-nodes-base.webhook",
     "credentials": ["slackWebhook"],
     "keyParameters": {
       "payload": {
         "text": "New JIRA issue created: {{ $node["Create Issue"].json["key"] }}"
       }
     }
   }
   ```
2. **Lưu log hoạt động:**
   - Sử dụng node `stickyNote` để ghi lại lịch sử xử lý email.
3. **Báo cáo định kỳ:**
   - Thêm node `scheduleTrigger` khác để gửi báo cáo số lượng ticket được xử lý hàng tuần.
4. **Tự động giải quyết ticket:**
   - Kết hợp với **AI Agent** để tự động trả lời email hỗ trợ (ví dụ: thông báo ticket đã được tạo).
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng đội ngũ kỹ thuật** khỏi công việc lặp lại, giúp họ tập trung vào **giải quyết vấn đề thực sự** thay vì quản lý ticket. **Chỉ cần 10 phút cấu hình**, các sếp đã có một hệ thống tự động hóa **chạy 24/7**!

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động liên tục).
2. **Tùy chỉnh hệ thống prompt** của AI theo quy trình công ty.
3. **Bật workflow và xem AI làm việc!**

🚀 **Hãy thử ngay và giảm 90% thời gian triệt để ticket!**