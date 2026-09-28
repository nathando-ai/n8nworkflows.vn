---
title: "🤖 **Tự Động Trích Xuất & Phân Tích Trang Web Bằng AI Gemini + Apify (Không Cần Code!)**"
description: "Workflow tự động hóa hoàn toàn bằng n8n giúp các sếp **trích xuất dữ liệu từ website**, **phân tích nội dung theo yêu cầu cá nhân hóa** bằng AI Gemini (Google), và **tích hợp với LangChain** để tối ưu hóa quy trình. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công!"
slug: "tieu-dung-trich-xuat-phan-tich-website-ai-gemini-apify"
tags: [n8n, automation, no-code, ai-rag, gemini, apify, langchain, web-scraping]
keywords: [n8n workflow tự động hóa, trích xuất dữ liệu website, AI Gemini phân tích trang web, Apify + LangChain, tự động hóa không code, giải pháp RAG cho doanh nghiệp]
---

# 🚀 **Tự Động Trích Xuất & Phân Tích Trang Web Bằng AI Gemini + Apify (Không Cần Code!)**

Hiện nay, việc **trích xuất dữ liệu từ website** như thông tin liên hệ, danh sách sản phẩm, tin tức mới nhất hay phân tích nội dung một cách thủ công không chỉ tốn thời gian mà còn dễ xảy ra lỗi. Các sếp thường phải **quét từng trang, sao chép dữ liệu, và phân tích bằng tay**—quá trình này không chỉ mất nhiều giờ mà còn **không đảm bảo độ chính xác** khi có nhiều trang hoặc nội dung động.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động trích xuất nội dung** từ website theo yêu cầu (số lượng trang tùy chọn).
✅ **Phân tích AI thông minh** bằng **Gemini 2.5 (Google)** để trả về kết quả **cá nhân hóa** theo prompt của bạn.
✅ **Tích hợp Apify** để lấy dữ liệu **sạch và có cấu trúc** (Markdown).
✅ **Áp dụng LangChain** để quản lý quy trình AI một cách logic và hiệu quả.
✅ **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào máy tính cá nhân.

---
## 🎯 **Kết quả các sếp nhận được**

:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Độ chính xác cao** nhờ AI phân tích tự động (không bị lỗi copy-paste).
- **Cá nhân hóa kết quả** theo yêu cầu cụ thể (ví dụ: "trích xuất tất cả email liên hệ", "tóm tắt nội dung", "lấy danh sách sản phẩm").
- **Hoạt động liên tục** trên VPS, không cần phải mở máy tính.
- **Dữ liệu sạch và có cấu trúc** (JSON/Markdown), dễ dàng tích hợp vào CRM, ERP hoặc hệ thống nội bộ.
- **Mở rộng ứng dụng** cho nhiều trường hợp: từ **tìm kiếm thông tin tuyển dụng** đến **phân tích đối thủ cạnh tranh**.
:::

---
## 🔧 **Yêu cầu cần thiết**

