---
title: "🚀 Tự Động Lưu Hóa Đơn QuickBooks Sang Google Drive (PDF) - Giảm 90% Thời Gian Làm Thủ Công"
description: "Workflow tự động hóa hoàn toàn không cần code giúp lưu trữ hóa đơn QuickBooks dưới dạng PDF vào Google Drive ngay khi tạo mới, tiết kiệm thời gian và giảm rủi ro mất mát dữ liệu. Phù hợp cho doanh nghiệp nhỏ, trung và các công ty cần quản lý tài chính hiệu quả."
slug: "tieu-dong-luu-hoa-don-quickbooks-sang-google-drive"
tags: [n8n, automation, quickbooks, google-drive, invoice-processing, no-code]
keywords: [tự động hóa hóa đơn quickbooks, lưu hóa đơn pdf google drive, workflow n8n quickbooks, tự động hóa tài chính, giảm thời gian làm thủ công]
---

# 🚀 **Tự Động Lưu Hóa Đơn QuickBooks Sang Google Drive (PDF) - Không Cần Code**

## **💡 Nỗi Đau Của Các Sếp: Làm Thủ Công Hóa Đơn Làm Giảm Sức Sống**
Hàng ngày, các sếp và nhân viên tài chính phải:
- **Kiểm tra liên tục** QuickBooks để biết hóa đơn mới được tạo.
- **Tải PDF** hóa đơn một cách thủ công từ QuickBooks.
- **Lưu trữ** vào Google Drive hoặc hệ thống khác, dễ bị quên hoặc mất.
- **Tốn thời gian** lên đến **30 phút/ngày** cho mỗi công ty nhỏ/mittelstand.

**Kết quả?** Dữ liệu không đồng bộ, rủi ro mất mát cao, và hiệu suất làm việc giảm sút.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 90% thời gian** làm thủ công (từ 30 phút/ngày xuống còn 2 phút).
✅ **Lưu trữ tự động** hóa đơn PDF vào Google Drive ngay khi tạo mới.
✅ **Giảm rủi ro mất dữ liệu** do không cần kiểm tra thủ công.
✅ **Dễ dàng chia sẻ** hóa đơn với khách hàng hoặc bộ phận khác.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản QuickBooks**
- **Tài khoản QuickBooks Online** (cần quyền **Developer** để cấu hình webhook).
- **API Key** từ [Intuit Developer Portal](https://developer.intuit.com/) (đăng ký miễn phí).
- **Webhook URL** của workflow (sẽ được tạo khi import).

### **2. Tài Khoản Google Drive**
- **Tài khoản Google** (đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/)).
- **Google Client Credentials** (cần cấp quyền **Google Drive API**).
- **Folder Google Drive** để lưu hóa đơn (cần tạo trước).

