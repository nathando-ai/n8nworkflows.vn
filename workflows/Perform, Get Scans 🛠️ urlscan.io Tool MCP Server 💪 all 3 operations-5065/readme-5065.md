---
title: "🚀 Tự Động Hóa Quét URL Bằng URLScan.io - Giúp Các Sếp Phát Hiện Threat Online Miễn Chi Phí & 24/7"
description: "Workflow này tự động hóa việc quét URL, lấy kết quả scan và quản lý danh sách URL cần theo dõi trên URLScan.io - giải pháp an ninh mạng không cần code. Các sếp có thể phát hiện các mối đe dọa như malware, phishing, hoặc nội dung độc hại ngay lập tức."
slug: "tu-dong-hoa-quet-url-bang-urlscan-io"
tags: [n8n, automation, urlscan.io, an-ninh-mang, no-code, ai-security]
keywords: [n8n workflow urlscan, tự động hóa quét URL, phát hiện malware, an ninh mạng không code, urlscan.io automation]
---

# 🚀 **Tự Động Hóa Quét URL & Quản Lý Scan Bằng URLScan.io - Bảo Vệ Mạng Miễn Chi Phí**

Hiện nay, với sự phát triển của internet, các sếp thường phải đối mặt với rủi ro từ các URL độc hại như malware, phishing, hoặc nội dung vi phạm chính sách nội bộ. Thao tác quét URL thủ công không chỉ tốn thời gian mà còn dễ bị bỏ quên, dẫn đến nguy cơ bị tấn công. **Workflow này giúp tự động hóa toàn bộ quy trình quét URL, lấy kết quả scan và quản lý danh sách URL một cách hiệu quả, không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính bảo mật và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét URL thủ công, workflow tự động thực hiện mọi việc trong vài giây.
- **Phát hiện threat tức thời**: Nhận kết quả scan ngay lập tức qua email, Slack, hoặc Telegram.
- **Quản lý danh sách URL**: Tự động lấy và lưu trữ kết quả scan của nhiều URL trong một lần chạy.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc của các sếp.
- **Không cần code**: Dễ dàng tùy chỉnh và mở rộng với giao diện drag-and-drop của n8n.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản URLScan.io**:
   - Đăng ký tại [URLScan.io](https://urlscan.io/) và lấy **API Key** từ trang cá nhân.
   - [Hướng dẫn lấy API Key](https://urlscan.io/api#authentication).
2. **Danh sách URL cần quét** (có thể là danh sách từ file CSV, Google Sheets, hoặc input từ webhook).
3. **N8n Self-hosted** (để workflow chạy liên tục).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/5065) hoặc sử dụng mã JSON dưới đây:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "MCP Server",
        "type": "mcpTrigger",
        "typeVersion": 1,
        "position": [
          200,
          300
        ]
      },
      {
        "parameters": {
          "operation": "getScan"
        },
        "name": "Get a scan",
        "type": "urlScanIoTool",
        "typeVersion": 1,
        "position": [
          400,
          300
        ],
        "credentials": {
          "urlscanIoToolApiKey": "your-api-key-here"
        }
      },
      {
        "parameters": {
          "operation": "getScans"
        },
        "name": "Get many scans",
        "type": "urlScanIoTool",
        "typeVersion": 1,
        "position": [
          400,
          500
        ],
        "credentials": {
          "urlscanIoToolApiKey": "your-api-key-here"
        }
      },
      {
        "parameters": {
          "operation": "performScan"
        },
        "name": "Perform a scan",
        "type": "urlScanIoTool",
        "typeVersion": 1,
        "position": [
          600,
          300
        ],
        "credentials": {
          "urlscanIoToolApiKey": "your-api-key-here"
        }
      }
    ],
    "connections": {
      "MCP Server": [
        {
          "node": "Get a scan",
          "type": "main",
          "position": 0
        },
        {
          "node": "Get many scans",
          "type": "main",
          "position": 1
        },
        {
          "node": "Perform a scan",
          "type": "main",
          "position": 2
        }
      ]
    }
  }
  ```
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô **Import Workflow**.
  - **Không quên thay thế `your-api-key-here` bằng API Key thực tế của URLScan.io!**

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần cấu hình như sau:

| **Node**                     | **Loại Node**               | **Cấu hình cần thiết**                                                                 | **Lưu ý**                                                                                     |
|------------------------------|-----------------------------|---------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| **MCP Server**               | `mcpTrigger`                | Không cần cấu hình thêm, node này kích hoạt các node khác.                          | Nếu muốn kích hoạt thủ công, các sếp có thể sử dụng **Webhook** hoặc **Schedule Trigger**. |
| **Get a scan**               | `urlScanIoTool`             | - **Operation**: `getScan` (đã mặc định).                                            | Sử dụng để lấy kết quả scan của một URL cụ thể.                                               |
| **Get many scans**           | `urlScanIoTool`             | - **Operation**: `getScans` (đã mặc định).                                             | Sử dụng để lấy kết quả scan của **nhiều URL** trong một lần gọi API.                          |
| **Perform a scan**           | `urlScanIoTool`             | - **Operation**: `performScan` (đã mặc định).                                           | Sử dụng để **quét URL mới** và lấy kết quả tức thời.                                           |

##### **Cách cấu hình API Key**:
1. Vào **Credentials** trong n8n Editor.
2. Tạo một **new credential** với loại `urlscanIoToolApiKey`.
3. Nhập **API Key** từ URLScan.io vào trường `apiKey`.
4. Gán credential này cho **tất cả 3 node** `urlScanIoTool` trong workflow.

##### **Cách cung cấp danh sách URL**:
- **Lựa chọn 1**: Sử dụng **Webhook** để gửi danh sách URL từ bên ngoài (ví dụ: từ Google Sheets, API, hoặc form).
- **Lựa chọn 2**: Sử dụng **Schedule Trigger** để chạy workflow định kỳ (ví dụ: hàng ngày).
- **Lựa chọn 3**: Sử dụng **Set Node** để hardcode danh sách URL trong workflow (không khuyến nghị cho danh sách lớn).

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và kiểm tra kết quả trong **Execution View**.
   - Đảm bảo kết quả scan được trả về đúng định dạng (JSON).
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Sau khi quét xong, gửi kết quả scan qua **Slack** hoặc **Telegram** để các sếp được thông báo tức thời.
   - Sử dụng node **Slack** hoặc **Telegram Bot** để tự động gửi thông báo.

2. **Lưu log vào Google Sheets/Database**:
   - Sử dụng node **Google Sheets** hoặc **Database** để lưu trữ lịch sử scan và kết quả.
   - Có thể tạo báo cáo định kỳ để theo dõi các URL nguy hiểm.

3. **Tự động quét URL mới từ nguồn dữ liệu**:
   - Nếu các sếp có danh sách URL từ **Google Drive**, **CSV**, hoặc **API**, có thể sử dụng node **File System** hoặc **HTTP Request** để tự động lấy danh sách và quét.

4. **Bộ lọc kết quả scan**:
   - Sử dụng **Function Node** để lọc các URL có kết quả scan **dangerous** hoặc **malicious** và gửi thông báo ưu tiên.

5. **Sử dụng Schedule Trigger**:
   - Đặt workflow chạy tự động hàng ngày/lần tuần bằng **Schedule Trigger** để không bỏ lỡ bất kỳ URL nào.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc quét URL và phát hiện threat online một cách hiệu quả. Với **không cần viết code**, các sếp có thể yên tâm rằng hệ thống sẽ hoạt động 24/7, bảo vệ mạng an toàn khỏi các mối đe dọa tiềm ẩn.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình API Key.
3. **Kích hoạt và bắt đầu quét URL** để bảo vệ mạng của doanh nghiệp!

Nếu có bất kỳ câu hỏi hoặc cần hỗ trợ, các sếp có thể liên hệ với **David Ashby** (tác giả workflow) qua [Github](https://github.com/davidashby) hoặc [Discord](https://discord.gg/n8n). 🚀

---
**Chúc các sếp thành công với việc tự động hóa an ninh mạng!** 🔒💻