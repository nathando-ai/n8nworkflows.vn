---
title: "🚀 Tự động phân loại & ghi log email đến bằng GPT‑4, Excel 365 & Telegram"
description: "Workflow n8n tự động đọc email, tóm tắt nội dung bằng GPT‑4, lưu vào Excel 365 và gửi thông báo Telegram – giảm 90% công việc thủ công."
slug: "tu-dong-phan-loai-ghi-log-email-gpt4-excel-telegram"
tags: [n8n, automation, no-code, email, AI, Excel, Telegram]
keywords: [n8n workflow, tự động hóa email, GPT-4, Excel 365, Telegram, AI summarization]
---

# 🚀 Tự động phân loại & ghi log email đến bằng GPT‑4, Excel 365 & Telegram

Doanh nghiệp ngày càng nhận được lượng email khối lượng lớn: yêu cầu hỗ trợ, ticket, báo cáo… Việc **đọc, tóm tắt, phân loại và lưu trữ** từng email một cách thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Các sếp thường phải mất hàng giờ mỗi ngày chỉ để cập nhật bảng theo dõi và thông báo cho các bộ phận liên quan.

**Workflow này** sẽ **đọc email tự động qua IMAP**, **sử dụng GPT‑4 tóm tắt nội dung**, **ghi lại vào Excel 365**, **xác định bộ phận liên quan** và **gửi thông báo Telegram ngay lập tức** – mọi thứ diễn ra 100 % không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý mọi email đến, không còn công việc nhập liệu thủ công.  
- **Độ chính xác cao**: GPT‑4 tóm tắt và phân loại nội dung dựa trên ngữ cảnh thực tế.  
- **Báo cáo ngay lập tức**: Thông báo Telegram cho bộ phận liên quan trong vòng vài giây.  
- **Lưu trữ có cấu trúc**: Dữ liệu được ghi vào Excel 365, dễ dàng phân tích và báo cáo.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản email** (IMAP) – Username, Password, IMAP host, Port.  
- **API Key OpenAI** (để gọi GPT‑4).  
- **Tài khoản Microsoft 365** – Excel file đã tạo, quyền chỉnh sửa, và **OAuth2 credentials** cho n8n.  
- **Bot Telegram** – Token và Chat ID (có thể là nhóm hoặc cá nhân).  
- **n8n** (cài đặt trên VPS hoặc n8n.cloud) với các credentials đã tạo sẵn.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (được cung cấp ở cuối README).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
   *Hoặc* copy toàn bộ nội dung JSON và dán vào **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và hướng dẫn cấu hình chi tiết:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **Email Trigger (IMAP)** | `emailReadImap` | - Chọn **Credentials** → **IMAP Account**.<br>- Điền **Host**, **Port**, **User**, **Password**.<br>- Đánh dấu **Mark as read** nếu muốn email được đánh dấu đã đọc sau khi xử lý. |
| **Extract Email Fields** | `set` | - Thêm các trường: `subject`, `from`, `body` (được lấy từ `{{$json["mail"]["subject"]}}` …).<br>- Đặt **Keep Only Set** để loại bỏ các trường không cần. |
| **Parse Summary** | `code` (JavaScript) | - Script sẽ gọi **Message a model** (node OpenAI) để tóm tắt nội dung.<br>- Đảm bảo **Input** là `body` và **Output** trả về `summary`. |
| **Message a model** | `openAi` (LangChain) | - Chọn **Credentials** → **OpenAI API**.<br>- Model: `gpt-4`.<br>- Prompt mẫu: <br>```text\nSummarize the email content in Vietnamese, highlight the main request and any required actions.\n``` |
| **Validate Department** | `if` | - Điều kiện: `{{$json["department"]}}` **exists** và **not empty**.<br>- True → tiếp tục tới **Send Notification**.<br>- False → có thể thêm **Sticky Note** để log lỗi. |
| **Lookup Department** | `microsoftExcel` | - **Operation**: `Read Rows`.<br>- **File**: Excel workbook chứa bảng “Departments”.<br>- **Range**: `A:B` (Department → Email).<br>- Dùng **Filter** để tìm bộ phận dựa trên từ khóa trong `subject`. |
| **Prepare Excel Row** | `set` | - Tạo các trường: `Date`, `From`, `Subject`, `Summary`, `Department`.<br>- Sử dụng **Expressions** như `{{$now}}` cho ngày hiện tại. |
| **Append rows to table** | `microsoftExcel` | - **Operation**: `Append Row`.<br>- Chọn **Workbook** và **Worksheet** (ví dụ: “Tickets”).<br>- Map các trường từ node **Prepare Excel Row**. |
| **Send email** | `emailSend` | - **From**: địa chỉ email công ty.<br>- **To**: `{{$json["departmentEmail"]}}` (kết quả từ Lookup).<br>- **Subject**: `Ticket: {{$json["subject"]}}`.<br>- **HTML Body**: chèn `summary` và link tới Excel nếu cần. |
| **Send Notification** | `telegram` | - **Credentials**: Bot Token.<br>- **Chat ID**: ID nhóm hoặc cá nhân.<br>- **Message**: `New ticket from {{$json["from"]}} – {{$json["summary"]}}`. |
| **Sticky Note** | `stickyNote` | - Dùng để ghi chú lỗi hoặc thông tin debug (không ảnh hưởng tới luồng). |

