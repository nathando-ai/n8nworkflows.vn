---
title: "🚀 Tự Động Xử Lý Nhiều Prompt Song Song với Azure OpenAI Batch API – Không Cần Code"
description: "Workflow này giúp các sếp tự động hóa việc gửi và xử lý hàng loạt yêu cầu (prompts) đến Azure OpenAI một cách song song, tiết kiệm thời gian lên đến 90% so với cách làm thủ công. Phù hợp cho các dự án AI lớn, phân tích dữ liệu, hoặc xây dựng hệ thống chatbot thông minh."
slug: "tieu-ly-nhieu-prompt-song-song-azure-openai"
tags: [n8n, automation, azure-openai, ai, batch-processing, no-code]
keywords: [n8n workflow azure openai, tự động hóa AI, xử lý batch prompt, Azure OpenAI batch api, tự động hóa không code]
---

# 🚀 **Tự Động Xử Lý Nhiều Prompt Song Song với Azure OpenAI Batch API – Không Cần Code**

### **Giải pháp cho các sếp muốn xử lý hàng loạt yêu cầu AI một cách hiệu quả, tiết kiệm thời gian và chi phí**

Hiện nay, khi các sếp cần phân tích dữ liệu, xây dựng chatbot, hoặc thực hiện các tác vụ AI phức tạp, việc gửi từng yêu cầu (prompt) một cách riêng lẻ đến Azure OpenAI là một quá trình **tốn thời gian, dễ sai sót và không hiệu quả**. Thậm chí, với số lượng lớn, việc này có thể **chậm trễ và tốn kém** do giới hạn API rate limit.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Xử lý song song** (parallel processing) nhiều prompt cùng một lúc, giảm thời gian xử lý từ **giờ xuống phút**.
✅ **Tối ưu hóa chi phí** bằng cách gửi batch yêu cầu thay vì từng yêu cầu riêng lẻ.
✅ **Tự động hóa hoàn toàn** – không cần viết code, chỉ cần cấu hình và chạy.
✅ **Phù hợp với các dự án AI lớn**, như phân tích văn bản, tổng hợp thông tin, hoặc xây dựng hệ thống chatbot thông minh.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Điều này đảm bảo:
✔ **Tốc độ xử lý nhanh** (không phụ thuộc vào n8n.cloud).
✔ **An toàn và riêng tư** (dữ liệu không bị lưu trên cloud công cộng).
✔ **Không giới hạn API rate limit** (n8n self-hosted không bị hạn chế như phiên bản cloud).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo ổn định cho workflow AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công (không cần gửi từng prompt một).
- **Giảm chi phí Azure OpenAI** bằng cách xử lý batch thay vì từng yêu cầu.
- **Xử lý song song** – nhiều prompt được xử lý đồng thời, không phải chờ đợi.
- **Tự động hóa hoàn toàn** – không cần can thiệp thủ công sau khi cấu hình.
- **Phù hợp với các dự án AI lớn**, như phân tích văn bản, tổng hợp thông tin, hoặc xây dựng chatbot.
- **Dễ dàng mở rộng** – có thể kết nối với Slack, Email, hoặc cơ sở dữ liệu để tự động hóa thêm các tác vụ liên quan.
:::

---

### 🔧 **Yêu cầu cần thiết**

Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Azure OpenAI** (và **API Key** tương ứng).
✔ **Dữ liệu đầu vào** (các prompt cần xử lý, có thể là danh sách JSON, CSV, hoặc dữ liệu từ cơ sở dữ liệu).
✔ **N8n self-hosted** (không khuyến nghị sử dụng phiên bản cloud vì giới hạn API rate limit).
✔ **Tham số cấu hình** (nếu cần, như `api-version`, `deployment-name` của Azure OpenAI).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **file JSON**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/3537](https://n8n.io/workflows/3537) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste vào n8n Editor** (tab "Import").

:::note[Lưu ý khi import]
- **Không chỉnh sửa JSON** nếu chưa hiểu rõ logic, để tránh lỗi.
- **Kiểm tra các node quan trọng** sau khi import (xem phần dưới).
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

Workflow này **phức tạp** vì xử lý batch song song, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình Azure OpenAI**
- **Node `Create batch job`** (type: `httpRequest`):
  - **URL**: `https://<your-region>.openai.azure.com/openai/deployments/<deployment-name>/batch/jobs?api-version=<api-version>`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer <your-api-key>",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "requests": [/* Dữ liệu từ node trước */],
      "completionOptions": {
        "engine": "<engine-name>",
        "maxTokens": <max-tokens>,
        "temperature": <temperature>
      }
    }
    ```

- **Node `Track batch job progress`** (type: `httpRequest`):
  - **URL**: `https://<your-region>.openai.azure.com/openai/deployments/<deployment-name>/batch/jobs/<job-id>?api-version=<api-version>`
  - **Headers** giống như trên.

