---
title: "🔄 Chuyển Dữ Liệu API FileMaker Sang Mảng Dữ Liệu Flat (Flat File Array) - Tự Động Hóa 100% Không Code"
description: "Workflow này giúp các sếp tự động chuyển đổi dữ liệu phức tạp từ API FileMaker thành mảng dữ liệu flat (array) dễ dàng sử dụng cho các ứng dụng khác, tiết kiệm thời gian và giảm thiểu lỗi thủ công. Phù hợp cho doanh nghiệp quản lý khách hàng, CRM hoặc tích hợp hệ thống."
slug: "chuyen-doi-api-filemaker-sang-flat-file-array"
tags: [n8n, automation, no-code, filemaker, api-integration, data-transformation]
keywords: [n8n workflow filemaker, chuyển đổi dữ liệu API, flat file array, tự động hóa filemaker, tích hợp CRM, data processing]
---

# 🔄 **Chuyển Dữ Liệu API FileMaker Sang Mảng Dữ Liệu Flat (Flat File Array)**

### **Giải pháp tự động hóa cho doanh nghiệp quản lý dữ liệu phức tạp**
Các sếp đang gặp khó khăn khi phải xử lý dữ liệu từ **API FileMaker** để sử dụng trong các ứng dụng khác? Dữ liệu từ API thường có cấu trúc nhúng (nested) hoặc phức tạp, khiến việc chuyển đổi sang định dạng **mảng dữ liệu flat (flat file array)** trở nên phức tạp và tốn thời gian. **Workflow này giúp tự động hóa quá trình này 100% không code**, đảm bảo dữ liệu được chuyển đổi chính xác và nhanh chóng, phù hợp cho CRM, báo cáo hoặc tích hợp hệ thống.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết code hoặc xử lý thủ công dữ liệu từ API.
- **Chính xác 100%**: Tránh sai sót khi chuyển đổi cấu trúc dữ liệu phức tạp.
- **Dễ tích hợp**: Mảng dữ liệu flat sẵn sàng để sử dụng trong các ứng dụng khác (Google Sheets, Airtable, API khác...).
- **Hoạt động liên tục**: Workflow có thể chạy 24/7 trên VPS tự host, tự động cập nhật dữ liệu mới.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **API Key hoặc Credentials của FileMaker**:
   - Địa chỉ API của FileMaker (ví dụ: `https://your-filemaker-server/fmi/data/v1/database/your-db/records`).
   - Thông tin xác thực (username, password, hoặc token API).
2. **Cấu trúc dữ liệu đầu vào**:
   - Workflow giả định dữ liệu từ API FileMaker có dạng **JSON nhúng** (nested), ví dụ:
     ```json
     {
       "data": [
         {
           "id": 1,
           "name": "John Doe",
           "contact": {
             "email": "john@example.com",
             "phone": "123456789"
           }
         }
       ]
     }
     ```
3. **n8n Self-hosted** (không dùng phiên bản miễn phí của n8n.io để đảm bảo ổn định).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/) (nếu tự host) hoặc editor của phiên bản self-hosted.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/1537)).
3. Chọn **"Import"** để tải workflow vào hệ thống.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **3 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: FileMaker Data API Contacts (n8n-nodes-base.function)**
- **Cấu hình API Request**:
  - **Method**: `GET` (hoặc `POST` nếu cần).
  - **URL**: Điền địa chỉ API của FileMaker (ví dụ: `https://your-filemaker-server/fmi/data/v1/database/your-db/records`).
  - **Headers**:
    - `Authorization`: `Basic <base64-encoded-credentials>` (hoặc `Bearer <token>`).
    - `Content-Type`: `application/json`.
  - **Body (nếu cần)**: Điền tham số query (nếu API yêu cầu).
  - **Credentials**: Chọn tài khoản đã cấu hình trước trong n8n (ví dụ: `FileMaker-API`).

##### **Node 2: FileMaker response.data (n8n-nodes-base.itemLists)**
- **Chức năng**: Chuyển đổi dữ liệu từ API thành danh sách các mục (item lists) để xử lý tiếp.
- **Cấu hình**:
  - **Property**: Chọn `data` (hoặc tên property chứa danh sách dữ liệu từ API).
  - **Mode**: Chọn `Array` (nếu dữ liệu là mảng JSON).

##### **Node 3: Return item.fieldData (n8n-nodes-base.functionItem)**
- **Chức năng**: Trích xuất và chuyển đổi dữ liệu nhúng thành mảng flat.
- **Cấu hình**:
  - **Function Code**: Sử dụng mã JavaScript để chuyển đổi dữ liệu. Ví dụ:
    ```javascript
    // Giả sử dữ liệu từ API có cấu trúc như sau:
    // { id: 1, name: "John", contact: { email: "john@example.com" } }
    return {
      id: item.id,
      name: item.name,
      email: item.contact.email,
      phone: item.contact.phone
    };
    ```
  - **Output**: Dữ liệu sẽ được chuyển đổi thành mảng flat, ví dụ:
    ```json
    [
      { "id": 1, "name": "John Doe", "email": "john@example.com", "phone": "123456789" },
      { "id": 2, "name": "Jane Smith", "email": "jane@example.com", "phone": "987654321" }
    ]
    ```

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào nút **"Run"** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra **output** để đảm bảo dữ liệu được chuyển đổi đúng cấu trúc.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang trạng thái **"Active"**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp với Google Sheets/Airtable**:
   - Sau khi chuyển đổi dữ liệu thành flat array, các sếp có thể sử dụng **node Google Sheets** hoặc **Airtable** để lưu trữ hoặc cập nhật dữ liệu tự động.
2. **Gửi báo cáo định kỳ**:
   - Sử dụng **node Email** hoặc **Slack** để gửi báo cáo dữ liệu mới mỗi ngày/tuần.
3. **Lưu log hoạt động**:
   - Thêm **node Log** để ghi lại lịch sử chuyển đổi dữ liệu, giúp theo dõi và debug dễ dàng.
4. **Tự động cập nhật khi có dữ liệu mới**:
   - Sử dụng **webhook** hoặc **cron job** để kích hoạt workflow khi có dữ liệu mới từ FileMaker.
:::

---

### 📌 **Kết luận**
Workflow **"Convert FileMaker Data API to Flat File Array"** là giải pháp **tự động hóa hoàn hảo** cho các doanh nghiệp cần xử lý dữ liệu từ FileMaker một cách nhanh chóng và chính xác. **Không cần viết code**, các sếp chỉ cần cấu hình API và chạy workflow trên VPS tự host để đảm bảo hoạt động 24/7.

👉 **Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu lỗi trong quản lý dữ liệu!**
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn trong quá trình cấu hình, các sếp có thể tham khảo [cộng đồng n8n](https://community.n8n.io/) hoặc liên hệ với tác giả **Dick** qua [link gốc](https://n8n.io/workflows/1537).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::