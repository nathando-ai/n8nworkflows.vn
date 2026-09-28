---
title: "🤖 **AI Research Agent Team: Tự Động Hoàn Thành Nghiên Cứu & Tạo Bài Viết Cùng Trích Dẫn Chứng Minh (OpenRouter + Perplexity)**"
description: "Workflow tự động hóa AI giúp các sếp xây dựng đội ngũ trợ lý nghiên cứu thông minh, tự động thu thập thông tin từ nhiều nguồn, phân tích và tổng hợp bài viết chuyên sâu với trích dẫn chính xác từ Perplexity và OpenRouter - không cần viết code!"
slug: "ai-research-agent-team-tich-dinh-chung-minh"
tags: [n8n, automation, ai-research, no-code, openrouter, perplexity, langchain]
keywords: [n8n workflow nghiên cứu AI, tự động hóa viết bài với trích dẫn, OpenRouter Perplexity n8n, AI agent team, tự động hóa content creation]
---

# 🚀 **AI Research Agent Team: Tự Động Hoàn Thành Nghiên Cứu & Tạo Bài Viết Cùng Trích Dẫn Chứng Minh**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu & Viết Bài**
Các sếp thường phải mất **từ 3-5 tiếng** để:
✅ **Thu thập thông tin** từ nhiều nguồn (Google Scholar, Perplexity, OpenAI, hoặc các API khác).
✅ **Phân tích và tổng hợp** dữ liệu một cách logic và khoa học.
✅ **Tạo bài viết** với cấu trúc rõ ràng và **trích dẫn chính xác** theo tiêu chuẩn học thuật.
✅ **Tránh plagiarism** và đảm bảo tính độc lập của nội dung.

