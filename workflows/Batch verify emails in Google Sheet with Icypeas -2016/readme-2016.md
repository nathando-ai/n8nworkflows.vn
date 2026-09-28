---
title: "🚀 Tự Động Kiểm Tra Email Bulk Trên Google Sheet Với Icypeas (Không Cần Code)"
description: "Workflow này giúp các sếp tự động kiểm tra tính hợp lệ của hàng loạt email từ Google Sheet chỉ với một nhấp chuột, tiết kiệm thời gian và tăng độ chính xác cho danh sách khách hàng/một phần của bạn."
slug: "tieu-dong-kiem-tra-email-bulk-google-sheet-icypeas"
tags: [n8n, automation, sales, marketing, google-sheets, email-verification]
keywords: [tự động hóa email, kiểm tra email bulk, n8n workflow, icypeas api, google sheets tự động]
---

# 🚀 **Tự Động Kiểm Tra Email Bulk Trên Google Sheet Với Icypeas**

### **Giải quyết vấn đề gì?**
Các sếp thường phải mất **giờ đồng hồ** để kiểm tra tính hợp lệ của email thủ công, đặc biệt khi có danh sách khách hàng lớn. Với workflow này, chỉ cần **nhấp một nút**, hệ thống sẽ tự động:
✅ **Đọc danh sách email** từ Google Sheet.
✅ **Kết nối với Icypeas** để kiểm tra tính hợp lệ.
✅ **Trả về kết quả** (đúng/sai) trong Icypeas và email tự động.

**Kết quả?** Tiết kiệm **thời gian lên đến 80%** và giảm thiểu lỗi nhân sự!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra email một một.
- **Chính xác cao**: Sử dụng API Icypeas để xác minh email chuyên nghiệp.
- **Hoạt động liên tục**: Chạy tự động khi cần, không phụ thuộc vào nhân viên.
- **Dữ liệu cập nhật**: Kết quả được gửi về email và hiển thị trên Icypeas.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Icypeas**:
   - Đăng ký tại [icypeas.com](https://icypeas.com).
   - Lấy **API Key**, **API Secret** và **User ID** từ [đây](https://app.icypeas.com/bo/profile).
2. **Google Sheet**:
   - Tạo một bảng Google Sheet với **cột đầu tiên là "email"** (header chính xác là `email`).
   - Chia sẻ bảng với n8n bằng cách tạo **credentials Google Sheets** trong n8n.
3. **n8n Self-hosted** (không dùng phiên bản cloud).
4. **Crypto module** (nếu self-hosted, theo hướng dẫn bên dưới).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2016).
- Trong **n8n Editor**, nhấn **"Import"** và chọn file JSON.
- Hoặc **copy/paste** JSON vào ô **"Import Workflow"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Node "Reads lastname, firstname and company from your sheet" (Google Sheets)**
- **Chọn Credentials**:
  - Nhấn **"Add"** và chọn **"Google Sheets"** (nếu chưa có).
  - Điền **Email** và **Password** của tài khoản Google liên kết với Sheet.
- **Config Node**:
  - **Sheet Name**: Tên của Google Sheet.
  - **Range**: Chọn **"Sheet1!A:A"** (nếu cột email ở cột A).
  - **Headers**: Bật **"Use headers for column names"**.

##### **B. Node "Authenticates to your Icypeas account" (Code)**
- Mở node **Code** và thay thế:
  ```javascript
  const API_KEY = "**PUT_API_KEY_HERE**";
  const API_SECRET = "**PUT_API_SECRET_HERE**";
  const USER_ID = "**PUT_USER_ID_HERE**";
  ```
  - **Lấy từ Icypeas**:
    - API Key: `https://app.icypeas.com/bo/profile` → **API Key**.
    - API Secret: `https://app.icypeas.com/bo/profile` → **API Secret**.
    - User ID: `https://app.icypeas.com/bo/profile` → **User ID**.

- **Nếu self-hosted**:
  - Theo hướng dẫn bên dưới để **bật Crypto module**:
    ```markdown
    1. Truy cập n8n instance → Settings → General.
    2. Tìm phần **"Additional Node Packages"** → Check **"crypto"**.
    3. Save và restart n8n.
    ```

##### **C. Node "Run bulk search (email-verif)" (HTTP Request)**
- **Thiết lập Credentials**:
  - Nhấn **"Add"** → **"Create new Credential"** → Tên: **"Authorization"**.
  - Trong **Value**, chọn **"Expression"** và điền:
    ```javascript
    {{ $json.api.key + ':' + $json.api.signature }}
    ```
  - **Lưu** và chọn credential này trong node HTTP Request.

- **Config Node**:
  - **Method**: `POST`.
  - **URL**: `https://api.icypeas.com/v1/bulksearch/email-verification`.
  - **Headers**:
    - `Content-Type`: `application/json`.
    - `Authorization`: (sử dụng credential vừa tạo).
  - **Body**:
    ```json
    {
      "emails": [
        {"email": "{{ $node["Reads lastname, firstname and company from your sheet"].json[0].email }}"}
      ],
      "api_key": "{{ $json.api.key }}",
      "api_secret": "{{ $json.api.secret }}"
    }
    ```
    - **Lưu ý**: Nếu Sheet có nhiều email, cần **loop** qua danh sách (xem phần **Mẹo nâng cao**).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **"Execute Workflow"** (node Manual Trigger).
  - Kiểm tra **log** và kết quả trên Icypeas: [https://app.icypeas.com/bo/bulksearch](https://app.icypeas.com/bo/bulksearch).
- **Bật Active**:
  - Chuyển toggle **"Active"** sang **ON**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Xử lý danh sách email dài**:
   - Sử dụng **Loop** (node `Function`) để xử lý từng email một trong một danh sách lớn.
   - Ví dụ:
     ```javascript
     // Node Function trước HTTP Request
     return {
       json: {
         emails: $node["Reads lastname, firstname and company from your sheet"].json.map(email => ({
           email: email.email
         }))
       }
     };
     ```

2. **Gửi báo cáo tự động**:
   - Thêm node **Email** (n8n-nodes-base.email) để gửi kết quả về email định kỳ.
   - Config:
     - **To**: Email của bạn.
     - **Subject**: `"Kết quả kiểm tra email bulk - [Ngày]`".
     - **Body**: `{{ $json.results }}`.

3. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo kết quả ngay khi hoàn thành.

4. **Lưu log vào Google Sheet**:
   - Sử dụng node **Google Sheets (Write)** để ghi kết quả (đúng/sai) vào một Sheet mới.

---

### 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa quy trình kiểm tra email bulk chỉ trong vài phút**, tiết kiệm thời gian và tăng độ chính xác. **Hãy áp dụng ngay** và giảm bớt công việc thủ công!

👉 **Bắt đầu ngay**: [Tải workflow](https://n8n.io/workflows/2016) và **import** vào n8n của bạn!

---
**Chia sẻ ý kiến** hoặc **hỏi đáp** trong comment bên dưới! 🚀