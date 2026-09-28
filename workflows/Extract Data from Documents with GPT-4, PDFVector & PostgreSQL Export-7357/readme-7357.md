---
title: "🚀 Tự động trích xuất dữ liệu từ PDF, hợp đồng, báo cáo bằng GPT‑4 & PDFVector → PostgreSQL"
description: "Workflow n8n giúp đọc tài liệu PDF/Word, chuyển thành dữ liệu có cấu trúc bằng GPT‑4, lưu vào PostgreSQL và xuất CSV chỉ trong vài giây."
slug: "tu-dong-trich-xuat-du-lieu-pdf-gpt4-pdfvector"
tags: [n8n, automation, no-code, pdf, openai, postgres]
keywords: [n8n workflow, tự động hóa, trích xuất PDF, GPT-4, PDFVector, PostgreSQL]
---

# 🚀 Tự động trích xuất dữ liệu từ PDF, hợp đồng, báo cáo bằng GPT‑4 & PDFVector → PostgreSQL

Bạn đã bao giờ phải mở hàng loạt file PDF, hợp đồng, báo cáo, rồi sao chép từng dòng dữ liệu vào bảng tính hay hệ thống ERP?  
Việc này vừa tốn thời gian, vừa dễ gây lỗi nhập liệu, còn làm giảm năng suất của đội ngũ.  

**Workflow này** sẽ giải quyết toàn bộ quy trình **từ lúc nhận file, phân tích nội dung bằng AI, làm sạch dữ liệu, phân loại tự động và lưu trữ vào PostgreSQL** – **không cần viết một dòng code nào**.  

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng chục tài liệu trong giây lát, thay vì giờ đồng hồ.  
- **Độ chính xác cao**: GPT‑4 + PDFVector giảm thiểu lỗi nhập liệu so với việc nhập tay.  
- **Tự động phân loại**: Hóa đơn, hợp đồng, báo cáo, mẫu đơn được lưu vào bảng riêng ngay lập tức.  
- **Hoạt động liên tục 24/7**: Khi có file mới trong thư mục, workflow tự động khởi chạy.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **PDFVector API Key** – đăng ký tại https://pdfvector.com và tạo API key.  
- **OpenAI API Key** – có quyền truy cập model `gpt-4`.  
- **PostgreSQL database** – URL, database name, user, password, và 2 bảng (`invoices`, `other_documents`).  
- **Thư mục giám sát** – `/documents/incoming` trên server chạy n8n (có quyền đọc/ghi).  
- **n8n** – phiên bản mới nhất, đã cài các node: PDFVector, OpenAI, PostgreSQL, Write Binary File.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n > Workflows > Import**.  
2. Tải file JSON của workflow (được cung cấp ở cuối README) hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard**.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần thay đổi | Hướng dẫn chi tiết |
|------|----------------------|--------------------|
| **Watch Folder** | `Path` | Đặt đường dẫn tới thư mục chứa tài liệu mới (mặc định: `/documents/incoming`). Đảm bảo n8n có quyền truy cập. |
| **PDF Vector - Parse Document** | `Operation` = *parse*<br>`Resource` = *document*<br>`API Key` | Chọn **Credentials → PDFVector API** → dán API key đã tạo. Đặt `File` = `{{$json["binary"]["data"]["file"]}}` (được truyền từ node Watch Folder). |
| **Extract Structured Data** (OpenAI) | `Model` = *gpt-4*<br>`Prompt` | Sử dụng prompt mẫu (có trong sticky note trên canvas) hoặc tùy chỉnh: <br>```text\nBạn là một chuyên gia trích xuất dữ liệu. Hãy trả về JSON có các trường: invoice_number, date, total_amount, vendor_name, ... dựa trên nội dung tài liệu.\n``` |
| **Validate & Clean Data** (Code) | JavaScript code | Kiểm tra JSON trả về, loại bỏ trường null, chuẩn hoá ngày (`YYYY-MM-DD`) và tiền tệ. Nếu dữ liệu không hợp lệ, `throw new Error('Invalid data')`. |
| **Route by Document Type** (Switch) | `Value` = `{{$json["type"]}}` | Thêm 2 case: **Invoice** → đi tới node *Store Invoice Data*; **Other** → đi tới node *Store Other Documents*. |
| **Store Invoice Data** (Postgres) | `Credentials` → PostgreSQL<br>`Table` = `invoices`<br>`Columns` | Map các trường JSON tới cột bảng (invoice_number → invoice_number, date → invoice_date, …). |
| **Store Other Documents** (Postgres) | `Credentials` → PostgreSQL<br>`Table` = `other_documents` | Map toàn bộ JSON (type, extracted_fields, raw_text) vào các cột tương ứng. |
| **Export to CSV** (Write Binary File) | `File Name` = `extracted_{{$now}}.csv`<br>`Data` = `{{$json["csv"]}}` | Đảm bảo node trước (thường là một **Set** hoặc **Function**) tạo chuỗi CSV hợp lệ. File sẽ được lưu trong thư mục `./exports`. |

