---
title: "💰 **Tự Động Xử Lý Hóa Đơn với Telegram, GPT-4o, OCR & SAP – Giảm 90% Thời Gian Nhập Dữ liệu**"
description: "Workflow tự động hóa xử lý hóa đơn từ Telegram → OCR → GPT-4o phân tích → SAP nhập liệu tự động, giảm thiểu sai sót và tiết kiệm thời gian cho bộ phận tài chính."
slug: "tự-dộng-xử-ly-hoa-don-telegram-gpt-4o-sap"
tags: [n8n, automation, ai, sap, ocr, telegram-bot, gpt-4o, no-code, tài chính]
keywords: [tự động hóa hóa đơn, n8n workflow, OCR tự động, GPT-4o xử lý văn bản, SAP tự động nhập liệu, Telegram bot tài chính]
---

# 🚀 **Tự Động Xử Lý Hóa Đơn từ Telegram → SAP: Giảm 90% Công Việc Nhập Dữ liệu**

### **Nỗi Đau Của Các Sếp Tài Chính**
Hàng ngày, bộ phận tài chính phải:
- **Nhập liệu hóa đơn thủ công** từ file PDF/đính kèm Telegram → tốn thời gian và dễ sai sót.
- **Phân tích nội dung hóa đơn** (mã hàng, số lượng, giá trị, ngày giao dịch) → công việc mệt mỏi và dễ bị lỗi.
- **Nhập dữ liệu vào SAP** → rủi ro mất mát thông tin hoặc nhập sai mã sản phẩm.
- **Không có hệ thống tự động** → phụ thuộc vào nhân viên, gây chậm trễ trong xử lý.

