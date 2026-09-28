---
title: "💰 Tự Động Hóa Đồng Bộ Hoá Hóa Đơn Stripe PDF Sang S3 Bucket (One-Way Sync) - Giảm 90% Thời Gian Chăm Sóc Tài Chính"
description: "Workflow tự động hóa đồng bộ hóa đơn PDF từ Stripe sang S3 Bucket hàng tháng, giúp các sếp tiết kiệm thời gian, tránh mất mát dữ liệu và dễ dàng truy cập hóa đơn qua AWS. Hoạt động 24/7, không cần code."
slug: "tieu-dong-hoa-hoa-don-stripe-sang-s3"
tags: [n8n, automation, finance, aws-s3, stripe, no-code]
keywords: [tự động hóa hóa đơn Stripe, đồng bộ hóa đơn PDF sang S3, AWS S3 automation, workflow Stripe, tự động hóa tài chính]
---

# 🚀 **Tự Động Hóa Đồng Bộ Hóa Đơn Stripe PDF Sang S3 Bucket (One-Way Sync)**

### **Giải Pháp Cho Các Sếp Bị "Bị Đè" Với Công Việc Chăm Sóc Hóa Đơn**
Hàng tháng, các sếp phải mất **giờ đồng hồ** để tải hóa đơn từ Stripe, lưu trữ và quản lý chúng thủ công. Kết quả? **Rủi ro mất mát dữ liệu**, **tốn thời gian**, và **không thể truy cập nhanh** khi cần. **Workflow này tự động hóa toàn bộ quy trình**, đồng bộ hóa đơn PDF từ Stripe sang S3 Bucket hàng tháng, giúp các sếp **tiết kiệm 90% thời gian** và **tránh sai sót**.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần can thiệp thủ công, hoạt động **24/7** hàng tháng.
- **Dữ liệu an toàn**: Hóa đơn được lưu trữ trên **AWS S3** với tính bảo mật cao.
- **Cấu trúc logic**: Hóa đơn được sắp xếp theo **năm/tháng** (ví dụ: `invoices/2024/12/invoice-123.pdf`).
- **Dễ dàng truy cập**: Các sếp có thể tải hóa đơn từ S3 bất kỳ lúc nào, ngay cả khi Stripe bị down.
- **Tiết kiệm chi phí**: Tránh mất thời gian của nhân viên, giảm rủi ro sai sót.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Stripe** (API Key) để lấy hóa đơn.
2. **Tài khoản AWS** với quyền truy cập vào **S3 Bucket** (IAM Role hoặc Access Key).
3. **n8n Self-hosted** (không dùng phiên bản miễn phí, vì cần **Schedule Trigger** và **AWS S3 Node**).
4. **Tham số cấu hình** (xem phần **Cách Import & Lưu Ý**).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/2450) (hoặc copy JSON từ link trên).
2. Vào **n8n Editor** → **Import Workflow** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **12 node**, nhưng các node **đánh dấu `*`** là **quan trọng nhất** cần cấu hình:

| **Node** | **Loại** | **Lưu Ý Cần Chỉnh** |
|----------|---------|----------------------|
| **Get all Invoices\*** | `httpRequest` | Điền **Stripe API Key** và **Endpoint**: `https://api.stripe.com/v1/invoices` |
| **Upload to S3 Bucket\*** | `awsS3` | Chọn **Bucket Name**, **Folder Path** (ví dụ: `invoices/{{$node["Set-Subpath"].json["year"]}}/{{$node["Set-Subpath"].json["month"]}}`), và **File Name** (ví dụ: `invoice-{{$json.id}}.pdf`). |
| **ENV\*** | `set` | Cấu hình **`folderName`**, **`bucketName`**, và **`year`/`month`** (có thể tự động lấy tháng trước hoặc nhập thủ công). |
| **Clean and Escape ENV** | `set` | **Không cần chỉnh**, nó tự động xử lý biến môi trường. |

##### **Cấu Hình Chi Tiết Các Node Quan Trọng**
1. **`ENV*` (Node `set`)**
   - **`folderName` (tùy chọn)**: Thư mục con cho hóa đơn (ví dụ: `invoices`).
   - **`bucketName` (bắt buộc)**: Tên **S3 Bucket** muốn đồng bộ.
   - **`year` và `month`**:
     - **Tự động**: Sử dụng biểu thức `{{ $now.format("YYYY") }}` và `{{ $now.format("MM") }}` để lấy tháng trước.
     - **Thủ công**: Nhập năm/tháng cụ thể (ví dụ: `2024` và `12` để lấy hóa đơn tháng 12/2024).

   **Ví dụ cấu hình:**
   ```json
   {
     "folderName": "invoices",
     "bucketName": "my-stripe-invoices-bucket",
     "year": "{{ $now.subtract(1, 'month').format('YYYY') }}",
     "month": "{{ $now.subtract(1, 'month').format('MM') }}"
   }
   ```