Trước khi **lên đồ** workflow này, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (đăng ký miễn phí tại [apify.com](https://apify.com)) và **API Token**.
   - Hướng dẫn lấy token: [Apify Docs - API Token](https://docs.apify.com/api/token/)
2. **API Key OpenRouter** (đăng ký tại [openrouter.ai](https://openrouter.ai)) để sử dụng **Gemini 2.5** và **Gemini Pro Preview**.
   - **Mã giảm giá 10% cho API Key OpenRouter** (đăng ký qua [đây](https://openrouter.ai/signup?ref=VPSN8N) với mã **VPSN8N**).
3. **N8n Self-hosted** (cài trên VPS để workflow hoạt động 24/7).
   - 👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **JSON**, các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/6754](https://n8n.io/workflows/6754) và import vào **n8n Editor**.
- **Copy/paste JSON** từ link trên vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không chỉnh sửa JSON trực tiếp** trên canvas n8n (có thể làm hỏng workflow).
- **Sử dụng phiên bản n8n mới nhất** (cần cài đặt **nodes LangChain** và **OpenRouter**).
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **🔹 Node 1: "When Executed by Another Workflow"**
- **Không cần cấu hình gì**, chỉ dùng để **trigger** workflow từ bên ngoài.

#### **🔹 Node 2: "HTTP Request" (Gửi yêu cầu đến Apify)**
- **Method:** `POST`
- **URL:** `https://api.apify.com/v2/actors/mohamedgb00714/firescraper-ai-website-content-markdown-scraper/runs`
- **Headers:**
  ```
  Authorization: Bearer <API_TOKEN_APIFY>
  Content-Type: application/json
  ```
- **Body (JSON):**
  ```json
  {
    "input": {
      "enqueue": true,
      "maxPages": 5,
      "url": "https://apify.com",
      "method": "GET",
      "prompt": "collect all contact informations available on this website"
    }
  }
  ```
  - **Thay đổi:**
    - `url`: Địa chỉ website cần trích xuất.
    - `maxPages`: Số lượng trang tối đa (ví dụ: 5, 10, 20).
    - `prompt`: Yêu cầu AI phân tích (ví dụ: "tóm tắt nội dung", "trích xuất tất cả email", "lấy danh sách sản phẩm").

#### **🔹 Node 3: "Loop Over Items" (SplitInBatches)**
- **Chọn `jsonpath: $`** để xử lý tất cả dữ liệu từ Apify.
- **Batch Size:** Đặt thành **1** (mỗi trang được xử lý riêng).

#### **🔹 Node 4 & 5: "AI Agent" + "OpenRouter Chat Model" (Gemini 2.5 Flash)**
- **Credentials:** Chọn `openRouterApi` (đã cấu hình trước).
- **Model:** `google/gemini-2.5-flash` (mô hình nhanh, phù hợp cho phân tích cơ bản).
- **Prompt Template:**
  ```plaintext
  Analyze the following webpage content and answer the question: "{prompt}".
  Content: {content}
  ```
  - `{prompt}`: Được truyền từ input (ví dụ: "trích xuất tất cả email").
  - `{content}`: Nội dung từ trang web (do Apify trích xuất).

#### **🔹 Node 6 & 7: "AI Agent1" + "OpenRouter Chat Model1" (Gemini Pro Preview)**
- **Credentials:** Chọn `openRouterApi`.
- **Model:** `google/gemini-2.5-pro-preview` (mô hình cao cấp, phù hợp cho phân tích chi tiết).
- **Prompt Template:**
  ```plaintext
  Based on the aggregated results from previous pages, provide a structured summary or answer: "{prompt}".
  Previous results: {json}
  ```
  - **Sử dụng để tổng hợp kết quả** từ tất cả trang.

#### **🔹 Node 8: "Aggregate"**
- **JSONPath:** `$.json`
- **Function:** `JSON.stringify($item)`
- **Kết quả:** Tạo một JSON duy nhất từ tất cả kết quả phân tích.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu (ví dụ: URL `https://apify.com` và prompt `"trích xuất tất cả thông tin liên hệ"`).
2. **Bật Active** workflow.
3. **Gọi từ bên ngoài** bằng cách gửi JSON đến node `HTTP Request` (ví dụ: từ một workflow khác hoặc API).

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 1. Tích hợp với Slack/Telegram để báo cáo kết quả**
- Sử dụng **node Slack Webhook** hoặc **Telegram Bot** để gửi kết quả tự động khi workflow hoàn thành.
- **Cách làm:**
  - Thêm node `Set` sau `Aggregate` để lưu kết quả vào biến `$json`.
  - Thêm node `Slack` hoặc `Telegram` với payload:
    ```json
    {
      "text": "Kết quả phân tích trang web đã hoàn thành!",
      "attachments": [{"text": $json}]
    }
    ```

### **🔹 2. Lưu log vào Google Sheets/Notion**
- Sử dụng **node Google Sheets** hoặc **Notion** để ghi lại lịch sử phân tích.
- **Cách làm:**
  - Thêm node `Set` sau `Aggregate` để định dạng JSON.
  - Thêm node `Google Sheets` với sheet name `"Website Analysis Log"` và payload:
    ```json
    {
      "url": $url,
      "prompt": $prompt,
      "result": $json,
      "timestamp": $now
    }
    ```

### **🔹 3. Tự động chạy định kỳ (ví dụ: mỗi ngày)**
- Sử dụng **node `executeWorkflowTrigger`** để gọi workflow từ một **cron job** trên VPS.
- **Cách làm:**
  - Cài đặt **cron** trên VPS:
    ```bash
    0 9 * * * curl -X POST http://<IP_VPS>:5678/webhook/your-workflow-id
    ```
  - Thay `<IP_VPS>` bằng IP của VPS và `your-workflow-id` bằng ID của workflow.

### **🔹 4. Kết hợp với AI Agent khác (MCP)**
- Sử dụng kết quả này như **input cho AI Agent khác** (ví dụ: tự động gửi email, tạo báo cáo Word).
- **Cách làm:**
  - Lưu kết quả vào **Google Drive** hoặc **Notion**.
  - Sử dụng **node `executeWorkflowTrigger`** để gọi workflow mới xử lý dữ liệu.

---
## 📌 **Kết luận**

Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa trích xuất và phân tích website** một cách **không cần code**, với **độ chính xác cao** nhờ AI Gemini và **tích hợp Apify** để lấy dữ liệu sạch.

**🚀 Hành động ngay:**
1. **Đăng ký VPS** để chạy workflow 24/7: [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**).
2. **Import workflow** và **cấu hình API Key** (Apify + OpenRouter).
3. **Test với URL đầu tiên** và **tích hợp vào quy trình làm việc** của doanh nghiệp!

**💡 Nếu có nhu cầu tùy chỉnh workflow này cho mục đích cụ thể (ví dụ: trích xuất dữ liệu từ website đối thủ), hãy liên hệ với tác giả [Mohamed El Hadi](https://n8n.io/workflows/6754) để hợp tác!**

---
**🔥 Bạn đã sẵn sàng tự động hóa quy trình của mình chưa?** 🚀