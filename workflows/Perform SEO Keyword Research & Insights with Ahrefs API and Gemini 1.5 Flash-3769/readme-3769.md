---
title: "🔍 **Tự Động Hóa Nghiên Cứu Từ Khóa SEO Với Ahrefs API + Gemini 1.5 Flash (Không Cần Code!)**"
description: "Workflow này tự động phân tích từ khóa SEO từ Ahrefs API, xử lý dữ liệu bằng Gemini 1.5 Flash và trả về báo cáo chi tiết, giúp các sếp tiết kiệm thời gian lên đến 80% so với cách làm thủ công. Hỗ trợ cá nhân hóa, chính xác và hoạt động 24/7."
slug: "tieu-dong-hoa-nghien-cuu-tu-khoa-seo-ahrefs-gemini"
tags: [n8n, automation, SEO, Ahrefs API, Gemini AI, AI Agent, no-code]
keywords: [n8n workflow SEO, tự động hóa nghiên cứu từ khóa, Ahrefs API + Gemini, tự động hóa marketing, AI Agent cho SEO]
---

# 🚀 **Tự Động Hóa Nghiên Cứu Từ Khóa SEO Với Ahrefs API + Gemini 1.5 Flash**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 80% thời gian** so với cách phân tích từ khóa thủ công.
- **Nhận báo cáo SEO chi tiết** từ Ahrefs API, được tổng hợp và cá nhân hóa bởi Gemini 1.5 Flash.
- **Hoạt động liên tục** mà không cần can thiệp của con người.
- **Xử lý lỗi chính tả tự động** và tối ưu hóa từ khóa trước khi gửi yêu cầu API.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Xử lý hàng trăm từ khóa trong vài giây thay vì vài giờ.
✅ **Dữ liệu chính xác**: Gemini 1.5 Flash tự động sửa lỗi chính tả và lọc từ khóa phù hợp.
✅ **Báo cáo cá nhân hóa**: Nhận kết quả tổng hợp từ Ahrefs API với định dạng linh hoạt.
✅ **Hoạt động tự động**: Khởi động workflow qua Telegram, WhatsApp, hoặc Webhook mà không cần can thiệp.
✅ **Tối ưu chi phí**: Tránh trả phí API cho các yêu cầu không cần thiết.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Ahrefs API**:
   - API Key từ [Ahrefs API](https://ahrefs.com/api) (đăng ký tại đây).
   - Đăng ký tại [RapidAPI](https://rapidapi.com/environmentn1t21r5/api/ahrefs-keyword-tool) để lấy endpoint và API Key.
2. **Google Cloud API Key**:
   - API Key cho **Gemini 1.5 Flash** từ [Google AI Studio](https://aistudio.google.com/).
3. **Credentials trong n8n**:
   - Thêm **Google Palm API** (credentials name: `googlePalmApi`) trong n8n với API Key Gemini.
   - Thêm **Ahrefs API Key** trong node `Ahrefs Keyword API Request` (điền vào `x-rapidapi-key` và `x-rapidapi-host`).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3769](https://n8n.io/workflows/3769) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
- **Không quên chọn workspace** để lưu workflow.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Trigger Node (Bắt đầu workflow)**
- Node: **"When chat message received"** (type: `chatTrigger`).
- **Lưu ý**:
  - Đây là **mẫu trigger** (sample). Các sếp có thể thay thế bằng:
    - **Webhook** (nếu muốn gọi từ bên ngoài).
    - **Telegram/Slack/Email** (thêm node `n8n-nodes-base.telegram` hoặc `n8n-nodes-base.email`).
  - **Cấu hình**:
    - Điền **tên chatbot** (ví dụ: `@SEO_Bot`).
    - **Tham số bắt buộc**: `keyword_query` (ví dụ: `tự động hóa n8n`).

#### **B. Cấu hình Ahrefs API Request**
- Node: **"Ahrefs Keyword API Request"** (type: `httpRequest`).
- **Lưu ý**:
  - **Endpoint**: `https://ahrefs-keyword-tool.p.rapidapi.com/api/keyword-overview` (hoặc `answer-the-public` nếu muốn từ khóa liên quan).
  - **Headers**:
    - `x-rapidapi-key`: API Key từ RapidAPI.
    - `x-rapidapi-host`: `ahrefs-keyword-tool.p.rapidapi.com`.
  - **Body**:
    ```json
    {
      "keyword": "{{ $node["Keyword Query Extraction & Cleaning Agent"].json["keyword"] }}"
    }
    ```
  - **Lưu ý quan trọng**:
    - Nếu API trả về lỗi, kiểm tra **keyword input** từ node `Keyword Query Extraction & Cleaning Agent`.

#### **C. Cấu hình Gemini 1.5 Flash**
- Node: **"Google Gemini Chat Model"** và **"Google Gemini Chat Model1"** (type: `lmChatGoogleGemini`).
- **Lưu ý**:
  - **Credentials**: Chọn `googlePalmApi` (đã thêm trước đó).
  - **System Prompt** (cần chỉnh sửa để phù hợp):
    ```plaintext
    You are an SEO expert assistant. Your task is to:
    1. Extract the main keyword from the Ahrefs API response.
    2. Summarize the keyword insights in a professional format.
    3. Suggest 10 related keywords with their search volume and difficulty.
    ```
  - **Input Variables**:
    - Đối với node `Keyword Query Extraction & Cleaning Agent`:
      ```json
      {
        "keyword": "{{ $node["When chat message received"].json["keyword_query"] }}"
      }
      ```
    - Đối với node `Keyword Data Response Formatter`:
      ```json
      {
        "api_response": "{{ $node["Ahrefs Keyword API Request"].json }}",
        "keyword": "{{ $node["Keyword Query Extraction & Cleaning Agent"].json["keyword"] }}"
      }
      ```

#### **D. Cấu hình Agent (AI Logic)**
- Node: **"Keyword Query Extraction & Cleaning Agent"** (type: `agent`).
  - **Lưu ý**:
    - **System Prompt**:
      ```plaintext
      You are a keyword cleaner. Your task is to:
      1. Take the input keyword and correct any spelling mistakes.
      2. Return ONLY the cleaned keyword in JSON format:
      {
        "keyword": "cleaned_keyword"
      }
      ```
    - **Input**: `{{ $node["When chat message received"].json["keyword_query"] }}`

- Node: **"Keyword Data Response Formatter"** (type: `agent`).
  - **Lưu ý**:
    - **System Prompt**:
      ```plaintext
      You are an SEO report generator. Take the Ahrefs API response and format it into a clear summary:
      - Main keyword: [Keyword]
      - Search volume: [Number]
      - Keyword difficulty: [Number]
      - Top 10 related keywords with their metrics.
      ```
    - **Input**: `{{ $node["Ahrefs Keyword API Request"].json }}`

#### **E. Cấu hình Code Node (Extract Data)**
- Node: **"Extract Main Keyword & 10 related Keyword data"** (type: `code`).
  - **Lưu ý**:
    - **JavaScript Function** (cần chỉnh sửa nếu muốn lấy dữ liệu khác):
      ```javascript
      return {
        json: {
          main_keyword: $input.all()[0].json.keyword,
          related_keywords: $input.all()[0].json.related_keywords.slice(0, 10)
        }
      };
      ```
    - **Output**: Dữ liệu được gửi đến node `Aggregate Keyword Data`.

#### **F. Cấu hình Memory Buffer (Lưu trữ dữ liệu)**
- Node: **"Simple Memory"** (type: `memoryBufferWindow`).
  - **Lưu ý**:
    - **Thời gian lưu trữ**: Đặt thành `1h` (hoặc tùy chỉnh theo nhu cầu).
    - **Key**: `keyword_data` (để lưu trữ kết quả cho các workflow tương lai).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một **keyword mẫu** (ví dụ: `tự động hóa n8n`) qua trigger (Telegram/Slack/Webhook).
   - Kiểm tra **output** của mỗi node để đảm bảo dữ liệu truyền đúng.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Lưu ý**: Nếu workflow bị lỗi, kiểm tra **logs** trong tab `Execution`.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để nhận báo cáo tự động.
   - **Ví dụ**:
     ```json
     {
       "text": "🔍 **SEO Report for '{{ $node["Keyword Data Response Formatter"].json.keyword }}'**:\n\n{{ $node["Keyword Data Response Formatter"].json.summary }}"
     }
     ```

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.notion` để lưu lịch sử nghiên cứu từ khóa.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần/monthly và gửi báo cáo qua Email/Slack.

4. **Tối ưu hóa API Call**:
   - Nếu workflow bị rate limit, thêm node `n8n-nodes-base.delay` để chờ 5 giây trước khi gọi API.

5. **Cải thiện System Prompt của Gemini**:
   - Nếu kết quả không phù hợp, chỉnh sửa **system prompt** trong node `lmChatGoogleGemini` đểGemini trả về định dạng mong muốn.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa nghiên cứu từ khóa SEO mà không cần viết code. Với sự kết hợp giữa **Ahrefs API** (dữ liệu chính xác) và **Gemini 1.5 Flash** (xử lý logic AI), các sếp sẽ tiết kiệm thời gian, giảm thiểu lỗi và nhận được báo cáo cá nhân hóa.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với keyword mẫu** để đảm bảo hoạt động.
3. **Kết nối với Slack/Telegram** để nhận báo cáo tự động.

**Cần hỗ trợ?** Liên hệ với tác giả Joseph tại [joseph@uppfy.com](mailto:joseph@uppfy.com) để được tư vấn chi tiết!

---
**Chúc các sếp thành công với chiến dịch SEO của mình!** 🚀