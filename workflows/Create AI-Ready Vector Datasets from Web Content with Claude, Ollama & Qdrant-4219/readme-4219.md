---
title: "🚀 Tự Động Tạo Dataset Vector Sẵn Sàng AI Từ Nội Dung Web Với Claude, Ollama & Qdrant"
description: "Workflow tự động hóa hoàn toàn không cần code để trích xuất, vector hóa và lưu trữ dữ liệu từ trang web thành dataset sẵn sàng cho AI, giúp các sếp tiết kiệm thời gian và nâng cao hiệu suất phân tích dữ liệu. Kết hợp Claude 3.7 Sonnet, Ollama và Qdrant để tạo cơ sở dữ liệu vector chuyên nghiệp."
slug: "tay-dong-tao-dataset-vector-ai-claude-ollama-qdrant"
tags: [n8n, automation, ai, vector-database, ollama, qdrant, claud-ai, no-code, web-scraping]
keywords: [tự động hóa n8n, dataset vector cho ai, ollama embeddings, qdrant vector store, claud ai agent, trích xuất dữ liệu web, tự động hóa không code]
---

# 🚀 **Tự Động Tạo Dataset Vector Sẵn Sàng AI Từ Nội Dung Web Với Claude, Ollama & Qdrant**

## **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Hiện nay, việc **trích xuất, xử lý và chuyển đổi nội dung web thành dataset vector** để sử dụng cho mô hình AI là một quá trình **tốn thời gian, phức tạp và dễ sai sót** khi làm thủ công. Các sếp thường phải:
- **Làm thủ công** trích xuất dữ liệu từ nhiều trang web khác nhau.
- **Chỉnh sửa và định dạng** dữ liệu thành JSON hoặc CSV phù hợp với mô hình AI.
- **Vector hóa** dữ liệu bằng cách gọi API Ollama, sau đó lưu trữ vào Qdrant.
- **Quản lý cơ sở dữ liệu vector** một cách thủ công, dễ dẫn đến lỗi hoặc mất mát dữ liệu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình, từ trích xuất nội dung web đến lưu trữ dataset vector sẵn sàng cho AI!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
✅ **Chính xác 100%** với việc trích xuất và vector hóa tự động.
✅ **Dataset sẵn sàng AI** với cấu trúc JSON chuẩn, embeddings Ollama và lưu trữ Qdrant.
✅ **Hoạt động liên tục 24/7** khi chạy trên VPS tự host.
✅ **Kết nối Discord/Slack** để nhận báo cáo và kết quả AI ngay lập tức.
✅ **Cơ sở dữ liệu vector chuyên nghiệp** với cosine similarity và metadata đầy đủ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản Scrapeless** (để trích xuất nội dung web):
   - Đăng ký tại [https://app.scrapeless.com](https://app.scrapeless.com) và cấu hình **Web Unlocker** cho trang web mục tiêu.
   - **Lưu ý**: Cần có **API Key** của Scrapeless để gọi API trích xuất.

✔ **API Key của Claude AI** (để trích xuất và định dạng dữ liệu):
   - Đăng ký tại [https://console.anthropic.com](https://console.anthropic.com) và lấy **x-api-key**.
   - **Model sử dụng**: `claude-3-7-sonnet-20250219` (đã được cấu hình sẵn trong workflow).

✔ **Ollama** (để tạo embeddings vector):
   - Cài đặt Ollama trên máy chủ hoặc VPS:
     ```bash
     curl -fsSL https://ollama.ai/install.sh | sh
     ```
   - Tải model **All-MiniLM-L6-v2** (hoặc model khác phù hợp):
     ```bash
     ollama pull all-minilm-l6-v2
     ```

✔ **Qdrant** (để lưu trữ vector database):
   - Cài đặt Qdrant bằng Docker:
     ```bash
     docker run -p 6333:6333 -p 6334:6334 qdrant/qdrant
     ```
   - **Lưu ý**: Workflow sẽ tự động tạo **collection** nếu chưa tồn tại.

✔ **Webhook cho Discord/Slack** (tùy chọn):
   - Cấu hình webhook tại Discord/Slack để nhận kết quả AI và báo cáo.
   - **Lưu ý**: Workflow đã hỗ trợ định dạng JSON cho cả hai nền tảng.

✔ **VPS Tự Host** (khuyến nghị):
   - Để workflow chạy **liên tục 24/7**, các sếp nên cài n8n trên VPS.
   - 👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/4219) (hoặc copy từ canvas).
- Mở **n8n Editor** → **Import Workflow** → Dán JSON hoặc tải file.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **14 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

#### **🔹 Node "Scrapeless Web Request" (HTTP Request)**
- **Cấu hình**:
  - **URL**: Điền URL của trang web cần trích xuất (ví dụ: `https://example.com`).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_SCRAPELESS_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "url": "https://example.com",
      "selectors": ["body"] // Chọn phần tử HTML cần trích xuất
    }
    ```
- **Lưu ý**: Cần **cấu hình trước tại Scrapeless** để tránh lỗi 403.

#### **🔹 Node "Claude Data Extractor" (Code)**
- **Cấu hình**:
  - **Headers** phải bao gồm:
    ```json
    {
      "anthropic-version": "2023-10-01",
      "x-api-key": "YOUR_CLAUDE_API_KEY",
      "content-type": "application/json"
    }
    ```
  - **Prompt** đã được tối ưu cho việc trích xuất và định dạng JSON:
    ```json
    {
      "prompt": "Extract structured data from the following HTML content and return as JSON. Use claude-3-7-sonnet-20250219 model.",
      "max_tokens": 4096
    }
    ```

#### **🔹 Node "Ollama Embeddings" (Code)**
- **Cấu hình**:
  - **API Call** đến Ollama:
    ```bash
    curl http://localhost:11434/api/embeddings -d '{"model": "all-minilm-l6-v2", "input": "YOUR_TEXT"}'
    ```
  - **Lưu ý**: Chạy Ollama trên cùng một máy chủ với n8n để tránh lỗi kết nối.

#### **🔹 Node "Qdrant Vector Store" (Code)**
- **Cấu hình**:
  - **URL Qdrant**: `http://localhost:6333` (nếu chạy Docker trên cùng máy).
  - **Collection Name**: Workflow sẽ tự động tạo nếu chưa tồn tại.
  - **Payload**:
    ```json
    {
      "vectors": [embeddings_array],
      "payload": {
        "id": "numeric_id",
        "metadata": { "source": "web_content" }
      }
    }
    ```

