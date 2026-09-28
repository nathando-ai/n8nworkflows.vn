---
title: "🎨 Tự Động Xóa Nền Hình Ảnh với APImage AI: Từ Airtable → Google Drive (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn xóa nền ảnh từ Airtable, xử lý bằng AI APImage và lưu kết quả vào Google Drive. Giúp các sếp tiết kiệm 10+ giờ/tháng trong chỉnh sửa hình ảnh, đồng thời đảm bảo chất lượng cao và tự động hóa liên tục 24/7."
slug: "tieu-nen-hinh-apimage-airtable-google-drive"
tags: [n8n, automation, content-creation, multimodal-ai, airtable, google-drive, apimage]
keywords: [tự động hóa xóa nền ảnh, workflow n8n airtable google drive, apimage ai, tự động hóa thiết kế đồ họa, xử lý hình ảnh bằng AI]
---

# 🚀 **Tự Động Xóa Nền Hình Ảnh với APImage AI: Từ Airtable → Google Drive**

### **Giải pháp hoàn toàn tự động hóa cho các sếp cần xử lý hàng trăm ảnh mỗi tháng**
Làm thủ công xóa nền ảnh cho từng hình ảnh trong Airtable không chỉ tốn thời gian mà còn dễ gây mệt mỏi và sai sót. **Workflow này tự động hóa toàn bộ quy trình** từ lấy dữ liệu Airtable → xử lý bằng AI APImage → lưu kết quả vào Google Drive, giúp các sếp:
- **Tiết kiệm 10+ giờ/tháng** trong việc chỉnh sửa hình ảnh.
- **Đảm bảo chất lượng nhất quán** với AI xử lý tự động.
- **Hoạt động liên tục 24/7** mà không cần can thiệp.
- **Tích hợp hoàn toàn** với hệ thống hiện có (Airtable + Google Drive).

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, chỉ cần kích hoạt workflow.
- **Chất lượng cao**: AI APImage xử lý nền ảnh với độ chính xác cao, phù hợp cho thiết kế đồ họa, marketing, và nội dung số.
- **Tích hợp đa nền tảng**: Lấy dữ liệu từ Airtable, xử lý bằng API, lưu kết quả vào Google Drive (hoặc thay thế bằng Dropbox, AWS S3...).
- **Dễ dàng mở rộng**: Thêm logic tùy chỉnh như thay đổi tên file, thêm metadata, hoặc gửi thông báo qua Slack/Email.
- **Hoạt động liên tục**: Chạy trên VPS tự động hóa (Self-hosted) để không bị giới hạn bởi phiên làm việc.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Airtable**:
   - Một **base** (cơ sở dữ liệu) với bảng chứa hình ảnh (ví dụ: "Media Files").
   - Bảng phải có trường chứa **URL thumbnail** (có thể là trường `Thumbnail` hoặc `Image` tùy thuộc vào cấu trúc).
   - **API Key Airtable**: Tạo tại [Airtable API](https://airtable.com/api) và thêm vào n8n dưới tên `airtableTokenApi`.

2. **Tài khoản APImage AI**:
   - Đăng ký tại [APImage](https://apimage.org/) và lấy **API Key** từ Dashboard.
   - **Lưu ý**: API Key này sẽ được sử dụng trong node `APImage API` để xác thực.

3. **Tài khoản Google Drive**:
   - **API Key Google Drive**: Tạo tại [Google Cloud Console](https://console.cloud.google.com/) và thêm vào n8n dưới tên `googleDrive`.
   - **Folder lưu kết quả**: Workflow sẽ tự động tạo folder `bg_removal` trong Google Drive root (hoặc tùy chỉnh theo yêu cầu).

4. **n8n Self-hosted**:
   - Để workflow chạy 24/7, các sếp nên cài đặt n8n trên **VPS** (không phụ thuộc vào phiên làm việc).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/6457) hoặc sử dụng mã JSON dưới đây.
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán mã JSON.
3. **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

```json
{
  "nodes": [
    {
      "parameters": {
        "operation": "getRecord",
        "tableName": "Media Files",
        "viewName": "",
        "fields": ["*"],
        "maxRecords": 100,
        "apiKey": "airtableTokenApi"
      },
      "name": "Get a record",
      "type": "n8n-nodes-base.airtable",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "code": "// Current field mappings\nfileName: record.fields['File Name']\nmediaType: record.fields['Media Type']\nuploadDate: record.fields['Upload Date']\nfileSize: record.fields['File Size']\nthumbnailUrl: record.fields.Thumbnail[0].url\n\n// Output structure\noutputItems.push({\n  json: {\n    recordId: record.id,\n    fileName: fileName,\n    mediaType: mediaType,\n    uploadDate: uploadDate,\n    fileSize: fileSize,\n    thumbnailUrl: thumbnailUrl,\n    cleanFileName: fileName.replace(/[^a-zA-Z0-9]/g, '_').toLowerCase()\n  }\n});"
      },
      "name": "Code",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [450, 300]
    },
    {
      "parameters": {},
      "name": "Split Out",
      "type": "n8n-nodes-base.splitOut",
      "typeVersion": 1,
      "position": [650, 300]
    },
    {
      "parameters": {
        "method": "post",
        "url": "https://api.apimage.org/v1/remove-background",
        "headers": {
          "Authorization": "Bearer YOUR_API_KEY",
          "Content-Type": "application/json"
        },
        "body": {
          "image_url": "$json.thumbnailUrl"
        }
      },
      "name": "APImage API",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [850, 300]
    },
    {
      "parameters": {
        "method": "get",
        "url": "$json.image_url",
        "headers": {
          "Accept": "image/png"
        }
      },
      "name": "Download",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [1050, 300]
    },
    {
      "parameters": {
        "file": "$binary",
        "folderId": "root",
        "fileName": "$json.cleanFileName + '_bg_removed.png'",
        "apiKey": "googleDrive"
      },
      "name": "Upload file",
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 1,
      "position": [1250, 300]
    },
    {
      "parameters": {},
      "name": "Remove Background",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [150, 100]
    }
  ],
  "connections": {
    "manualTrigger": {
      "main": [
        [
          {
            "node": "Get a record",
            "connection": "main",
            "type": "direct"
          }
        ]
      ]
    },
    "Get a record": {
      "main": [
        [
          {
            "node": "Code",
            "connection": "main",
            "type": "direct"
          }
        ]
      ]
    },
    "Code": {
      "main": [
        [
          {
            "node": "Split Out",
            "connection": "main",
            "type": "direct"
          }
        ]
      ]
    },
    "Split Out": {
      "main": [
        [
          {
            "node": "APImage API",
            "connection": "main",
            "type": "direct"
          }
        ]
      ]
    },
    "APImage API": {
      "main": [
        [
          {
            "node": "Download",
            "connection": "main",
            "type": "direct"
          }
        ]
      ]
    },
    "Download": {
      "main": [
        [
          {
            "node": "Upload file",
            "connection": "main",
            "type": "direct"
          }
        ]
      ]
    }
  }
}
```

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **a. Cấu hình API Key APImage**
1. Mở node **`APImage API`** (HTTP Request).
2. Thay thế `_YOUR_API_KEY_` trong header `Authorization` bằng **API Key** của bạn (tìm tại [Dashboard APImage](https://apimage.org/dashboard)).
   - **Ví dụ**:
     ```json
     "headers": {
       "Authorization": "Bearer sk_your_api_key_here",
       "Content-Type": "application/json"
     }
     ```

#### **b. Cấu hình Airtable**
1. Mở node **`Get a record`** (Airtable).
2. Đảm bảo:
   - **Table Name** là tên bảng chứa hình ảnh (ví dụ: `Media Files`).
   - **Fields** bao gồm trường chứa URL thumbnail (có thể là `Thumbnail`, `Image`, hoặc tên tùy chỉnh).
   - **API Key** đã được thêm vào n8n với tên `airtableTokenApi`.

#### **c. Cấu hình Google Drive**
1. Mở node **`Upload file`** (Google Drive).
2. Đảm bảo:
   - **Folder ID** là `root` (hoặc tùy chỉnh theo yêu cầu).
   - **File Name** sử dụng định dạng:
     ```
     $json.cleanFileName + '_bg_removed.png'
     ```
     (đảm bảo tên file không chứa ký tự đặc biệt).
   - **API Key** đã được thêm vào n8n với tên `googleDrive`.

#### **d. Cấu hình Node Code (tùy chỉnh)**
Node **`Code`** xử lý dữ liệu từ Airtable. Các sếp có thể tùy chỉnh để phù hợp với cấu trúc bảng của mình:
- **Thay đổi tên trường**: Ví dụ, nếu trường thumbnail là `Photo` thay vì `Thumbnail`, sửa:
  ```javascript
  thumbnailUrl: record.fields.Photo[0].url
  ```
- **Thêm metadata**: Ví dụ, thêm trường `category` hoặc `brand` vào output:
  ```javascript
  outputItems.push({
    json: {
      recordId: record.id,
      fileName: record.fields['File Name'],
      category: record.fields['Category'] || 'Unknown',
      thumbnailUrl: record.fields.Thumbnail[0].url,
      cleanFileName: record.fields['File Name'].replace(/[^a-zA-Z0-9]/g, '_').toLowerCase()
    }
  });
  ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra với một bản ghi mẫu.
   - Kiểm tra kết quả trong Google Drive (folder `bg_removal`).
2. **Bật Active**:
   - Đặt workflow thành **Active** để tự động chạy khi kích hoạt.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Thay thế Manual Trigger bằng Schedule Trigger**
- **Lợi ích**: Chạy tự động hàng ngày/ngày nào đó thay vì kích hoạt thủ công.
- **Cách làm**:
  1. Thay thế node **`Remove Background`** (Manual Trigger) bằng **`Schedule Trigger`**.
  2. Cấu hình thời gian chạy (ví dụ: 8h sáng hàng ngày).
  3. **Lưu ý**: Đảm bảo node **`Get a record`** có thể lấy dữ liệu mới (có thể thêm điều kiện `modifiedDate` trong Airtable).

### **2. Gửi thông báo qua Slack/Email khi hoàn thành**
- **Cách làm**:
  1. Thêm node **`Slack`** hoặc **`Send Email`** sau node **`Upload file`**.
  2. Cấu hình nội dung thông báo:
     ```
     "Hình ảnh [fileName] đã xóa nền thành công và lưu tại: [Google Drive Link]"
     ```
  3. **Lưu ý**: Sử dụng node **`Set`** để truyền dữ liệu từ node trước.

### **3. Lưu log xử lý vào Airtable**
- **Cách làm**:
  1. Thêm node **`Update Record`** (Airtable) sau node **`Upload file`**.
  2. Cập nhật trường `status` từ `pending` → `completed` và thêm trường `processedAt`.
  3. **Lợi ích**: Theo dõi trạng thái xử lý của từng hình ảnh.

### **4. Xử lý lỗi và retry tự động**
- **Cách làm**:
  1. Thêm node **`IF`** sau node **`APImage API`** để kiểm tra lỗi (status code != 200).
  2. Nếu lỗi, chuyển đến node **`Retry`** (HTTP Request) với logic retry sau 5 giây.
  3. **Lưu ý**: Sử dụng node **`Set`** để lưu trạng thái lỗi vào Airtable.

### **5. Tùy chỉnh tên file theo cấu trúc cụ thể**
- **Ví dụ**: Nếu tên file trong Airtable là `Product_12345.jpg`, muốn lưu thành `product-12345_bg_removed.png`:
  ```javascript
  // Trong node Code
  cleanFileName: record.fields['File Name']
    .replace(/Product_/, 'product-')
    .replace(/\.jpg$/, '')
    .toLowerCase()
  ```

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa xử lý hình ảnh với AI, tiết kiệm thời gian và đảm bảo chất lượng. Bằng cách tích hợp Airtable, APImage AI và Google Drive, các sếp có thể:
- **Xử lý hàng trăm hình ảnh** trong vài phút thay vì nhiều giờ.
- **Tự động hóa hoàn toàn** với VPS n8