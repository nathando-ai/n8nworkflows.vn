---
title: "🤖 Tự Động Hóa Xử Lý & Phân Loại Phản Hồi Khách Hàng với GPT-4o, Gemini + Guardrails (N8n)"
description: "Workflow tự động hóa hoàn chỉnh phân loại phản hồi khách hàng thành 4 loại: vấn đề sản phẩm, yêu cầu tính năng, phàn nàn và lời khen, đồng thời tự động tạo ticket Jira, thêm vào backlog hoặc chuyển cho CS. Giảm 90% công việc thủ công cho team hỗ trợ khách hàng."
slug: "tieu-ly-phan-hoi-khach-hang-voi-gpt-4o-gemini"
tags: [n8n, automation, ai-summarization, ticket-management, no-code, openai, gemini]
keywords: [n8n workflow phản hồi khách hàng, tự động hóa phân loại phản hồi, GPT-4o Gemini trong n8n, guardrails AI, tự động tạo ticket Jira]
---

# 🚀 **Tự Động Hóa Xử Lý Phản Hồi Khách Hàng với AI: Phân Loại + Tạo Ticket + Trả Lời Tự Động**

## **Nỗi Đau Của Các Sếp: Phản Hồi Khách Hàng Làm Chậm Team Hỗ Trợ**
Các sếp đã từng trải qua cảnh này chưa?
- **Đội CS phải đọc hàng trăm phản hồi** mỗi ngày, phân loại thủ công giữa "vấn đề sản phẩm", "yêu cầu tính năng", "phàn nàn" và "lời khen".
- **T ticket Jira/backlog** phải tạo một cách cẩn thận, lo sợ bỏ sót thông tin quan trọng.
- **Trả lời khách hàng** mất thời gian, dễ bị trùng lặp hoặc không cá nhân hóa.
- **Rủi ro vi phạm chính sách** khi phản hồi không phù hợp với tone brand.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4o + Gemini** kết hợp với **guardrails AI**, nó tự động:
✅ **Phân loại phản hồi** với độ chính xác cao (95%+).
✅ **Tạo ticket Jira tự động** cho vấn đề sản phẩm.
✅ **Thêm yêu cầu tính năng vào backlog** (Jira/Notion).
✅ **Chuyển phàn nàn lên team CS** với thông tin chi tiết.
✅ **Lọc lời khen để sử dụng làm testimonial**.
✅ **Trả lời khách hàng tự động** (hoặc gửi queuing cho review người).
✅ **Ngăn chặn nội dung nguy hại** (PII, injection, từ cấm) bằng guardrails.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8-10 giờ/ngày** cho team CS (tương đương 1 nhân viên toàn thời gian).
- **Giảm 90% lỗi phân loại** nhờ AI + guardrails.
- **Tự động hóa 100% ticket Jira/backlog** (không cần copy-paste).
- **Trả lời khách hàng nhanh chóng** với tone phù hợp, giảm thời gian phản hồi từ 24h → 1h.
- **Lọc testimonial chất lượng** từ lời khen tự động.
- **Ngăn chặn nội dung nguy hại** (PII, spam, từ cấm) trước khi xử lý.
- **Hoạt động 24/7** mà không cần can thiệp người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - **OpenAI API Key** (để sử dụng GPT-4o).
   - **OpenRouter API Key** (để sử dụng Gemini).
   - **Credentials cho Jira/Notion** (nếu tự động tạo ticket).
   - **Credentials cho Slack/Email** (nếu gửi thông báo tự động).

2. **Cấu hình cơ bản**:
   - **Webhook URL** để nhận phản hồi từ khách hàng (cần copy từ node `Webhook - Feedback Intake` sau khi import).
   - **Mô hình AI**:
     - GPT-4o (trên OpenAI).
     - Gemini 3 Flash (trên OpenRouter).