#### **🔹 Node "Webhook for Discord/Slack" (Code)**
- **Cấu hình**:
  - **URL Webhook**: Điền URL webhook từ Discord/Slack.
  - **Payload**:
    ```json
    {
      "content": "AI Response: {response}",
      "embeds": [{
        "title": "Dataset Vector Ready",
        "description": "Dataset đã được vector hóa và lưu trữ thành công!"
      }]
    }
    ```

#### **🔹 Node "Check Collection Exists" (HTTP Request)**
- **Cấu hình**:
  - **URL**: `http://localhost:6333/collections/{collection_name}/points/count`
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json"
    }
    ```
  - **Lưu ý**: Nếu collection không tồn tại, workflow sẽ tự động tạo.

---

### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **"Test Workflow"** để chạy với dữ liệu mẫu.
  - Kiểm tra **log** và **webhook** để xác nhận kết quả.
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
✅ **Kết hợp với Slack/Telegram**:
   - Thay vì Discord, các sếp có thể cấu hình webhook cho **Slack** hoặc **Telegram Bot** để nhận báo cáo.

✅ **Lưu Log Dữ Liệu**:
   - Sử dụng **Google Sheets** hoặc **Airtable** để lưu trữ lịch sử trích xuất và vector hóa.

✅ **Tự Động Chạy Hàng Ngày**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow định kỳ (ví dụ: mỗi ngày 8h sáng).

✅ **Tối Ưu Hóa Ollama**:
   - Nếu có nhiều dữ liệu, các sếp có thể **cache embeddings** để tránh gọi API liên tục.

✅ **Sử Dụng Multiple Collections**:
   - Workflow hỗ trợ **tạo nhiều collection** trong Qdrant, phù hợp cho nhiều dự án khác nhau.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa trích xuất, vector hóa và lưu trữ dữ liệu web** một cách **không cần code**, với kết quả **chính xác, chuyên nghiệp và sẵn sàng sử dụng cho AI**.

**Hãy áp dụng ngay và tiết kiệm thời gian cho việc phân tích dữ liệu!** 🚀

---
**🔹 Cần hỗ trợ thêm?**
- **Join Cộng Đồng n8n Việt Nam**: [Facebook Group](https://www.facebook.com/groups/n8nvietnam/)
- **Hỗ Trợ Tech**: [n8n.io/support](https://n8n.io/support)