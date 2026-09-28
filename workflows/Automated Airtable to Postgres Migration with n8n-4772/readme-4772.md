---
title: "🔄 **Tự Động Hóa Di Chuyển Dữ Liệu Airtable → Postgres Miễn Code (N8n) – Khắc Phục Nỗi Đau Dữ Liệu Phân Tán & Khó Tìm Kiếm**"
description: "Workflow này tự động hóa việc di chuyển toàn bộ dữ liệu từ Airtable sang PostgreSQL một cách chính xác, bảo toàn cấu trúc và không cần viết một dòng code. Giúp các sếp tiết kiệm thời gian lên đến 80% trong việc quản lý dữ liệu và tối ưu hóa hiệu suất truy vấn."
slug: "tự-dộng-hoa-di-chuyen-airtable-sang-postgres"
tags: [n8n, automation, airtable, postgresql, no-code, it-ops, database-migration]
keywords: [n8n workflow airtable postgresql, tự động hóa di chuyển dữ liệu, migrate airtable sang postgres, tự động hóa no-code, giải pháp quản lý dữ liệu hiệu quả]
---

# 🚀 **Tự Động Hóa Di Chuyển Dữ Liệu Airtable → Postgres Miễn Code với n8n**

### **Giải pháp hoàn hảo cho các sếp đang mắc kẹt với:**
- **Dữ liệu phân tán** giữa Airtable và PostgreSQL, khiến việc truy vấn và phân tích trở nên phức tạp.
- **Thời gian mất nhiều giờ** để đồng bộ hóa thủ công, gây ra rủi ro sai sót và mất hiệu quả.
- **Không biết cách bắt đầu** việc di chuyển dữ liệu lớn mà không cần viết code.
- **Cần bảo toàn cấu trúc** của bảng và dữ liệu khi chuyển đổi giữa hai hệ thống khác nhau.

Workflow này **tự động hóa toàn bộ quá trình**, từ lấy dữ liệu Airtable, xử lý cấu trúc bảng, đến đồng bộ hóa vào PostgreSQL với **tốc độ cao và chính xác 100%**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và xử lý lượng dữ liệu lớn, các sếp nên **self-host n8n** trên một VPS mạnh mẽ.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (phù hợp cho workflow này)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
✅ **Bảo toàn toàn bộ cấu trúc dữ liệu**, không mất mát hay sai sót.
✅ **Hoạt động tự động 24/7**, không cần can thiệp của con người.
✅ **Không cần viết code**, chỉ cần cấu hình các tham số cơ bản.
✅ **Dữ liệu đồng bộ hóa liên tục**, giảm thiểu rủi ro sai lệch.
✅ **Thích ứng với dữ liệu lớn**, xử lý hàng ngàn bản ghi một cách hiệu quả.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Airtable** (API Key hoặc OAuth 2.0).
- **Tài khoản PostgreSQL** (thông tin kết nối: Host, Port, Database Name, Username, Password).
- **Dữ liệu mẫu** (nếu muốn test trước khi chạy toàn bộ).
- **Quá trình làm việc** của n8n (n8n.io) hoặc một VPS đã cài đặt n8n.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/4772).
2. Trong n8n Editor, chọn **Import Workflow** và chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **Create Workflow** → **Import JSON**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Webhook (Bước khởi động)**
Workflow này sử dụng **Webhook** để bắt đầu quá trình di chuyển dữ liệu. Các sếp cần:
1. **Tạo một Webhook mới** trong n8n:
   - Tìm node **"Airtable - Postgres"** (type: `webhook`).
   - Chọn **Create** và lưu lại **URL Webhook** (sẽ dùng sau).
2. **Gửi yêu cầu khởi động** từ Airtable hoặc một API khác:
   - Gửi một **POST request** đến URL Webhook với payload cơ bản:
     ```json
     {
       "action": "start_migration"
     }
     ```

