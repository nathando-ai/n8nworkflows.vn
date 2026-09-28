---
title: "🚀 Tự Động Chuyển Yêu Cầu DevOps Trên Mattermost Sang Nhiệm Vụ Jira Với AI (N8n Workflow)"
description: "Workflow tự động hóa 100% không code chuyển đổi yêu cầu tự do từ Mattermost sang nhiệm vụ Jira chuẩn hóa, tích hợp AI để phân tích, phân loại và tạo tự động nhãn/phân loại. Giúp DevOps tiết kiệm 80% thời gian xử lý ticket thủ công."
slug: "tieu-dong-yeu-cau-devops-mattermost-sang-jira-voi-ai"
tags: [n8n, automation, devops, ai-rag, jira, mattermost, no-code]
keywords: [n8n workflow devops, tự động hóa jira, ai chuyển đổi yêu cầu, mattermost jira integration, tự động hóa devops]
---

# 🚀 **Tự Động Chuyển Yêu Cầu DevOps Trên Mattermost Sang Nhiệm Vụ Jira Với AI**

## **Giới Thiệu**
Các sếp DevOps thường phải chịu gánh nặng **xử lý hàng trăm yêu cầu tự do** trên Mattermost, sau đó phải **chuyển đổi thủ công** sang Jira với các định dạng khác nhau. Quá trình này không chỉ tốn thời gian mà còn dễ gây **sai sót, mất mát thông tin** và khó theo dõi tiến độ.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động chuyển đổi** yêu cầu từ Mattermost sang Jira với **định dạng chuẩn hóa**
✅ **Sử dụng AI (GPT-5.3 + Gemini Embeddings)** để phân tích nội dung, tự động **phân loại, thêm nhãn và mô tả chi tiết**
✅ **Tích hợp phân tích file đính kèm** (ảnh, PDF, log) thông qua sub-workflow
✅ **Trả lời tự động** trên Mattermost với liên kết Jira để theo dõi dễ dàng

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** xử lý ticket thủ công
- **Giảm sai sót** nhờ AI phân tích tự động
- **Cá nhân hóa nhãn/phân loại** theo quy trình DevOps của doanh nghiệp
- **Hoạt động 24/7** mà không cần can thiệp người dùng
- **Tích hợp hoàn hảo** với Mattermost và Jira hiện có
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **API Key & Credentials:**
   - **OpenRouter API Key** (hoặc OpenAI/Anthropic) cho mô hình AI (`gpt-5.3-codex`)
   - **Google Gemini API Key** (để tạo embedding cho phân tích)
   - **Jira API Credentials** (Cloud hoặc Server)
   - **Mattermost API Credentials** (để trả lời tự động)

✔ **Hệ thống hỗ trợ:**
   - **Qdrant Instance** (để lưu trữ embedding và tìm kiếm thông tin liên quan)
   - **Mattermost MCP Server** (để phân tích file đính kèm)
   - **Sub-workflow `attachmentsAnalyzer`** (để phân tích nội dung file)
   - **Workflow phân loại cha (Classifier Workflow)** để kích hoạt workflow này

✔ **Cấu hình thêm:**
   - **Đã index hóa tài liệu DevOps** vào Qdrant (ví dụ: docs về infrastructure, quy trình triage)
   - **Cấu hình Jira Project, Issue Type, Component** phù hợp với team
   - **Tùy chỉnh System Prompt** trong AI Agent để phù hợp với **taxonomy** của doanh nghiệp
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
```bash
# Cách import từ file JSON:
1. Tải workflow từ [n8n.io/workflows/15614](https://n8n.io/workflows/15614)
2. Click vào "Export" (icon hình file) và chọn "Export as JSON"
3. Trong n8n Editor, click "Import" và dán JSON vào
```

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** vì tích hợp AI + Jira + Mattermost, nên các sếp cần chú ý đến các node **quan trọng sau**:

#### **🔹 Node "SetVars" (Cấu hình biến toàn cục)**
- **Cần chỉnh sửa** các biến như:
  - `JIRA_PROJECT_KEY` (ví dụ: `DEVOPS`)
  - `JIRA_ISSUE_TYPE` (ví dụ: `Task`)
  - `JIRA_COMPONENT` (ví dụ: `Infrastructure`)
  - `MATTERMOST_CHANNEL` (đường dẫn channel Mattermost để trả lời)

