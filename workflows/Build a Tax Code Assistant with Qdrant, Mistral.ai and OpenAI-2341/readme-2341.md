---
title: "🤖 **Tự Động Hóa Trợ Lý Tư Vấn Mã Số Thuế AI với Qdrant, Mistral.ai & OpenAI (N8n) - Giúp Doanh Nghiệp Tiết Kiệm 1000+ Giây/Ngày**"
description: "Workflow này tự động hóa việc xây dựng một trợ lý AI thông minh trả lời câu hỏi về mã số thuế từ các tài liệu PDF chính thức, sử dụng Qdrant để lưu trữ vector, Mistral.ai và OpenAI để xử lý ngôn ngữ tự nhiên. Giúp các sếp tiết kiệm thời gian tra cứu thủ công, giảm sai sót và cung cấp câu trả lời chính xác 24/7."
slug: "tay-dong-hoa-tro-ly-tu-vien-ma-so-thue-ai"
tags: [n8n, automation, ai, qdrant, mistral-ai, openai, finance, no-code, vector-database, legal-assistant]
keywords: [n8n workflow mã số thuế, tự động hóa tra cứu thuế, trợ lý AI thuế, Qdrant với n8n, Mistral.ai n8n, OpenAI n8n, tự động hóa tài chính, giải pháp tra cứu PDF]
---

# 🚀 **Tự Động Hóa Trợ Lý Tư Vấn Mã Số Thuế AI với Qdrant, Mistral.ai & OpenAI**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Tra cứu mã số thuế, điều lệ thuế hoặc các quy định liên quan là một công việc **mệt mỏi, tốn thời gian và dễ sai sót** đối với các bộ phận tài chính, kế toán hoặc pháp lý. Thường thì các sếp phải:
- **Tìm kiếm thủ công** trên các tài liệu PDF lớn (thậm chí là hàng trăm trang).
- **Đọc lại nhiều lần** để xác minh thông tin, dẫn đến **sai sót cao** và **tốn thời gian**.
- **Không có khả năng tra cứu nhanh** khi khách hàng hoặc đồng nghiệp đặt câu hỏi đột xuất.

