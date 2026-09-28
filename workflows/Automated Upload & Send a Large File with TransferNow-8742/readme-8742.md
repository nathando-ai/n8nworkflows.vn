---
title: "🚀 Tự Động Hóa Tải & Gửi File Lớn (5GB+) Với TransferNow - Không Cần Code"
description: "Workflow n8n tự động hóa việc tải file lớn (tối đa 5GB) qua form web và gửi qua TransferNow, giải quyết vấn đề upload file thủ công, tiết kiệm thời gian và đảm bảo độ chính xác cao. Phù hợp cho doanh nghiệp cần chia sẻ tài liệu lớn như video, dataset, hoặc file dự án."
slug: "tieu-dong-hoa-tai-gui-file-lon-voi-transfernow"
tags: [n8n, automation, no-code, transfernow, upload-file-lon, content-creation]
keywords: [tự động hóa n8n, gửi file lớn 5gb, transfernow api, upload file tự động, workflow n8n cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa Tải & Gửi File Lớn (5GB+) Với TransferNow - Không Cần Code**

### **Giải pháp cho những "sếp" bị "đau đầu" với việc chia sẻ file lớn**
Có bao giờ các sếp phải mất **giờ đồng hồ** để upload file video, dataset, hoặc file dự án lên cloud và gửi cho khách hàng? Hay phải lo lắng về **quá trình upload bị gián đoạn** khi file quá lớn (trên 2GB)? Hoặc **không biết cách chia sẻ file an toàn** mà không làm chậm hệ thống email?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tạo form web tự động** để người dùng tải file lên (tối đa **5GB**).
✅ **Xử lý upload file lớn** một cách **mạnh mẽ** (không bị gián đoạn).
✅ **Gửi file qua TransferNow** (dịch vụ chia sẻ file lớn, hỗ trợ link download thời hạn).
✅ **Không cần code** – chỉ cần **cài n8n** và chạy workflow.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và **ổn định**, các sếp nên **self-host n8n** trên VPS. Dưới đây là **2 lựa chọn VPS chất lượng** với **mã giảm giá độc quyền**:
👉 **[TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[BNIX](https://my.bnix.one/aff.php?aff=172)** (VPS Xeon 4GB chỉ **50k/tháng**)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải upload thủ công file lớn (5GB+) qua email hoặc cloud.
- **Đảm bảo an toàn**: File được gửi qua **TransferNow** (hỗ trợ link download thời hạn, không giới hạn kích thước).
- **Trải nghiệm người dùng tốt**: Form web **dễ sử dụng**, không cần cài đặt phần mềm.
- **Hoạt động liên tục**: Workflow chạy **24/7** trên VPS, không phụ thuộc vào máy tính cá nhân.
- **Dễ dàng mở rộng**: Có thể **kết hợp với Slack/Telegram** để thông báo khi file đã sẵn sàng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản TransferNow** (miễn phí 14 ngày, [đăng ký tại đây](https://developers.transfernow.net/)).
✔ **API Key** của TransferNow (để cấu hình trong n8n).
✔ **Domain hoặc subdomain** (để host form web, ví dụ: `form.toname.com`).
✔ **n8n self-hosted** (cài đặt trên VPS như hướng dẫn [trên trang chủ n8n](https://n8n.io/)).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/8742) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trang `http://<your-n8n-domain>/editor`).
3. Nhấn **Import** và chọn file JSON vừa tải.
4. Workflow sẽ xuất hiện trên **canvas**.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [link này](https://n8n.io/workflows/8742) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** → **Paste JSON**.
3. Workflow sẽ được tạo tự động.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình chi tiết** các node quan trọng:

#### **🔹 Node "On form submission" (formTrigger)**
- **Mục đích**: Khởi động workflow khi người dùng submit form.
- **Cấu hình**:
  - **Endpoint**: Đặt tên form (ví dụ: `upload-file`).
  - **Domain**: Điền địa chỉ domain của form (ví dụ: `https://form.toname.com`).
  - **Form Fields**:
    - Thêm trường `file` (loại **File Upload**).
    - Thêm trường `name` (loại **Text**).

#### **🔹 Node "Set Transfer" & "Get Upload Url" (httpRequest)**
- **Mục đích**: Tạo request API để **lấy URL upload** từ TransferNow.
- **Cấu hình**:
  - **Headers**:
    - `x-api-key`: Điền **API Key** của TransferNow (từ tài khoản trên [TransferNow](https://developers.transfernow.net/)).
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "size": "{{ $node["Calculate size"].json["size"] }}",
      "name": "{{ $node["Form"].json["name"] }}"
    }
    ```
  - **Method**: `POST`.
  - **URL**: `https://api.transfernow.net/v1/transfers`.

#### **🔹 Node "Upload done" (httpRequest)**
- **Mục đích**: Xác nhận file đã upload thành công.
- **Cấu hình**:
  - **Headers**:
    - `x-api-key`: API Key TransferNow.
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "status": "completed"
    }
    ```
  - **Method**: `PUT`.
  - **URL**: `https://api.transfernow.net/v1/transfers/{{ $node["Get Upload Url"].json["id"] }}`.

#### **🔹 Node "Send Transfer" (httpRequest)**
- **Mục đích**: Gửi file qua TransferNow.
- **Cấu hình**:
  - **Headers**:
    - `x-api-key`: API Key TransferNow.
    - `Content-Type`: `multipart/form-data`.
  - **Body**:
    - **File**: Chọn `{{ $node["Form"].json["file"] }}`.
    - **Fields**:
      - `file`: `{{ $node["Form"].json["file"].name }}`.
  - **Method**: `POST`.
  - **URL**: `{{ $node["Get Upload Url"].json["url"] }}`.

#### **🔹 Node "Send UploadUrl" (httpRequest)**
- **Mục đích**: Gửi link download cho người dùng.
- **Cấu hình**:
  - **Headers**:
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "message": "File đã được upload thành công! Link download: {{ $node["Get transfer data"].json["downloadUrl"] }}"
    }
    ```
  - **Method**: `POST`.
  - **URL**: Địa chỉ email hoặc API của hệ thống thông báo (ví dụ: Slack Webhook).

---
### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Tạo một **file mẫu** (ví dụ: file text 1MB).
   - Submit form trên domain đã cấu hình.
   - Kiểm tra **log** trong n8n để xác nhận workflow chạy đúng.

2. **Bật Active workflow**:
   - Chọn workflow trên canvas → Nhấn **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÀY ĐỂ TĂNG CƯỜNG HỆ THỐNG]
- **Kết hợp với Slack/Telegram**:
  - Sau khi file upload thành công, **gửi thông báo** qua Slack/Telegram bằng node **HTTP Request** (Webhook).
  - Ví dụ:
    ```json
    {
      "text": "File {{ $node["Form"].json["name"] }} đã được upload thành công! Link download: {{ $node["Get transfer data"].json["downloadUrl"] }}"
    }
    ```
- **Lưu log upload**:
  - Sử dụng node **Google Sheets** hoặc **Database** để lưu lịch sử upload (tên file, kích thước, thời gian).
- **Thêm thời hạn download**:
  - TransferNow hỗ trợ **thời hạn download** (ví dụ: 7 ngày). Các sếp có thể cấu hình trong **API Key** hoặc thông qua **node Set**.
- **Tạo form riêng cho từng khách hàng**:
  - Sử dụng **subdomain** (ví dụ: `client1.form.toname.com`) để tạo form riêng cho từng khách hàng.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **upload file lớn thủ công**, đồng thời **đảm bảo an toàn và hiệu quả** khi chia sẻ file với khách hàng. **Chỉ cần 10 phút** để import và cấu hình, sau đó workflow sẽ **hoạt động tự động 24/7**.

👉 **Hành động ngay**:
1. **Đăng ký TransferNow** (miễn phí 14 ngày).
2. **Cài n8n trên VPS** (sử dụng mã giảm giá trên).
3. **Import workflow** và **cấu hình theo hướng dẫn**.
4. **Chia sẻ file lớn** một cách **nhanh chóng và an toàn**!

**Cần hỗ trợ?** Các sếp có thể liên hệ với tác giả Davide qua [LinkedIn](https://www.linkedin.com/in/davideboizza/) hoặc email **info@n3w.it**. 🚀