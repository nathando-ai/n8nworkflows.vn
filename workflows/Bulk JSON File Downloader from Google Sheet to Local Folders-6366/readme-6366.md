---
title: "📂 Tự Động Tải Hàng Chục File JSON Từ Google Sheets Về Máy"
description: "Hướng dẫn chi tiết workflow n8n giúp tải hàng loạt file JSON từ Google Sheets về thư mục cục bộ, tự động hóa quy trình quản lý file phức tạp chỉ với vài cú click."
slug: "tai-hang-loat-json-tu-google-sheets"
tags: [n8n, automation, no-code, google-sheets, file-management]
keywords: [n8n workflow, tự động hóa tải file, google sheets to local, bulk download json, n8n code node]
---

# 📂 Tự Động Tải Hàng Chục File JSON Từ Google Sheets Về Máy

Trong môi trường phát triển phần mềm hoặc quản lý dữ liệu, việc phải tải hàng chục, thậm chí hàng trăm file JSON từ các liên kết lưu trữ (như GitHub, S3, hoặc server nội bộ) là một cơn ác mộng. Làm thủ công nghĩa là bạn phải copy từng URL, mở trình duyệt, tải xuống, và đổi tên file cho đúng chuẩn. Chỉ cần sai sót một lần là mất hàng giờ đồng hồ và nguy cơ lỗi dữ liệu rất cao.

