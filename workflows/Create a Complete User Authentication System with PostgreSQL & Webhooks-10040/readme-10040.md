---
title: "🔐 **Hướng Dẫn Tự Động Hóa Hệ Thống Xác Thực Người Dùng (Signup/Login/Password Reset) Với PostgreSQL & Webhooks - N8n**"
description: "Workflow này tự động hóa toàn bộ quy trình xác thực người dùng (đăng ký, đăng nhập, quên mật khẩu) trên PostgreSQL/Supabase chỉ với 1 webhook duy nhất. Giúp các sếp tiết kiệm thời gian phát triển, giảm thiểu lỗi thủ công và đảm bảo an toàn thông tin người dùng."
slug: "tự-dộng-hoa-he-thong-xac-thuc-nguoi-dung-postgresql-webhooks-n8n"
tags: [n8n, automation, no-code, postgresql, supabase, authentication, webhook]
keywords: [n8n workflow xác thực người dùng, tự động hóa đăng ký đăng nhập, PostgreSQL với n8n, hệ thống xác thực không code, webhook xác thực người dùng]
---

# 🚀 **Tự Động Hóa Hệ Thống Xác Thực Người Dùng (Signup/Login/Password Reset) Với PostgreSQL & Webhooks**

### **Nỗi Đau Của Các Sếp**
Hiện nay, việc xây dựng một hệ thống xác thực người dùng (đăng ký, đăng nhập, quên mật khẩu) thường đòi hỏi:
- **Phát triển code thủ công** (Backend, API, logic xác thực).
- **Quản lý cơ sở dữ liệu** (PostgreSQL/Supabase) và cấu hình an toàn.
- **Xử lý lỗi thủ công** (trùng email, mật khẩu không khớp, email không tồn tại).
- **Tích hợp với frontend** (API calls, validation).

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** với **1 webhook duy nhất** (`/webhook/auth`).
✅ **Sử dụng PostgreSQL/Supabase** để lưu trữ và bảo mật dữ liệu người dùng.
✅ **Hỗ trợ 3 chức năng chính**:
   - **Đăng ký (Signup)**: Tạo tài khoản mới với mật khẩu được mã hóa bcrypt.
   - **Đăng nhập (Login)**: Xác thực email và mật khẩu (không phân biệt chữ hoa/thường).
   - **Quên mật khẩu (Forgot Password)**: Tạo mật khẩu ngẫu nhiên và cập nhật vào cơ sở dữ liệu.
✅ **Trả về phản hồi chuẩn JSON** để tích hợp dễ dàng với frontend (React, Vue, Flutter...).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và an toàn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho PostgreSQL).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian phát triển**: Không cần viết code backend cho xác thực.
- **An toàn tuyệt đối**: Mật khẩu được mã hóa bcrypt, email không phân biệt chữ hoa/thường.
- **Tích hợp dễ dàng**: API trả về JSON chuẩn, dễ dàng kết nối với frontend.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7 trên VPS.
- **Dễ dàng mở rộng**: Thêm chức năng như **OTP 2FA** hoặc **gửi email xác nhận** sau này.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Cơ sở dữ liệu PostgreSQL/Supabase**:
   - **Bảng `users`** với các cột: `id (UUID)`, `full_name`, `email`, `password_hash`, `created_at`.
   - **Extensions** được kích hoạt: `uuid-ossp` và `pgcrypto`.
   - **Constraint** duy nhất cho `email` để tránh trùng lặp.

2. **Credentials trong n8n**:
   - **PostgreSQL Credentials**: Thêm vào n8n với thông tin kết nối đến cơ sở dữ liệu của bạn.

3. **API Key (nếu sử dụng Supabase)**:
   - Nếu dùng Supabase, thêm **API Key** vào n8n để truy cập cơ sở dữ liệu.

