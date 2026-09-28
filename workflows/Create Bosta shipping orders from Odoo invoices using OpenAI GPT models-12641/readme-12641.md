---
title: "🚀 Tự động tạo đơn vận chuyển Bosta từ hoá đơn Odoo bằng AI GPT"
description: "Giải pháp không-code, dùng n8n + OpenAI GPT để chuyển dữ liệu hoá đơn Odoo thành đơn Bosta chỉ trong vài giây, giảm lỗi và tăng tốc độ giao hàng."
slug: "tu-dong-tao-don-van-chuyen-bosta-tu-odoo-bang-ai-gpt"
tags: [n8n, automation, no-code, Odoo, Bosta, OpenAI]
keywords: [n8n workflow, tự động hóa, Odoo, Bosta, OpenAI GPT, tạo đơn vận chuyển]
---

# 🚀 Tự động tạo đơn vận chuyển Bosta từ hoá đơn Odoo bằng AI GPT

Doanh nghiệp thường phải **nhập tay** thông tin hoá đơn Odoo vào hệ thống Bosta để tạo đơn vận chuyển. Quy trình này không chỉ tốn thời gian mà còn dễ gây lỗi nhập liệu, làm chậm quá trình giao hàng và ảnh hưởng đến trải nghiệm khách hàng.  

**Workflow n8n** này sẽ **tự động**:
1. Nhận hoá đơn mới từ Odoo qua webhook.  
2. Dùng **OpenAI GPT** (LangChain) để phân tích và chuyển đổi dữ liệu hoá đơn thành định dạng yêu cầu của API Bosta.  
3. Gửi yêu cầu tạo đơn Bosta qua **HTTP Request**.  
4. Thông báo kết quả ngay trên **Telegram** và lưu log vào **DataTable** để theo dõi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với nhập tay.  
- **Giảm lỗi nhập liệu** gần như 0% nhờ AI chuẩn hoá dữ liệu.  
- **Giao hàng nhanh hơn** vì đơn được tạo ngay khi hoá đơn xuất.  
- **Theo dõi toàn bộ lịch sử** tạo đơn qua DataTable, dễ audit.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Odoo** (API URL, Access Token).  
- **API Key OpenAI** (có quyền sử dụng GPT‑3.5/4).  
- **API Key Bosta** (Bearer token).  
- **Bot Telegram** và **Chat ID** để nhận thông báo.  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- (Tùy chọn) **DataTable** đã tạo sẵn để lưu log.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Editor.  
2. Click **Import** → **Upload JSON** và chọn file `bosta-from-odoo.json` (được cung cấp ở cuối bài viết) **hoặc** copy toàn bộ JSON và dán vào ô **Paste JSON** → **Import**.  
3. Workflow sẽ xuất hiện trong danh sách, đặt tên lại nếu muốn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **Webhook** | Nhận payload hoá đơn từ Odoo (hoặc webhook Odoo). | - **HTTP Method**: `POST` <br> - **Path**: `/odoo/invoice` (có thể tùy chỉnh). |
| **Odoo** | Lấy chi tiết hoá đơn dựa trên `invoice_id`. | - Chọn **Credential** Odoo của bạn. <br> - **Operation**: `Get` <br> - **Resource**: `Invoice` <br> - **Invoice ID**: `{{$json["invoice_id"]}}`. |
| **Set** (Prepare Data) | Định dạng lại dữ liệu (tên khách, địa chỉ, trọng lượng...). | - Đặt các trường: `customer_name`, `address`, `city`, `postal_code`, `weight`, `value`, … |
| **Code** (Prompt Builder) | Tạo prompt cho GPT: “Convert the following Odoo invoice data …”. | - Thêm đoạn code JavaScript để ghép chuỗi prompt, ví dụ: <br>```js\nreturn {prompt: `Create Bosta order from: ${JSON.stringify($json)}`};``` |
| **LangChain → LLM Chat OpenAI** | Gọi GPT để sinh JSON yêu cầu Bosta. | - Chọn **Credential** OpenAI. <br> - **Model**: `gpt-3.5-turbo` hoặc `gpt-4`. <br> - **Prompt**: `{{$node["Code"].json["prompt"]}}`. |
| **HTTP Request** (Bosta API) | Gửi yêu cầu POST tới `https://api.bosta.co/v1/orders`. | - **Authentication**: Bearer Token (Bosta API Key). <br> - **Body**: `{{$node["LangChain"].json["response"]}}` (đảm bảo là JSON hợp lệ). |
| **Telegram** | Thông báo kết quả tạo đơn cho bộ phận logistics. | - Chọn **Credential** Bot Telegram. <br> - **Chat ID**: ID nhóm/kênh. <br> - **Message**: `✅ Đơn Bosta đã tạo: {{ $json["order_id"] }}` hoặc thông báo lỗi. |
| **DataTable** | Lưu log chi tiết vào bảng. | - Chọn **Credential** DataTable. <br> - **Table ID**: `bosta_orders_log`. <br> - **Columns**: `order_id`, `invoice_id`, `status`, `created_at`. |
| **Sticky Note** | Ghi chú hướng dẫn nhanh cho người dùng. | Không cần cấu hình, chỉ để hiển thị thông tin. |