#### **B. Cấu hình Credentials Airtable & PostgreSQL**
Workflow sử dụng **HTTP Request** để lấy dữ liệu từ Airtable và PostgreSQL. Các sếp cần:
1. **Thêm Credentials Airtable**:
   - Tìm node **"Get records"** (type: `httpRequest`).
   - Cấu hình:
     - **Method**: `GET`
     - **URL**: `https://api.airtable.com/v0/{base_id}/{table_name}`
     - **Headers**:
       ```json
       {
         "Authorization": "Bearer YOUR_AIRTABLE_API_KEY",
         "Content-Type": "application/json"
       }
       ```
   - Thay `{base_id}` và `{table_name}` bằng thông tin của bảng Airtable.

2. **Thêm Credentials PostgreSQL**:
   - Tìm node **"Test postgres credentials"** (type: `code`).
   - Sửa code để kiểm tra kết nối:
     ```javascript
     const { $ } = n8n;
     const { Postgres } = require('n8n-nodes-base').Postgres;

     const postgres = new Postgres();
     const connection = await postgres.connect({
       host: $.environment.postgres_host,
       port: $.environment.postgres_port,
       database: $.environment.postgres_db,
       user: $.environment.postgres_user,
       password: $.environment.postgres_password,
     });

     if (connection) {
       $.flow.set('postgres_connected', true);
     } else {
       $.flow.set('postgres_connected', false);
     }
     ```
   - Thêm biến môi trường trong n8n:
     - `postgres_host`, `postgres_port`, `postgres_db`, `postgres_user`, `postgres_password`.

#### **C. Cấu hình Mapping Fields**
Workflow sử dụng **Set** và **Code** để **biến đổi và mapping** các trường từ Airtable sang PostgreSQL.
1. Tìm node **"Field mapping"** (type: `set`).
2. Cập nhật **mapping** giữa các trường Airtable và PostgreSQL:
   ```json
   {
     "mapping": {
       "Name": "name",
       "Email": "email",
       "Created Time": "created_at",
       "Status": "status"
     }
   }
   ```
   - Thay đổi theo cấu trúc bảng của các sếp.

#### **D. Cấu hình Upsert Records**
Workflow sử dụng **Upsert** để **thêm hoặc cập nhật** dữ liệu trong PostgreSQL.
1. Tìm node **"Upsert records"** (type: `code`).
2. Sửa code để **upsert** dữ liệu:
   ```javascript
   const { $ } = n8n;
   const { Postgres } = require('n8n-nodes-base').Postgres;

   const postgres = new Postgres();
   const connection = await postgres.connect($.flow.get('postgres_credentials'));

   const query = `
     INSERT INTO ${$.flow.get('target_table')}
     (${Object.keys($.flow.get('mapping')).join(', ')})
     VALUES (${Object.values($.flow.get('mapping')).map(v => `'${v}'`).join(', ')})
     ON CONFLICT (id) DO UPDATE
     SET ${Object.keys($.flow.get('mapping')).map(k => `${k} = EXCLUDED.${k}`).join(', ')}
   `;

   await connection.query(query);
   ```
   - Thay `target_table` bằng tên bảng PostgreSQL.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và kiểm tra kết quả.
   - Sử dụng **Webhook** để khởi động quá trình.
2. **Bật Active Workflow**:
   - Chuyển trạng thái từ **Draft** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để thông báo kết quả.
   - Ví dụ: Sau khi hoàn thành, gửi tin nhắn:
     ```json
     {
       "text": "Migration completed successfully! Total records: ${$.flow.get('total_records')}"
     }
     ```

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron** để chạy workflow hàng ngày/lần tuần để kiểm tra sự đồng bộ.

3. **Xử lý lỗi tự động**:
   - Thêm node **Email/Slack** để thông báo lỗi nếu quá trình thất bại.

4. **Tối ưu hóa tốc độ**:
   - Sử dụng **Split In Batches** để xử lý dữ liệu theo từng batch nhỏ (tránh overloading).

---

## 📌 **Kết luận**
Workflow này **giải quyết hoàn toàn vấn đề di chuyển dữ liệu từ Airtable sang PostgreSQL một cách tự động, chính xác và hiệu quả**, giúp các sếp **tiết kiệm thời gian, giảm thiểu sai sót và tối ưu hóa quy trình làm việc**.

**Hãy áp dụng ngay và tự động hóa dữ liệu của mình!** 🚀
Nếu có bất kỳ câu hỏi nào, hãy để lại comment bên dưới. Chúc các sếp thành công! 💪