**Workflow này giải quyết tất cả!** Một đội ngũ **AI Research Agent Team** sẽ:
- **Tự động nghiên cứu** theo yêu cầu của bạn.
- **Tạo bài viết** với cấu trúc chuyên nghiệp.
- **Thêm trích dẫn** từ Perplexity và OpenRouter.
- **Cập nhật liên tục** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **5 tiếng** xuống còn **5 phút** để chỉ cần nhập yêu cầu.
- **Bài viết chuyên nghiệp**: Cấu trúc rõ ràng, logic, và **trích dẫn chính xác** theo tiêu chuẩn học thuật.
- **Tự động cập nhật**: AI liên tục nghiên cứu và bổ sung thông tin mới nhất.
- **Không cần viết code**: Sử dụng **n8n + LangChain** để tự động hóa toàn bộ quy trình.
- **Hỗ trợ nhiều nguồn dữ liệu**: Kết nối với **Perplexity, OpenRouter, và các API khác**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Keys**:
   - **OpenRouter API Key** (đăng ký tại [OpenRouter](https://openrouter.ai/)).
   - **Perplexity API Key** (đăng ký tại [Perplexity](https://www.perplexity.ai/)).
   - **n8n Credentials** (để kết nối với các API trên).
2. **Dịch vụ hỗ trợ**:
   - **n8n Self-hosted** (để chạy workflow liên tục).
   - **LangChain Node** (đã được cài đặt trong n8n).
3. **Yêu cầu đầu vào**:
   - **Tiêu đề nghiên cứu** (ví dụ: *"Tác động của AI vào ngành y tế năm 2024"*).
   - **Yêu cầu cụ thể** (ví dụ: *"Tìm 5 nghiên cứu mới nhất về AI và tim mạch"*).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/2607](https://n8n.io/workflows/2607).
2. Mở **n8n Editor** → **Import Workflow** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **LangChain + AI Agents**, vì vậy cần cấu hình **cẩn thận** các node quan trọng:

##### **A. Cấu Hình API Keys**
- **Node `Perplexity API`** (type: `httpRequest`):
  - **URL**: `https://api.perplexity.ai/chat/completions`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_PERPLEXITY_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "model": "perplexity/llama-3.1-70b-online",
      "messages": [
        {"role": "user", "content": "$json.input.text"}
      ]
    }
    ```

- **Node `OpenAI Chat Model`** (type: `lmChatOpenAi`):
  - **Model**: `openrouter/mistral-7b` (hoặc model khác từ OpenRouter).
  - **API Key**: Điền **OpenRouter API Key**.
  - **Parameters**:
    ```json
    {
      "temperature": 0.7,
      "max_tokens": 1000
    }
    ```

##### **B. Cấu Hình AI Agents**
Workflow sử dụng **3 loại AI Agent** chính:
1. **`Research Leader 🔬`** (type: `agent`):
   - **Role**: Chỉ đạo quá trình nghiên cứu.
   - **Tools**:
     - `Perplexity_tool` (gọi API Perplexity).
     - `OpenAI Chat Model` (gọi API OpenRouter).
   - **Prompt**:
     ```plaintext
     Bạn là một nhà nghiên cứu AI chuyên nghiệp. Hãy phân tích yêu cầu của người dùng và phân công cho các trợ lý nghiên cứu.
     ```

2. **`Research Assistant`** (type: `agent`):
   - **Role**: Thực hiện nghiên cứu cụ thể.
   - **Tools**:
     - `Perplexity_tool1` (gọi API Perplexity).
     - `OpenAI Chat Model1` (gọi API OpenRouter).
   - **Prompt**:
     ```plaintext
     Bạn là một trợ lý nghiên cứu. Hãy tìm kiếm và tổng hợp thông tin từ các nguồn đáng tin cậy về chủ đề được chỉ định.
     ```

3. **`Editor`** (type: `agent`):
   - **Role**: Tạo bài viết và thêm trích dẫn.
   - **Tools**:
     - `OpenAI Chat Model3` (gọi API OpenRouter).
   - **Prompt**:
     ```plaintext
     Bạn là một biên tập viên chuyên nghiệp. Hãy viết bài viết với cấu trúc rõ ràng và thêm trích dẫn từ các nguồn đã thu thập.
     ```

##### **C. Cấu Hình Node `Structured Output Parser`**
- **Schema**:
  ```json
  {
    "type": "object",
    "properties": {
      "title": { "type": "string" },
      "content": { "type": "string" },
      "citations": {
        "type": "array",
        "items": {
          "type": "object",
          "properties": {
            "source": { "type": "string" },
            "quote": { "type": "string" }
          }
        }
      }
    }
  }
  ```
- **Mục đích**: Đảm bảo bài viết được cấu trúc với **tiêu đề, nội dung và trích dẫn**.

##### **D. Node `Merge chapters title and text`**
- **Merge** dữ liệu từ các AI Agent thành một **bài viết hoàn chỉnh**.

##### **E. Node `Final article text` (type: `code`)**
- **JavaScript Code** (nếu cần chỉnh sửa cuối cùng):
  ```javascript
  // Chỉnh sửa nội dung bài viết trước khi xuất
  return {
    ...node.inputData[0].json,
    formattedContent: node.inputData[0].json.content.replace(/\n/g, "<br>")
  };
  ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Điền **tiêu đề nghiên cứu** vào **n8n Form Trigger**.
   - Chạy **Manual Test** để kiểm tra kết quả.
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Sử dụng **n8n Node Slack/Telegram** để nhận thông báo kết quả nghiên cứu.
   - **Cách làm**:
     - Thêm **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram**.
     - Gửi kết quả từ **Final article text** đến kênh Slack/Telegram.

2. **Lưu Log & Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Node Google Sheets** hoặc **n8n Node Airtable** để lưu lịch sử nghiên cứu.
   - **Cách làm**:
     - Thêm **n8n-nodes-base.googleSheets**.
     - Gửi dữ liệu từ **Final article text** vào bảng Google Sheets.

3. **Tối Ưu Hóa Prompt**:
   - Nếu kết quả không tốt, **cập nhật prompt** của các AI Agent để rõ ràng hơn.
   - **Ví dụ**:
     ```plaintext
     Bạn phải trích dẫn **tối thiểu 3 nguồn** và đảm bảo trích dẫn chính xác theo tiêu chuẩn APA/MLA.
     ```

4. **Sử Dụng Nhiều Model AI**:
   - Thay đổi **model** trong `OpenAI Chat Model` để thử nghiệm hiệu suất.
   - **Lựa chọn model**:
     - `openrouter/mistral-7b` (nhanh, hiệu quả).
     - `openrouter/gpt-4` (chất lượng cao hơn).

---

### 📌 **Kết Luận**
Workflow **AI Research Agent Team** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa nghiên cứu** và viết bài với **trích dẫn chính xác**.
✔ **Tiết kiệm thời gian** và **tăng hiệu suất** công việc.
✔ **Không cần viết code** nhờ **n8n + LangChain**.

**Hãy thử ngay!** Import workflow, cấu hình API Keys, và **nhận bài viết chuyên nghiệp trong vài phút** thay vì mất cả ngày!

---
**💡 Mẹo cuối**: Nếu gặp vấn đề, hãy **check log** trong n8n và **cập nhật prompt** của AI Agents để tối ưu hóa kết quả.