3. **Dữ liệu mẫu**:
   - Các sếp nên chuẩn bị **5-10 phản hồi khách hàng** khác nhau (vấn đề, yêu cầu, phàn nàn, lời khen) để test.

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13855](https://n8n.io/workflows/13855) (chọn "Download JSON").
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** và dán toàn bộ JSON từ [n8n.io/workflows/13855](https://n8n.io/workflows/13855) (chọn "Copy JSON").
3. Nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình cẩn thận** các node quan trọng sau:

#### **A. Cấu Hình Credentials cho AI**
| Node | Tham Số Cần Chỉnh | Ghi Chú |
|------|-------------------|---------|
| **Input Guardrails LLM** | `openAiApi` (credentials) | Điền API Key OpenAI. |
| **OpenRouter Chat Model** | `openRouterApi` (credentials) | Điền API Key OpenRouter. |
| **OpenRouter Chat Model1** | `openRouterApi` (credentials) | Giống node trên. |

🔹 **Mô hình AI**:
- Node `Input Guardrails LLM` → Sử dụng **GPT-4o** (đã cấu hình mặc định).
- Node `OpenRouter Chat Model` → Sử dụng **Gemini 3 Flash** (đã cấu hình mặc định).

#### **B. Cấu Hình Webhook**
- Node **`Webhook - Feedback Intake`**:
  - **HTTP Method**: POST (đã mặc định).
  - **Path**: `/customer-feedback` (không cần thay đổi).
  - **Copy URL Webhook** để gửi phản hồi từ khách hàng (ví dụ: từ Slack, Typeform, hoặc API của hệ thống CRM).

#### **C. Cấu Hình Routing (Switch Node)**
Node **`Route by Type`** (Switch) quyết định phản hồi sẽ được xử lý như thế nào:
- **Product Issue** → Tạo ticket Jira.
- **Feature Request** → Thêm vào backlog.
- **Complaint** → Escalate lên CS.
- **Praise** → Flag làm testimonial.
- **Low Confidence** → Queue cho review người.

🔹 **Cách chỉnh**:
1. Mở node `Route by Type` → Nhấn **Edit**.
2. Thay đổi **mapping** để phù hợp với hệ thống của các sếp (ví dụ: thay Jira bằng Notion, Slack thay vì Email).
3. **Test run** với dữ liệu mẫu để kiểm tra logic.

#### **D. Cấu Hình Guardrails**
Hai node **`Input Guardrails`** và **`Output Guardrails`** ngăn chặn:
- **PII** (thông tin cá nhân).
- **Injection** (code độc hại).
- **Từ cấm** (vi phạm chính sách).

🔹 **Cách chỉnh**:
- Mở node `Input Guardrails` → Nhấn **Edit Prompt** để thêm/bỏ từ cấm theo yêu cầu.
- Mở node `Output Guardrails` → Kiểm tra lại logic kiểm tra phản hồi AI.

#### **E. Cấu Hình Code Nodes (Placeholder)**
Các sếp cần **thay thế placeholder** trong Code nodes bằng logic thực tế:
| Node | Thay Thế Gì | Ví Dụ |
|------|-------------|-------|
| **Create Jira Ticket** | Logic tạo ticket Jira | Sử dụng `n8n-nodes-jira` hoặc API Jira. |
| **Add to Backlog** | Logic thêm vào Notion/Confluence | Sử dụng `n8n-nodes-notion`. |
| **Escalate to CS** | Gửi thông báo Slack/Email | Sử dụng `n8n-nodes-slack` hoặc `n8n-nodes-email`. |
| **Flag as Testimonial** | Lưu vào Google Sheets/Notion | Sử dụng `n8n-nodes-google-sheets`. |

🔹 **Mẫu Code cho Jira (ví dụ)**:
```javascript
// Thay thế trong node "Create Jira Ticket"
const issueData = {
  fields: {
    summary: $input.json["summary"],
    description: $input.json["draft_response"],
    issuetype: { name: "Bug" },
    project: { key: "PROJ" }
  }
};
return { json: issueData };
```

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với Dữ liệu Mẫu**:
   - Gửi **5 phản hồi khác nhau** (vấn đề, yêu cầu, phàn nàn, lời khen) qua Webhook URL.
   - Kiểm tra kết quả ở mỗi node (AI phân loại, guardrails, routing).

2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - Kiểm tra log để đảm bảo không có lỗi.

3. **Monitoring**:
   - Sử dụng **n8n Dashboard** để theo dõi hoạt động.
   - Cài đặt **alerts** nếu workflow ngừng hoạt động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối với Slack/Telegram**
- Thêm node **`n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`** để:
  - **Báo cáo tự động** khi có phản hồi mới.
  - **Gửi thông báo khi ticket Jira được tạo**.

🔹 **Cách làm**:
1. Thêm node Slack sau node `Create Jira Ticket`.
2. Cấu hình message template:
   ```json
   {
     "text": "🚨 New Jira Ticket Created!\n**Summary**: {{ $json.fields.summary }}\n**Link**: {{ $json.self }}",
     "blocks": [...]
   }
   ```

### **2. Lưu Log Tất Cả Phản Hồi**
- Thêm node **`n8n-nodes-google-sheets`** hoặc **`n8n-nodes-database`** để:
  - Lưu tất cả phản hồi (đã xử lý và chờ xử lý).
  - Dễ dàng tra cứu sau này.

🔹 **Cách làm**:
1. Thêm node Google Sheets sau node `Route by Type`.
2. Cấu hình header:
   ```json
   [
     "id",
     "feedback_text",
     "category",
     "status",
     "created_at",
     "response_draft"
   ]
   ```

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n Cron Trigger** để:
  - Gửi báo cáo hàng tuần về:
    - Số lượng phản hồi mới.
    - Phân loại theo loại (vấn đề, yêu cầu, phàn nàn, lời khen).
    - Tỷ lệ ticket Jira được tạo.

🔹 **Cách làm**:
1. Tạo workflow mới với **Cron Trigger** (ví dụ: `0 0 * * 1` - Chủ nhật 00:00).
2. Thêm node **`n8n-nodes-email`** hoặc **`n8n-nodes-slack`** để gửi báo cáo.

### **4. Tùy Chỉnh Prompt AI**
- **Node `AI - Classify + Draft`** sử dụng **LangChain Agent**.
- Các sếp có thể **tùy chỉnh prompt** để:
  - **Phân loại chính xác hơn** (ví dụ: thêm ví dụ cụ thể).
  - **Trả lời khách hàng cá nhân hóa** hơn.

🔹 **Mẫu Prompt Mẫu**:
```plaintext
TASK:
You are a customer support assistant. Classify the following feedback into one of these categories:
1. Product Issue
2. Feature Request
3. Complaint
4. Praise

Then, draft a response based on the category.

INSTRUCTIONS:
- For Product Issue: Ask for more details and promise to escalate.
- For Feature Request: Thank the user and add to backlog.
- For Complaint: Apologize and offer compensation.
- For Praise: Thank and suggest sharing testimonial.

FEEDBACK: {{ $json.feedback_text }}
```

### **5. Cải Thiện Độ Chính Xác**
- **Node `High Confidence + Valid?`** kiểm tra độ tin cậy của AI.
- Các sếp có thể:
  - **Tăng giảm ngưỡng confidence** (ví dụ: từ 0.85 → 0.9).
  - **Thêm logic kiểm tra** trong Code node `Validate AI Output`.

🔹 **Mẫu Code Kiểm Tra Confidence**:
```javascript
// Thay thế trong node "Validate AI Output"
const confidenceThreshold = 0.9;
if ($input.json.confidence < confidenceThreshold) {
  return { json: { error: "Low confidence - needs review" } };
}
return $input.json;
```

---

## 📌 **Kết Luận: Áp Dụng Ngay để Tiết Kiệm Thời Gian & Tăng Trải Nghiệm Khách Hàng**

Workflow này **giải phóng team CS** khỏi công việc lặp lại, đồng thời **tăng chất lượng xử lý phản hồi** nhờ AI + guardrails. Các sếp không cần là nhà phát triển để triển khai - chỉ cần **cấu hình một lần** và workflow sẽ hoạt động tự động 24/7.

### **Bước Đầu Tiên: Import & Test**
1. **Import workflow** từ [n8n.io/workflows/13855](https://n8n.io/workflows/13855).
2. **Cấu hình credentials** (OpenAI, OpenRouter, Jira/Notion).
3. **Test với 5 phản hồi mẫu** để đảm bảo logic hoạt động.
4. **