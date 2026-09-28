---
title: "🔐 Hệ Thống Xác Minh JWT Tự Hosted: Đăng Ký, Đăng Nhập & Quản Lý Token Mạnh Mẽ Cho Ứng Dụng Của Các Sếp"
description: "Workflow này tự động hóa toàn bộ quy trình xác minh JWT (JSON Web Token) với quản lý token an toàn, bao gồm đăng ký, đăng nhập, xác thực và làm mới token. Giúp các sếp xây dựng hệ thống xác minh chuyên nghiệp, an toàn và không cần viết code thủ công."
slug: "he-thong-xac-minh-jwt-tu-hosted"
tags: [n8n, authentication, jwt, self-hosted, no-code, security, database]
keywords: [n8n workflow jwt, tự động hóa xác minh jwt, quản lý token an toàn, đăng ký đăng nhập tự động, n8n self-hosted, hệ thống xác thực không code]
---

# 🚀 Hệ Thống Xác Minh JWT Tự Hosted: Đăng Ký, Đăng Nhập & Quản Lý Token Cho Ứng Dụng

## 📌 Nỗi Đau Của Các Sếp
Hiện nay, khi xây dựng ứng dụng web hoặc API, các sếp thường phải đầu tư thời gian và nguồn lực để triển khai hệ thống xác minh (authentication) phức tạp như JWT. Các giải pháp truyền thống yêu cầu viết code thủ công, quản lý secret keys, và đảm bảo an toàn cho token, dẫn đến:
- **Rủi ro bảo mật cao**: Token bị lộ hoặc không được bảo vệ an toàn.
- **Quá trình đăng ký/dăng nhập phức tạp**: Phải kiểm tra trùng lặp username/email, mã hóa mật khẩu, và quản lý token.
- **Không linh hoạt**: Khi cần thay đổi cấu hình (ví dụ: thời hạn token), phải sửa code thủ công.
- **Không tự động hóa**: Các quy trình như làm mới token hay revoke token phải thực hiện thủ công.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình xác minh JWT với **an toàn cao, không cần code**, và dễ dàng tùy chỉnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Xác minh JWT chuyên nghiệp**: Đăng ký, đăng nhập, xác thực và làm mới token một cách tự động.
- **Bảo mật cao**: Sử dụng salt, HMAC-SHA256, và hai loại token (access + refresh) để giảm thiểu rủi ro.
- **Quản lý token linh hoạt**: Làm mới token tự động khi access token hết hạn, revoke token khi cần.
- **Không cần viết code**: Tất cả logic xác minh được tự động hóa trong n8n.
- **Dễ dàng tùy chỉnh**: Thay đổi thời hạn token, thuật toán hash, hoặc cấu trúc JWT chỉ bằng cách chỉnh sửa các node code.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không cần can thiệp thủ công.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted**: Cài đặt n8n trên VPS (hướng dẫn [tại đây](https://docs.n8n.io/)).
2. **Bảng dữ liệu (Data Tables)** trong n8n:
   - **Table `users`**: Chứa thông tin người dùng (email, username, password_hash, refresh_token).
   - **Table `refresh_tokens`**: Chứa token refresh đã hash (token_hash, user_id, expires_at).
3. **Secret Keys**:
   - **ACCESS_SECRET**: Chữ ký cho access token.
   - **REFRESH_SECRET**: Chữ ký cho refresh token.
   *(Xem hướng dẫn [migrating to Variables](#migrating-to-variables) để sử dụng biến toàn cầu thay vì Set Node.)*
4. **API Keys hoặc Credentials**: Không cần, workflow này hoàn toàn tự chứa logic xác minh.
5. **Kiến thức cơ bản về JWT**: Hiểu về cấu trúc token, header, payload, và signature để tùy chỉnh dễ dàng.
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/9660).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
   *Hoặc* copy toàn bộ nội dung JSON và dán vào **Import Workflow** trong giao diện.

#### 2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌
Workflow này gồm **63 node** và được chia thành 4 flow chính: **Registration**, **Login**, **Verify Token**, và **Refresh Token**. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu Hình Bảng Dữ Liệu (Data Tables)**
Trước khi kích hoạt workflow, các sếp cần tạo **hai bảng dữ liệu** trong n8n:
1. **Table `users`**:
   - **Cột**:
     - `email` (string): Địa chỉ email của người dùng.
     - `username` (string): Tên đăng nhập.
     - `password_hash` (string): Dạng `"salt:hash"` (ví dụ: `"a4f9c8:9f86d0..."`).
     - `refresh_token` (string): Token refresh hiện tại (nếu có).
   - *Lưu ý*: Cột `password_hash` sẽ được tự động cập nhật khi người dùng đăng ký.

2. **Table `refresh_tokens`**:
   - **Cột**:
     - `token_hash` (string): Token refresh đã hash (SHA-256).
     - `user_id` (number): ID người dùng sở hữu token.
     - `expires_at` (datetime): Thời gian hết hạn token.

##### **B. Cấu Hình Secret Keys**
Workflow này sử dụng **hai secret key** để chữ ký token:
- **ACCESS_SECRET**: Dùng để chữ ký access token.
- **REFRESH_SECRET**: Dùng để chữ ký refresh token.
*Không thể thiếu*: Các secret này **phải giống nhau** trong tất cả các workflow liên quan (Login, Verify, Refresh).

**Lưu ý quan trọng**:
- **Không nên đặt secret keys trong Set Node** (ví dụ: `'SET ACCESS AND REFRESH SECRET'`). Thay vào đó, các sếp nên sử dụng **Variables** để quản lý toàn cầu.
- Hướng dẫn [migrating to Variables](#migrating-to-variables) sẽ giúp các sếp chuyển đổi từ Set Node sang Variables.

##### **C. Cấu Hình Node Quản Lý Token**
1. **Node `SET ACCESS AND REFRESH SECRET`**:
   - Thay vì đặt secret keys trực tiếp, các sếp nên tạo **Variables** trong n8n:
     - Tạo biến `ACCESS_SECRET` và `REFRESH_SECRET` với giá trị ngẫu nhiên (ví dụ: `abc123xyz456`).
     - Sử dụng biến này trong các node `Sign Access Token`, `Sign Refresh Token`, `Verify Signature`, và `Verify HMAC Signature`.

2. **Node `Generate Salt` và `Hash Password`**:
   - Các node này tự động tạo salt và hash mật khẩu. **Không cần chỉnh sửa**.

3. **Node `Registration Webhook` và `Login Webhook`**:
   - Cấu hình **path** và **HTTP Method** như trong danh sách nodes:
     - `register-user` (POST)
     - `login` (POST)
   - Các node này sẽ xử lý yêu cầu đăng ký và đăng nhập từ client.

4. **Node `Verify Access Token` và `Refresh Access Token`**:
   - Cấu hình **path**:
     - `verify-token` (POST)
     - `refresh` (POST)
   - Các node này sẽ xử lý yêu cầu xác thực và làm mới token.

##### **D. Cấu Hình Node Code**
Workflow này sử dụng nhiều node **Code** để xử lý logic phức tạp. Các sếp **không cần chỉnh sửa** nội dung code trong các node này, nhưng có thể tùy chỉnh:
- **Thời hạn token**: Tìm và thay đổi giá trị trong node `Create JWT Payload` (ví dụ: `exp: now + (15 * 60)` thành `exp: now + (30 * 60)` để token hết hạn sau 30 phút).
- **Cấu trúc JWT**: Thêm hoặc loại bỏ trường trong payload (ví dụ: `sub`, `iat`, `exp`, `user_id`).

##### **E. Node `DataTable`**
- Các node `Get User`, `Create User`, `Update User Refresh Token`, và `Store Refresh Token` sẽ tương tác với bảng `users` và `refresh_tokens`.
- **Không cần cấu hình thêm**, workflow sẽ tự động xử lý.

#### 3. Kích Hoạt ⚡️
1. **Test Run**:
   - Các sếp có thể chạy **test run** với dữ liệu mẫu để kiểm tra workflow:
     - **Registration**: Gửi yêu cầu POST đến `/register-user` với payload:
       ```json
       {
         "email": "test@example.com",
         "username": "testuser",
         "password": "password123"
       }
       ```
     - **Login**: Gửi yêu cầu POST đến `/login` với payload:
       ```json
       {
         "email": "test@example.com",
         "password": "password123"
       }
       ```
     - **Verify Token**: Gửi yêu cầu POST đến `/verify-token` với payload:
       ```json
       {
         "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
       }
       ```
     - **Refresh Token**: Gửi yêu cầu POST đến `/refresh` với payload:
       ```json
       {
         "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
       }
       ```
   - Kiểm tra phản hồi từ workflow để đảm bảo logic hoạt động đúng.

2. **Bật Active Workflow**:
   - Sau khi test thành công, các sếp có thể **bật Active** workflow để nó hoạt động liên tục.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
:::info[Mẹo Sử Dụng]
1. **Lưu Log Cho Debugging**:
   - Thêm node **Sticky Note** hoặc **Set** để lưu thông tin debug (ví dụ: token, thời gian hết hạn) vào một bảng dữ liệu riêng.
   - Ví dụ: Tạo bảng `logs` với cột `timestamp`, `action`, `user_id`, `token`, và `status`.

2. **Gửi Báo Cáo Token Hết Hạn**:
   - Sử dụng node **Email** hoặc **Slack** để thông báo khi refresh token sắp hết hạn.
   - Ví dụ: Khi `expires_at` trong `refresh_tokens` gần ngày hôm nay, gửi email cảnh báo cho admin.

3. **Revoke Token Tự Động**:
   - Thêm logic để revoke tất cả token của một người dùng khi họ đăng xuất.
   - Sử dụng node `Delete` để xóa token trong `refresh_tokens` khi người dùng đăng xuất.

4. **Kết Hợp Với Ứng Dụng Client**:
   - Sử dụng **n8n Webhook** để client gửi yêu cầu đăng ký/dăng nhập/xác thực.
   - Ví dụ: Trong ứng dụng React/Vue, gọi API đến `/register-user`, `/login`, `/verify-token`, và `/refresh`.

5. **Tùy Chỉnh Thời Hạn Token**:
   - Thay đổi thời hạn token trong node `Create JWT Payload`:
     - Access token: `exp: now + (15 * 60)` (15 phút).
     - Refresh token: `exp: now + (7 * 24 * 60 * 60)` (7 ngày).

6. **Sử Dụng Variables Cho Secret Keys**:
   - Thay vì đặt secret keys trong Set Node, tạo **Variables** trong n8n:
     - Tạo biến `ACCESS_SECRET` và `REFRESH_SECRET`.
     - Sử dụng biến này trong các node `Sign Access Token`, `Sign Refresh Token`, `Verify Signature`, và `Verify HMAC Signature`.
   - Hướng dẫn chi tiết [migrating to Variables](#migrating-to-variables).

7. **Bảo Mật Token Refresh**:
   - Token refresh được **hash trước khi lưu vào database** (SHA-256), giúp bảo vệ nếu database bị rò rỉ.
   - Khi client gửi token refresh, workflow sẽ **hash lại** và so sánh với token đã lưu.

8. **Xác Minh Multi-Factor (MFA) Nâng Cao**:
   - Thêm bước xác minh MFA (ví dụ: OTP) trước khi cấp refresh token.
   - Sử dụng node **Code** để kiểm tra OTP từ client.

---

### 🔒 Migrating to Variables (Cách Sử Dụng Variables Thay Vì Set Node)
Workflow này ban đầu sử dụng **Set Node** để đặt secret keys (`ACCESS_SECRET` và `REFRESH_SECRET`). Tuy nhiên, **không khuyến khích** cách này vì:
- Secret keys sẽ bị giới hạn trong workflow cụ thể.
- Khó khăn khi chia sẻ secret keys giữa các workflow.

**Hướng dẫn chuyển đổi**:
1. **Tạo Variables**:
   - Trong n8n, chuyển đến **Settings** > **Variables**.
   - Tạo hai biến mới:
     - `ACCESS_SECRET`: Giá trị ngẫu nhiên (ví dụ: `abc123xyz456`).
     - `REFRESH_SECRET`: Giá trị ngẫu nhiên khác (ví dụ: `xyz789abc123`).

2. **Chỉnh Sửa Node**:
   - **Node `Sign Access Token`**:
     - Thay đổi `ACCESS_SECRET` từ giá trị trong Set Node thành `$ACCESS_SECRET`.
   - **Node `Sign Refresh Token`**:
     - Thay đổi `REFRESH_SECRET` từ giá trị trong Set Node thành `$REFRESH_SECRET`.
   - **Node `Verify Signature`**:
     - Thay đổi `ACCESS_SECRET` thành `$ACCESS_SECRET`.
   - **Node `Verify HMAC Signature`**:
     - Thay đổi `REFRESH_SECRET` thành `$REFRESH_SECRET`.
   - **Node `Sign New Access Token`**:
     - Thay đổi `ACCESS_SECRET` thành `$ACCESS_SECRET`.

3. **Xóa Set Node**:
   - Xóa các node `SET ACCESS AND REFRESH SECRET`, `SET ACCESS AND REFRESH SECRET1