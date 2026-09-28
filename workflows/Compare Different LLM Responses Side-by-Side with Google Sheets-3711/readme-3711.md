---
title: "🤖 So Sánh Trực Quan Hiệu Suất Các Mô Hình LLM Bằng Google Sheets - Tự Động Hóa 100% Không Code"
description: "Workflow này giúp các sếp so sánh hiệu suất, tính nhất quán và chất lượng phản hồi của 2+ mô hình LLM (như GPT-4 vs Mistral) một cách trực quan qua giao diện chat và bảng Google Sheets. Giúp lựa chọn mô hình phù hợp cho dự án AI mà không cần viết code."
slug: "so-sanh-llm-bang-google-sheets"
tags: [n8n, automation, ai, google-sheets, openrouter, langchain, no-code]
keywords: [n8n workflow so sánh LLM, tự động hóa so sánh mô hình AI, chatbot so sánh GPT-4 vs Mistral, Google Sheets AI evaluation, OpenRouter n8n]
---

# 🚀 So Sánh Trực Quan Hiệu Suất Các Mô Hình LLM Bằng Google Sheets

## 🔍 **Nỗi Đau Của Các Sếp Khi Lựa Chọn Mô Hình AI**
Mỗi khi phát triển một AI agent hoặc chatbot, các sếp phải đối mặt với quyết định khó khăn: **"Lựa chọn mô hình LLM nào hiệu quả nhất cho dự án?"**
- **Không có cách so sánh trực quan**: Phải chạy từng mô hình riêng rẽ, ghi chép phản hồi vào file Excel, mất thời gian và dễ sai sót.
- **Không nhất quán**: Các mô hình LLM không phải lúc nào cũng trả lời giống nhau với cùng một input (non-deterministic).
- **Không có dữ liệu lịch sử**: Không biết mô hình nào tốt hơn trong trường hợp cụ thể của doanh nghiệp.
- **Chi phí không rõ ràng**: Không biết mô hình nào tiết kiệm token hơn mà vẫn đảm bảo chất lượng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **So sánh phản hồi của 2+ mô hình LLM cùng một lúc** trong giao diện chat.
✅ **Lưu tất cả dữ liệu vào Google Sheets** để đánh giá sau này (thậm chí tự động hóa bằng AI).
✅ **Hiển thị kết quả trực quan** để các sếp và team không kỹ thuật cũng dễ so sánh.
✅ **Tiết kiệm thời gian và chi phí** bằng cách loại bỏ mô hình kém hiệu quả sớm.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Lựa chọn mô hình AI chính xác hơn** dựa trên dữ liệu thực tế chứ không phải dựa vào cảm nhận.
- **Tiết kiệm chi phí token** bằng cách loại bỏ mô hình không hiệu quả.
- **Dữ liệu đánh giá lâu dài** để cải thiện chất lượng chatbot theo thời gian.
- **Giao diện chat trực quan** cho phép so sánh phản hồi của 2 mô hình ngay lập tức.
- **Không cần viết code** – chỉ cần cài đặt và chạy.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để kết nối với Google Sheets và OpenRouter).
2. **API Key OpenRouter** (hoặc Vertex AI nếu muốn thay thế).
   - Đăng ký tại: [https://openrouter.ai/](https://openrouter.ai/)
3. **Google Sheet mẫu** (sẽ được hướng dẫn copy).
4. **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo ổn định 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**Các node quan trọng cần cấu hình:**
| Node | Loại | Yêu cầu |
|------|------|----------|
| **OpenRouter Chat Model** | `lmChatOpenRouter` | API Key OpenRouter, danh sách mô hình muốn so sánh (ví dụ: `["openai/gpt-4.1", "mistralai/mistral-large"]`) |
| **Google Sheets** | `googleSheets` | Credentials Google API, Sheet ID từ file mẫu |
| **AI Agent** | `agent` | Cần thiết lập **System Prompt** và **Tools** phù hợp với use case |
| **Chat Memory Manager** | `memoryManager` | Để lưu trữ lịch sử chat cho mỗi mô hình |

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/3711).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** (Ctrl+Shift+I).

#### 2. **Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Node "Define Models to Compare"**
- Node này định nghĩa danh sách mô hình muốn so sánh.
- **Cách chỉnh:**
  ```json
  {
    "json": {
      "models": ["openai/gpt-4.1", "mistralai/mistral-large"]
    }
  }
  ```
  - Thay thế danh sách mô hình theo nhu cầu (ví dụ: `["gpt-4.0", "llama-3.1"]`).
  - Nếu dùng **Vertex AI**, thay thế bằng ID mô hình của Google.

