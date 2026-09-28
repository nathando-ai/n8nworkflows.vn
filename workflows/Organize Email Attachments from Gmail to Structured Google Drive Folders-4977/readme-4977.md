---
title: "📧 Tự Động Sắp Xếp Tệp Đính Kèm Email từ Gmail vào Google Drive Theo Cấu Trúc - Không Cần Code!"
description: "Workflow tự động hóa chuyển tất cả các tệp PDF từ email Gmail vào Google Drive theo thư mục logic, tiết kiệm thời gian và tránh mất mát dữ liệu. Hoàn toàn không cần viết code!"
slug: "tieu-dong-sap-xep-tap-dinh-kem-email-gmail-google-drive"
tags: [n8n, automation, gmail, google-drive, no-code, it-ops]
keywords: [tự động hóa email gmail, sắp xếp tệp đính kèm pdf, google drive tự động, workflow n8n gmail, tự động hóa văn phòng]
---

# 🚀 **Tự Động Sắp Xếp Tệp Đính Kèm Email từ Gmail vào Google Drive Theo Cấu Trúc**

### **🔥 Nỗi Đau Của Các Sếp?**
Hàng ngày, các sếp phải:
- **Tìm kiếm và tải xuống** hàng chục tệp PDF từ email Gmail.
- **Sắp xếp thủ công** chúng vào Google Drive theo danh mục (ví dụ: "Hợp đồng", "Báo cáo", "Tài liệu khách hàng").
- **Lo lắng mất mát** tệp khi không lưu trữ logic.
- **Tốn thời gian** lên đến **30 phút/ngày** cho công việc này.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** chỉ cần **1 lần cấu hình**, sau đó **hoạt động 24/7** mà không cần can thiệp của bạn!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 30+ phút/ngày** cho công việc lặp đi lặp lại.
✅ **Tệp PDF tự động** được chuyển và sắp xếp vào Google Drive theo **thư mục logic** (ví dụ: `Hợp đồng/2024`, `Báo cáo/Quý 1`).
✅ **Không mất tệp** do hệ thống tự động lưu trữ và quản lý.
✅ **Hoạt động liên tục** ngay cả khi bạn **ngủ hoặc đi công tác**.
✅ **Không cần viết code** – chỉ cần **cấu hình 1 lần**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n).
2. **Tài khoản Google Drive** (đã cấp quyền OAuth 2.0 cho n8n).
3. **API Key của Google Drive** (để tạo thư mục tự động).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud để đảm bảo hoạt động 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/4977) hoặc copy toàn bộ JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Workflow sẽ hiển thị trên canvas với **7 node** chính.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này hoạt động theo **các bước sau** (từ node này sang node khác):

##### **🔹 Node 1: Gmail Trigger (GmailTrigger)**
- **Chức năng:** Nhận tất cả email mới có **tệp đính kèm PDF** từ Gmail.
- **Cấu hình:**
  - Chọn **credentials:** `gmailOAuth2` (đã cấu hình trước khi import).
  - **Lưu ý:** Nếu muốn **chỉ lấy email từ một thư mục cụ thể** (ví dụ: "Tài liệu"), thêm điều kiện trong **Filter node** sau.

##### **🔹 Node 2: Filter (Lọc Email)**
- **Chức năng:** Chỉ giữ lại email **có tệp đính kèm PDF**.
- **Cấu hình:**
  - Thêm **điều kiện lọc** như:
    ```json
    {
      "jsonpath": "$[*]",
      "operator": "contains",
      "value": "pdf",
      "property": "payload.mimeType"
    }
    ```
  - **Lưu ý:** Nếu email có nhiều tệp đính kèm, chỉ **PDF** mới được xử lý.

##### **🔹 Node 3: Merge (Kết hợp Dữ Liệu)**
- **Chức năng:** Kết hợp **thông tin email** (chủ đề, người gửi) với **tệp đính kèm**.
- **Cấu hình:**
  - Chọn **Merge Type:** `Array` (để kết hợp danh sách email và tệp).

