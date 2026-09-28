---
title: "🔒 API Truy Cập MongoDB An Toàn: Tự Động Hóa Lấy Dữ Liệu Với Kiểm Tra Thuộc Tính & Trả Lời HTTP"
description: "Workflow này tự động hóa việc tạo API HTTP an toàn để lấy toàn bộ tài liệu từ một collection MongoDB cụ thể, với kiểm tra tên collection, tránh tấn công injection và trả về dữ liệu chuẩn JSON. Giúp các sếp tiết kiệm thời gian phát triển và bảo mật dữ liệu hiệu quả."
slug: "api-mongodb-an-toan-tu-dong-hoa"
tags: [n8n, automation, no-code, mongodb, api-security, http-webhook]
keywords: [n8n workflow mongodb, tự động hóa api mongodb, kiểm tra tên collection, bảo mật api, webhook n8n, tự động hóa no-code]
---

# 🔒 API Truy Cập MongoDB An Toàn: Tự Động Hóa Lấy Dữ Liệu Với Kiểm Tra Thuộc Tính & Trả Lời HTTP

## 📌 Nỗi Đau Của Các Sếp
Hiện nay, nhiều doanh nghiệp phải mất thời gian và công sức để xây dựng API truy cập MongoDB thủ công. Các sếp thường phải:
- **Phát triển mã code** để kiểm tra tên collection và bảo mật API.
- **Lo lắng về an ninh** khi không kiểm tra được tên collection hợp lệ, dẫn đến nguy cơ tấn công injection.
- **Tốn thời gian** để chuẩn hóa dữ liệu trả về từ MongoDB (ví dụ: đổi `_id` thành `id`).
- **Không có giải pháp tự động hóa** để trả về dữ liệu một cách nhanh chóng và an toàn.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình với **không cần viết một dòng code nào**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **API an toàn**: Kiểm tra tên collection trước khi truy vấn, ngăn chặn tấn công injection và truy cập collection hệ thống.
- **Tiết kiệm thời gian phát triển**: Không cần viết code để kiểm tra và chuẩn hóa dữ liệu.
- **Trả về dữ liệu chuẩn**: Chuyển đổi `_id` thành `id` để dễ sử dụng trong ứng dụng.
- **Hoạt động liên tục**: Webhook hoạt động 24/7, không cần can thiệp thủ công.
- **Bảo mật cao**: Trả về mã lỗi 400 nếu tên collection không hợp lệ.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản MongoDB**:
   - Thông tin kết nối (URI MongoDB, tên database, tên collection).
   - **Credentials** trong n8n: Tạo credential mới với loại `MongoDB` và điền thông tin kết nối.
2. **n8n Instance**:
   - Đã cài đặt và chạy n8n (self-hosted hoặc dùng dịch vụ cloud).
3. **URL Webhook**:
   - Workflow sẽ tạo một endpoint dạng:
     ```
     https://<your-n8n-instance>/webhook/<uuid>/:nameCollection
     ```
     Ví dụ: `https://n8n.example.com/webhook/abc123/users` (truy vấn collection `users`).

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/7674).
2. Mở **n8n Editor** và nhấn `Import` → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào `Import Workflow` trong Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

##### **A. Node Webhook**
- **Không cần thay đổi gì** vì nó tự động tạo endpoint với tham số `:nameCollection`.
- Ví dụ: Khi gọi `GET https://n8n.example.com/webhook/abc123/customers`, `:nameCollection` sẽ là `customers`.

##### **B. Node MongoDB**
- **Credentials**:
  - Đi đến `Credentials` trong n8n → Tạo credential mới với loại `MongoDB`.
  - Điền:
    - **URI**: `mongodb://username:password@host:port/database`.
    - **Database Name**: Tên database bạn muốn truy cập.
  - Chọn credential này trong node **MongoDB** của workflow.
- **Query**:
  - Workflow sẽ tự động lấy tên collection từ `:nameCollection` và truy vấn toàn bộ tài liệu trong collection đó.

