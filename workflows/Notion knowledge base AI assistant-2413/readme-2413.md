---
title: "🤖 Trợ lý AI Tự động Học tập từ Notion: Tự động hóa Trả lời Câu hỏi HR/IT 100% Không Code"
description: "Workflow này tự động hóa việc trả lời câu hỏi liên quan đến tri thức nội bộ (HR, IT Ops) từ Notion Knowledge Base bằng trí tuệ nhân tạo (AI). Giúp tiết kiệm thời gian lên tới 80% cho việc tra cứu và giải đáp, đồng thời đảm bảo tính chính xác cao nhờ tích hợp OpenAI/GPT-4o."
slug: "tro-ly-ai-notion-knowledge-base"
tags: [n8n, automation, ai, notion, hr, it-ops, langchain, openai]
keywords: [n8n workflow notion ai, tự động hóa trả lời câu hỏi, trợ lý tri thức nội bộ, gpt-4o với notion, langchain n8n, ai chatbot nội bộ]
---

# 🚀 **Trợ lý AI Tự động Học tập từ Notion: Giải pháp Trả lời Câu hỏi HR/IT 24/7**

## **Nỗi đau thực tế của các sếp**
Hàng ngày, các sếp và đội ngũ HR/IT phải mất **giờ đồng hồ** để:
- Tra cứu thông tin trong Notion Knowledge Base (KB) để trả lời câu hỏi của nhân viên.
- Đảm bảo tính chính xác của thông tin, tránh sai sót khi giải đáp.
- Cập nhật liên tục tri thức mới vào hệ thống, làm cho quá trình tra cứu trở nên phức tạp.

