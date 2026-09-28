---
title: "🤖 **Tự Động Hóa AI Data Analyst: Chatbot Phân Tích Dữ Liệu Tự Động Cho Doanh Nghiệp**"
description: "Tạo một chatbot AI thông minh phân tích dữ liệu từ Google Sheets, tính toán số liệu, và trả lời câu hỏi phức tạp về doanh số, refund, và xu hướng bán hàng chỉ với 1 workflow. Giúp các sếp tiết kiệm 10+ giờ/tháng phân tích dữ liệu thủ công."
slug: "tay-dong-hoa-chatbot-phan-tich-du-lieu-ai"
tags: [n8n, automation, no-code, ai-data-analysis, google-sheets, langchain]
keywords: [n8n workflow phân tích dữ liệu, chatbot AI tự động hóa doanh số, tự động hóa báo cáo bán hàng, n8n + OpenAI + Google Sheets, tự động hóa phân tích refund]
---

# 🚀 **Tạo Chatbot AI Data Analyst: Phân Tích Doanh Số, Refund & Xu Hướng Bán Hàng Tự Động**

Hiện nay, các sếp thường phải mất **giờ đồng hồ** để tra cứu, tính toán và tổng hợp dữ liệu từ Google Sheets để trả lời các câu hỏi như:
- *"Doanh số tháng này tăng bao nhiêu so với tháng trước?"*
- *"Số lượng refund cao nhất là do lý do gì?"*
- *"Doanh thu từ sản phẩm A trong quý 1 là bao nhiêu?"*

