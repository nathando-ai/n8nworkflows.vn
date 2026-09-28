---
title: "🚀 Tự Động Hóa Trích Xuất & Theo Dõi Hóa Đơn PDF với Google Drive, AI Claude & Telegram (Không Cần Code)"
description: "Workflow này tự động phát hiện hóa đơn PDF mới trên Google Drive, trích xuất dữ liệu quan trọng (tên khách hàng, số hóa đơn, số tiền, ngày hạn), ghi vào Google Sheets, và gửi thông báo định dạng AI lên Telegram cho đội ngũ kế toán. Giúp tiết kiệm 10+ giờ/tháng và giảm thiểu lỗi nhập liệu."
slug: "tieu-dong-hoa-trich-xuat-va-theo-doi-hoa-don-pdf"
tags: [n8n, automation, invoice processing, ai-summarization, google-drive, telegram-notification, no-code]
keywords: [n8n workflow hóa đơn, tự động hóa kế toán, trích xuất dữ liệu PDF, AI Claude, Telegram alert, Google Sheets tự động]
---

# 🚀 **Tự Động Hóa Trích Xuất & Theo Dõi Hóa Đơn PDF với Google Drive, AI Claude & Telegram**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, đội ngũ kế toán phải:
- **Tải xuống** hàng chục hóa đơn PDF từ email, Google Drive, hoặc các hệ thống khác.
- **Nhập liệu thủ công** vào phần mềm kế toán hoặc Google Sheets, dễ gây ra lỗi và mất thời gian.
- **Theo dõi thủ công** các hóa đơn đã thanh toán, quá hạn, hoặc cần xử lý ưu tiên.
- **Phân tích lại** hóa đơn để tổng hợp báo cáo cho ban lãnh đạo.

**Kết quả?** Thời gian và công sức bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi AI và tự động hóa có thể giải phóng họ để tập trung vào việc **quyết định chiến lược** thay vì nhập liệu.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** bằng cách loại bỏ việc nhập liệu thủ công.
- **Chính xác 100%** với AI trích xuất dữ liệu từ PDF (không còn sai sót do con người).
- **Theo dõi thực thời** hóa đơn qua Telegram (báo cáo quá hạn, hóa đơn mới, tổng hợp AI).
- **Báo cáo tự động** với dữ liệu được ghi vào Google Sheets, sẵn sàng cho phân tích.
- **Cá nhân hóa thông báo** với Claude AI định dạng tin nhắn Telegram theo phong cách chuyên nghiệp.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive**:
   - **Folder cụ thể** để lưu hóa đơn PDF mới (cần chia sẻ cho n8n với quyền đọc).
   - **OAuth 2.0 Credentials** của Google Drive (cài đặt trong n8n).
2. **Google Sheets**:
   - **Bảng tính mới** để lưu trữ dữ liệu hóa đơn (cấu trúc gồm cột: `Invoice Number`, `Client Name`, `Amount`, `Due Date`, `Status`, `Notes`).
   - **Chia sẻ bảng với n8n** (quyền chỉnh sửa).