4. **Frontend (tùy chọn)**:
   - Một ứng dụng hoặc trang web gửi request POST đến `/webhook/auth` với payload JSON.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10040](https://n8n.io/workflows/10040) hoặc copy/paste JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": {
      "1": {
        "parameters": {
          "path": "auth",
          "httpMethod": "POST"
        },
        "name": "Webhook",
        "type": "n8n-nodes-base.webhook"
      },
      "2": {
        "parameters": {},
        "name": "Router",
        "type": "n8n-nodes-base.switch"
      },
      "3": {
        "parameters": {
          "operation": "executeQuery",
          "query": "INSERT INTO users (full_name, email, password_hash) VALUES ('{{$json[\"name\"]}}', '{{$json[\"email\"]}}', crypt('{{$json[\"password\"]}}', gen_salt('bf'))) RETURNING id, full_name, email, created_at;"
        },
        "name": "Signup",
        "type": "n8n-nodes-base.postgres",
        "credentials": {
          "postgres": "postgres"
        }
      },
      "4": {
        "parameters": {
          "operation": "executeQuery",
          "query": "SELECT id, full_name, email, (password_hash = crypt('{{$json[\"password\"]}}', password_hash)) AS \"isPasswordMatch\" FROM users WHERE LOWER(email) = LOWER('{{$json[\"email\"]}}');"
        },
        "name": "Login",
        "type": "n8n-nodes-base.postgres",
        "credentials": {
          "postgres": "postgres"
        }
      },
      "5": {
        "parameters": {
          "condition": {
            "logic": "and",
            "values": [
              {
                "propertyName": "id",
                "operator": "isNotNull"
              },
              {
                "propertyName": "isPasswordMatch",
                "operator": "isTrue"
              }
            ]
          }
        },
        "name": "Check Login",
        "type": "n8n-nodes-base.if"
      },
      "6": {
        "parameters": {
          "operation": "executeQuery",
          "query": "WITH new_pass AS (SELECT substring(md5(random()::text) from 1 for 8) AS plain_password) UPDATE users SET password_hash = crypt(new_pass.plain_password, gen_salt('bf')) FROM new_pass WHERE LOWER(email) = LOWER('{{$json[\"email\"]}}') RETURNING email, new_pass.plain_password AS newPassword;"
        },
        "name": "Reset Password",
        "type": "n8n-nodes-base.postgres",
        "credentials": {
          "postgres": "postgres"
        }
      },
      "7": {
        "parameters": {},
        "name": "Respond",
        "type": "n8n-nodes-base.respondToWebhook"
      }
    },
    "connections": {
      "main": [
        {
          "node": "1",
          "connection": "main",
          "port": "trigger",
          "to": "2"
        },
        {
          "node": "2",
          "connection": "main",
          "port": "signup",
          "to": "3"
        },
        {
          "node": "3",
          "connection": "main",
          "port": "json",
          "to": "7"
        },
        {
          "node": "2",
          "connection": "main",
          "port": "signin",
          "to": "4"
        },
        {
          "node": "4",
          "connection": "main",
          "port": "json",
          "to": "5"
        },
        {
          "node": "5",
          "connection": "iftrue",
          "port": "true",
          "to": "7"
        },
        {
          "node": "5",
          "connection": "iffalse",
          "port": "false",
          "to": "7"
        },
        {
          "node": "2",
          "connection": "main",
          "port": "forgot",
          "to": "6"
        },
        {
          "node": "6",
          "connection": "main",
          "port": "json",
          "to": "7"
        }
      ]
    }
  }
  ```

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **🔹 Node Webhook (Node 1)**
- **Path**: Đặt là `auth` (không đổi).
- **HTTP Method**: Chỉ hỗ trợ `POST`.
- **Payload**: Nhận JSON với cấu trúc:
  ```json
  {
    "path": "signup|signin|forgot",
    "email": "string",
    "password": "string",
    "name": "string"  // (chỉ cần khi signup)
  }
  ```
  **Ví dụ**:
  ```json
  {
    "path": "signup",
    "email": "user@example.com",
    "password": "Pass123!",
    "name": "John Doe"
  }
  ```

##### **🔹 Node Switch (Node 2 - Router)**
- **Cấu hình rules** để phân luồng:
  - `signup` → Node **Signup (Node 3)**.
  - `signin` → Node **Login (Node 4)**.
  - `forgot` → Node **Reset Password (Node 6)**.
- **Lưu ý**: Giá trị `path` **phải là lowercase** (ví dụ: `"signup"` chứ không phải `"SIGNUP"`).

##### **🔹 Node PostgreSQL (Signup, Login, Reset Password)**
- **Credentials**: Chọn **postgres** (đã cấu hình trước).
- **Query SQL**:
  - **Signup**: Sử dụng `crypt()` để mã hóa mật khẩu bcrypt.
  - **Login**: Kiểm tra mật khẩu bằng `crypt()` và so sánh với mật khẩu đã lưu.
  - **Reset Password**: Tạo mật khẩu ngẫu nhiên 8 ký tự và cập nhật vào cơ sở dữ liệu.

##### **🔹 Node IF (Check Login - Node 5)**
- **Điều kiện**: Kiểm tra `id` không null **và** `isPasswordMatch` là `true`.
- **Nếu đúng**: Trả về phản hồi thành công.
- **Nếu sai**: Trả về lỗi (mật khẩu hoặc email không đúng).

##### **🔹 Node Respond (Node 7)**
- **Phản hồi chuẩn JSON**:
  ```json
  {
    "status": "success|error",
    "message": "string",
    "data": {}
  }
  ```
  - **Thành công**:
    ```json
    {
      "status": "success",
      "message": "User created/Logged in successfully",
      "data": { "id": "uuid", "email": "user@example.com" }
    }
    ```
  - **Lỗi**:
    ```json
    {
      "status": "error",
      "message": "Invalid email or password",
      "data": {}
    }
    ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi request POST đến `http://<your-n8n-url>/webhook/auth` với payload:
     ```json
     {
       "path": "signup",
       "email": "test@example.com",
       "password": "Test123!",
       "name": "Test User"
     }
     ```
   - Kiểm tra phản hồi trong **n8n Dashboard**.

2. **Bật Active workflow**:
   - Chuyển trạng thái từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Gửi Email Xác Nhận (OTP)**:
   - Thêm node **Email** (n8n-nodes-base.email) sau **Signup** để gửi email xác nhận đăng ký.

2. **Log Lịch Sử Hành Động**:
   - Thêm node **Sticky Note** (n8n-nodes-base.stickyNote) để ghi log tất cả các request (đăng ký, đăng nhập, quên mật khẩu).

3. **Tích Hợp Slack/Telegram**:
   - Sau khi **Reset Password**, gửi thông báo đến Slack/Telegram thông báo mật khẩu mới.

4. **Cập Nhật Mật Khẩu Hết Hạn**:
   - Thêm logic kiểm tra mật khẩu cũ và yêu cầu người dùng cập nhật sau một thời gian.

5. **Bảo Mật API Key**:
   - **Không bao giờ** chia sẻ API Key PostgreSQL/Supabase với bên thứ ba.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp** khỏi việc phát triển code xác thực từ đầu, đồng thời **đảm bảo an toàn và hiệu quả** với PostgreSQL/Supabase. **Chỉ cần 1 webhook duy nhất** đã đủ để quản lý **đăng ký, đăng nhập và quên mật khẩu** một cách tự động hóa hoàn toàn.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình PostgreSQL.
3. **Test với frontend** của bạn và **bắt đầu sử dụng ngay!**

🚀 **N8n không chỉ tự động hóa, mà còn làm cho công việc trở nên đơn giản hơn!**