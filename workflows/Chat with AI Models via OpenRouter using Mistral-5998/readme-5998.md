---
title: "🤖 Tự Động Hỏi Đáp AI với Mistral qua OpenRouter - Không Cần Code!"
description: "Workflow này giúp các sếp tự động hóa việc chat với các mô hình AI tiên tiến của Mistral thông qua API OpenRouter, tiết kiệm thời gian và nâng cao hiệu quả làm việc. Chỉ cần nhấn nút, hệ thống sẽ trả lời ngay lập tức với độ chính xác cao."
slug: "tieu-dong-hoi-dap-ai-voi-mistral-qua-openrouter"
tags: [n8n, automation, ai-chatbot, openrouter, mistral-ai, no-code]
keywords: [n8n workflow ai, tự động hóa chatbot ai, openrouter api, mistral ai chat, tự động hóa không code]
---

# 🚀 **Tự Động Hỏi Đáp AI với Mistral qua OpenRouter - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp thường phải tốn thời gian để tìm kiếm thông tin, hỏi các chuyên gia hoặc tra cứu tài liệu để giải quyết các vấn đề phức tạp. Thậm chí, khi cần tư vấn từ AI, việc phải nhập prompt một cách thủ công vào các trang web hoặc API khác nhau là một quá trình tẻ nhạt và dễ mắc lỗi. **Workflow này giải quyết vấn đề đó bằng cách tự động hóa toàn bộ quy trình, cho phép các sếp chỉ cần nhấn một nút và nhận được câu trả lời từ AI Mistral thông qua OpenRouter một cách nhanh chóng và chính xác!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập prompt thủ công vào các trang web hoặc API.
- **Trả lời tức thì**: Nhấn một nút, hệ thống tự động gửi yêu cầu đến AI Mistral và trả về kết quả ngay lập tức.
- **Độ chính xác cao**: Sử dụng mô hình AI tiên tiến của Mistral để đảm bảo câu trả lời logic và phù hợp.
- **Hoạt động liên tục**: Workflow có thể được tự động hóa và chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc của cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **API Key của OpenRouter**:
   - Đăng ký tài khoản tại [OpenRouter](https://openrouter.ai/) và lấy API Key từ trang cá nhân.
   - **Lưu ý**: API Key này sẽ được sử dụng để kết nối với mô hình AI Mistral.
2. **Dữ liệu đầu vào (Prompt)**:
   - Các câu hỏi hoặc yêu cầu cần gửi đến AI (có thể nhập thủ công hoặc tự động hóa từ các nguồn khác như Slack, Email, hoặc Webhook).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Vào **Workflow** > **Create Workflow** > **Import Workflow**.
3. Chọn file JSON hoặc dán JSON từ [link gốc](https://n8n.io/workflows/5998) vào ô nhập liệu.
4. Nhấn **Import** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Manual Trigger (Kích Hoạt Thủ Công)**
- **Tên Node**: *When clicking ‘Execute workflow’*
- **Lưu ý**:
  - Node này dùng để kích hoạt workflow thủ công. Các sếp có thể nhấn nút **Execute Workflow** để bắt đầu quá trình.
  - **Không cần cấu hình gì** ngoài việc kích hoạt.

##### **Node 2: HTTP Request (Gửi Yêu Cầu đến OpenRouter)**
- **Tên Node**: *OpenRouter.ai*
- **Cấu hình cần thiết**:
  - **Method**: `POST`
  - **URL**: `https://openrouter.ai/api/v1/chat/completions`
  - **Headers**:
    ```
    {
      "Authorization": "Bearer YOUR_API_KEY_HERE",
      "Content-Type": "application/json"
    }
    ```
    - Thay `YOUR_API_KEY_HERE` bằng API Key của OpenRouter.
  - **Body (JSON)**:
    ```json
    {
      "model": "mistral-tiny",
      "messages": [
        {
          "role": "user",
          "content": "{{ $node["Set Model & Prompt"].json["prompt"] }}"
        }
      ]
    }
    ```
    - Node này sẽ gửi yêu cầu đến API OpenRouter với mô hình `mistral-tiny` (có thể thay đổi thành `mistral-small` hoặc `mistral-large` nếu cần).

##### **Node 3: Set Model & Prompt (Cấu Hình Mô Hình và Prompt)**
- **Tên Node**: *Set Model & Prompt*
- **Cấu hình cần thiết**:
  - **JSON Path**: `$.prompt`
  - **Giá trị**: Các sếp có thể nhập **prompt** thủ công hoặc tự động hóa từ các nguồn khác (ví dụ: từ một node **HTTP Request** hoặc **Webhook**).
  - **Ví dụ**:
    ```json
    {
      "prompt": "Giải thích cách tự động hóa quy trình với n8n cho người mới bắt đầu."
    }
    ```
    - **Lưu ý**: Prompt này sẽ được truyền vào node **HTTP Request** để AI trả lời.

##### **Node 4: Summarize (Tóm Tắt Kết Quả)**
- **Tên Node**: *Summarize*
- **Cấu hình cần thiết**:
  - **Model**: Chọn mô hình AI để tóm tắt (nếu cần).
  - **Text**: Sử dụng kết quả từ node **HTTP Request** (trả về câu trả lời của AI Mistral).
  - **Lưu ý**: Node này **không bắt buộc** nhưng có thể được sử dụng để tóm tắt câu trả lời dài hoặc phân tích thêm.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn nút **Execute Workflow** để kích hoạt.
   - Nhập **prompt** vào node **Set Model & Prompt** (hoặc sử dụng dữ liệu tự động hóa).
   - Kiểm tra kết quả từ node **HTTP Request** và **Summarize** (nếu áp dụng).
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram** để nhận prompt từ các kênh thông báo và tự động trả lời qua AI.
2. **Lưu Log Kết Quả**:
   - Sử dụng node **Google Sheets** hoặc **Database** để lưu lịch sử câu hỏi và trả lời của AI.
3. **Gửi Báo Cáo Định Kỳ**:
   - Tự động hóa việc gửi báo cáo tổng hợp từ AI qua Email hoặc Slack hàng tuần/tháng.
4. **Thay Đổi Mô Hình AI**:
   - Thay đổi mô hình từ `mistral-tiny` sang `mistral-large` trong node **HTTP Request** để cải thiện chất lượng trả lời.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc tương tác với AI Mistral thông qua OpenRouter **không cần viết code**. Bằng cách chỉ cần nhấn một nút, các sếp sẽ tiết kiệm thời gian, tăng hiệu suất và đảm bảo câu trả lời luôn chính xác. **Hãy áp dụng ngay và trải nghiệm sự tiện lợi của tự động hóa!**

---
**💡 Bạn có thể tùy chỉnh workflow này để phù hợp với các mô hình AI khác trên OpenRouter hoặc kết hợp với các dịch vụ khác như Zapier, Make (Integromat), hoặc các API khác!**