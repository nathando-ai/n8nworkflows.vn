---
title: "🚀 Tự Động Hóa Tạo Nhiệm Vụ Smenso Từ Gmail Với Giao Nhiệm Tuỳ Chọn Tự Động"
description: "Workflow này tự động chuyển đổi email có chủ đề 'smenso Task' thành nhiệm vụ trong Smenso, gán tự động vào dự án phù hợp dựa trên từ khóa trong tiêu đề, trả lời xác nhận và đánh dấu email là đã đọc. Giúp tiết kiệm thời gian quản lý nhiệm vụ lên tới 90% cho các sếp."
slug: "tu-dong-hoa-tao-nhiem-vu-smenso-tu-gmail"
tags: [n8n, automation, project-management, smenso, gmail-integration]
keywords: [n8n workflow smenso, tự động hóa quản lý dự án, gmail tự động tạo nhiệm vụ, smenso api, tự động gán dự án]
---

# 🚀 Tự Động Hóa Tạo Nhiệm Vụ Smenso Từ Gmail Với Giao Nhiệm Tuỳ Chọn Tự Động

## 📌 Nỗi Đau Của Các Sếp
Hàng ngày, các sếp phải mất thời gian quét email, phân loại nhiệm vụ, gán dự án và gửi xác nhận thủ công. Điều này không chỉ tốn thời gian mà còn dễ gây lỗi trong quá trình chuyển đổi thông tin. **Workflow này giải quyết vấn đề này bằng cách tự động hóa toàn bộ quy trình chỉ trong vài giây!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải mở email, sao chép tiêu đề, gán dự án thủ công.
- **Chính xác 100%**: Nhiệm vụ được tự động gán vào dự án phù hợp dựa trên từ khóa trong tiêu đề.
- **Hoạt động liên tục**: Workflow hoạt động 24/7, không cần can thiệp của con người.
- **Trải nghiệm tốt cho khách hàng**: Người gửi email nhận được phản hồi tự động ngay lập tức.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Các sếp cần chuẩn bị:
- **Tài khoản Gmail** với quyền truy cập OAuth2 (để n8n có thể đọc email).
- **API Key của Smenso** (để tạo và quản lý nhiệm vụ).
- **Domain email doanh nghiệp** (để lọc email từ người gửi đáng tin cậy).
- **ID dự án mặc định** (dùng khi không tìm thấy từ khóa phù hợp).
- **Subdomain Smenso** (ví dụ: `doanhnghiep.smenso.cloud`).
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1️⃣ Import Workflow 📥
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/15267) hoặc sao chép JSON từ canvas.
- **Bước 2**: Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
- **Bước 3**: Nhấn **Import** và dán JSON vào hoặc tải file JSON đã tải xuống.

#### 2️⃣ Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
Workflow này bao gồm **7 node** chính, các sếp cần chú ý cấu hình sau:

##### **1️⃣ Node "Gmail Trigger"**
- **Cấu hình**:
  - Chọn **OAuth2** và kết nối tài khoản Gmail.
  - Thiết lập **polling interval** (thời gian kiểm tra email) là **60 giây** (mặc định).
  - **Lọc email**: Chỉ lấy email **unread** với tiêu đề chứa `"smenso Task"`.

##### **2️⃣ Node "Filter by Sender Domain"**
- **Cấu hình**:
  - Thay thế `@YOUR-DOMAIN.com` bằng **domain email của doanh nghiệp** (ví dụ: `@acme.com`).
  - Ví dụ: `sender.email.endsWith("@acme.com")`.

##### **3️⃣ Node "Get All Projects" (Smenso)**
- **Cấu hình**:
  - Kết nối **API Key Smenso** (đã tạo trong tài khoản Smenso).
  - Node này sẽ lấy tất cả dự án **active** từ Smenso.

##### **4️⃣ Node "Match Project by Keyword" (Code)**
- **Cấu hình**:
  - **Mã JavaScript** trong node này sẽ **trích xuất từ khóa** trong tiêu đề email (ví dụ: `[Marketing]` trong `"smenso Task [Marketing]: Create brief"`).
  - Thay thế `YOUR_DEFAULT_PROJECT_ID_HERE` bằng **ID dự án mặc định** (dùng khi không tìm thấy từ khóa).
  - **Lưu ý**: Các sếp có thể chỉnh sửa mã để phù hợp với cách đặt tên dự án của mình.

##### **5️⃣ Node "Create smenso Task"**
- **Cấu hình**:
  - Chọn **operation = create**, **resource = task**.
  - **Tham số tự động**:
    - **Tiêu đề nhiệm vụ** = Tiêu đề email.
    - **Mô tả nhiệm vụ** = Nội dung email.
    - **Dự án** = Dự án được trích xuất từ node "Match Project by Keyword".

##### **6️⃣ Node "Send Confirmation Reply"**
- **Cấu hình**:
  - Thay thế `YOUR_WORKSPACE` bằng **subdomain Smenso** (ví dụ: `acme.smenso.cloud` → `acme`).
  - **Nội dung email tự động**:
    ```plaintext
    Xin chào [Tên người gửi],

    Nhiệm vụ của bạn đã được tạo thành công trong dự án [Tên dự án] trên Smenso.

    Cảm ơn!
    ```

##### **7️⃣ Node "Mark as Read"**
- **Cấu hình**:
  - Node này sẽ **đánh dấu email** là đã đọc để không bị lặp lại.

#### 3️⃣ Kích Hoạt ⚡️
- **Test Run**: Chạy thử với một email mẫu để kiểm tra workflow hoạt động như mong đợi.
- **Bật Active**: Sau khi kiểm tra, nhấn **Active** để workflow bắt đầu hoạt động tự động.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết nối với Slack/Telegram**: Gửi thông báo khi nhiệm vụ được tạo thành công.
- **Lưu log hoạt động**: Sử dụng node **StickyNote** để ghi lại lịch sử nhiệm vụ.
- **Báo cáo định kỳ**: Tạo báo cáo tự động về số nhiệm vụ được tạo trong ngày.
- **Thêm trường tùy chọn**: Cho phép người gửi email gửi thêm thông tin (ví dụ: deadline) thông qua tiêu đề.
:::

---

### 📌 Kết Luận
Workflow này **giúp các sếp tự động hóa hoàn toàn quá trình chuyển đổi email thành nhiệm vụ**, tiết kiệm thời gian và giảm thiểu lỗi. **Hãy áp dụng ngay để quản lý dự án hiệu quả hơn!**

:::tip[LÀM GÌ TIẾP?]
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test run** và bật workflow để bắt đầu tự động hóa!
:::