**Workflow này giải quyết tất cả!** Sử dụng **Telegram Bot + GPT-4o + OCR + SAP API**, hóa đơn được tự động:
✅ **Nhận từ Telegram** (đính kèm file PDF/JPG).
✅ **Phân tích nội dung** bằng GPT-4o (trích xuất thông tin chính xác).
✅ **Nhập liệu tự động vào SAP** (không cần nhập thủ công).
✅ **Gửi báo cáo kết quả** qua Telegram (các sếp kiểm tra nhanh).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho OCR và AI).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** nhập liệu hóa đơn (từ 30 phút/lần xuống còn 5 phút).
- **Giảm sai sót 100%** nhờ GPT-4o và OCR tự động trích xuất dữ liệu.
- **Nhập liệu SAP tự động** → không cần nhân viên chờ đợi.
- **Báo cáo ngay lập tức** qua Telegram (các sếp kiểm tra từ xa).
- **Hoạt động 24/7** → không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot Telegram với **API Token** (mã xác thực).
   - **Chat ID** của nhóm/người dùng sẽ nhận hóa đơn.
   - [Hướng dẫn tạo Telegram Bot](https://core.telegram.org/bots#botfather).

2. **API Key OpenAI (GPT-4o)**:
   - Đăng ký tài khoản [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Chọn mô hình **`gpt-4o-mini`** (rẻ và hiệu quả).

3. **Google Sheets (OAuth 2.0)**:
   - Tạo file Google Sheets để lưu **header** và **detail** hóa đơn.
   - Cấp quyền **OAuth 2.0 API** cho n8n (mã xác thực).

4. **SAP API Credentials**:
   - **URL API** của hệ thống SAP (ví dụ: `https://your-sap-api.com`).
   - **Username/Password** hoặc **OAuth Token** để kết nối.
   - **Endpoint** để tạo hóa đơn mua (`/api/purchase-invoices`).

5. **LlamaIndex API (nếu sử dụng OCR)**:
   - Nếu muốn sử dụng **OCR từ file PDF/JPG**, cần API của [LlamaIndex](https://llamaindex.ai/) hoặc dịch vụ OCR khác (ví dụ: Tesseract).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4849](https://n8n.io/workflows/4849) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/4849) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **27 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ:

##### **A. Cấu Hình Telegram Bot**
- **Node `Trigger Receive Message`** (TelegramTrigger):
  - Chọn **`telegramApi`** (credentials đã tạo trước).
  - **Chat ID** phải là nhóm/người dùng sẽ gửi hóa đơn.
  - **Filter**: Chỉ lấy tin nhắn có **file đính kèm** (PDF/JPG).

- **Node `File Received`** (Telegram):
  - Chọn **`telegramApi`** cùng credentials.
  - **Action**: `sendMessage` (gửi tin nhắn xác nhận nhận file).

- **Node `Download File`** (Telegram):
  - Chọn **`telegramApi`**.
  - **Resource**: `file` (để tải file đính kèm).

##### **B. Cấu Hình GPT-4o (OCR & Phân Tích)**
- **Node `OpenAI Chat Model`** (lmChatOpenAi):
  - Chọn **`gpt-4o-mini`** (mô hình rẻ và hiệu quả).
  - **API Key**: Điền từ OpenAI.
  - **Prompt mẫu** (cần chỉnh sửa theo yêu cầu):
    ```json
    "You are an invoice processing assistant. Extract the following from the attached document:
    - Supplier Name
    - Invoice Number
    - Date
    - Items (Product Code, Quantity, Unit Price, Total Price)
    - Total Amount
    - Due Date
    Return the data in JSON format."
    ```

- **Node `Basic LLM Chain`** (chainLlm):
  - Kết nối với **`OpenAI Chat Model`**.
  - **Input**: Dữ liệu từ **`Download File`** (file PDF/JPG sau khi OCR).

##### **C. Cấu Hình SAP API**
- **Node `Connect to SAP`** (httpRequest):
  - **Method**: `POST`.
  - **URL**: `https://your-sap-api.com/api/purchase-invoices`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_SAP_TOKEN",
      "Content-Type": "application/json"
    }
    ```
  - **Body**: Dữ liệu JSON từ **`Create JSON`** (node sau).

- **Node `POST PurchaseInvoices`** (httpRequest):
  - Giống như trên, nhưng **body** là JSON đã chuẩn bị từ **`Generate DocumentLines`**.

##### **D. Cấu Hình Google Sheets (Lưu Log)**
- **Node `Header`** và **`Detail`** (googleSheets):
  - Chọn **`googleSheetsOAuth2Api`**.
  - **Sheet Name**: Đặt tên file Google Sheets (ví dụ: `Invoice_Log`).
  - **Operation**: `append` (thêm dữ liệu mới vào cuối).

##### **E. Cấu Hình Telegram Hỏi Đáp (Xác Nhận)**
- **Node `¿Upload to SAP?`** (Telegram):
  - Gửi tin nhắn hỏi: **"Bạn có muốn nhập hóa đơn này vào SAP không? (Yes/No)"**.
  - **Credentials**: `telegramApi`.

- **Node `Callback Waiting Answer`** (telegramTrigger):
  - Chờ phản hồi từ Telegram (`Yes`/`No`).
  - Nếu `Yes` → tiếp tục nhập SAP.
  - Nếu `No` → dừng và lưu log vào Google Sheets.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với file mẫu:
   - Gửi hóa đơn PDF/JPG qua Telegram Bot.
   - Kiểm tra **Google Sheets** xem dữ liệu có được lưu không.
   - Kiểm tra **SAP** xem hóa đơn có được tạo không.

2. **Bật Active**:
   - Chuyển workflow từ **`Inactive`** sang **`Active`**.
   - Đảm bảo **Telegram Bot** đang online và **SAP API** hoạt động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Log Lịch Sử**:
   - Sử dụng **`stickyNote`** để ghi lại thời gian xử lý và trạng thái (thành công/thất bại).
   - Ví dụ: `Hóa đơn #INV-001 đã được xử lý thành công vào 10:30 AM`.

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **`googleSheets`** + **`telegram`** để gửi báo cáo tổng hợp hàng ngày.
   - Ví dụ: `Tổng số hóa đơn xử lý: 50, Tổng giá trị: 100.000.000 VND`.

3. **Kết Nối Slack/Email**:
   - Thay thế **Telegram** bằng **Slack** hoặc **Email** để thông báo kết quả.
   - Sử dụng node **`slack`** hoặc **`email`** để gửi thông báo tự động.

4. **Sử Dụng OCR Tesseract (Nếu Không Có LlamaIndex)**:
   - Nếu không muốn dùng LlamaIndex, có thể sử dụng **OCR Tesseract** qua **`httpRequest`** để trích xuất văn bản từ file PDF/JPG trước khi gửi cho GPT-4o.

5. **Tự Động Xóa File Sau Xử Lý**:
   - Thêm node **`telegram`** để xóa file sau khi đã xử lý thành công.

---

### 📌 **Kết Luận**
Workflow này **giải phóng bộ phận tài chính** khỏi công việc nhọc nhằn nhập liệu hóa đơn, đồng thời **giảm thiểu sai sót** nhờ AI và tự động hóa. Với **n8n + GPT-4o + SAP**, các sếp có thể:
✔ **Nhập liệu SAP chỉ với 1 nhấp chuột**.
✔ **Kiểm tra hóa đơn từ xa** qua Telegram.
✔ **Tiết kiệm hàng giờ công việc** mỗi ngày.

**Hãy thử ngay!** Import workflow, cấu hình các credentials, và bắt đầu tự động hóa hóa đơn của mình. Nếu có vấn đề, **hãy để lại comment** dưới đây, chúng tôi sẽ hỗ trợ!

---
**🚀 Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow từ n8n.io](https://n8n.io/workflows/4849)