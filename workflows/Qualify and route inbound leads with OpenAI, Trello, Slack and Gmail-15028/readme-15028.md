---
title: "🚀 Tự Động Học Sàng Lọc & Phân Loại Lead Tiềm Năng với AI (OpenAI) + Trello + Gmail + Slack"
description: "Workflow tự động hóa 100% không code giúp doanh nghiệp nhanh chóng phân loại lead (HOT/WARM/COLD) từ form, gửi thông báo tự động đến Slack/Gmail và tạo task trên Trello để theo dõi nhanh chóng. Giảm thời gian phản hồi từ 24h xuống dưới 1 phút!"
slug: "tieu-dong-hoc-sang-loc-lead-voi-openai-trello-gmail-slack"
tags: [n8n, automation, lead-generation, ai-summarization, openai, trello, gmail, slack, no-code]
keywords: [tự động hóa lead, phân loại lead hot warm cold, n8n workflow, ai chatbot, openai gpt-4, trello automation, gmail automation, slack notification]
---

# 🚀 **Tự Động Học Sàng Lọc & Phân Loại Lead Tiềm Năng với AI (OpenAI) + Trello + Gmail + Slack**

### **Giải pháp cho nỗi đau của các sếp Marketing/Sales:**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Lọc thủ công** hàng trăm lead từ form, email, hoặc chatbot.
- **Phân loại lead** theo mức độ tiềm năng (HOT/WARM/COLD) dựa trên thông tin budget/timeline.
- **Gửi thông báo trễ** đến team, khiến lead "lạnh" trước khi phản hồi.
- **Quên theo dõi** lead quan trọng trong biển số task trên Trello/Notion.

