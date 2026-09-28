---
title: "🗑️ Tự Động Xóa Tệp PNG Cũ Trên Dropbox Sau 48 Giây (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn để xóa tự động tất cả tệp PNG trên Dropbox đã cũ hơn 48 giờ, giúp tiết kiệm không gian lưu trữ và duy trì hệ thống sạch sẽ 24/7. Phù hợp cho doanh nghiệp quản lý nhiều tệp tạm thời hoặc hình ảnh AI."
slug: "tieu-dong-xoa-tap-png-cung-tren-dropbox"
tags: [n8n, tự động hóa, Dropbox, file management, no-code]
keywords: [tự động hóa Dropbox, xóa tệp cũ, n8n workflow, quản lý file PNG, tự động hóa lưu trữ]
---

# 🗑️ **Tự Động Xóa Tệp PNG Cũ Trên Dropbox Sau 48 Giây (Không Cần Code)**

## **😩 Nỗi Đau Của Các Sếp**
Các sếp có biết rằng **tệp PNG tạm thời, hình ảnh AI, hoặc cache** tích lũy trên Dropbox có thể chiếm đến **50% dung lượng lưu trữ** mà không ai quản lý? Điều này không chỉ làm **chậm hệ thống**, mà còn **tốn chi phí không cần thiết** cho các gói lưu trữ premium.

- **Thủ công xóa tệp cũ?** Tốn thời gian và dễ bỏ quên.
- **Sử dụng công cụ bên thứ ba?** Phức tạp, mất tiền và không an toàn.
- **Không tự động hóa?** Rủi ro bị **vi phạm quy định bảo mật** khi lưu trữ quá nhiều file không cần thiết.

**Workflow này giải quyết tất cả!** Nó **xóa tự động tất cả tệp PNG cũ hơn 48 giờ** trên Dropbox **một cách an toàn và không cần code**, đồng thời **bỏ qua các tệp quan trọng** như `admin_1.png` hoặc file trong thư mục `icons`.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm không gian lưu trữ** (giảm thiểu chi phí Dropbox)
✅ **Duy trì hệ thống sạch sẽ** (không bị lạm dụng bởi cache hoặc file tạm)
✅ **Bảo vệ file quan trọng** (có thể tùy chỉnh danh sách bỏ qua)
✅ **Hoạt động 24/7** (không cần can thiệp thủ công)
✅ **Không giới hạn API** (xử lý tệp theo batch để tránh bị chặn)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Dropbox** (và **OAuth 2.0 API Key** đã cấu hình trong n8n)
- **n8n Self-hosted** (để workflow chạy liên tục)
- **Dung lượng lưu trữ Dropbox** (đảm bảo không xóa quá nhiều tệp một lúc)

:::info[CHUẨN BỊ]
👉 **Nếu chưa có VPS**, các sếp có thể đăng ký **VPS TinoHost** với mã giảm giá **VPSN8N** (giảm tới 39%):
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste mã JSON** vào **n8n Editor**:
```json
{
  "nodes": [
    {
      "parameters": {
        "schedule": "0 0 */2 * *"
      },
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger"
    },
    {
      "parameters": {
        "resource": "search",
        "query": "*.png",
        "credentials": "dropboxOAuth2Api"
      },
      "name": "Query",
      "type": "n8n-nodes-base.dropbox"
    },
    {
      "parameters": {
        "code": "// Filter logic:\n// 1. Only .png files\n// 2. Older than 48 hours\n// 3. Not excluded files\n\nconst excludedFiles = [\n  'admin_1.png',\n  'icons/*'\n];\n\nconst now = new Date();\nconst fortyEightHoursAgo = new Date(now.getTime() - 48 * 60 * 60 * 1000);\n\nreturn $input.all().filter(file => {\n  const fileDate = new Date(file.clientModified);\n  const isPng = file.path.toLowerCase().endsWith('.png');\n  const isNotExcluded = !excludedFiles.some(exclude => {\n    if (exclude.endsWith('*')) {\n      return file.path.includes(exclude.replace('*', ''));\n    }\n    return file.path === exclude;\n  });\n\n  return isPng && fileDate < fortyEightHoursAgo && isNotExcluded;\n});"
      },
      "name": "Code in JavaScript",
      "type": "n8n-nodes-base.code"
    },
    {
      "parameters": {
        "size": 100
      },
      "name": "Loop Over Items",
      "type": "n8n-nodes-base.splitInBatches"
    },
    {
      "parameters": {
        "operation": "delete",
        "path": "={{ $json.path }}",
        "credentials": "dropboxOAuth2Api"
      },
      "name": "Delete a file",
      "type": "n8n-nodes-base.dropbox"
    }
  ],
  "connections": {
    "scheduleTrigger": {
      "main": ["Query"]
    },
    "Query": {
      "main": ["Code in JavaScript"]
    },
    "Code in JavaScript": {
      "main": ["Loop Over Items"]
    },
    "Loop Over Items": {
      "main": ["Delete a file"]
    }
  }
}
```

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **🔹 Node "Schedule Trigger"**
- **Thời gian chạy mặc định:** **Mỗi 2 ngày** (`0 0 */2 * *`).
- **Các sếp có thể điều chỉnh** theo nhu cầu:
  - **Mỗi ngày:** `0 0 * * *`
  - **Mỗi giờ:** `0 0 * * * *`
  - **Thời gian cụ thể:** `0 8 * * *` (8h sáng hàng ngày)

