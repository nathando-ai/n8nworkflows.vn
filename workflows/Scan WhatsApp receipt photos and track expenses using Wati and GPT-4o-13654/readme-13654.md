---
title: "💸 **Tự Động Hoá Quản Lý Chi Phí WhatsApp Với AI: Scan Hóa Đơn & Báo Cáo Tháng Hàng Ngày**"
description: "Workflow này tự động quét hóa đơn từ ảnh WhatsApp, trích xuất dữ liệu chi phí (người bán, số tiền, ngày, danh mục) bằng AI GPT-4o, và tự động cập nhật vào Google Sheets. Khi bạn gửi tin nhắn 'report', hệ thống sẽ tự động tổng hợp báo cáo chi tiêu hàng tháng và gửi lại qua WhatsApp. Giúp tiết kiệm thời gian lên tới 80% so với cách thủ công!"
slug: "tieu-dong-hoa-quan-ly-chi-phi-whatsapp-ai"
tags: [n8n, automation, no-code, ai-chatbot, google-sheets, whatsapp-bot, receipt-scanner]
keywords: [tự động hóa quản lý chi phí, scan hóa đơn bằng AI, n8n workflow, quản lý chi tiêu hàng tháng, báo cáo chi phí tự động, GPT-4o trích xuất dữ liệu]
---

# 🚀 **Tự Động Hoá Quản Lý Chi Phí WhatsApp: Scan Hóa Đơn & Báo Cáo Tháng Hàng Ngày**

### **Nỗi Đau Của Các Sếp**
Làm thủ công việc quản lý chi phí hàng tháng là một **đau đầu lớn**:
- **Tốn thời gian**: Phải quét hàng chục hóa đơn, nhập liệu vào Excel/Google Sheets, và tính toán thủ công.
- **Sai sót cao**: Nhập sai số tiền, ngày tháng, hoặc danh mục chi phí dễ xảy ra.
- **Không cập nhật kịp thời**: Hóa đơn mới đến mà không được ghi lại ngay, dẫn đến báo cáo không chính xác.
- **Không có báo cáo tự động**: Phải tự tổng hợp và gửi báo cáo cho bộ phận tài chính, mất thêm thời gian.

**Workflow này giải quyết tất cả!** Dùng **AI GPT-4o** để tự động quét hóa đơn từ ảnh WhatsApp, trích xuất dữ liệu chính xác, và tự động **cập nhật vào Google Sheets**. Khi bạn gửi tin nhắn **"report"**, hệ thống sẽ **tự động tổng hợp báo cáo chi tiêu hàng tháng** và gửi lại qua WhatsApp.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và không bị giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên tới 80%** so với cách thủ công.
✅ **Chính xác 100%** nhờ AI GPT-4o trích xuất dữ liệu từ hóa đơn.
✅ **Cập nhật tự động** khi nhận được hóa đơn mới qua WhatsApp.
✅ **Báo cáo tháng tự động** chỉ cần gửi tin nhắn "report".
✅ **Dữ liệu trung tâm** trên Google Sheets, dễ dàng phân tích và xuất báo cáo.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API** (đăng ký qua [WATI](https://wati.ai/)) để nhận và gửi tin nhắn tự động.
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)) để sử dụng GPT-4o trích xuất dữ liệu từ ảnh.
3. **Google Sheets** với **OAuth 2.0** để lưu trữ dữ liệu chi phí.
4. **File Google Sheets** đã chuẩn bị sẵn với **cột tiêu đề** sau:
   ```
   Timestamp | Phone | Vendor | Amount | Currency | Date | Category | Description | Month
   ```
