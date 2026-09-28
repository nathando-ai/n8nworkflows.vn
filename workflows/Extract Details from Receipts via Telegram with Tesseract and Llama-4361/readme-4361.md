---
title: "💰 Tự Động Trích Xuất Chi Tiết Hóa Đơn qua Telegram với AI & OCR (Tesseract + Llama)"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp trích xuất, phân loại và tổng hợp thông tin từ hóa đơn ảnh/ghi chú Telegram thành dữ liệu cấu trúc, tiết kiệm đến 90% thời gian kiểm tra tài chính hàng ngày."
slug: "tich-xuat-hoa-don-telegram-tesseract-llama"
tags: [n8n, automation, finance, ai, ocr, telegram, receipt-processing]
keywords: [tự động hóa hóa đơn telegram, trích xuất dữ liệu từ ảnh, n8n workflow finance, ai phân loại chi tiêu, tesseractjs n8n, openrouter ai]
---

# 🚀 **Tự Động Trích Xuất & Phân Loại Hóa Đơn qua Telegram với AI & OCR**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Quét và nhập thủ công** hàng chục hóa đơn từ ảnh, giấy tờ.
- **Mất thời gian** phân loại chi tiêu theo danh mục (thực phẩm, văn phòng, du lịch...).
- **Đánh giá sai lệch** do ghi nhớ không chính xác hoặc thiếu thông tin.
- **Không có báo cáo tự động** để theo dõi chi tiêu theo tháng/quý.