#### **🔹 Node "Query" (Tìm kiếm tệp)**
- **Tham số `query`:** `*.png` (tìm tất cả tệp PNG).
- **Các sếp có thể thay đổi** thành:
  - `*.jpg` (xóa JPG)
  - `*.mp4` (xóa video)
  - `*.tmp` (xóa cache)

#### **🔹 Node "Code" (Lógica lọc)**
- **Cấu trúc mã hiện tại:**
  - **Bỏ qua tệp `admin_1.png`**
  - **Bỏ qua tệp trong thư mục `icons/`**
- **Các sếp có thể thêm vào danh sách `excludedFiles`:**
  ```javascript
  const excludedFiles = [
    'admin_1.png',
    'icons/*',
    'backup_*.zip',  // Ví dụ: bỏ qua tất cả file backup
    'important_project/*'  // Bỏ qua toàn bộ thư mục
  ];
  ```

#### **🔹 Node "Delete a file" (Xóa tệp)**
- **Lưu ý quan trọng:** **Xóa tệp là hành động vĩnh viễn!**
- **Test trước khi kích hoạt:** Các sếp nên **chạy thử với một tệp mẫu** trước khi bật workflow chính thức.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một tệp PNG cũ (đảm bảo không phải tệp quan trọng).
2. **Kiểm tra log** trong n8n để xác nhận tệp đã được xóa.
3. **Bật Active** khi đã an toàn.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **🔹 Kết hợp với Slack/Telegram để báo cáo**
- **Thêm node `n8n-nodes-base.slack`** sau node `Delete a file` để thông báo:
  ```json
  {
    "parameters": {
      "message": "✅ Xóa thành công {{ $node["Loop Over Items"].json.length }} tệp PNG cũ trên Dropbox!",
      "channel": "#automation-reports"
    },
    "name": "Notify Slack",
    "type": "n8n-nodes-base.slack"
  }
  ```

### **🔹 Lưu log vào Google Sheets**
- **Thêm node `n8n-nodes-base.googleSheets`** để ghi lịch sử xóa:
  ```json
  {
    "parameters": {
      "operation": "createRow",
      "sheetName": "Dropbox_Cleanup_Log",
      "credentials": "googleSheetsOAuth2Api",
      "rowData": {
        "Date": "={{ $node["Schedule Trigger"].json.date }}",
        "Files_Deleted": "={{ $node["Loop Over Items"].json.length }}",
        "Status": "Success"
      }
    },
    "name": "Log to Google Sheets",
    "type": "n8n-nodes-base.googleSheets"
  }
  ```

### **🔹 Tùy chỉnh thời gian giữ tệp**
- **Thay đổi `48 hours` thành `7 days`** trong node Code:
  ```javascript
  const fortyEightHoursAgo = new Date(now.getTime() - 7 * 24 * 60 * 60 * 1000); // 7 ngày
  ```

### **🔹 Xóa theo thư mục cụ thể**
- **Thêm điều kiện trong Code node** để chỉ xóa trong một thư mục nhất định:
  ```javascript
  const isInTargetFolder = file.path.includes('temp_images/');
  return isPng && fileDate < fortyEightHoursAgo && isNotExcluded && isInTargetFolder;
  ```

---

## **📌 Kết Luận**
**Workflow này không chỉ giúp các sếp tự động hóa việc xóa tệp cũ trên Dropbox mà còn:**
✔ **Tiết kiệm không gian lưu trữ**
✔ **Giảm thiểu rủi ro vi phạm bảo mật**
✔ **Không cần code hoặc kỹ năng kỹ thuật cao**

**Hãy áp dụng ngay để hệ thống của các sếp luôn sạch sẽ và hiệu quả!**
👉 **Bắt đầu tự động hóa Dropbox của mình [tại đây](https://n8n.io/workflows/15079)**.

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký tư vấn 1:1** với Afigo Sam (tác giả workflow): [https://afigo.vn](https://afigo.vn)
- **Đăng ký VPS n8n** với mã giảm giá: [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)