**Giải pháp?** Một **chatbot AI Data Analyst** được tự động hóa hoàn toàn trên nền tảng **n8n**, kết hợp **OpenAI (GPT-4o)** và **Google Sheets**, giúp trả lời tất cả câu hỏi chỉ trong **vài giây** mà không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Trả lời tất cả câu hỏi phân tích dữ liệu trong **vài giây** thay vì mất **giờ đồng hồ** thủ công.
✅ **Chính xác 100%**: AI tính toán từ dữ liệu thực tế trên Google Sheets, không sai sót như tính toán bằng Excel.
✅ **Cá nhân hóa**: Chatbot trả lời **câu hỏi phức tạp** như *"So sánh doanh số sản phẩm A và B trong 3 tháng gần đây"* một cách logic.
✅ **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp của người dùng.
✅ **Kết hợp nhiều công cụ**: Sử dụng **OpenAI (GPT-4o)**, **Google Sheets**, và **Calculator AI** để phân tích sâu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** và **API Key OAuth 2.0** (để kết nối với Google Sheets).
   - Hướng dẫn cài đặt: [Tại đây](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)
   - **Lưu ý**: Sử dụng **file Google Sheets mẫu** từ [đây](https://docs.google.com/spreadsheets/d/18A4d7KYrk8-uEMbu7shoQe_UIzmbTLV1FMN43bjA7qc/edit) và **copy URL** để thay thế trong workflow.

2. **API Key OpenAI** (để sử dụng GPT-4o).
   - Mua tại: [openai.com](https://platform.openai.com/)
   - **Lưu ý**: Workflow hỗ trợ **GPT-4o** (mô hình mới nhất) hoặc **Gemini (Google)** miễn phí.

3. **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud miễn phí).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/3050](https://n8n.io/workflows/3050) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/3050) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **14 node** với các bước quan trọng sau:

##### **A. Cấu hình Google Sheets**
- **Node**: `Google Sheets request`, `Get transactions by product name`, `Get all transactions`, `Get transactions by status`.
- **Hành động**:
  1. Thay thế **URL của file Google Sheets** trong tất cả các node liên quan (xem chú thích trong canvas).
     - **Ví dụ**:
        ```json
        "url": "https://sheets.googleapis.com/v4/spreadsheets/YOUR_SHEET_ID/g ranges=Sheet1!A1:Z100"
        ```
  2. Đăng ký **OAuth 2.0** trong n8n:
     - Tạo **credentials** mới với tên `googleSheetsOAuth2Api`.
     - Chọn **Google Sheets API** và kết nối với tài khoản Google.

##### **B. Cấu hình OpenAI (GPT-4o)**
- **Node**: `OpenAI Chat Model` (tên: `lmChatOpenAi`).
- **Hành động**:
  1. Thêm **API Key OpenAI** vào **credentials** với tên `openAiApi`.
  2. Chọn mô hình: `gpt-4o` (hoặc `gpt-4` nếu không có).

##### **C. Cấu hình AI Agent**
- **Node**: `AI Agent` (tên: `agent`).
- **Hành động**:
  - AI sẽ tự động quyết định sử dụng **Calculator**, **Google Sheets**, hoặc **Buffer Memory** dựa trên câu hỏi.
  - **Lưu ý**: AI sử dụng `$fromAI` để truyền dữ liệu giữa các tool.

##### **D. Cấu hình Buffer Memory (Nhớ lịch sử chat)**
- **Node**: `Buffer Memory` (tên: `memoryBufferWindow`).
- **Hành động**:
  - AI sẽ nhớ **5 lần chat gần nhất** để trả lời liên tục (ví dụ: *"Tôi đã hỏi về refund tháng trước, hãy so sánh với tháng này"*).

##### **E. Cấu hình Sub-Workflow (Lọc dữ liệu theo ngày)**
- **Node**: `Records by date` (tên: `toolWorkflow`).
- **Hành động**:
  - Đây là **sub-workflow** để lấy dữ liệu theo **ngày tháng** (tránh lỗi lọc phức tạp của Google Sheets API).
  - **Lưu ý**: Sub-workflow tự động trả về kết quả cho AI.

##### **F. Cấu hình Filter & Aggregate**
- **Node**: `Filter by status`, `Aggregate`.
- **Hành động**:
  - **Filter** giúp lọc dữ liệu theo trạng thái (ví dụ: `success`, `refund`).
  - **Aggregate** tổng hợp tất cả dữ liệu thành **1 JSON** để AI trả lời một cách logic.

##### **G. Node Code (Chuyển đổi dữ liệu thành JSON)**
- **Node**: `Code` (tên: `code`).
- **Hành động**:
  - Dữ liệu từ Google Sheets API thường **rối rắm**, nên sử dụng **mã JavaScript** (do ChatGPT tạo) để chuyển đổi thành **JSON sạch**.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với câu hỏi mẫu:
   - *"Hỏi về số lượng refund tháng 1 và tổng số tiền refund."*
   - *"Hỏi về doanh số thành công tháng 1 năm 2025 và tổng doanh thu."*
   - *"Hỏi lý do phổ biến nhất dẫn đến refund."*
2. **Bật Active workflow** và **chạy thử** trên n8n.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng **node `webhook`** để chatbot trả lời trên Slack/Telegram thay vì chỉ trong n8n.
   - **Cách làm**:
     ```json
     "url": "https://hooks.slack.com/services/YOUR_WEBHOOK_URL"
     ```

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `executeWorkflowTrigger`** để chạy workflow tự động mỗi ngày và gửi báo cáo qua email (sử dụng **node `email`**).

3. **Cập nhật dữ liệu tự động**:
   - Sử dụng **node `setInterval`** để cập nhật dữ liệu từ Google Sheets mỗi ngày.

4. **Sử dụng mô hình AI miễn phí**:
   - Thay vì GPT-4o, các sếp có thể thử **Google Gemini** (miễn phí) trong `lmChatOpenAi`.

---

### 📌 **Kết luận**
**Chatbot AI Data Analyst** này là **giải pháp hoàn hảo** để tự động hóa phân tích dữ liệu doanh nghiệp, tiết kiệm **thời gian và giảm sai sót**. Các sếp chỉ cần:
✅ **Import workflow** và **cấu hình Google Sheets + OpenAI**.
✅ **Test với câu hỏi mẫu** và **bật chạy**.
✅ **Sử dụng hàng ngày** để trả lời tất cả câu hỏi phân tích dữ liệu một cách **tự động và chính xác**.

**Hành động ngay!** [Tải workflow](https://n8n.io/workflows/3050) và **tự động hóa phân tích dữ liệu** của doanh nghiệp trong **vài phút**!

---
**💡 Cần hỗ trợ?** Liên hệ tác giả Solomon qua:
- Email: [automations.solomon@gmail.com](mailto:automations.solomon@gmail.com)
- Telegram: [@salomaoguilherme](https://t.me/salomaoguilherme)