Workflow **"Bulk JSON File Downloader from Google Sheet to Local Folders"** do Rahul Joshi phát triển chính là giải pháp "cứu cánh" cho vấn đề này. Nó cho phép các sếp liệt kê toàn bộ URL và tên file cần tải trong một bảng Google Sheets, sau đó n8n sẽ tự động quét, tải về và lưu vào thư mục cục bộ trên máy chủ một cách chính xác 100%, không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và có thể truy cập vào hệ thống file cục bộ (Local Disk), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian cực đại:** Thay vì tải thủ công 50 file mất 30 phút, workflow chỉ mất chưa tới 1 phút để hoàn tất.
- **Chính xác tuyệt đối:** Loại bỏ hoàn toàn lỗi đánh máy tên file hay sai URL do con người gây ra.
- **Quản lý tập trung:** Chỉ cần cập nhật Google Sheets, toàn bộ quy trình tải file được đồng bộ hóa.
- **Tự động hóa quy trình:** Có thể tích hợp thêm bước xử lý dữ liệu sau khi tải về (parse, validate) ngay trong n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Chạy trên Self-hosted (VPS/Docker) để có quyền truy cập vào hệ thống file cục bộ (Local File System).
- **Google Sheets:** Một bảng tính chứa 2 cột: `FileName` (Tên file muốn lưu) và `URL` (Đường dẫn trực tiếp đến file JSON).
- **Thư mục đích:** Một thư mục trống trên máy chủ nơi các file sẽ được lưu trữ (ví dụ: `/home/user/downloads`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [link gốc trên n8n.io](https://n8n.io/workflows/6366) hoặc copy toàn bộ code JSON bên dưới và dán vào n8n Editor.

```json
{
  "name": "Bulk JSON File Downloader from Google Sheet to Local Folders",
  "nodes": [
    {
      "parameters": {},
      "id": "a1b2c3d4-1111-2222-3333-444455556666",
      "name": "When clicking ‘Execute workflow’",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "operation": "read",
        "documentId": {
          "__rl": true,
          "mode": "list",
          "value": ""
        },
        "sheetName": {
          "__rl": true,
          "mode": "list",
          "value": ""
        },
        "options": {}
      },
      "id": "a1b2c3d4-1111-2222-3333-444455556667",
      "name": "Get row(s) in sheet",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [470, 300],
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "YOUR_GOOGLE_SHEETS_CREDENTIAL_ID",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Lấy tên file và URL từ dữ liệu Google Sheets\nconst items = $input.all();\n\nreturn items.map(item => {\n  return {\n    json: {\n      fileName: item.json['FileName'],\n      url: item.json['URL']\n    }\n  };\n});"
      },
      "id": "a1b2c3d4-1111-2222-3333-444455556668",
      "name": "Take name and URL",
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [690, 300]
    },
    {
      "parameters": {
        "batchSize": 1,
        "options": {}
      },
      "id": "a1b2c3d4-1111-2222-3333-444455556669",
      "name": "Loop Over Items",
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [910, 300]
    },
    {
      "parameters": {
        "method": "GET",
        "url": "={{ $json.url }}",
        "options": {
          "response": {
            "response": {
              "responseFormat": "file",
              "outputPropertyName": "data"
            }
          }
        }
      },
      "id": "a1b2c3d4-1111-2222-3333-444455556670",
      "name": "HTTP Request",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [1130, 300]
    },
    {
      "parameters": {
        "operation": "write",
        "fileName": "={{ '/home/user/downloads/' + $json.fileName }}",
        "dataPropertyName": "data",
        "options": {}
      },
      "id": "a1b2c3d4-1111-2222-3333-444455556671",
      "name": "Read/Write Files from Disk",
      "type": "n8n-nodes-base.readWriteFile",
      "typeVersion": 1,
      "position": [1350, 300]
    },
    {
      "parameters": {
        "jsCode": "// Xử lý sau khi tải xong (nếu cần)\nreturn $input.all();"
      },
      "id": "a1b2c3d4-1111-2222-3333-444455556672",
      "name": "Code2",
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [1570, 300]
    },
    {
      "parameters": {
        "jsCode": "// Chuyển đổi URL nếu cần (ví dụ: thêm prefix)\nreturn $input.all();"
      },
      "id": "a1b2c3d4-1111-2222-3333-444455556673",
      "name": "url to downloadurl",
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [1130, 500]
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Get row(s) in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet": {
      "main": [
        [
          {
            "node": "Take name and URL",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Take name and URL": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Loop Over Items": {
      "main": [
        [
          {
            "node": "HTTP Request",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Code2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request": {
      "main": [
        [
          {
            "node": "Read/Write Files from Disk",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Read/Write Files from Disk": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "pinData": {}
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow này có 3 node then chốt cần các sếp cấu hình lại cho phù hợp với môi trường của mình:

1.  **Node `Get row(s) in sheet` (Google Sheets)**
    *   **Credentials:** Chọn hoặc tạo mới credential Google Sheets OAuth2.
    *   **Document ID:** Chọn đúng file Google Sheets chứa danh sách file cần tải.
    *   **Sheet Name:** Chọn đúng tab (sheet) chứa dữ liệu.
    *   *Lưu ý:* Đảm bảo bảng tính có đúng 2 cột tiêu đề là `FileName` và `URL`.

2.  **Node `HTTP Request`**
    *   Node này sử dụng biến `={{ $json.url }}` để lấy địa chỉ tải file.
    *   Nếu URL của các sếp cần thêm tham số xác thực (token) hoặc prefix, hãy chỉnh sửa công thức trong trường `URL`. Ví dụ: `={{ 'https://api.example.com/download?file=' + $json.url }}`.
    *   Đảm bảo `Response Format` được đặt là `File` để n8n có thể xử lý dữ liệu nhị phân (binary data) của file JSON.

3.  **Node `Read/Write Files from Disk`**
    *   **Operation:** Chọn `Write`.
    *   **File Name:** Đây là nơi các sếp chỉ định đường dẫn thư mục đích.
        *   Ví dụ: `={{ '/var/www/html/downloads/' + $json.fileName }}`
        *   *Cảnh báo:* Đảm bảo user mà n8n đang chạy (thường là `n8n` hoặc `root` trong Docker) có quyền ghi (write permission) vào thư mục này.
    *   **Data Property Name:** Giữ nguyên là `data` (tên thuộc tính chứa dữ liệu file từ node HTTP Request).

4.  **Node `Loop