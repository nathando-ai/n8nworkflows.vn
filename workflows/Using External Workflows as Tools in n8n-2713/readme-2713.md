---
title: "🚀 Sử dụng Workflow Ngoài làm Công Cụ trong n8n – Tự Động Crawl & Gửi URL"
description: "Kết nối nhanh workflow nội bộ với các AI Agent hoặc Workspace khác để crawl website và trả về URL, không cần viết code."
slug: "su-dung-workflow-ngoai-trong-n8n"
tags: [n8n, automation, no-code, AI, integration]
keywords: [n8n workflow, tự động hóa, external workflow, AI agents, HTTP request, crawl website]
---

# 🚀 Sử dụng Workflow Ngoài làm Công Cụ trong n8n – Tự Động Crawl & Gửi URL

Khi các doanh nghiệp muốn tích hợp **công cụ crawl** vào quy trình AI Agent hoặc các workspace khác, thường phải viết đoạn code riêng, duy trì server, và xử lý lỗi phức tạp. Điều này gây tốn thời gian, tăng chi phí và dễ mắc lỗi khi thay đổi yêu cầu.

**Workflow “Using External Workflows as Tools in n8n”** giải quyết vấn đề này 100 % **không cần code**: chỉ cần gửi một JSON chứa `url` tới workflow, n8n sẽ tự động gọi dịch vụ Crawl (FireCrawl), xử lý kết quả và trả về cho bất kỳ AI Agent nào. Các sếp có thể tái sử dụng ngay trong các dự án AI, chatbot, hoặc hệ thống nội bộ mà không lo về hạ tầng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết script crawl, chỉ gửi URL.
- **Độ chính xác cao**: Dựa trên API FireCrawl đã được tối ưu.
- **Tích hợp liền mạch**: Dùng làm “tool” cho bất kỳ AI Agent hay workspace nào.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên server riêng, không gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self‑hosted hoặc Cloud) với quyền tạo workflow.
- **API Key của FireCrawl** (được lưu dưới credentials `httpHeaderAuth`).
- **Credential “Execute Workflow Trigger”** nếu muốn gọi workflow từ workflow khác.
- **Kết nối internet ổn định** để gọi API bên ngoài.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON của workflow (được cung cấp ở cuối README) hoặc **Copy/Paste** nội dung JSON vào ô import.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần chỉnh |
|------|-----------|--------------------|
| **Execute Workflow Trigger** | Đóng vai “công cụ” để nhận request từ bên ngoài. | - Đặt **Workflow ID** của workflow hiện tại (để các workflow khác gọi). <br> - Chọn **Credential** nếu cần xác thực (ví dụ: API Key nội bộ). |
| **FireCrawl** (httpRequest) | Gửi yêu cầu crawl tới API FireCrawl. | - **Method**: `POST` <br> - **URL**: `https://api.firecrawl.dev/v0/crawl` (hoặc endpoint bạn dùng). <br> - **Headers**: Thêm `Authorization: Bearer <YOUR_FIRECRAWL_API_KEY>` – chọn credential `httpHeaderAuth`. <br> - **Body (JSON)**: <br>```json { "url": "{{$json[\"url\"]}}" }``` <br>  (sử dụng biểu thức để lấy URL từ request đầu vào). |
| **Edit Fields** (set) | Định dạng lại dữ liệu trả về cho AI Agent. | - Thêm **Field**: `crawledUrl` → `{{$json["data"]["url"]}}` (hoặc trường trả về thực tế). <br> - Nếu muốn trả về toàn bộ payload, thêm trường `result` → `{{$json}}`. |
| **Sticky Note** (không bắt buộc) | Ghi chú hướng dẫn cho người dùng cuối. | - Đảm bảo nội dung “Send URL got Crawl” vẫn hiện trên canvas để các sếp biết cách gọi. |

> **Lưu ý:** Đảm bảo **Credentials** được gán đúng cho node `FireCrawl`. Nếu credential chưa tạo, vào **Credentials → New Credential → HTTP Header Auth**, nhập `Authorization` và giá trị `Bearer <API_KEY>`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Sử dụng **Execute Workflow Trigger** → **Run Node** → nhập JSON mẫu:  
   ```json
   {
     "url": "https://example.com"
   }
   ```  
   Kiểm tra log để chắc chắn API trả về và `Edit Fields` định dạng đúng.
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow luôn sẵn sàng nhận yêu cầu.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `Edit Fields` để tự động gửi link đã crawl cho kênh nhóm.
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại `url`, `status`, `timestamp` cho mục đích audit.
- **Báo cáo định kỳ**: Kết hợp `Cron` + `HTTP Request` để tự động crawl danh sách URL mỗi ngày và gửi báo cáo qua email.
- **Xử lý lỗi**: Thêm node `Error Trigger` để gửi thông báo khi API FireCrawl trả về lỗi (rate‑limit, invalid URL, …).

### 📌 Kết luận
Với workflow này, các sếp có thể **biến n8n thành một công cụ “service”** cho mọi AI Agent hoặc workspace nội bộ chỉ bằng một lời gọi HTTP. Không cần viết code, không cần duy trì server riêng cho crawler – mọi thứ đã được gói gọn trong một workflow ngắn gọn, dễ mở rộng và an toàn.

Hãy **import ngay**, cấu hình API Key, và bắt đầu tự động crawl mọi URL trong vòng vài phút! 🚀

---  

**File JSON để import** (copy toàn bộ nội dung dưới đây và lưu thành `using-external-workflows.json`):

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "Execute Workflow Trigger",
      "type": "n8n-nodes-base.executeWorkflowTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "url": "https://api.firecrawl.dev/v0/crawl",
        "method": "POST",
        "jsonParameters": true,
        "options": {},
        "bodyParametersJson": "={\"url\": $json[\"url\"]}"
      },
      "name": "FireCrawl",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        500,
        300
      ],
      "credentials": {
        "httpHeaderAuth": "FireCrawl API Key"
      }
    },
    {
      "parameters": {
        "values": {
          "string": [
            {
              "name": "crawledUrl",
              "value": "={{$json[\"data\"][\"url\"]}}"
            }
          ]
        },
        "options": {}
      },
      "name": "Edit Fields",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [
        750,
        300
      ]
    },
    {
      "parameters": {
        "text": "## Send URL got Crawl\nThis can be reused by Ai Agents and any Workspace to crawl a site. All that Workspace has to do is send a request:\n\n```json\n {\n    \"url\": \"Some URL to Get\"\n  }\n```"
      },
      "name": "Sticky Note",
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        250,
        150
      ]
    }
  ],
  "connections": {
    "Execute Workflow Trigger": {
      "main": [
        [
          {
            "node": "FireCrawl",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "FireCrawl": {
      "main": [
        [
          {
            "node": "Edit Fields",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {},
  "id": "1"
}
```