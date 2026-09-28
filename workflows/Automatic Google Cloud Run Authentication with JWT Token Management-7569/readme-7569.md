---
title: "🔐 Tự Động Hóa Xác Thực Google Cloud Run Với JWT Token - Không Cần Code!"
description: "Giải pháp tự động hóa 100% không cần code để quản lý JWT token cho Google Cloud Run, tự động kiểm tra và tái tạo token khi hết hạn, giảm thiểu rủi ro lỗi xác thực và tiết kiệm API quota."
slug: "tu-dong-hoa-xac-thuc-google-cloud-run-jwt-token"
tags: [n8n, automation, google-cloud-run, jwt, api-authentication, no-code]
keywords: [n8n workflow google cloud run, tự động hóa xác thực jwt, quản lý token google cloud, tự động hóa không code, api authentication n8n]
---

# 🚀 **Tự Động Hóa Xác Thực Google Cloud Run Với JWT Token - Không Cần Code!**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải đối mặt với những vấn đề phức tạp khi làm việc với **Google Cloud Run**:
- **Xác thực thủ công**: Phải tự viết mã hoặc sử dụng các công cụ phức tạp để quản lý token JWT.
- **Rủi ro token hết hạn**: Token JWT có thời hạn (thường 60 phút), nếu không kiểm tra kịp thời, API sẽ bị từ chối.
- **Tốn thời gian và API quota**: Mỗi lần gọi API để lấy token mới sẽ tiêu tốn quota của Google Cloud.
- **Không tự động hóa**: Các workflow phải dừng lại khi token hết hạn, gây gián đoạn công việc.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động kiểm tra token hiện tại** trước khi sử dụng.
✅ **Tái tạo token mới chỉ khi cần thiết** (trong vòng 5 phút trước khi hết hạn).
✅ **Tiết kiệm API quota** bằng cách tránh gọi API không cần thiết.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết mã hoặc quản lý token thủ công.
- **Tăng tính bảo mật**: Token được tự động kiểm tra và tái tạo khi cần thiết.
- **Hoạt động liên tục**: Workflow không bị gián đoạn do token hết hạn.
- **Tối ưu API quota**: Tránh gọi API không cần thiết, tiết kiệm chi phí.
- **Dễ dàng tích hợp**: Sử dụng được trong các workflow lớn hơn với **Execute Workflow** node.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **Google Cloud Run Service**:
   - Đã cấu hình **Require authentication** (Yêu cầu xác thực).
   - **Service Account** với quyền **Cloud Run Invoker**.
2. **File `.json key`** của Service Account:
   - Trích xuất **`client_email`** và **`private_key`** (để tạo credential JWT trong n8n).
3. **Credentials JWT trong n8n**:
   - **Key Type**: `PEM Key`
   - **Private Key**: Nội dung của `private_key` (bao gồm cả `-----BEGIN PRIVATE KEY-----` và `-----END PRIVATE KEY-----`).
   - **Algorithm**: `RS256`.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/7569](https://n8n.io/workflows/7569).
2. Trong **n8n Editor**, chọn **Import Workflow** và chọn file JSON đã tải.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** từ menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **10 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu Hình Credential JWT (`jwtAuth`)**
- **Node**: `Decode JWT` và `Sign New JWT`.
- **Hành động**:
  1. Tạo **new credential** trong n8n với tên `jwtAuth`.
  2. Chọn **Key Type**: `PEM Key`.
  3. Điền **Private Key**: Nội dung của `private_key` từ file `.json key` (không bỏ sót dòng đầu và cuối).
  4. Chọn **Algorithm**: `RS256`.

##### **B. Cấu Hình Node `Bearer Token Request`**
- **Node**: `Bearer Token Request` (HTTP Request).
- **Hành động**:
  - Điền **URL**: `https://[YOUR-CLOUD-RUN-SERVICE].a.run.app/[SERVICE-PATH]` (thay `[YOUR-CLOUD-RUN-SERVICE]` và `[SERVICE-PATH]` bằng URL thực tế của dịch vụ Cloud Run).
  - **Headers**:
    - `Authorization`: `Bearer ${{$json["id_token"]}}` (token JWT sẽ được tự động điền từ workflow).
  - **Method**: `GET` (hoặc `POST` tùy thuộc vào API của bạn).

##### **C. Cấu Hình Node `Execute Workflow Trigger` (Start)**
- **Node**: `Start` (Execute Workflow Trigger).
- **Hành động**:
  - Nếu sử dụng **standalone**, các sếp cần **pin** giá trị `service_url` và `service_path` vào **Execution Parameters**.
  - Nếu sử dụng **sub-workflow**, các sếp chỉ cần truyền **`id_token`** (nếu có) vào node này.

##### **D. Cấu Hình Node `If` (Kiểm Tra Token)**
- **Node**: `If Token` và `If` (các node điều kiện).
- **Hành động**:
  - Các node này tự động kiểm tra token:
    - Nếu token **hết hạn**, workflow sẽ tạo token mới.
    - Nếu token **còn hiệu lực**, workflow sẽ sử dụng token đó.
    - Nếu token **sắp hết hạn (trong 5 phút)**, workflow sẽ tự động tái tạo token mới.

##### **E. Cấu Hình Node `Merge` (Combine Context)**
- **Node**: `Combine Context` (Merge).
- **Hành động**:
  - Node này kết hợp các dữ liệu từ các node trước đó (như `id_token`, `service_url`, `service_path`) để trả về kết quả cuối cùng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và truyền dữ liệu mẫu (nếu có).
   - Kiểm tra kết quả trong **Execution Details** để đảm bảo token được tạo và sử dụng đúng.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi token hết hạn hoặc tái tạo thành công.
   - Ví dụ: `{{$json["message"]}}: Token đã được tái tạo thành công!`.

2. **Lưu Log Token**:
   - Sử dụng node **Google Sheets** hoặc **Database** để lưu lịch sử token (giúp theo dõi và debug dễ dàng).

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow định kỳ (ví dụ: hàng ngày) để kiểm tra và tái tạo token nếu cần.

4. **Tích Hợp Với Workflow Khác**:
   - Sử dụng **Execute Workflow** node để gọi workflow này từ các workflow lớn hơn (ví dụ: khi gọi API Cloud Run từ một workflow tự động hóa khác).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **xác thực Google Cloud Run** mà **không cần viết một dòng code**. Bằng cách tự động kiểm tra và tái tạo token JWT, workflow này **giảm thiểu rủi ro lỗi**, **tiết kiệm thời gian** và **tối ưu hóa chi phí API**.

**Hãy áp dụng ngay để:**
✔ **Tự động hóa hoàn toàn** quá trình xác thực.
✔ **Tránh gián đoạn** do token hết hạn.
✔ **Tiết kiệm API quota** của Google Cloud.

**Bắt đầu ngay với n8n và Google Cloud Run hôm nay!** 🚀