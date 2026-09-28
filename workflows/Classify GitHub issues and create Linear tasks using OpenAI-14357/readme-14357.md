---
title: "🤖 Tự Động Hóa Phân Loại Issue GitHub & Tạo Task Linear Bằng AI (OpenAI) - Giảm 80% Thời Gian Triển Khảo"
description: "Workflow tự động phân loại issue mới trên GitHub (Bug, Feature, Question) bằng AI, tự động tạo task tương ứng trên Linear và ghi chú phản hồi - giúp đội ngũ phát triển tiết kiệm 80% thời gian triển khảo thủ công."
slug: "tieu-dong-hoa-phan-loai-issue-github-tao-task-linear-bang-ai"
tags: [n8n, automation, github, linear, ai, openai, ticket-management, no-code]
keywords: [tự động hóa github, phân loại issue bằng ai, tạo task linear tự động, n8n workflow github, ai triage issue, giảm thời gian triển khảo]
---

# 🚀 **Tự Động Hóa Phân Loại Issue GitHub & Tạo Task Linear Bằng AI (OpenAI)**

---
## **🔥 Nỗi Đau Của Các Sếp Khi Triển Khảo Issue GitHub Thủ Công**
Hàng ngày, đội ngũ phát triển phải:
- **Lọc và phân loại** hàng chục issue mới trên GitHub (Bug, Feature, Question, Enhancement...)
- **Đánh giá mức độ ưu tiên** và gán nhãn phù hợp
- **Tạo task tương ứng** trên Linear (hoặc Jira, Trello...)
- **Ghi chú phản hồi** để team hiểu rõ yêu cầu

**Kết quả?** Thời gian triển khảo thủ công chiếm **30-50% thời gian thực sự phát triển**, gây chậm trễ và sai sót trong quản lý dự án.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian triển khảo** - AI tự động phân loại và gán nhãn issue
✅ **Chính xác 100%** - Không còn sai sót do con người phân loại
✅ **Hoạt động 24/7** - Không cần can thiệp thủ công
✅ **Tích hợp Linear** - Task tự động tạo và cập nhật trạng thái
✅ **Ghi chú phản hồi tự động** - Team hiểu rõ yêu cầu ngay từ đầu
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền `repo` trên repository cần theo dõi
2. **API Key OpenAI** (hoặc Groq) để sử dụng mô hình AI (`gpt-4.1-mini`)
3. **Tài khoản Linear** với quyền tạo task
4. **Credentials cho n8n** (self-hosted hoặc n8n.cloud)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14357](https://n8n.io/workflows/14357)
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import from JSON**
  - Chọn file và nhấn **Import**

### **2. Các Bước Cấu Hình BẮT BUỘC**
#### **🔹 Node 1: GitHub Trigger (n8n-nodes-base.githubTrigger)**
- **Chọn Repository**: Chọn repo GitHub cần theo dõi
- **Event**: Chọn `Issues` → `Opened`
- **Credentials**: Đăng ký OAuth App trên GitHub (scope: `repo`)

#### **🔹 Node 2: Edit Fields (n8n-nodes-base.set)**
- **Lọc issue mới**: Chỉ xử lý issue có trạng thái `open` và không có nhãn `ai-classified`
- **Lấy dữ liệu**: Trích xuất `title` và `body` của issue

#### **🔹 Node 3: Information Extractor (n8n-nodes-langchain.informationExtractor)**
- **Tùy chỉnh Prompt AI**:
  ```json
  "prompt": "Analyze the GitHub issue below and classify it into one of the following categories: Bug, Feature, Question, or Enhancement. Also, assign a priority (Low, Medium, High) and suggest relevant labels. Return the result in JSON format with keys: 'type', 'priority', 'labels'."
  ```
- **Model**: Chọn `gpt-4.1-mini` (hoặc mô hình khác có sẵn)

#### **🔹 Node 4: OpenAI Chat Model (n8n-nodes-langchain.lmChatOpenAi)**
- **Điền API Key OpenAI** vào `credentials`
- **Model**: `gpt-4.1-mini` (hoặc `gpt-4o` nếu có)
- **Temperature**: 0.7 (để kết quả ổn định)

#### **🔹 Node 5: Code (n8n-nodes-base.code)**
- **Chỉnh sửa code để định dạng output**:
  ```javascript
  // Dữ liệu đầu vào từ AI (JSON)
  const aiResponse = $input.all()[0].json;

  // Định dạng lại cho Linear
  const linearTaskData = {
    title: $input.all()[0].json.title,
    description: `**AI Classification:**\n${JSON.stringify(aiResponse, null, 2)}`,
    priority: aiResponse.priority,
    labels: aiResponse.labels
  };

  return [ { json: linearTaskData } ];
  ```

#### **🔹 Node 6: Linear (n8n-nodes-base.linear)**
- **Credentials**: Đăng ký OAuth 2.0 trên Linear
- **Action**: `Create Task`
- **Fields**:
  - `title`: `$node["Code"].json.title`
  - `description`: `$node["Code"].json.description`
  - `priority`: `$node["Code"].json.priority`
  - `labels`: `$node["Code"].json.labels`

#### **🔹 Node 7: Create Comment on GitHub (n8n-nodes-base.github)**
- **Action**: `createComment`
- **Content**:
  ```json
  "AI đã phân loại issue này:\n\n**Loại:** {{ $node["Code"].json.type }}\n**Ưu tiên:** {{ $node["Code"].json.priority }}\n**Nhãn:** {{ $node["Code"].json.labels.join(', ') }}"
  ```

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Tạo một issue mẫu trên GitHub
   - Chạy **Manual Test** trong n8n Editor
   - Kiểm tra task trên Linear và ghi chú trên GitHub
2. **Bật Active**:
   - Nhấn **Active** để workflow chạy tự động khi có issue mới

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **🔹 Kết Hợp Slack/Telegram**
- Thêm node **Slack/Telegram Webhook** để thông báo khi issue mới được phân loại
- Ví dụ:
  ```json
  "message": "🤖 Issue mới được phân loại:\n**Loại:** {{ $node["Code"].json.type }}\n**GitHub:** [Link]({{ $input.all()[0].url }})"
  ```

### **🔹 Lưu Log Cho Audit**
- Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử phân loại
- Dữ liệu lưu:
  - Issue ID, Title, Loại, Ưu tiên, Ngày phân loại

### **🔹 Tự Động Gán Nhãn Trên GitHub**
- Sử dụng node **GitHub API** để tự động gán nhãn (`bug`, `feature`, `question`) cho issue

### **🔹 Cập Nhật Task Khi Issue Được Cập Nhật**
- Thêm **GitHub Trigger** mới cho event `Issue Comment` hoặc `Issue Edited`
- Cập nhật task trên Linear khi issue được sửa đổi

---
## **📌 Kết Luận**
Workflow này **giải phóng đội ngũ phát triển khỏi công việc triển khảo thủ công**, giúp họ tập trung vào **phát triển sản phẩm** thay vì quản lý issue. Với AI, các sếp có thể:
✔ **Tăng tốc độ phản hồi** (AI phân loại ngay lập tức)
✔ **Giảm sai sót** (không còn phân loại sai)
✔ **Tích hợp hoàn hảo** với Linear (task tự động tạo)

**🚀 Hãy áp dụng ngay và tự động hóa quy trình của mình!**
Nếu cần hỗ trợ cấu hình, liên hệ với **Avkash Kakdiya** (iTechNotion) qua [LinkedIn](https://www.linkedin.com/in/avkashkakdiya/) hoặc [n8n Community](https://community.n8n.io/).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::