> **Lưu ý:** Mỗi node **Credentials** phải được tạo trước trong **n8n > Credentials**. Đừng quên bật **"Allow self‑signed certificates"** nếu bạn dùng DB nội bộ.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** → chọn **Run Once** để kiểm tra với một file mẫu.  
2. Kiểm tra log của từng node, chắc chắn dữ liệu được lưu vào PostgreSQL và file CSV xuất ra.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi góc trên bên phải) để workflow tự động chạy khi có file mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau mỗi lưu thành công để báo cho bộ phận kế toán.  
- **Lưu log chi tiết**: Dùng node **Postgres** hoặc **MongoDB** để ghi lại toàn bộ payload, giúp debug nhanh khi có lỗi.  
- **Xử lý đa ngôn ngữ**: Thêm `language` vào prompt và dùng `detect-language` của OpenAI để tự động chuyển ngữ.  
- **Tự động xóa file gốc**: Sau khi xuất CSV, dùng node **Delete File** (n8n‑node‑filesystem) để dọn dẹp thư mục `/incoming`.  

### 📌 Kết luận
Với workflow **“Extract Data from Documents with GPT‑4, PDFVector & PostgreSQL Export”**, các sếp có thể biến **đống tài liệu rải rác** thành **dữ liệu sạch, có cấu trúc và sẵn sàng phân tích** chỉ trong vài giây. Hãy triển khai ngay hôm nay, giảm tải công việc nhập liệu và tăng tốc độ ra quyết định!  

---  

**File JSON của workflow** (copy toàn bộ nội dung dưới đây và import vào n8n):

```json
{
  "nodes": [
    {
      "parameters": {
        "path": "/documents/incoming"
      },
      "name": "Watch Folder",
      "type": "n8n-nodes-base.localFileTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "operation": "parse",
        "resource": "document",
        "fileBinaryPropertyName": "data"
      },
      "name": "PDF Vector - Parse Document",
      "type": "n8n-nodes-pdfvector.pdfVector",
      "typeVersion": 1,
      "position": [
        500,
        300
      ],
      "credentials": {
        "pdfVectorApi": "PDFVector API"
      }
    },
    {
      "parameters": {
        "model": "gpt-4",
        "messages": [
          {
            "role": "system",
            "content": "You are a data extraction expert. Return a JSON with fields: invoice_number, date, total_amount, vendor_name, contract_id, etc."
          },
          {
            "role": "user",
            "content": "{{$node[\"PDF Vector - Parse Document\"].json[\"text\"]}}"
          }
        ]
      },
      "name": "Extract Structured Data",
      "type": "n8n-nodes-base.openAi",
      "typeVersion": 1,
      "position": [
        750,
        300
      ],
      "credentials": {
        "openAiApi": "OpenAI API"
      }
    },
    {
      "parameters": {
        "functionCode": "const data = $json;\n// Clean & validate\nif (!data.invoice_number) throw new Error('Missing invoice number');\n// Example: format date\nif (data.date) {\n  const d = new Date(data.date);\n  data.date = d.toISOString().split('T')[0];\n}\nreturn [{ json: data }];"
      },
      "name": "Validate & Clean Data",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        1000,
        300
      ]
    },
    {
      "parameters": {
        "value": "={{$json[\"type\"]}}",
        "rules": [
          {
            "operation": "equal",
            "value": "Invoice"
          },
          {
            "operation": "equal",
            "value": "Other"
          }
        ]
      },
      "name": "Route by Document Type",
      "type": "n8n-nodes-base.switch",
      "typeVersion": 1,
      "position": [
        1250,
        300
      ]
    },
    {
      "parameters": {
        "operation": "insert",
        "table": "invoices",
        "columns": [
          {
            "name": "invoice_number",
            "value": "={{$json[\"invoice_number\"]}}"
          },
          {
            "name": "invoice_date",
            "value": "={{$json[\"date\"]}}"
          },
          {
            "name": "total_amount",
            "value": "={{$json[\"total_amount\"]}}"
          },
          {
            "name": "vendor_name",
            "value": "={{$json[\"vendor_name\"]}}"
          }
        ]
      },
      "name": "Store Invoice Data",
      "type": "n8n-nodes-base.postgres",
      "typeVersion": 1,
      "position": [
        1500,
        200
      ],
      "credentials": {
        "postgres": "PostgreSQL DB"
      }
    },
    {
      "parameters": {
        "operation": "insert",
        "table": "other_documents",
        "columns": [
          {
            "name": "doc_type",
            "value": "={{$json[\"type\"]}}"
          },
          {
            "name": "content",
            "value": "={{$json[\"text\"]}}"
          },
          {
            "name": "extracted_json",
            "value": "={{JSON.stringify