> **Lưu ý:** Sau khi import, **đừng quên** thay thế tất cả các placeholder (`<YOUR_...>`) bằng thông tin thực tế của các credentials và file Excel của bạn.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhập một email mẫu vào hộp thư và chạy workflow ở chế độ **Execute Workflow**. Kiểm tra:
   - Summary được tạo trong node **Parse Summary**.  
   - Dòng mới xuất hiện trong Excel.  
   - Thông báo Telegram nhận được.  
2. Khi mọi thứ ổn, bật **Active** (nút toggle ở góc trên bên phải) để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: Dùng node Slack để gửi thông báo song song với Telegram.  
- **Lưu log chi tiết**: Kết nối node **Code** để ghi log vào Google Sheets hoặc một file CSV trên S3.  
- **Báo cáo định kỳ**: Tạo workflow thứ hai chạy hàng ngày, tổng hợp số ticket mới và gửi báo cáo PDF qua email.  
- **Phân loại nâng cao**: Sử dụng **OpenAI Function Calling** để trả về trường `department` trực tiếp từ GPT‑4, giảm nhu cầu lookup Excel.

### 📌 Kết luận
Với workflow này, các sếp sẽ **giải phóng thời gian**, **đảm bảo dữ liệu luôn chính xác** và **nhận thông báo ngay lập tức** khi có email quan trọng. Hãy triển khai ngay trên môi trường n8n của mình, tùy chỉnh các trường và credentials cho phù hợp, và cảm nhận sức mạnh của tự động hóa AI!

---

#### 📥 File JSON workflow (để import)
```json
{
  "nodes": [
    {
      "parameters": {
        "imapHost": "<IMAP_HOST>",
        "imapPort": 993,
        "secure": true,
        "email": "<EMAIL_ADDRESS>",
        "password": "<EMAIL_PASSWORD>",
        "mailbox": "INBOX",
        "markAsRead": true,
        "options": {}
      },
      "name": "Email Trigger (IMAP)",
      "type": "n8n-nodes-base.emailReadImap",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "keepOnlySet": true,
        "set": [
          {
            "name": "subject",
            "value": "={{$json[\"mail\"][\"subject\"]}}"
          },
          {
            "name": "from",
            "value": "={{$json[\"mail\"][\"from\"][\"address\"]}}"
          },
          {
            "name": "body",
            "value": "={{$json[\"mail\"][\"text\"]}}"
          }
        ]
      },
      "name": "Extract Email Fields",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [500, 300]
    },
    {
      "parameters": {
        "functionCode": "const emailBody = $json[\"body\"];\nreturn [{ json: { body: emailBody } }];"
      },
      "name": "Parse Summary",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [750, 300]
    },
    {
      "parameters": {
        "operation": "append",
        "sheetId": "<EXCEL_SHEET_ID>",
        "range": "Tickets!A:E",
        "valueInputOption": "RAW",
        "values": [
          [
            "={{$now}}",
            "={{$json[\"from\"]}}",
            "={{$json[\"subject\"]}}",
            "={{$json[\"summary\"]}}",
            "={{$json[\"department\"]}}"
          ]
        ]
      },
      "name": "Append rows to table",
      "type": "n8n-nodes-base.microsoftExcel",
      "typeVersion": 1,
      "position": [1250, 300]
    },
    {
      "parameters": {
        "keepOnlySet": true,
        "set": [
          {
            "name": "date",
            "value": "={{$now}}"
          },
          {
            "name": "from",
            "value": "={{$json[\"from\"]}}"
          },
          {
            "name": "subject",
            "value": "={{$json[\"subject\"]}}"
          },
          {
            "name": "summary",
            "value": "={{$json[\"summary\"]}}"
          },
          {
            "name": "department",
            "value": "={{$json[\"department\"]}}"
          }
        ]
      },
      "name": "Prepare Excel Row",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [1000, 300]
    },
    {
      "parameters": {
        "fromEmail": "<FROM_EMAIL>",
        "toEmail": "={{$json[\"departmentEmail\"]}}",
        "subject":