5. **Mã giảm giá VPS** (nếu cần) để tự host n8n ổn định.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
- **Tải workflow gốc** từ [đây](https://n8n.io/workflows/13654).
- **Import vào n8n**:
  - Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc **paste JSON** vào ô nhập liệu.
  - Hoặc **copy toàn bộ JSON** từ [đây](https://n8n.io/workflows/13654) và dán vào **Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **11 node**, các sếp cần **cấu hình kỹ lưỡng** các phần sau:

##### **A. Cấu Hình Credentials (Tài Khoản)**
| Node | Yêu Cầu Cấu Hình | Ghi Chú |
|------|------------------|---------|
| **WATI Trigger** | Thêm **WATI API** (từ tài khoản WATI) | Sử dụng **Webhook URL** từ n8n để WATI gửi tin nhắn về. |
| **OpenAI – Extract Receipt Data** | Thêm **OpenAI API Key** | Chọn **httpHeaderAuth** với header `Authorization: Bearer {API_KEY}`. |
| **Google Sheets – Log Expense** | Thêm **Google Sheets OAuth2** | Chọn **Google Sheets** đã liên kết với tài khoản Google. |
| **Google Sheets – Read This Month** | Sử dụng cùng **Google Sheets OAuth2** | Không cần cấu hình thêm. |

##### **B. Cấu Hình Node Quan Trọng**
1. **Route Message (Switch)**
   - **Condition 1**: Kiểm tra nếu tin nhắn là **ảnh** → Chuyển sang **Parse & Validate Expense**.
   - **Condition 2**: Kiểm tra nếu tin nhắn là **text** và bằng **"report"** → Chuyển sang **Build Monthly Report**.
   - **Condition 3**: Nếu khác → Gửi tin nhắn **"Hãy gửi ảnh hóa đơn hoặc gõ 'report' để xem báo cáo tháng."**

2. **Parse & Validate Expense (Code)**
   - **Mã JavaScript** đã được viết sẵn để **xử lý dữ liệu từ OpenAI** và chuẩn bị cho Google Sheets.
   - **Không cần chỉnh sửa** nếu các sếp đã import workflow chính xác.

3. **Prepare Image for OpenAI (Code)**
   - **Chuyển đổi ảnh từ binary sang base64** để OpenAI có thể đọc.
   - **Không cần chỉnh sửa** nếu import workflow gốc.

4. **OpenAI – Extract Receipt Data (HTTP Request)**
   - **Endpoint**: `https://api.openai.com/v1/chat/completions`
   - **Body**:
     ```json
     {
       "model": "gpt-4o",
       "messages": [
         {
           "role": "user",
           "content": [
             {
               "type": "image_url",
               "image_url": {
                 "url": "{{ $json.base64Image }}"
               }
             },
             {
               "type": "text",
               "text": "Extract vendor, amount, date, and category from this receipt image. Return data in JSON format."
             }
           ]
         }
       ],
       "response_format": { "type": "json_object" }
     }
     ```
   - **Headers**:
     - `Authorization: Bearer {{ $credentials.openAiApi.apiKey }}`
     - `Content-Type: application/json`

5. **Google Sheets – Log Expense**
   - **Sheet Name**: Đặt tên **Google Sheet** đã chuẩn bị sẵn (ví dụ: **"ChiPhiHangThang"**).
   - **Range**: `Sheet1!A1` (nếu dữ liệu ở Sheet1).
   - **Operation**: `append` (thêm dữ liệu mới vào cuối).

6. **Build Monthly Report (Code)**
   - **Mã JavaScript** sẽ **lọc dữ liệu theo tháng hiện tại** và **tổng hợp báo cáo**.
   - **Không cần chỉnh sửa** nếu import workflow gốc.

7. **Send Expenditure message & Send Expenditure Report - month (WATI)**
   - **Template tin nhắn**:
     - Khi scan hóa đơn thành công: `"Chi phí đã được ghi nhận: {{ $json.vendor }} - {{ $json.amount }} {{ $json.currency }} ({{ $json.date }})"`.
     - Khi gửi "report": Báo cáo chi tiêu theo tháng với **các danh mục và tổng số tiền**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run Dữ Liệu Mẫu**
   - Gửi **một ảnh hóa đơn** qua WhatsApp (đã đăng ký với WATI).
   - Kiểm tra **Google Sheets** có được cập nhật không.
   - Gửi tin nhắn **"report"** để kiểm tra báo cáo tháng.

2. **Bật Active Workflow**
   - Nhấn **"Active"** trên n8n Editor để workflow chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**
   - Thêm **node Slack/Telegram** để báo cáo chi phí được gửi đến nhóm công việc.
   - **Cách làm**:
     - Thêm **node `n8n-nodes-slack.slack`** hoặc **`n8n-nodes-telegram.telegram`**.
     - Gửi tin nhắn báo cáo sau khi hoàn thành.

2. **Lưu Log Lịch Sử**
   - Thêm **node `n8n-nodes-base.chronolog`** để lưu **lịch sử hoạt động** của workflow.
   - Giúp theo dõi **ai gửi hóa đơn**, **thời gian**, và **dữ liệu chi tiết**.

3. **Báo Cáo Định Kỳ (Tuần/Quý)**
   - Sử dụng **node `n8n-nodes-base.schedule`** để **gửi báo cáo tự động** vào cuối tháng/quý.
   - **Cấu hình**:
     - Thiết lập **lịch trình** (ví dụ: ngày 1 hàng tháng).
     - Gửi báo cáo qua **WhatsApp, Email, hoặc Slack**.

4. **Phân Loại Chi Phí Tự Động**
   - Sử dụng **node `n8n-nodes-base.code`** để **tự động phân loại chi phí** (ví dụ: "Ăn uống", "Điện thoại", "Xe cộ").
   - **Cách làm**:
     - Thêm **rule logic** trong node `Parse & Validate Expense` để **nhận diện danh mục** từ tên người bán hoặc nội dung hóa đơn.

5. **Xác Minh OTP Tự Động**
   - Nếu hóa đơn có **OTP xác minh**, thêm **node `n8n-nodes-base.httpRequest`** để gọi API xác minh và **gửi OTP lại** cho người dùng.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc **quét hóa đơn và nhập liệu thủ công**, đồng thời **tăng độ chính xác** nhờ AI GPT-4o. **Báo cáo tháng tự động** giúp quản lý tài chính trở nên **dễ dàng và minh bạch** hơn.

**Hành động ngay hôm nay!**
1. **Đăng ký WATI, OpenAI, và Google Sheets**.
2. **Import workflow** và **cấu hình credentials**.
3. **Test với một hóa đơn mẫu** và **bắt đầu tự động hóa quản lý chi phí!**

**🚀 Còn chần chừ gì nữa?** Hãy **tự động hóa ngay** và **tiết kiệm thời gian** cho công việc quan trọng hơn! 💼💰