##### **B. Cấu Hình Node "OpenRouter Chat Model"**
- **Credentials:** Chọn `openRouterApi` (đã cấu hình trước khi import).
- **Key Parameters:**
  - `model`: `$json.model` (được truyền từ node trước).
  - **Lưu ý:** Nếu dùng mô hình khác OpenRouter, cần thay đổi node này thành `lmChatOpenAI` hoặc `lmChatVertexAI`.

##### **C. Cấu Hình Node "AI Agent"**
- **System Prompt:** Thiết lập để mô phỏng scenario thực tế (ví dụ: "Bạn là một chuyên gia tư vấn marketing").
- **Tools:** Nếu cần, thêm các tool hỗ trợ (ví dụ: API tìm kiếm, API tính toán).
- **Memory:** Sử dụng `Simple Memory` (hoặc Redis/Postgres nếu cần).

##### **D. Cấu Hình Node "Add Model Results to Google Sheet"**
- **Credentials:** Chọn `googleApi` (đã cấu hình trước).
- **Key Parameters:**
  - `operation`: `append` (thêm dữ liệu mới vào sheet).
- **Sheet Structure:**
  - Cột `model_1_eval` và `model_2_eval` được thiết lập với dropdown `"Good"`, `"Correct"`, `"Bad"` để đánh giá sau này.

##### **E. Cấu Hình Node "Prepare Data for Chat and Google Sheets"**
- **Output Format:** Đảm bảo cột `output` trong Sheets hiển thị phản hồi của mô hình với định dạng phân cách rõ ràng (ví dụ: `--- Model 1 --- [Phản hồi] --- Model 2 --- [Phản hồi]`).

#### 3. **Kích Hoạt ⚡️**
1. **Test Run:** Nhấn **Run Once** với một input mẫu (ví dụ: "Giải thích cách marketing cho sản phẩm AI").
2. **Kiểm tra Google Sheets:** Đảm bảo dữ liệu được ghi vào sheet đúng cột.
3. **Bật Active:** Chuyển workflow sang **Active** để chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm mô hình thứ 3+:**
   - Cần mở rộng logic trong node `splitInBatches` và `aggregate` để xử lý nhiều mô hình hơn.
   - Cập nhật cột trong Google Sheets tương ứng.

2. **Tự động đánh giá bằng AI:**
   - Sử dụng một mô hình mạnh như `o3` (OpenAI) để tự động đánh giá phản hồi của 2 mô hình.
   - Ví dụ: **"So sánh phản hồi của mô hình A và B, cho điểm từ 1-10 về tính chính xác và sáng tạo."**

3. **Gửi báo cáo định kỳ:**
   - Sử dụng node **Slack/Telegram** để thông báo kết quả so sánh hàng tuần.
   - Ví dụ: **"Mô hình Mistral có hiệu suất cao hơn GPT-4 trong 3/5 trường hợp."**

4. **Optimize token usage:**
   - Nếu chi phí token cao, sử dụng **prompt engineering** để rút ngắn input.
   - Ví dụ: Thay vì gửi toàn bộ lịch sử chat, chỉ gửi 3 message gần nhất.

5. **Lưu log chi tiết:**
   - Thêm node **Set** để lưu thêm thông tin như `token_used`, `response_time` vào Google Sheets.

---

### 📌 **Kết Luận**
Workflow này là **công cụ không thể thiếu** cho các sếp phát triển AI muốn:
✔ **So sánh mô hình LLM một cách khoa học** mà không cần viết code.
✔ **Lựa chọn mô hình phù hợp** với chi phí thấp nhất.
✔ **Cải thiện chất lượng chatbot** dựa trên dữ liệu thực tế.

**Hành động ngay hôm nay:**
1. Copy Google Sheet mẫu: [https://docs.google.com/spreadsheets/d/1grO5jxm05kJ7if9wBIOozjkqW27i8tRedrheLRrpxf4/](https://docs.google.com/spreadsheets/d/1grO5jxm05kJ7if9wBIOozjkqW27i8tRedrheLRrpxf4/)
2. Import workflow và chạy thử với mô hình của bạn.
3. **Đánh giá và tối ưu hóa** để đưa ra quyết định chính xác!

---
**💡 Chia sẻ ý kiến:** Các sếp có thể comment bên dưới về cách tối ưu workflow này cho dự án của mình!