##### **C. Node "IDS format" (Code)**
- **Không cần chỉnh sửa** vì nó tự động chuyển đổi `_id` thành `id` trong dữ liệu trả về.

##### **D. Node "Validate Pattern" (Code)**
- **Regex kiểm tra tên collection**:
  ```javascript
  ^(?!system\.)[a-zA-Z0-9._]{1,120}$
  ```
  - **Nghĩa của regex**:
    - **Không cho phép** tên collection bắt đầu bằng `system.` (tránh truy cập collection hệ thống).
    - **Chỉ chấp nhận** ký tự: chữ cái (a-z, A-Z), số (0-9), dấu gạch dưới (`_`), và dấu chấm (`.`).
    - **Độ dài**: Từ 1 đến 120 ký tự.
  - **Nếu tên collection không hợp lệ**, workflow sẽ trả về **mã lỗi 400** với thông báo:
    ```json
    {
      "code": 400,
      "message": "Invalid collection name"
    }
    ```

##### **E. Node "If" (Kiểm tra hợp lệ)**
- **Nếu tên collection hợp lệ** → Tiếp tục truy vấn MongoDB.
- **Nếu tên collection không hợp lệ** → Trả về **mã lỗi 400** (node "Respond code 400").

##### **F. Node "Respond to Webhook" (Trả lời cuối cùng)**
- **Không cần chỉnh sửa** vì nó tự động trả về dữ liệu đã được chuẩn hóa (đổi `_id` thành `id`).

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Gọi endpoint với tên collection hợp lệ (ví dụ: `GET https://n8n.example.com/webflow/abc123/users`).
   - Kiểm tra phản hồi trong **n8n Editor** (tab `Executions`).
2. **Bật Active workflow**:
   - Đảm bảo workflow ở trạng thái **Active** để hoạt động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo lỗi đến Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** vào branch trả về lỗi (mã 400) để cảnh báo khi có yêu cầu không hợp lệ.
2. **Lưu log truy vấn**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại tất cả yêu cầu truy vấn (tên collection, thời gian, IP) để theo dõi và phân tích.
3. **Thêm xác thực API**:
   - Sử dụng node **HTTP Request** để yêu cầu API key trong header trước khi xử lý yêu cầu.
4. **Chỉnh sửa query MongoDB**:
   - Thêm filter hoặc sort trong node **MongoDB** để trả về dữ liệu theo yêu cầu cụ thể (ví dụ: chỉ lấy tài liệu mới nhất).
5. **Tạo API cho nhiều database**:
   - Sử dụng node **Code** để phân biệt database dựa trên tham số URL (ví dụ: `:databaseName`).
:::

---

### 📌 Kết luận
Workflow này **giúp các sếp xây dựng một API truy cập MongoDB an toàn, hiệu quả và không cần code**! Bằng cách tự động hóa việc kiểm tra tên collection, chuẩn hóa dữ liệu và trả về phản hồi HTTP chuẩn, các sếp sẽ tiết kiệm thời gian phát triển và giảm thiểu rủi ro bảo mật.

**Hãy áp dụng ngay workflow này và tự động hóa quy trình truy cập dữ liệu MongoDB của doanh nghiệp!** 🚀

---
:::note[LƯU Ý CUỐI CUNG]
- **Không sử dụng tên collection chứa dấu cách hoặc ký tự đặc biệt** (regex chỉ chấp nhận `a-z, A-Z, 0-9, _, .`).
- **Không truy cập collection hệ thống** (ví dụ: `system.users`), vì nó sẽ bị từ chối.
- **Nếu cần mở rộng**, các sếp có thể tham khảo [tài liệu chính thức của n8n](https://docs.n8n.io/) để thêm node mới.
:::

---
**Tác giả**: Samuel Heredia (n8n Community)
**Nguồn gốc**: [n8n Workflow 7674](https://n8n.io/workflows/7674)