**Workflow này giải quyết tất cả!** Bằng cách tích hợp **Notion + OpenAI (GPT-4o) + LangChain**, trợ lý AI sẽ:
✅ **Trả lời tự động** câu hỏi từ nhân viên trong Slack/Telegram/Email.
✅ **Học tập liên tục** từ Notion KB, cập nhật tri thức mới mà không cần can thiệp thủ công.
✅ **Hoạt động 24/7** mà không cần người quản lý.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian tra cứu và trả lời câu hỏi.
- **Tính chính xác cao**: AI sử dụng tri thức từ Notion KB, tránh sai sót của con người.
- **Cập nhật tự động**: Khi Notion KB được sửa đổi, trợ lý AI sẽ tự động học tập thông tin mới.
- **Trải nghiệm cá nhân hóa**: Trả lời linh hoạt dựa trên ngữ cảnh và yêu cầu cụ thể của người dùng.
- **Hoạt động liên tục**: Không cần can thiệp thủ công, hoạt động 24/7.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Notion**:
   - Một **Notion Knowledge Base** đã được thiết lập (sử dụng [mẫu template](https://www.notion.so/templates/knowledge-base-ai-assistant-with-n8n)).
   - **API Key Notion**: Tạo từ [Notion Developers](https://developers.notion.com/docs/create-a-notion-integration).
   - **Chia sẻ quyền truy cập** với n8n để AI có thể đọc dữ liệu.

2. **Tài khoản OpenAI (hoặc Anthropic)**:
   - **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys)).
   - **Model GPT-4o** (hoặc Claude 3.5) để xử lý logic AI.

3. **n8n Workspace**:
   - Cài đặt **n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
   - Cài đặt **n8n LangChain nodes** (để hỗ trợ AI Agent).

4. **Dịch vụ chat (lựa chọn)**:
   - **Slack/Telegram/Email** (để nhận câu hỏi từ nhân viên).
   - **Webhook** (để kết nối với dịch vụ chat).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/2413](https://n8n.io/workflows/2413) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** và chọn file JSON tải xuống.
3. Chọn **Workspace** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** và tạo một **Workflow mới**.
2. Nhấn **Import** > **Paste JSON** và dán nội dung JSON từ [n8n.io/workflows/2413](https://n8n.io/workflows/2413).
3. Chọn **Workspace** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Notion API**
1. **Thêm Credential Notion**:
   - Trên **n8n Editor**, nhấn **Credentials** > **Add Credential** > **Notion**.
   - Điền:
     - **API Key**: API Key từ Notion Developers.
     - **Integration Token**: Token từ Notion (tạo trong Notion Developers).
   - Lưu credential với tên **`notionApi`**.

2. **Cấu hình các Node Notion**:
   - **`Get database details`**:
     - Chọn **Credential**: `notionApi`.
     - Chọn **Database**: Chọn Notion KB đã tạo (từ **Step 2** trong hướng dẫn dưới).
   - **`Search notion database`** và **`Search inside database record`**:
     - Chọn **Notion API**: `notionApi`.

#### **🔹 Cấu hình OpenAI (GPT-4o)**
1. **Thêm Credential OpenAI**:
   - Trên **n8n Editor**, nhấn **Credentials** > **Add Credential** > **OpenAI**.
   - Điền:
     - **API Key**: API Key từ OpenAI.
     - **Model**: `gpt-4o` (hoặc `claude-3.5` nếu dùng Anthropic).
   - Lưu credential với tên **`openAiApi`**.

2. **Cấu hình Node `OpenAI Chat Model`**:
   - Chọn **Credentials**: `openAiApi`.
   - Đảm bảo **Model** được đặt là `gpt-4o`.

#### **🔹 Cấu hình Node `When chat message received`**
- Nếu muốn nhận câu hỏi từ **Slack/Telegram/Email**, cần cấu hình:
  - **Slack**: Sử dụng **n8n-nodes-slack** và kết nối với Webhook Slack.
  - **Telegram**: Sử dụng **n8n-nodes-telegram** và kết nối với Bot Telegram.
  - **Email**: Sử dụng **n8n-nodes-email** và kết nối với Gmail/Outlook.

#### **🔹 Cấu hình Node `AI Agent`**
- Node này sẽ tự động xử lý logic AI dựa trên:
  - **Memory Buffer Window**: Lưu trữ lịch sử câu hỏi-trả lời để AI học tập.
  - **ToolHttpRequest**: Tìm kiếm trong Notion KB.
  - **ChatTrigger**: Nhận câu hỏi từ người dùng.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và gửi một **câu hỏi mẫu** (ví dụ: *"Làm thế nào để xin phép nghỉ phép?"*).
   - Kiểm tra AI trả lời có chính xác không.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Activate Workflow**.
   - Sao chép **Chat URL** từ node **`When chat message received`** để chia sẻ với nhân viên.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Kết hợp với Slack/Telegram**
- **Slack**: Sử dụng **n8n-nodes-slack** để nhận câu hỏi từ kênh Slack.
- **Telegram**: Sử dụng **n8n-nodes-telegram** để tạo bot trả lời tự động.

### **🔹 Lưu log hoạt động**
- Thêm **n8n-nodes-base.quick** để lưu log câu hỏi-trả lời vào Notion hoặc Google Sheets.

### **🔹 Gửi báo cáo định kỳ**
- Sử dụng **n8n-nodes-base.schedule** để gửi báo cáo tổng hợp về hoạt động của trợ lý AI.

### **🔹 Cập nhật tri thức mới**
- Khi Notion KB được cập nhật, AI sẽ tự động học tập thông tin mới trong lần chạy tiếp theo.

---

## 📌 **Kết luận**
Workflow **Notion Knowledge Base AI Assistant** là giải pháp **tự động hóa hoàn hảo** cho việc trả lời câu hỏi HR/IT, giúp các sếp:
✔ **Tiết kiệm thời gian** lên tới 80%.
✔ **Đảm bảo tính chính xác** nhờ AI học tập từ Notion KB.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay để nâng cao hiệu suất công việc của đội ngũ!**
👉 [Tải workflow](https://n8n.io/workflows/2413) và bắt đầu tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chú ý**: Nếu gặp lỗi `The resource you are requesting could not be found` trong node **`Get database details`**, đảm bảo đã **chia sẻ Notion KB với credential Notion** và chọn **Database chính xác** trong dropdown.