---
title: "🚀 Tự Động Tạo Contact Trên Drift Mới Chỉ Với 1 Nhấp Chữa - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn miễn phí để tạo contact trên Drift chỉ bằng một nút bấm, tiết kiệm thời gian và giảm thiểu lỗi nhập liệu cho bộ phận Sales."
slug: "tu-dong-tao-contact-tren-drift"
tags: [n8n, automation, sales, drift, no-code]
keywords: [n8n workflow drift, tự động hóa sales, tạo contact drift tự động, tiết kiệm thời gian sales]
---

# 🚀 Tự Động Tạo Contact Trên Drift - Giải Pháp Tiết Kiệm Thời Gian Cho Bộ Phận Sales

### 📌 **Nỗi Đau Thực Tế Của Các Sếp Sales**
Hàng ngày, các sếp và nhân viên Sales phải mất thời gian quý báu để:
- **Nhập liệu thủ công** vào Drift từ các nguồn khác (CRM, email, form website).
- **Đảm bảo tính chính xác** của thông tin contact để tránh mất lead hoặc phản hồi sai.
- **Quản lý nhiều contact** đồng thời, dễ gây nhầm lẫn và mất hiệu quả.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động tạo contact trên Drift chỉ với một cú nhấp chuột!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, tự động hóa hoàn toàn.
- **Tính chính xác cao**: Giảm thiểu lỗi nhập liệu, đảm bảo thông tin contact chính xác.
- **Hoạt động liên tục**: Chỉ cần kích hoạt workflow, hệ thống sẽ tự động xử lý mọi khi cần.
- **Tích hợp dễ dàng**: Hoàn toàn không cần kiến thức code, chỉ cần cấu hình đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
- **Tài khoản Drift** và **API Key** của Drift (được tạo từ tài khoản Drift của bạn).
- **Tài khoản n8n** (cả phiên bản Cloud hoặc Self-hosted).
- **Thông tin contact** (tên, email, số điện thoại, và các trường tùy chọn khác) để tự động tạo trên Drift.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
- **Bước 1**: Truy cập [n8n Editor](https://n8n.io/) và chọn **Create Workflow**.
- **Bước 2**: Nhấp vào **Import** và chọn file JSON của workflow (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/497)).
- **Bước 3**: Chọn **Import** để tải workflow vào n8n.

#### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này chỉ có **2 node** cơ bản, nhưng cần cấu hình chính xác như sau:

##### **Node 1: Manual Trigger (Nhấn "Execute")**
- **Tên node**: "On clicking 'execute'"
- **Lưu ý**: Node này chỉ là nút kích hoạt thủ công. Các sếp có thể thay thế bằng **Webhook** hoặc **Trigger từ CRM** (ví dụ: khi có lead mới từ HubSpot) để tự động hóa hoàn toàn.

##### **Node 2: Drift (Tạo Contact)**
- **Tên node**: "Drift"
- **Credentials**: Chọn **"driftApi"** (đã cấu hình trước khi import).
- **Cấu hình chi tiết**:
  - **API Key**: Điền **API Key** của Drift (tìm trong **Settings > API Keys** của tài khoản Drift).
  - **Thông tin contact**:
    - **Name**: Tên của contact (có thể lấy từ biến hoặc nhập thủ công).
    - **Email**: Email của contact (bắt buộc).
    - **Phone**: Số điện thoại (tùy chọn).
    - **Custom Fields**: Nếu có trường tùy chỉnh trong Drift, điền theo yêu cầu.
  - **Test Run**: Nhấp **Execute** để kiểm tra workflow với dữ liệu mẫu.

#### 3. **Kích Hoạt ⚡️**
- **Bước 1**: Nhấp **Active** để bật workflow.
- **Bước 2**: Nhấn nút **"Execute"** trên node **Manual Trigger** để tạo contact trên Drift.
- **Bước 3**: Kiểm tra trên **Drift Dashboard** để xác nhận contact đã được tạo thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TIẾP CẬN THÊM]
- **Tích hợp với CRM khác**: Thay thế **Manual Trigger** bằng **Webhook từ HubSpot/Zoho** để tự động tạo contact khi có lead mới.
- **Lưu log hoạt động**: Sử dụng **Node Logs** để theo dõi lịch sử tạo contact và giải quyết lỗi nhanh chóng.
- **Gửi thông báo Slack/Email**: Kết hợp với **Node Slack/Email** để thông báo khi contact được tạo thành công.
- **Tự động cập nhật từ form website**: Sử dụng **Node Form Submit** (n8n-nodes-base.formSubmit) để nhận dữ liệu từ form và tự động chuyển vào Drift.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp Sales **tiết kiệm thời gian, giảm thiểu lỗi và tự động hóa quy trình tạo contact** trên Drift. **Chỉ cần một cú nhấp chuột**, hệ thống sẽ tự động xử lý mọi việc!

**👉 Hãy áp dụng ngay và trải nghiệm sự hiệu quả mà tự động hóa mang lại!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::