2. **`Upload to S3 Bucket*` (Node `awsS3`)**
   - **Bucket Name**: Điền tên bucket đã tạo trên AWS.
   - **Key**: Sử dụng biểu thức để tạo đường dẫn:
     ```
     {{ $node["Set-Subpath"].json["folderName"] }}/{{ $node["Set-Subpath"].json["year"] }}/{{ $node["Set-Subpath"].json["month"] }}/invoice-{{ $json.id }}.pdf
     ```
   - **Storage Class**: Chọn **`STANDARD`** (hoặc tùy chọn khác như `GLACIER` nếu lưu dài hạn).
   - **ACL**: Chọn **`private`** (nếu không muốn ai cũng xem được).

3. **`Get all Invoices*` (Node `httpRequest`)**
   - **Method**: `GET`
   - **URL**: `https://api.stripe.com/v1/invoices`
   - **Headers**:
     ```
     Authorization: Bearer {{ $env["STRIPE_API_KEY"] }}
     Idempotency-Key: {{ $node["Inject s3 Subpath"].json["idempotencyKey"] }}
     ```
   - **Body**: Không cần.

4. **`Download Invoice PDF from Stripe` (Node `httpRequest`)**
   - **Method**: `GET`
   - **URL**: `{{ $json.document_url }}` (đường dẫn PDF từ Stripe).
   - **Headers**:
     ```
     Authorization: Bearer {{ $env["STRIPE_API_KEY"] }}
     ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **`When clicking ‘Test workflow’`** (node `manualTrigger`) và nhấn **Run**.
   - Kiểm tra **S3 Bucket** xem hóa đơn đã được upload chưa.
2. **Bật Schedule Trigger**:
   - Đi đến **`Every Month the First Day of the Month`** (node `scheduleTrigger`).
   - Chọn **`Active`** và cấu hình:
     - **Cron**: `0 0 1 * *` (chạy vào ngày 1 hàng tháng).
     - **Timezone**: Chọn timezone phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
3. **Bật Workflow**:
   - Đi đến **Workflow Settings** → Chọn **Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Email khi đồng bộ thành công**:
   - Thêm node **`slack`** hoặc **`email`** sau node **`Upload to S3 Bucket`** để báo cáo kết quả.
   - **Ví dụ**: Gửi tin nhắn Slack: *"Hóa đơn tháng {{ $node["Set-Subpath"].json["month"] }}/{{ $node["Set-Subpath"].json["year"] }} đã đồng bộ thành công!"*

2. **Lưu log hoạt động**:
   - Thêm node **`set`** sau **`Upload to S3 Bucket`** để lưu thông tin vào **Google Sheets** hoặc **Notion**.
   - **Cách làm**:
     - Tạo một sheet Google Sheets với cột: `Date`, `Month`, `Year`, `Invoice ID`, `Status`.
     - Sử dụng node **`googleSheets`** để ghi dữ liệu.

3. **Tự động xóa hóa đơn cũ trên Stripe (nếu cần)**:
   - Thêm node **`httpRequest`** sau **`Upload to S3 Bucket`** để gọi API Stripe xóa hóa đơn đã đồng bộ (nếu không cần lưu trên Stripe).

4. **Tạo báo cáo định kỳ**:
   - Sử dụng **n8n + Google Data Studio** để tự động tạo báo cáo số hóa đơn, tổng doanh thu từ S3.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công chăm sóc hóa đơn**, đồng thời **tăng cường tính bảo mật và truy cập dữ liệu**. Với **AWS S3**, các sếp có thể:
✅ **Truy cập hóa đơn bất kỳ lúc nào** (không phụ thuộc Stripe).
✅ **Tiết kiệm thời gian** (tự động hóa hàng tháng).
✅ **Dễ dàng phân tích dữ liệu** (kết hợp với Google Sheets/Notion).

**Hãy áp dụng ngay workflow này và tự động hóa tài chính của doanh nghiệp!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bạn có thắc mắc gì về workflow?** Hãy để lại comment bên dưới! 👇