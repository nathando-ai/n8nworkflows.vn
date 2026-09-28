---
title: "🔧 Tạo Mảng Đối Tượng (Array of Objects) Tự Động trong n8n – Cách Sử Dụng Building Blocks"
description: "Hướng dẫn chi tiết cách tạo mảng đối tượng (array of objects) trong n8n bằng Building Blocks, giúp các sếp tự động hóa việc xử lý dữ liệu phức tạp chỉ với 2 node đơn giản."
slug: "tao-mang-doi-tuong-trong-n8n"
tags: [n8n, automation, no-code, building-blocks, array-of-objects]
keywords: [n8n building blocks, tạo mảng đối tượng, tự động hóa dữ liệu, n8n functions, array trong n8n]
---

# 🔧 **Tạo Mảng Đối Tượng (Array of Objects) Tự Động trong n8n – Cách Sử Dụng Building Blocks**

### **Giải quyết vấn đề gì?**
Các sếp thường phải **tạo thủ công** mảng đối tượng (array of objects) trong các workflow n8n để xử lý dữ liệu phức tạp như:
- **Tạo danh sách sản phẩm** từ các trường dữ liệu khác nhau.
- **Chuyển đổi dữ liệu thô** thành định dạng JSON chuẩn cho API.
- **Tạo input cho AI** (LLM) từ các trường dữ liệu rời rạc.

Với **Building Blocks** của n8n, các sếp có thể **tạo mảng đối tượng tự động** chỉ với **2 node**, không cần viết code!

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến 80% so với cách làm thủ công.
- **Chính xác 100%** – Không lo lỗi syntax khi tạo mảng.
- **Dễ dàng mở rộng** – Thêm/loại trường dữ liệu chỉ với vài cú click.
- **Hoạt động liên tục** – Phù hợp cho các workflow tự động hóa 24/7.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
- **Không cần tài khoản API** – Workflow này sử dụng **Mock Data** để tạo mẫu.
- **N8n phiên bản mới nhất** (để sử dụng Building Blocks).
- **Khả năng cấu hình node Function** (n8n-nodes-base.function).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow này từ file JSON hoặc **copy/paste** mã JSON vào **n8n Editor**:
```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "Mock Data",
      "type": "function",
      "typeOptions": {
        "code": "return [\n  { name: 'Product 1', price: 100, category: 'Electronics' },\n  { name: 'Product 2', price: 200, category: 'Clothing' },\n  { name: 'Product 3', price: 150, category: 'Home' }\n];"
      }
    },
    {
      "name": "Create an array of objects",
      "type": "function",
      "typeOptions": {
        "code": "return $input.all();"
      }
    }
  ],
  "connections": {
    "Mock Data": {
      "main": ["Create an array of objects"]
    }
  }
}
```
**Cách thực hiện:**
1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn **"From JSON"** → Dán mã trên.
2. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/767) (nếu link vẫn hoạt động).

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **Node 1: Mock Data (Tạo dữ liệu mẫu)**
- **Chức năng:** Tạo một mảng đối tượng mẫu để sử dụng trong workflow.
- **Cấu hình:**
  - **Type:** `Function`
  - **Code:** Sửa đổi phần `return` để phù hợp với dữ liệu của các sếp:
    ```javascript
    return [
      { name: 'Product 1', price: 100, category: 'Electronics' },
      { name: 'Product 2', price: 200, category: 'Clothing' },
      { name: 'Product 3', price: 150, category: 'Home' }
    ];
    ```
  - **Lưu ý:** Các sếp có thể **thêm/bỏ trường** hoặc **thay đổi giá trị** tùy ý.

##### **Node 2: Create an array of objects (Trả về mảng)**
- **Chức năng:** Trả về mảng đối tượng đã tạo từ Node 1.
- **Cấu hình:**
  - **Type:** `Function`
  - **Code:** Sử dụng `$input.all()` để lấy dữ liệu từ Node trước.
    ```javascript
    return $input.all();
    ```
  - **Lưu ý:** Nếu muốn **chuyển đổi hoặc xử lý dữ liệu**, các sếp có thể thêm logic vào node này.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run:** Chạy workflow với **dữ liệu mẫu** để kiểm tra kết quả.
2. **Active Workflow:** Sau khi kiểm tra, **bật Active** để workflow hoạt động liên tục.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với API:**
   - Sử dụng kết quả mảng này để **gửi request API** (ví dụ: tạo đơn hàng trên Shopify).
   - **Node gợi ý:** `HTTP Request` → `JSON Body` = `$json`.

2. **Tạo log tự động:**
   - Sử dụng **n8n-nodes-base.terminal** để log kết quả mảng ra console.
   - **Cú pháp:**
     ```javascript
     console.log($input.all());
     ```

3. **Tích hợp với Slack/Telegram:**
   - Gửi kết quả mảng dưới dạng **bảng dữ liệu** qua Slack/Telegram.
   - **Node gợi ý:** `Slack Webhook` → `Custom Payload` = `$json`.

4. **Tự động hóa báo cáo hàng ngày:**
   - Sử dụng **n8n-nodes-base.schedule** để chạy workflow hàng ngày và **gửi email báo cáo** (node `Email`).

---

### 📌 **Kết luận**
Với **Building Blocks** này, các sếp **không cần viết code** mà vẫn có thể tạo **mảng đối tượng phức tạp** một cách nhanh chóng và chính xác. **Áp dụng ngay** để tự động hóa việc xử lý dữ liệu trong n8n!

---
:::note[CHÚ Ý]
- Nếu muốn **tạo mảng động từ dữ liệu thực tế**, các sếp có thể thay thế **Mock Data** bằng **HTTP Request** (lấy từ API) hoặc **Google Sheets** (lấy từ bảng tính).
- **N8n Self-hosted** (VPS) là lựa chọn tối ưu để workflow chạy **24/7** mà không bị giới hạn.
:::