**Workflow này tự động hóa toàn bộ quy trình trong 3 bước:**
1. **Nhận lead** từ form (Google Form, Typeform, hoặc webhook).
2. **AI phân loại lead** (HOT/WARM/COLD) bằng OpenAI GPT-4.1-mini.
3. **Gửi thông báo tự động** đến Slack/Gmail và **tạo task trên Trello** cho team Sales/Marketing.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** cho team Marketing/Sales.
- **Phân loại lead chính xác** với AI (không sai sót như con người).
- **Phản hồi lead HOT trong vòng 1 phút** thay vì 24h.
- **Tự động tạo task trên Trello** để team không quên theo dõi.
- **Gửi thông báo Slack/Gmail** cho team Sales biết lead mới.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản n8n** (Self-hosted hoặc Cloud) – [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N** (giảm 39%).
✅ **API Key OpenAI** – [Mua tại OpenAI](https://platform.openai.com/api-keys) (đã tích hợp GPT-4.1-mini).
✅ **Trello API Key** – [Tạo tại Trello Developer](https://trello.com/app-key).
✅ **Gmail OAuth2 Credentials** – [Cài đặt tại Google Cloud Console](https://console.cloud.google.com/).
✅ **Slack Webhook URL** – [Tạo tại Slack App](https://api.slack.com/messaging/composing).
✅ **Form Tool** (Google Form, Typeform, hoặc webhook từ website).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải file JSON từ [n8n Workflow Official](https://n8n.io/workflows/15028).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create new workflow**.
2. Nhấn **Import** → Chọn **Paste JSON** và dán toàn bộ mã JSON từ [n8n Workflow Official](https://n8n.io/workflows/15028).

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **9 node** chính, các sếp cần cấu hình kỹ lưỡng các phần sau:

#### **🔹 Node 1: On form submission (formTrigger)**
- **Cấu hình:**
  - Chọn **Webhook** (nếu form từ website) hoặc **Google Form** (nếu dùng Google Forms).
  - **Test trigger** bằng cách gửi form mẫu (ví dụ: `Budget: 5000$, Timeline: ASAP`).

#### **🔹 Node 2 & 3: AI Agent + OpenAI Chat Model (agent + lmChatOpenAi)**
- **Cấu hình OpenAI:**
  - Điền **API Key OpenAI** vào `n8n-nodes-langchain.lmChatOpenAi`.
  - Chọn **Model:** `gpt-4.1-mini` (đã mặc định).
  - **Prompt AI** (đã sẵn sàng, không cần chỉnh):
    > *"You are a lead qualification assistant. Analyze the lead data and return ONLY one word: HOT, WARM, or COLD. Rules: - HOT: Budget is $5,000 or above AND timeline is ASAP or this week. High motivation. - WARM: Budget is $1,000–$5,000 OR timeline is within a month. Interested but not urgent. - COLD: Budget under $1,000 OR just exploring OR vague answers. Return ONLY the single word. No explanation. No punctuation."*

#### **🔹 Node 4: Structured Output Parser (outputParserStructured)**
- **Cấu hình:**
  - Chọn **Schema:** `{"type": "string", "enum": ["HOT", "WARM", "COLD"]}` (đã mặc định).
  - **Test** với dữ liệu mẫu để đảm bảo AI trả về đúng định dạng.

#### **🔹 Node 5: Switch (rules mode)**
- **Cấu hình quy tắc:**
  - **Rule 1:** `$.json.output.HOT` → Chuyển đến **Edit Fields** (node 7).
  - **Rule 2:** `$.json.output.WARM` → Chuyển đến **Send a message (Slack)** (node 6).
  - **Rule 3:** `$.json.output.COLD` → Chuyển đến **Send a message2 (Gmail)** (node 9).

#### **🔹 Node 6: Send a message (Slack)**
- **Cấu hình:**
  - Chọn **Slack Webhook URL** (đã tạo trước).
  - **Message template:**
    ```json
    {
      "text": "🔥 **WARM LEAD ALERT** 🔥\nLead mới: {{ $json.json.email }}\nBudget: {{ $json.json.budget }}\nTimeline: {{ $json.json.timeline }}\nLink: {{ $json.json.link }}"
    }
    ```

#### **🔹 Node 7: Edit Fields (set)**
- **Cấu hình:**
  - **Thêm trường mới** vào JSON input (ví dụ: `priority: "high"` cho lead HOT).
  - **Dùng để Trello tạo task ưu tiên cao**.

#### **🔹 Node 8: Send a message1 (Gmail - cho lead WARM)**
- **Cấu hình:**
  - Chọn **Gmail OAuth2 Credentials** (đã tạo trước).
  - **Email template:**
    ```json
    {
      "to": "team-sales@example.com",
      "subject": "📩 Lead WARM cần theo dõi",
      "text": "Lead mới: {{ $json.json.email }}\nBudget: {{ $json.json.budget }}\nTimeline: {{ $json.json.timeline }}\nLink: {{ $json.json.link }}"
    }
    ```

#### **🔹 Node 9: Send a message2 (Gmail - cho lead COLD)**
- **Cấu hình tương tự node 8**, nhưng **chỉ gửi cho team Marketing** (ví dụ: `marketing@example.com`).

---
### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi form với thông tin:
     ```
     Email: test@example.com
     Budget: 3000$
     Timeline: Next month
     ```
   - Kiểm tra:
     - AI trả về **WARM**.
     - Slack/Gmail nhận được thông báo.
     - Trello (nếu kết nối) tạo task.

2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor.
   - **Kiểm tra webhook** (nếu dùng form website) hoặc **Google Form Webhook** (nếu dùng Google Forms).

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN THÊM]
- **Kết nối Trello (nếu chưa có):**
  - Thêm node **Trello Create Card** sau **Edit Fields** để tự động tạo task.
  - **Template Trello:**
    ```json
    {
      "name": "{{ $json.json.name }} ({{ $json.output }})",
      "desc": "Budget: {{ $json.json.budget }}\nTimeline: {{ $json.json.timeline }}\nLink: {{ $json.json.link }}",
      "labels": ["{{ $json.output }}"]
    }
    ```

- **Lưu log lead vào Google Sheets:**
  - Thêm node **Google Sheets** sau **Switch** để ghi lịch sử lead.
  - **Dùng để báo cáo cho CEO**.

- **Gửi báo cáo hàng tuần:**
  - Thêm node **n8n-nodes-base.email** để gửi tổng hợp lead HOT/WARM/COLD cho team.

- **Cập nhật AI Prompt:**
  - Nếu cần phân loại phức tạp hơn, chỉnh sửa **Prompt AI** để bao gồm thêm điều kiện (ví dụ: ngành nghề, vị trí công việc).
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng team Marketing/Sales** khỏi công việc lặp lại, giúp:
✅ **Phân loại lead chính xác** với AI.
✅ **Phản hồi lead HOT trong vòng 1 phút**.
✅ **Tự động tạo task trên Trello** để team không quên.
✅ **Gửi thông báo Slack/Gmail** cho team Sales.

**Hành động ngay:**
1. **Đăng ký VPS TinoHost** với mã **VPSN8N** để self-host n8n ổn định.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với dữ liệu mẫu** trước khi bật live.

**🚀 [Tải workflow ngay từ n8n.io](https://n8n.io/workflows/15028)** và bắt đầu tự động hóa lead của bạn! 🎯