- **Node `Retrieve batch job output file`** (type: `httpRequest`):
  - **URL**: `https://<your-region>.openai.azure.com/openai/deployments/<deployment-name>/batch/jobs/<job-id>/output?api-version=<api-version>`
  - **Headers** giống như trên.

##### **B. Cấu hình dữ liệu đầu vào**
- **Node `Setup defaults`** (type: `set`):
  - Điền các tham số mặc định như:
    ```json
    {
      "api-version": "2023-07-01-preview",
      "deployment-name": "<your-deployment-name>",
      "engine": "gpt-4",
      "maxTokens": 500,
      "temperature": 0.7
    }
    ```
- **Node `Construct 'requests' array`** (type: `aggregate`):
  - Đảm bảo dữ liệu đầu vào là **mảng JSON** với cấu trúc:
    ```json
    [
      {"prompt": "Yêu cầu 1"},
      {"prompt": "Yêu cầu 2"},
      ...
    ]
    ```

##### **C. Cấu hình Memory (nếu sử dụng)**
- **Node `Simple Memory Store`** (type: `memoryBufferWindow`):
  - Cấu hình **số lượng prompt lưu trữ** (ví dụ: 10).
- **Node `Fill Chat Memory with example data`** (type: `memoryManager`):
  - Nếu cần, thêm dữ liệu mẫu vào bộ nhớ.

##### **D. Cấu hình File Upload (nếu cần)**
- **Node `Convert requests jsonl to File`** (type: `convertToFile`):
  - Chọn **mime type**: `application/x-ndjson`.
  - **File name**: `<custom-name>.jsonl`.

---

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Sử dụng node `Run example` (type: `manualTrigger`) để thử nghiệm.
   - Kiểm tra kết quả ở node `Parse response` (type: `code`).
2. **Bật Active workflow**:
   - Chuyển trạng thái từ **Draft** sang **Active**.
   - **Kích hoạt node `When Executed by Another Workflow`** (type: `executeWorkflowTrigger`) nếu muốn chạy tự động từ workflow khác.

---

### ✍️ **Mẹo & gợi ý nâng cao**

#### **1. Kết nối với Slack/Email để báo cáo kết quả**
- Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.email`** để gửi thông báo khi batch hoàn thành.
- Ví dụ:
  ```json
  {
    "text": "Batch job <job-id> đã hoàn thành! Kết quả: {{ $json["results"].length }} prompt."
  }
  ```

#### **2. Lưu log kết quả vào cơ sở dữ liệu**
- Sử dụng **node `n8n-nodes-base.database`** (MySQL, PostgreSQL) hoặc **Google Sheets** để lưu kết quả.
- Ví dụ:
  ```json
  {
    "sheetName": "AzureOpenAI_Results",
    "range": "A1:B100",
    "values": [
      ["Prompt", "Result"],
      ["{{ $node["Parse response"].json["prompt"] }}", "{{ $node["Parse response"].json["result"] }}"]
    ]
  }
  ```

#### **3. Tự động xóa dữ liệu cũ**
- Sử dụng **node `n8n-nodes-base.filter`** để loại bỏ kết quả cũ hơn 7 ngày.
- Ví dụ:
  ```javascript
  // Trong node Code (type: code)
  $node["Filter First Prompt Results"].json = $node["First Prompt Result"].json.filter(item => new Date(item.timestamp) > new Date(Date.now() - 7 * 24 * 60 * 60 * 1000));
  ```

#### **4. Sử dụng LangChain (nếu cần quản lý chat history)**
- Nếu workflow liên quan đến **chatbot**, các sếp có thể kết nối với **LangChain** để quản lý lịch sử hội thoại.
- Cấu hình node `n8n-nodes-langchain.memoryManager` để lưu trữ và truy xuất dữ liệu chat.

---

### 📌 **Kết luận**

Workflow **"Process Multiple Prompts in Parallel with Azure OpenAI Batch API"** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa xử lý batch prompt** một cách hiệu quả.
✔ **Giảm thời gian và chi phí** so với cách làm thủ công.
✔ **Không cần viết code** – chỉ cần cấu hình và chạy.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n self-hosted.
2. **Cấu hình Azure OpenAI** và dữ liệu đầu vào.
3. **Kích hoạt và chạy** để tiết kiệm thời gian và nâng cao hiệu suất AI của doanh nghiệp!

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký VPS n8n** để self-host: [TinoHost](https://tino.vn/vps-n8n?affid=388)
- **Hỏi đáp cộng đồng n8n**: [n8n Community](https://community.n8n.io/)
- **Liên hệ chuyên gia AI**: [Greg Evseev](https://www.linkedin.com/in/greg-evseev/) (tác giả workflow)