#### **🔹 Node "AI Agent" (Mô hình GPT-5.3 + Qdrant)**
- **System Prompt** (định hướng AI):
  ```plaintext
  Bạn là một AI trợ lý DevOps chuyên phân tích yêu cầu từ Mattermost.
  Dựa vào:
  1. Nội dung yêu cầu (message)
  2. File đính kèm (nếu có)
  3. Tài liệu DevOps trong Qdrant (embedding)
  Hãy tạo một **Jira Task** với:
  - Tiêu đề: [Tóm tắt ngắn gọn]
  - Mô tả: [Chi tiết, bao gồm yêu cầu, rủi ro, giải pháp đề xuất]
  - Nhãn: [devops, critical, enhancement, bug]
  - Phân loại: [Infrastructure, Monitoring, CI/CD]
  ```
- **Cần tùy chỉnh** để phù hợp với **quy trình của team** (ví dụ: thêm/loại bỏ nhãn).

#### **🔹 Node "Qdrant Vector Store" (Tìm kiếm thông tin liên quan)**
- **Chỉnh URL & Collection Name** của Qdrant:
  ```json
  {
    "url": "https://your-qdrant-instance.com",
    "collectionName": "devops_docs"
  }
  ```
- **Yêu cầu:** Đã **index hóa tài liệu DevOps** (ví dụ: docs về Kubernetes, Terraform) vào Qdrant trước khi chạy.

#### **🔹 Node "Create an issue" (Tạo Jira Task)**
- **Chọn Project, Issue Type, Component** phù hợp:
  - **Project:** `DEVOPS` (hoặc tên project của doanh nghiệp)
  - **Issue Type:** `Task` (hoặc `Story`, `Bug`)
  - **Component:** `Infrastructure` (hoặc `Monitoring`, `CI/CD`)

#### **🔹 Node "Post a message" (Trả lời tự động trên Mattermost)**
- **Chỉnh `channel_id` và `message template`** để trả lời chính xác:
  ```json
  {
    "channel_id": "CHANNEL_ID",
    "message": "✅ Yêu cầu đã được chuyển thành Jira: <{{ $json["jiraUrl"] }}|Task DEVOPS-123>"
  }
  ```

#### **🔹 Node "Execute Workflow" (Kích hoạt sub-workflow `attachmentsAnalyzer`)**
- **Đảm bảo sub-workflow này đã được import và cấu hình:**
  - **Input:** `file_ids` từ yêu cầu Mattermost
  - **Output:** Kết quả phân tích file (nếu có)

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Sử dụng **Webhook Test** hoặc **Execute Workflow Trigger** với payload mẫu:
     ```json
     {
       "message": "Fix high CPU usage on prod-server-01",
       "file_ids": ["file123", "file456"],
       "category": "Infrastructure",
       "confidence": 0.95
     }
     ```
2. **Kiểm tra kết quả:**
   - Jira Task được tạo thành công?
   - Trả lời Mattermost có đúng không?
   - AI có phân tích chính xác không?
3. **Bật Active workflow** khi đã kiểm tra xong.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Tích hợp Slack/Telegram:** Sử dụng node `httpRequestTool` để gửi thông báo khi Jira Task được tạo.
- **Lưu log hoạt động:** Sử dụng node `stickyNote` hoặc `executeWorkflow` để ghi lại lịch sử.
- **Báo cáo định kỳ:** Tạo một workflow riêng để **tổng hợp thống kê** số lượng ticket, thời gian giải quyết.
- **Cải thiện System Prompt:** Thêm **ví dụ thực tế** của team vào System Prompt để AI học hỏi tốt hơn.
- **Phân tích file tự động:** Nếu có file log/ảnh, sub-workflow `attachmentsAnalyzer` sẽ **tự động extraxt thông tin** (ví dụ: lỗi CPU, cấu hình mạng).
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp DevOps khỏi công việc **chuyển đổi ticket thủ công**, đồng thời **tăng cường chính xác** nhờ AI. **Chỉ cần cấu hình một lần**, workflow sẽ **hoạt động tự động 24/7**, giúp team **tăng hiệu suất và giảm sai sót**.

**🚀 Hãy áp dụng ngay và tự động hóa quy trình DevOps của doanh nghiệp!**

---
:::note[CHÚ Ý CUỐI CÙNG]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow **không bị giới hạn** về số lượng request.
- **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%)**
- **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
**Bạn có thắc mắc về cách cấu hình cụ thể? Hãy để lại comment bên dưới!** 🚀