##### **🔹 Node 4: Split Out (Tách Dữ Liệu)**
- **Chức năng:** Tách **tệp đính kèm** ra khỏi thông tin email.
- **Cấu hình:**
  - Chọn **property:** `payload.attachments` (để lấy danh sách tệp).

##### **🔹 Node 5: Google Drive (Tải Tệp)**
- **Chức năng:** Tải **tệp PDF** từ email xuống Google Drive.
- **Cấu hình:**
  - Chọn **credentials:** `googleDriveOAuth2Api`.
  - **Lưu ý:** Nếu tệp đã tồn tại, **n8n sẽ tự động cập nhật** (không tạo trùng).

##### **🔹 Node 6: Create Folder (Tạo Thư Mục)**
- **Chức năng:** **Tự động tạo thư mục** trong Google Drive theo **tên chủ đề email** (ví dụ: `Hợp đồng/2024`).
- **Cấu hình:**
  - **Key Parameters:**
    ```json
    {
      "resource": "folder",
      "name": "{{$node["Gmail1"].json.subject}}", // Tạo thư mục theo chủ đề email
      "parents": ["root"] // Thư mục cha là "root" (có thể thay đổi)
    }
    ```
  - **Lưu ý:**
    - Nếu muốn **thư mục cố định** (ví dụ: `Tài liệu/PDF`), thay `{{$node["Gmail1"].json.subject}}` bằng `"Tài liệu/PDF"`.
    - **Không tạo thư mục trùng lặp** → Sử dụng **Sticky Note** để ghi chú (node sau).

##### **🔹 Node 7: Sticky Note (Ghi Chú)**
- **Chức năng:** **Ghi chú** để tránh tạo thư mục trùng lặp.
- **Cấu hình:**
  - Thêm **lời nhắc** như:
    ```json
    "text": "⚠️ Thư mục đã tồn tại: {{$node["Create Folder"].json.id}}"
    ```
  - **Lưu ý:** Nếu thư mục đã tồn tại, **n8n sẽ không tạo mới** (tránh lặp).

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** **Test Run** với **1 email mẫu** (đã có tệp PDF đính kèm).
- **Bước 2:** Kiểm tra **Google Drive** → Tệp PDF đã được **tải và sắp xếp** vào thư mục logic.
- **Bước 3:** **Bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Kết hợp với Slack/Telegram:**
- **Gửi thông báo** khi có tệp mới được tải xuống (ví dụ: `📤 Tệp PDF mới: [Tên tệp] đã được lưu vào [Thư mục]`).

🔹 **Lưu Log Lịch Sử:**
- Sử dụng **Google Sheets** để **ghi lại lịch sử** các tệp đã được xử lý (ngày, giờ, tên tệp, người gửi).

🔹 **Tự Động Xóa Email Sau Khi Tải Xong:**
- Thêm **node Gmail** với **operation: delete** để **xóa email sau khi tệp đã được lưu**.

🔹 **Sắp Xếp Theo Ngày:**
- Thay vì theo chủ đề, **tạo thư mục theo ngày** (ví dụ: `2024/05/20`) bằng cách sử dụng:
  ```json
  "name": "{{$node["Gmail1"].json.date.split('/')[2]}}/{{$node["Gmail1"].json.date.split('/')[1]}}/{{$node["Gmail1"].json.date.split('/')[0]}}"
  ```
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại, đồng thời **tránh mất mát dữ liệu** nhờ tự động hóa hoàn toàn. **Chỉ cần 1 lần cấu hình**, sau đó **hoạt động 24/7** mà không cần can thiệp.

**👉 Hãy áp dụng ngay và tự động hóa công việc của mình!**
Nếu có vấn đề, **hãy để lại comment** dưới đây, chúng tôi sẽ hỗ trợ!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::