**Workflow này tự động hóa toàn bộ quá trình** bằng cách:
✅ **Tải và phân tích** tất cả các tài liệu PDF về mã số thuế từ nguồn chính thức.
✅ **Chia nhỏ và lưu trữ** thông tin theo **chương, mục, điều** vào **Qdrant Vector Database** (cơ sở dữ liệu vector tiên tiến).
✅ **Sử dụng AI (Mistral.ai + OpenAI)** để trả lời **câu hỏi về thuế một cách chính xác và nhanh chóng**.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên **VPS chuyên dụng** thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 1000+ giây/ngày** tra cứu thủ công (tương đương **10+ giờ/tháng**).
- **Trả lời chính xác 100%** nhờ AI phân tích từ nguồn dữ liệu chính thức.
- **Cá nhân hóa câu trả lời** theo yêu cầu cụ thể của khách hàng/đồng nghiệp.
- **Hoạt động liên tục 24/7** mà không cần can thiệp con người.
- **Giảm thiểu rủi ro sai sót** trong việc tra cứu mã số thuế.
- **Kết hợp với Slack/Telegram** để tra cứu ngay từ ứng dụng chat.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản API chính thức** từ:
   - **[Mistral Cloud](https://mistral.ai/)** (để tạo **embeddings** cho dữ liệu).
   - **[OpenAI](https://platform.openai.com/)** (để chạy **AI Chatbot** trả lời câu hỏi).
   - **[Qdrant](https://qdrant.tech/)** (để lưu trữ và tra cứu **vector embeddings**).
✔ **Tài liệu PDF về mã số thuế** (có thể tải từ **[Cổng Thông Tin Điện Tử Bộ Tài Chính](https://www.mof.gov.vn/)**).
✔ **N8n Self-hosted** (để chạy workflow 24/7).

---
:::info[CHUẨN BỊ]
**Các API Key cần thiết:**
| Dịch vụ          | Tham số cần thiết                          | Ví dụ (ẩn trong n8n)                     |
|------------------|--------------------------------------------|------------------------------------------|
| **Mistral Cloud** | `MistralCloudApi`                          | `sk-...` (API Key từ Mistral)            |
| **OpenAI**       | `openAiApi`                                | `sk-...` (API Key từ OpenAI)             |
| **Qdrant**       | `qdrantApi`                                | `Bearer sk-...` (API Key từ Qdrant)      |
| **N8n Credentials** | `n8n-api-key` (nếu self-host)          | (Tạo trong **Settings > Credentials**)   |
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này có **31 node** và được thiết kế để **tự động hóa toàn bộ quy trình** từ tải file PDF đến trả lời câu hỏi AI. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/2341](https://n8n.io/workflows/2341) và **import vào n8n Editor**.
- **Copy/paste JSON** từ file vào **n8n Editor** (đường dẫn: `https://<your-n8n-instance>/editor`).

:::note[Lưu ý khi import]
- **Không sao chép toàn bộ JSON** từ trang web n8n.io (do có vấn đề với ký tự đặc biệt).
- **Sử dụng tab "Import"** trong n8n Editor để tải file `.json` chính xác.
- **Kiểm tra lại credentials** sau khi import (n8n sẽ cảnh báo nếu thiếu).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và yêu cầu cấu hình **cẩn thận** ở các node quan trọng. Dưới đây là **các bước chỉnh sửa bắt buộc**:

##### **🔹 Node 1: "Get Tax Code Zip File" (HTTP Request)**
- **Tham số cần chỉnh:**
  - **Method:** `GET`
  - **URL:** Địa chỉ **file ZIP** chứa các tài liệu PDF về mã số thuế (ví dụ: từ [Cổng Thông Tin Điện Tử Bộ Tài Chính](https://www.mof.gov.vn/)).
  - **Headers:**
    ```json
    {
      "Accept": "application/zip"
    }
    ```
- **Lưu ý:**
  - Nếu không tìm được file ZIP, các sếp có thể **tải từ nguồn khác** (nhưng phải là **tài liệu chính thức**).

##### **🔹 Node 2: "Extract Zip Files" (Compression)**
- **Tham số mặc định:** Được cấu hình sẵn để **tự động giải nén** file ZIP thành các file PDF.
- **Lưu ý:**
  - Nếu file ZIP quá lớn, n8n có thể **bị timeout**. Các sếp nên **tải file nhỏ hơn** hoặc **chia nhỏ** (ví dụ: 1 file ZIP/mỗi năm).

##### **🔹 Node 3: "Extract PDF Contents" (Extract From File)**
- **Tham số cần chỉnh:**
  - **Operation:** `pdf`
  - **Key Parameters:**
    ```json
    {
      "operation": "pdf",
      "extractText": true,
      "extractImages": false
    }
    ```
- **Lưu ý:**
  - Nếu PDF có **bảng biểu hoặc hình ảnh**, các sếp có thể **bỏ qua** (`extractImages: false`).

##### **🔹 Node 4: "Qdrant Vector Store" (Vector Store Qdrant)**
- **Tham số cần chỉnh:**
  - **Collection Name:** `tax_codes` (hoặc tên tùy chỉnh).
  - **Qdrant API URL:** `https://<your-qdrant-instance>/collections/<collection-name>`
  - **Credentials:** Chọn `qdrantApi` (đã cấu hình trước).
  - **Metadata Fields:** Đảm bảo có **chương, mục, điều** để tra cứu chính xác.
- **Lưu ý:**
  - Nếu **Qdrant chưa có collection**, workflow sẽ **tự tạo**.
  - **Throttling:** Do Mistral.ai có **gi hạn rate**, các sếp nên **chia nhỏ batch** (node `splitInBatches`).

##### **🔹 Node 5: "OpenAI Chat Model" (LM Chat OpenAI)**
- **Tham số cần chỉnh:**
  - **Model:** `gpt-4` hoặc `gpt-3.5-turbo` (tùy budget).
  - **API Key:** Chọn `openAiApi`.
  - **Prompt Template:** Được cấu hình sẵn để **trả lời câu hỏi về thuế** một cách **chính xác và ngắn gọn**.
- **Lưu ý:**
  - **Kiểm tra lại budget** để tránh **quá tải tài khoản OpenAI**.

##### **🔹 Node 6: "AI Agent" (Agent)**
- **Tham số cần chỉnh:**
  - **Tools:**
    - **Ask Tool:** Sử dụng **Mistral embeddings + Qdrant Search API**.
    - **Search Tool:** Sử dụng **Qdrant Scroll API** để lấy **chương mục cụ thể**.
  - **Memory Buffer:** Được cấu hình để **nhớ lịch sử trò chuyện** (node `memoryBufferWindow`).
- **Lưu ý:**
  - **Test lại với câu hỏi đơn giản** trước khi sử dụng với khách hàng.

---

#### **3. Kích Hoạt ⚡️ Workflow**
Sau khi cấu hình xong:
1. **Test Run** với **dữ liệu mẫu** (ví dụ: "Mã số thuế đối với doanh nghiệp nhỏ năm 2024 là gì?").
2. **Bật Active** workflow.
3. **Kết nối với Slack/Telegram** (nếu muốn tra cứu từ ứng dụng chat).

---
:::tip[Mẹo Test Trước Khi Sử Dụng]
- **Dùng câu hỏi đơn giản** như:
  - "Mã số thuế đối với doanh nghiệp nhỏ là bao nhiêu?"
  - "Tôi phải nộp thuế giá trị gia tăng (VAT) với mức nào?"
- **Kiểm tra kết quả** có **đúng với tài liệu chính thức** không.
- **Log lại lỗi** nếu AI trả lời sai (có thể do **dữ liệu không đầy đủ**).
:::

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**
   - Sử dụng **node `webhook`** để nhận câu hỏi từ Slack/Telegram và trả lời tự động.
   - **Cài đặt bot Slack/Telegram** và **đăng ký webhook**.

2. **Lưu Log Tra Cứu**
   - Sử dụng **node `set` + `executeWorkflowTrigger`** để **ghi lại lịch sử tra cứu**.
   - **Export log** thành Excel/CSV để **theo dõi hoạt động**.

3. **Cập Nhật Dữ liệu Thường Xuyên**
   - **Chạy workflow định kỳ** (ví dụ: **mỗi tháng**) để **cập nhật mã số thuế mới nhất**.
   - Sử dụng **node `executeWorkflowTrigger`** để **kích hoạt tự động**.

4. **Tối Ưu Hóa Prompt AI**
   - **Cải thiện prompt** trong node `lmChatOpenAi` để **trả lời ngắn gọn hơn**.
   - Ví dụ:
     ```json
     {
       "system": "Bạn là trợ lý tư vấn thuế chuyên nghiệp. Trả lời ngắn gọn, chính xác và dựa trên tài liệu chính thức. Nếu không biết, hãy nói 'Tôi không có thông tin về điều này.'"
     }
     ```

5. **Chia Sẻ Trợ Lý AI Cho Đội Ngũ**
   - **Tạo một link truy cập** (n8n có tính năng **Public URL**).
   - **Cung cấp cho đồng nghiệp** để **tra cứu nhanh chóng**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **tra cứu thủ công mã số thuế**, đồng thời **giảm thiểu sai sót** nhờ AI. Với **Qdrant + Mistral.ai + OpenAI**, trợ lý AI này **hiểu và trả lời câu hỏi một cách chính xác**, giống như một **người tư vấn thuế 24/7**.

**🚀 Hành động ngay:**
1. **Self-host n8n** trên VPS (để **chạy 24/7**).
2. **Import workflow** và **cấu hình API**.
3. **Test với câu hỏi mẫu** và **bật hoạt động**.
4. **Kết nối với Slack/Telegram** để **tra cứu từ mọi nơi**.

**💬 Cần hỗ trợ?**
- **Đăng ký VPS** với mã giảm giá: **[VPSN8N](https://tino.vn/vps-n8n?affid=388)**
- **Hỏi đáp trên Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Góp ý cải tiến**: [https://community.n8n.io/](https://community.n8n.io/)

**Happy Automating!** 🤖✨