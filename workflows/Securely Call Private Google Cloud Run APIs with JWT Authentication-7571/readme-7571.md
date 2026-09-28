---
title: "🔒 Gọi API Google Cloud Run Bị Bảo Mật Với JWT - Tự Động Hóa An Toàn 100% Không Code"
description: "Tự động hóa việc gọi API Google Cloud Run bị bảo mật bằng JWT từ n8n, tiết kiệm thời gian và đảm bảo an toàn cho các dịch vụ DevOps. Workflow này tạo token JWT và gọi API Cloud Run một cách an toàn, không cần viết code."
slug: "goi-api-google-cloud-run-bang-jwt"
tags: [n8n, automation, google-cloud-run, jwt-authentication, devops]
keywords: [n8n workflow cloud run, tự động hóa gọi api google cloud run, jwt authentication n8n, bảo mật api cloud run, tự động hóa devops]
---

# 🔒 **Tự Động Hóa Gọi API Google Cloud Run Bị Bảo Mật Với JWT**

## **Nỗi Đau Thực Tế Của Các Sếp**
Các sếp đang gặp khó khăn khi phải gọi API của **Google Cloud Run** bị bảo mật bằng JWT từ các hệ thống tự động hóa như n8n. Thường thì phải:
- **Tạo token JWT thủ công** bằng Python/Node.js.
- **Quản lý token** một cách phức tạp, dễ bị lỗi.
- **Không đảm bảo an toàn** nếu token rò rỉ.

**Workflow này giải quyết tất cả!** Nó tự động tạo **JWT token** và gọi API Cloud Run một cách **an toàn, tự động và không cần code**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7, các sếp nên cài **n8n trên VPS riêng** (Self-hosted) để đảm bảo an toàn và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần viết code để tạo JWT.
✅ **An toàn tuyệt đối** – JWT được tạo và sử dụng tự động, không rò rỉ.
✅ **Hoạt động liên tục** – Workflow chạy 24/7 trên VPS.
✅ **Dễ dàng mở rộng** – Có thể kết nối với Slack, Email hoặc lưu log.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Google Cloud Run Service** được cấu hình yêu cầu **authentication**.
2. **Service Account** với quyền **Cloud Run Invoker**.
3. **File `.json key`** từ Google Cloud Console (để lấy `private_key` và `client_email`).
4. **URL của Cloud Run service** (base URL).
5. **n8n Self-hosted** (không dùng n8n.cloud để đảm bảo an toàn).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7571](https://n8n.io/workflows/7571).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste** JSON từ file vào n8n Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **A. Tạo Credential JWT (`jwtAuth`)**
- **Node:** `JWT`
- **Cách cấu hình:**
  - **Key Type:** `PEM Key`
  - **Private Key:** Dán toàn bộ nội dung từ file `.json key` (bao gồm `-----BEGIN PRIVATE KEY-----` và `-----END PRIVATE KEY-----`).
  - **Algorithm:** `RS256`
  - **Credentials Name:** `jwtAuth`

##### **B. Thiết Lập Variables (Set)**
- **Node:** `Edit Fields` (type: `set`)
- **Cấu hình biến:**
  - `service_url` → Điền **URL base của Cloud Run** (ví dụ: `https://your-service-url.a.run.app`).
  - `client_email` → Lấy từ file `.json key` (ví dụ: `your-service-account@project.iam.gserviceaccount.com`).
  - `token_uri` → Thường là `https://oauth2.googleapis.com/token`.

##### **C. Gửi Request Lấy Token JWT**
- **Node:** `Bearer Token Request` (type: `httpRequest`)
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `{{$json.token_uri}}`
  - **Headers:**
    - `Content-Type: application/x-www-form-urlencoded`
  - **Body:**
    ```json
    grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer&assertion={{$json.jwt}}
    ```
  - **Credentials:** Không cần (sử dụng JWT từ node trước).

##### **D. Gọi API Cloud Run Với Token**
- **Node:** `Cloud Run Request` (type: `httpRequest`)
- **Cấu hình:**
  - **Method:** `GET`/`POST` (tùy thuộc vào API).
  - **URL:** `{{$json.service_url}}/path` (thêm đường dẫn API sau URL base).
  - **Headers:**
    - `Authorization: Bearer {{ $json.id_token }}`
  - **Credentials:** `httpBearerAuth` (nếu cần).

##### **E. Manual Trigger (Bắt Đầu Workflow)**
- **Node:** `Execute` (type: `manualTrigger`)
- **Lưu ý:** Các sếp có thể thay bằng **Webhook** hoặc **Schedule Trigger** để tự động hóa.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **Execute** để kiểm tra.
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram** để thông báo kết quả.
2. **Lưu log** vào Google Sheets hoặc Firebase để theo dõi.
3. **Tự động hóa định kỳ** bằng **Schedule Trigger** thay vì Manual Trigger.
4. **Cập nhật token tự động** bằng **Set Node** để tránh hết hạn.

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **gọi API Google Cloud Run an toàn, tự động và không cần code**. Đặc biệt phù hợp cho các dự án **DevOps, AI Multimodal** hoặc bất kỳ hệ thống nào cần gọi API bị bảo mật.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho công ty!**

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/7571)**
**📖 [Hướng dẫn chi tiết từ Marco Cassar](https://medium.com/@marcocodes/build-a-secure-google-cloud-run-api-then-call-it-from-n8n-88c03291a95f)**