> **Lưu ý:** Đảm bảo **JSON trả về từ GPT** đúng định dạng Bosta API (có các trường `recipient`, `address`, `weight`, `value`, …). Nếu có lỗi, chỉnh lại prompt trong node **Code** hoặc **LLM Chat OpenAI**.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một payload mẫu từ Postman hoặc curl tới webhook (`POST /odoo/invoice`). Kiểm tra log từng node, đặc biệt node **LLM Chat OpenAI** và **HTTP Request**.  
2. Khi mọi thứ hoạt động ổn, bật **Active** ở góc phải của workflow.  
3. Đặt **Cron** (nếu muốn tự động pull hoá đơn) hoặc để Odoo push tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack**: Thêm node Slack để gửi thông báo song song với Telegram.  
- **Retry & Error Handling**: Dùng node **Error Trigger** + **Set** để lưu lỗi vào DataTable và gửi báo cáo qua email.  
- **Batch Processing**: Thêm vòng lặp (SplitInBatches) để xử lý nhiều hoá đơn cùng lúc, giảm thời gian chờ.  
- **Dashboard**: Kết nối DataTable với Google Data Studio hoặc Grafana để theo dõi KPI (số đơn tạo, thời gian trung bình).  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình** từ hoá đơn Odoo tới đơn vận chuyển Bosta chỉ trong vài giây, giảm chi phí nhân lực, tăng độ chính xác và nâng cao trải nghiệm khách hàng. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc cho bạn!

---  

**File JSON workflow** (copy toàn bộ nội dung dưới đây và lưu thành `bosta-from-odoo.json`):

```json
{
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "odoo/invoice",
        "responseMode": "onReceived"
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "operation": "get",
        "resource": "invoice",
        "invoiceId": "={{$json[\"invoice_id\"]}}"
      },
      "name": "Odoo Get Invoice",
      "type": "n8n-nodes-base.odoo",
      "typeVersion": 1,
      "position": [500, 300],
      "credentials": {
        "odooApi": "Odoo Account"
      }
    },
    {
      "parameters": {
        "values": {
          "string": [
            {
              "name": "customer_name",
              "value": "={{$json[\"partner_id\"][1]}}"
            },
            {
              "name": "address",
              "value": "={{$json[\"partner_id\"][2].street}}"
            },
            {
              "name": "city",
              "value": "={{$json[\"partner_id\"][2].city}}"
            },
            {
              "name": "postal_code",
              "value": "={{$json[\"partner_id\"][2].zip}}"
            },
            {
              "name": "weight",
              "value": "={{$json[\"weight\"] || 1}}"
            },
            {
              "name": "value",
              "value": "={{$json[\"amount_total\"]}}"
            },
            {
              "name": "invoice_id",
              "value": "={{$json[\"id\"]}}"
            }
          ]
        }
      },
      "name": "Set Invoice Data",
      "type": "n8n-nodes-base.set",
      "typeVersion": 2,
      "position": [750, 300]
    },
    {
      "parameters": {
        "functionCode": "return [{ json: { prompt: `Create a Bosta order JSON from the following Odoo invoice data:\\n${JSON.stringify($json, null, 2)}` } }];"
      },
      "name": "Code – Prompt Builder",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [1000, 300]
    },
    {
      "parameters": {
        "model": "gpt-3.5-turbo",
        "messages": [
          {
            "role": "system",
            "content": "You are an assistant that converts Odoo invoice data into a Bosta order JSON. Return ONLY the JSON object."
          },
          {
            "role": "user",
            "content": "={{$node[\"Code – Prompt Builder\"].json[\"prompt\"]}}"
          }
        ],
        "temperature": 0.2,
        "maxTokens": 500
      },
      "name": "LLM Chat OpenAI",
      "type": "n8n-nodes-base.lmChatOpenAi",
      "typeVersion": 1,
      "position": [1250, 300],
      "credentials": {
        "openAiApi": "OpenAI API"
      }
    },
    {
      "parameters": {
        "url": "https://api.bosta.co/v1/orders",
        "method": "POST",
        "jsonParameters": true,
        "options": {},
        "bodyParametersJson": "={{$node[\"LLM Chat OpenAI\"].json[\"content\"]}}"
      },
      "name": "HTTP Request – Bosta",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 2,
      "position": [1500, 300],
      "credentials": {
        "httpBasicAuth": "Bosta API"
      }
    },
    {
      "parameters": {
        "chatId": "=-123456789",
        "text": "✅ Đơn Bosta đã tạo thành công! Order ID: {{ $json[\"order_id\"] }} – Hoá đơn Odoo: {{ $json[\"invoice_id\"] }}",
        "parseMode": "HTML"
      },
      "name": "Telegram – Notify",
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1,
      "position": [1750, 300],
      "credentials": {
        "telegramApi": "Telegram Bot"