3. **Telegram Bot**:
   - **Bot Telegram** (tạo tại [@BotFather](https://t.me/BotFather)).
   - **Chat ID** của nhóm/channel cần nhận thông báo (có thể lấy bằng [@userinfobot](https://t.me/userinfobot)).
4. **API Keys AI**:
   - **Anthropic Claude API Key** (đăng ký tại [Anthropic](https://www.anthropic.com/)).
   - **OpenAI API Key** (tùy chọn, nếu muốn sử dụng OpenAI thay Claude).
5. **n8n Self-hosted**:
   - Workflow này **không chạy được trên n8n Cloud** do sử dụng các node LangChain và API keys riêng tư. Các sếp cần **cài n8n trên VPS** (xem gợi ý dưới đây).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6480](https://n8n.io/workflows/6480) (ấn nút "Export").
- **Mở n8n Editor** (trên VPS hoặc [n8n.io](https://n8n.io/)) → **Import** file JSON.
- **Hoặc copy/paste** JSON từ file vào Editor → **Import**.

:::note[LƯU Ý]
- **Không sử dụng n8n Cloud** vì workflow này yêu cầu:
  - Node `informationExtractor` (LangChain).
  - API keys riêng tư (Claude/OpenAI).
  - Google Drive Trigger (chỉ hoạt động trên self-hosted).
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **10 node**, nhưng các bước **quan trọng nhất** cần điều chỉnh là:

##### **A. Cấu Hình Google Drive Trigger**
- **Node**: `Google Drive Trigger`
  - **Operation**: Chọn `Watch folder` (theo dõi folder chứa hóa đơn).
  - **Folder ID**: Điền **ID folder** của Google Drive (lấy từ liên kết folder: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
  - **File Types**: Chọn `PDF` (hoặc `*.pdf`).
  - **Credentials**: Chọn **OAuth 2.0 Credentials** của Google Drive đã tạo trước.

##### **B. Cấu Hình Trích Xuất Dữ Liệu từ PDF**
- **Node**: `Extract from File` (PDF)
  - **Operation**: Đảm bảo chọn `pdf`.
  - **File Path**: Auto lấy từ Google Drive Trigger (không cần chỉnh).

- **Node**: `Information Extractor` (LangChain)
  - **Model**: Chọn `claude-sonnet-4-20250514` (đã cấu hình sẵn).
  - **Prompt**: Workflow đã định sẵn prompt để trích xuất:
    ```json
    "Extract structured data from the invoice PDF. Return in JSON format with keys: invoice_number, client_name, amount, due_date, items, notes."
    ```
  - **Credentials**: Chọn **Anthropic API Key** đã thêm.

##### **C. Ghi Dữ Liệu vào Google Sheets**
- **Node**: `Google Sheets` (Append)
  - **Sheet Name**: Điền tên **bảng tính** muốn ghi dữ liệu (ví dụ: `Invoice Tracking`).
  - **Range**: Chọn **đầu tiên hàng trống** (ví dụ: `A1:A1`).
  - **Credentials**: Chọn **OAuth 2.0 Credentials** của Google Sheets.
  - **Headers**: Bật `Use headers` và điền tên cột theo mẫu:
    ```
    Invoice Number, Client Name, Amount, Due Date, Status, Notes
    ```

##### **D. Định Dạng Thông Báo Telegram với Claude AI**
- **Node**: `Anthropic Agent` (Chain LLM)
  - **Model**: Đã chọn `claude-sonnet-4-20250514`.
  - **Prompt**: Workflow tự động định dạng tin nhắn Telegram như:
    ```json
    "Create a professional Telegram notification for the billing team about this invoice. Include: invoice number, client name, amount, due date, and a summary of items. Format as a markdown table."
    ```
  - **Credentials**: Chọn **Anthropic API Key**.

- **Node**: `Telegram`
  - **Chat ID**: Điền **Chat ID** của nhóm/channel Telegram (lấy từ [@userinfobot](https://t.me/userinfobot)).
  - **Bot Token**: Điền **Token bot** từ [@BotFather](https://t.me/BotFather).
  - **Message**: Auto lấy từ node `Anthropic Agent`.

##### **E. NoOp & StickyNote (Lưu Ý)**
- **Node**: `No Operation` → **Không cần chỉnh**, chỉ để điều hướng workflow.
- **Node**: `StickyNote` → **Dùng để ghi chú** (ví dụ: "Chỉnh sửa lại prompt nếu AI trích xuất sai").

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **1 hóa đơn PDF mẫu**:
   - Tải 1 hóa đơn PDF lên folder Google Drive đã cấu hình.
   - Chạy **Manual Trigger** trong n8n Editor để kiểm tra:
     - Dữ liệu có được trích xuất không?
     - Google Sheets có ghi dữ liệu không?
     - Telegram có nhận được thông báo không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi có hóa đơn mới.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[MỞ RỘNG THÊM]
1. **Thêm Slack Notification**:
   - Sử dụng node `Slack` để gửi thông báo đồng thời lên Slack (cấu hình như Telegram).
2. **Lưu Log Lịch Sử**:
   - Thêm node `Set` hoặc `Google Drive` để lưu **tập tin log** của mỗi hóa đơn (ví dụ: `Invoice_2024_05_01.pdf.log`).
3. **Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần/tuần để tổng hợp báo cáo từ Google Sheets.
4. **Tự Động Xóa Hóa Đơn Sau Trích Xuất**:
   - Thêm node `Google Drive` với **operation: delete** để xóa hóa đơn sau khi trích xuất (nếu không cần lưu trữ).
5. **Cải Thiện Prompt AI**:
   - Nếu AI trích xuất sai, chỉnh sửa **prompt** trong node `Information Extractor` để cụ thể hơn (ví dụ: thêm ví dụ hóa đơn mẫu).
6. **Kết Nối với ERP**:
   - Sử dụng node `HTTP Request` để gửi dữ liệu trích xuất lên hệ thống ERP như **QuickBooks, Xero, hoặc SAP**.
:::

---

### **📌 Kết Luận**
Workflow này **giải phóng đội ngũ kế toán** khỏi việc nhập liệu thủ công, đồng thời **tăng cường tính chính xác và hiệu quả** với AI Claude và Telegram. **Chỉ cần 30 phút để setup**, sau đó workflow sẽ **hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Cài n8n trên VPS** (xem gợi ý dưới đây).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với 1 hóa đơn mẫu** và bật Active.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**Lưu ý**: N8n Cloud **không hỗ trợ** các node LangChain và API keys riêng tư, nên **cần self-hosted**.
:::

---
**Bạn có câu hỏi?** Để lại comment hoặc liên hệ với [Automate With Marc](https://www.youtube.com/@Automatewithmarc) để học cách tối ưu workflow này! 🚀