### **3. N8n Self-Hosted (Không dùng n8n.cloud)**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7232](https://n8n.io/workflows/7232) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. Nhấn **Import** và chọn file JSON vừa tải.
4. Workflow sẽ xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/7232](https://n8n.io/workflows/7232) (chọn **Export as JSON**).
2. **Mở n8n Editor** và nhấn **Import** → **Paste JSON**.
3. Workflow sẽ tự động được tạo.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: QuickBooks Webhook (n8n-nodes-base.webhook)**
- **Tên node:** `QuickBooks Webhook`
- **Cấu hình:**
  - **Path:** `quickbooks-invoice` (không đổi).
  - **HTTP Method:** `POST` (không đổi).
  - **Credentials:** Chọn **QuickBooks** (cần tạo trước trong **n8n Credentials**).
  - **Authentication:** Chọn **Bearer Token** (điền **OAuth 2.0 Token** từ Intuit Developer Portal).

#### **🔹 Node 2: Get an Invoice (n8n-nodes-base.quickbooks)**
- **Tên node:** `Get an invoice`
- **Cấu hình:**
  - **Resource:** `invoice` (không đổi).
  - **Credentials:** Chọn **QuickBooks** (giống Node 1).
  - **Query Parameters:**
    - `id`: `$json["id"]` (lấy ID hóa đơn từ webhook).
    - `include`: `items` (để lấy chi tiết hàng hóa).

#### **🔹 Node 3: Generate PDF File (n8n-nodes-base.httpRequest)**
- **Tên node:** `Generate PDF File`
- **Cấu hình:**
  - **Method:** `GET`.
  - **URL:** `https://quickbooks.api.intuit.com/v3/company/{companyId}/invoice/{invoiceId}/pdf` (thay `{companyId}` và `{invoiceId}` bằng biến):
    - `companyId`: `$json["companyId"]` (lấy từ QuickBooks).
    - `invoiceId`: `$json["id"]` (lấy từ Node 2).
  - **Headers:**
    - `Authorization`: `Bearer $credentials["quickbooks"]["oauth2"]["access_token"]`.
    - `Accept`: `application/pdf`.
  - **Response Format:** `Binary` (để lưu PDF).

#### **🔹 Node 4: Upload File (n8n-nodes-base.googleDrive)**
- **Tên node:** `Upload file`
- **Cấu hình:**
  - **Credentials:** Chọn **Google Drive** (cần tạo trước trong **n8n Credentials**).
  - **File:** `$binary` (lấy từ Node 3).
  - **Folder:** Chọn **Folder cụ thể** (đã tạo trước trong Google Drive).
  - **File Name:** `$json["doc"]["DocNumber"] + ".pdf"` (tên hóa đơn + `.pdf`).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với một hóa đơn mẫu:
   - Tạo một hóa đơn test trên QuickBooks.
   - Nhấn **Run Workflow** trên n8n Editor.
   - Kiểm tra **Google Drive** để xác nhận PDF đã được lưu.
2. **Bật Active Workflow**:
   - Nhấn **Active** trên nút trạng thái workflow.
   - Workflow sẽ **hoạt động liên tục** khi có hóa đơn mới được tạo.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tự Động Gửi Hóa Đơn Đến Khách Hàng**
- **Thêm Node Slack/Email** sau Node 4 để tự động gửi PDF hóa đơn cho khách hàng.
- **Cách làm:**
  - Thêm **n8n-nodes-base.slack** hoặc **n8n-nodes-base.email**.
  - Gửi tin nhắn/email với **link Google Drive** hoặc **PDF trực tiếp**.

### **2. Lưu Log Lịch Sử Hóa Đơn**
- **Thêm Node StickyNote** (đã có trong workflow) để ghi lại:
  - Thời gian tạo.
  - ID hóa đơn.
  - Link PDF.
- **Cách làm:**
  - Node `StickyNote` đã được cấu hình sẵn, chỉ cần **bật Active**.

### **3. Báo Cáo Định Kỳ**
- **Thêm Node Google Sheets** để tự động ghi chép hóa đơn mới vào bảng tính.
- **Cách làm:**
  - Thêm **n8n-nodes-base.googleSheets**.
  - Chọn **Sheet** và **Range** (ví dụ: `A1:D100`).
  - Ghi dữ liệu từ `$json` của Node 2.

### **4. Xử Lý Hóa Đơn Cập Nhật/Xóa**
- **Cấu hình thêm điều kiện** trong Node 2 và Node 3 để:
  - **Tạo PDF mới** khi hóa đơn được **cập nhật**.
  - **Xóa PDF cũ** khi hóa đơn được **xóa**.
- **Cách làm:**
  - Sử dụng **Expressions** trong Node 2:
    - Nếu `eventType === "Create" || eventType === "Update"` → Tiếp tục.
    - Nếu `eventType === "Delete"` → Bỏ qua.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc làm thủ công hóa đơn, đồng thời **giảm rủi ro mất dữ liệu** và **tăng tính chuyên nghiệp** trong quản lý tài chính.

**Hành động ngay:**
1. **Cài đặt n8n Self-Hosted** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test Run** với hóa đơn mẫu.
4. **Bật Active** và **quên đi việc kiểm tra thủ công**!

**Nếu gặp khó khăn**, liên hệ với **Intuz** qua [getstarted@intuz.com](mailto:getstarted@intuz.com) để hỗ trợ tùy chỉnh workflow phù hợp với doanh nghiệp của các sếp.

---
### **🔗 Tài Liệu Tham Khảo**
- [QuickBooks Webhook API](https://developer.intuit.com/app/developer/qbo/docs/api/reference/events/webhooks)
- [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python)
- [n8n QuickBooks Node](https://docs.n8n.io/integrations/builtins/nodes/quickbooks/)