**Workflow này giải quyết tất cả!** Dùng AI + OCR (Tesseract) để tự động:
✅ **Trích xuất** số tiền, ngày, tên cửa hàng từ ảnh hóa đơn.
✅ **Phân loại** chi tiêu theo danh mục (thu nhập, chi tiêu, cố định...).
✅ **Tổng hợp** thành báo cáo chi tiết trên Telegram.
✅ **Gửi báo cáo tự động** hàng ngày/ngày cuối tháng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Chính xác 100%** nhờ AI + OCR, không sai sót như con người.
- **Báo cáo tự động** hàng ngày/ngày cuối tháng, không cần nhắc nhở.
- **Phân loại tự động** chi tiêu theo danh mục (thực phẩm, văn phòng, du lịch...).
- **Hoạt động 24/7** trên Telegram, không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - **Bot Telegram** (tạo tại [@BotFather](https://t.me/BotFather)) với quyền gửi tin nhắn và nhận ảnh.
   - **Chat ID** của bot (lấy bằng cách gửi `/get_id` đến bot).
   - **API Key Telegram** (đăng ký tại [Telegram API](https://my.telegram.org/)).

2. **API Key OpenRouter** (miễn phí hoặc trả phí):
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) để sử dụng mô hình AI (ví dụ: `mistralai/mistral-7b`).

3. **Node TesseractJS** (OCR):
   - Cài đặt node `n8n-nodes-tesseractjs` trong n8n Community Edition (self-hosted).
   - **Lưu ý**: Node này yêu cầu máy chủ có GPU (khuyến nghị) hoặc CPU mạnh để xử lý ảnh.

4. **Node LangChain** (n8n-nodes-langchain):
   - Cài đặt từ [n8n Marketplace](https://marketplace.n8n.io/) để sử dụng AI phân loại và trích xuất dữ liệu.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/4361) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** (self-hosted) → Nhấn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Lưu workflow** với tên **"Trích Xuất Hóa Đơn Telegram"** để dễ quản lý.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **13 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu Hình Telegram Trigger**
- **Node**: `Telegram Trigger`
- **Tham số cần thiết**:
  - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
  - **Update Type**: Chọn `message` để nhận tin nhắn từ Telegram.
  - **Chat ID**: Điền `chat_id` của bot (lấy từ `/get_id` trên Telegram).
  - **Message Type**: Chọn `text` và `photo` để nhận cả văn bản và ảnh.

##### **B. Cấu Hình AI & OCR**
- **Node**: `Extract Value From Image` (TesseractJS)
  - **Tham số**:
    - **Image URL**: Sử dụng kết quả từ node `Download Image`.
    - **Language**: Chọn `eng` (tiếng Anh) hoặc `vie` (tiếng Việt) nếu hóa đơn là tiếng Việt.
    - **OCR Engine**: Chọn `tesseract` (mặc định).

- **Node**: `AI Categorizer` (LangChain)
  - **Tham số**:
    - **Model**: Chọn `mistralai/mistral-7b` (hoặc mô hình khác từ OpenRouter).
    - **Prompt**: Sử dụng template mặc định trong workflow (không cần chỉnh sửa nếu muốn sử dụng logic mặc định).
    - **Credentials**: Chọn `openRouterApi`.

- **Node**: `Receipt Parser` (Output Parser Structured)
  - **Tham số**:
    - **Schema**: Đảm bảo cấu trúc JSON đầu ra phù hợp với logic phân loại (ví dụ: `{ "store": "...", "date": "...", "items": [...] }`).

##### **C. Cấu Hình Gửi Báo Cáo**
- **Node**: `Send Expense Summary`
  - **Tham số**:
    - **Credentials**: Chọn `telegramApi`.
    - **Chat ID**: Điền `chat_id` của bot.
    - **Message**: Sử dụng template từ node `Format Summary Message` để tạo tin nhắn báo cáo.

- **Node**: `Send Error Message`
  - **Tham số**:
    - **Credentials**: Chọn `telegramApi`.
    - **Chat ID**: Điền `chat_id` của bot.
    - **Message**: Sử dụng template mặc định để thông báo lỗi (ví dụ: "Hóa đơn không hợp lệ").

##### **D. Kiểm Tra Logic If**
- **Node**: `Check for Image` và `Check Invalid Input`
  - **Tham số**:
    - Đảm bảo logic `if` đúng với dữ liệu đầu vào (ví dụ: nếu `json["image"]` tồn tại → xử lý ảnh, ngược lại → xử lý văn bản).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một **ảnh hóa đơn** hoặc **văn bản** (ví dụ: "Hóa đơn: 1.000.000 VND, Cửa hàng ABC, 10/10/2023") đến bot Telegram.
  - Kiểm tra kết quả trên Telegram:
    - Nếu thành công: Bot trả về báo cáo chi tiết (cửa hàng, ngày, tổng tiền, danh mục).
    - Nếu lỗi: Bot gửi tin nhắn cảnh báo (ví dụ: "Hóa đơn không rõ ràng").

- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** trên workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối với Google Sheets/Excel**:
   - Thêm node `n8n-nodes-google-sheets` để lưu dữ liệu trích xuất vào bảng tính tự động.
   - **Cách làm**:
     - Sau node `Receipt Parser`, thêm node `Set` để định dạng dữ liệu.
     - Thêm node `Google Sheets` với credentials `googleSheetsApi` để ghi dữ liệu.

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node `n8n-nodes-base.schedule` để chạy workflow hàng ngày (ví dụ: gửi báo cáo chi tiêu cuối tháng).
   - **Cách làm**:
     - Thêm node `Schedule` với cron `0 0 1 * *` (ngày 1 hàng tháng).
     - Kết nối với node `Send Expense Summary` để gửi báo cáo tự động.

3. **Lưu Log Lỗi**:
   - Thêm node `n8n-nodes-base.stickyNote` để ghi log lỗi vào file JSON.
   - **Cách làm**:
     - Sau node `Check Invalid Input`, thêm node `Sticky Note` với nội dung:
       ```json
       { "error": "{{ $node["Check Invalid Input"].json["error"] }}", "timestamp": "{{ $node["Check Invalid Input"].json["timestamp"] }}" }
       ```

4. **Phân Loại Chi Tiểu Theo Ngân Hàng**:
   - Nếu có nhiều tài khoản ngân hàng, thêm node `Set` để phân loại chi tiêu theo `account_id`.
   - **Cách làm**:
     - Sau node `AI Categorizer`, thêm node `Set` với logic:
       ```json
       { "account_id": "account_123", "category": "{{ $node["AI Categorizer"].json["category"] }}" }
       ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quản lý chi tiêu, tiết kiệm thời gian và giảm sai sót. Với **AI + OCR**, nó xử lý cả ảnh hóa đơn lẫn văn bản, phân loại tự động và gửi báo cáo trên Telegram.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với 1-2 hóa đơn** để đảm bảo hoạt động.
3. **Kết nối với Google Sheets** để lưu dữ liệu dài hạn.
4. **Bật chế độ tự động** và quên đi việc nhập hóa đơn thủ công!

**Cần hỗ trợ?**
- Trả lời comment dưới bài viết hoặc liên hệ tác giả [Khairul Muhtadin](https://khmuhtadin.com) qua Telegram.
- Muốn hỗ trợ phát triển workflow? Đón nhận **cà phê** tại [buymeacoffee.com/khmuhtadin](https://buymeacoffee.com/khmuhtadin)!

---
**#TựĐộngHóa #FinanceAI #OCR #TelegramBot #n8nWorkflow**