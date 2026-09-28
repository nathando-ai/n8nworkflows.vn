---
title: "🚀 Tự Động Hóa Gửi Bulk WhatsApp & Email (Gmail) Từ Google Sheets Với Theo Dõi Trạng Thái Chi Tiết"
description: "Giải pháp hoàn hảo cho các sếp marketing, sales hoặc startup cần gửi hàng loạt tin nhắn WhatsApp và email bulk một cách tự động, theo dõi trạng thái gửi thành công/lỗi, và tránh gửi trùng lặp. Workflow này kết hợp Google Sheets, WhatsApp API, Gmail, và InboxPlus để tối ưu hóa quy trình liên lạc với khách hàng."
slug: "tieu-dong-hoa-bulk-whatsapp-gmail-google-sheets"
tags: [n8n, automation, no-code, whatsapp-bulk, gmail-automation, google-sheets, inboxplus, sales-funnel]
keywords: [n8n workflow bulk whatsapp, tự động hóa gửi email bulk, theo dõi trạng thái gửi whatsapp, google sheets automation, inboxplus n8n, gửi tin nhắn bulk cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa Gửi Bulk WhatsApp & Email (Gmail) Từ Google Sheets Với Theo Dõi Trạng Thái Chi Tiết**

## **🔥 Giải Pháp Cho Các Sếp Đang Mất Thời Gian Với Quy Trình Liên Lạc Khách Hàng**
Hãy tưởng tượng một tình huống: Bạn là một sếp marketing hoặc trưởng bộ phận bán hàng, phải gửi hàng trăm tin nhắn WhatsApp và email hàng ngày để nhắc nhở khách hàng, gửi ưu đãi, hoặc theo dõi đơn hàng. **Làm thủ công không chỉ tốn thời gian mà còn dễ gây lỗi, gửi trùng lặp, và không theo dõi được trạng thái thực tế của mỗi tin nhắn.**

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách:
✅ **Gửi bulk WhatsApp & Email tự động** từ dữ liệu khách hàng trong Google Sheets.
✅ **Theo dõi trạng thái gửi** (đã gửi, đã giao, thất bại) và cập nhật ngay vào bảng Google Sheets.
✅ **Tránh gửi trùng lặp** nhờ kiểm tra trạng thái trước khi gửi.
✅ **Hỗ trợ hình ảnh trong email** (inline, attachment, hoặc cả hai).
✅ **Điều khiển tốc độ xử lý** bằng cách chia dữ liệu thành batch, tránh bị chặn API.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10-20 giờ/tuần** so với cách làm thủ công.
- **Tăng độ chính xác** với hệ thống theo dõi trạng thái tự động.
- **Cá nhân hóa tin nhắn** cho từng khách hàng từ Google Sheets.
- **Hoạt động 24/7** khi chạy trên VPS (self-hosted) mà không cần can thiệp.
- **Giảm chi phí** bằng cách tránh gửi trùng lặp và tối ưu hóa API.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với dữ liệu khách hàng có các cột sau:
   - `Phone Number` (số điện thoại WhatsApp)
   - `Email` (địa chỉ email)
   - `Message Sent` (trạng thái: `pending`, `sent`, `failed`)
   - `Mail Sent` (trạng thái: `pending`, `sent`, `failed`)
   *(Nếu chưa có, có thể tạo mẫu từ [đây](https://docs.google.com/spreadsheets/d/1ExampleSheet/edit))*

2. **API Keys & Credentials**:
   - **WhatsApp Cloud API** (đăng ký tại [Meta Developer](https://developers.facebook.com/))
   - **InboxPlus API** (đăng ký tại [InboxPlus](https://inboxplus.io/))
   - **Gmail OAuth 2.0** (tạo từ [Google Cloud Console](https://console.cloud.google.com/))
   - **Google Drive OAuth 2.0** (nếu sử dụng hình ảnh trong email)

3. **Mẫu tin nhắn WhatsApp & Email**:
   - Chuẩn bị **template WhatsApp** (HTML hoặc văn bản).
   - Chuẩn bị **template email HTML** (có thể chứa hình ảnh inline hoặc attachment).

4. **VPS Self-Hosted** (khuyến nghị):
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên máy chủ riêng.
   👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Workflow này được chia sẻ trên [n8n.io](https://n8n.io/workflows/11921). Các sếp có thể:
- **Tải file JSON** và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

:::note[**Lưu Ý**]
- **Không cần chỉnh sửa JSON** nếu đã import thành công.
- **Không kích hoạt workflow** ngay lập tức, vì cần cấu hình các node quan trọng trước.
:::

---

### **2. Các Bước Cấu Hình Bắt Buộc 📌**

#### **🔹 Node 1: Get Contacts (Lấy Dữ Liệu Từ Google Sheets)**
- **Chọn Credentials**: `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
- **Chọn Sheet**: Chọn bảng chứa dữ liệu khách hàng.
- **Range**: Chọn toàn bộ dữ liệu (ví dụ: `Sheet1!A:D`).
- **Kiểm tra cột bắt buộc**:
  - `Phone Number`, `Email`, `Message Sent`, `Mail Sent` phải tồn tại.

#### **🔹 Node 2: Split In Batches (Chia Dữ Liệu Thành Batch)**
- **Batch Size**: Đặt số lượng liên lạc xử lý mỗi lần (ví dụ: **50-100** để tránh bị chặn API).
- **Kiểm tra**: Nếu số lượng lớn, tăng batch size để tăng tốc độ.

#### **🔹 Node 3: Has Phone Number & Has Email Address (Kiểm Tra Trống)**
- **Cấu hình**:
  - Nếu `Phone Number` hoặc `Email` trống, **bỏ qua** liên lạc đó.
  - **Lưu ý**: Các node `IF` này sẽ loại bỏ dữ liệu không hợp lệ.

#### **🔹 Node 4: IF WhatsApp Pending & IF Mail Pending (Kiểm Tra Trạng Thái)**
- **Điều kiện**:
  - Chỉ gửi WhatsApp nếu `Message Sent = "pending"`.
  - Chỉ gửi Email nếu `Mail Sent = "pending"`.
  - **Lý do**: Tránh gửi trùng lặp khi workflow chạy lại.

#### **🔹 Node 5: Send WhatsApp (Gửi Tin Nhắn WhatsApp)**
- **Chọn Credentials**: `whatsAppApi`.
- **Template**: Chọn template WhatsApp đã chuẩn bị.
- **Tham số động**:
  - `phoneNumber`: Lấy từ cột `Phone Number` trong Google Sheets.
  - **Lưu ý**: Đảm bảo số điện thoại có định dạng `+84123456789` (không có dấu cách).

#### **🔹 Node 6: PrepareEmail (Chuẩn Bị Email)**
- **Chọn Credentials**: `inboxPlusApi`.
- **Template**: Chọn template email HTML.
- **Tham số động**:
  - `to`: Lấy từ cột `Email`.
  - **Hình ảnh**: Nếu sử dụng hình ảnh, cấu hình ở node `Fetch Email Image` (xem dưới).

#### **🔹 Node 7: Build HTML Email (Xây Dựng Email)**
- **Nếu sử dụng hình ảnh**:
  - Node `Fetch Email Image` sẽ tải hình từ Google Drive.
  - Thêm vào email bằng cách sử dụng **HTML template** với tham số động:
    ```html
    <img src="{{ $json["imageUrl"] }}" alt="Logo">
    ```

#### **🔹 Node 8: Send Gmail (Gửi Email)**
- **Chọn Credentials**: `gmailOAuth2`.
- **Template**: Chọn template email đã chuẩn bị.
- **Tham số động**:
  - `to`: Lấy từ cột `Email`.
  - **Subject**: Có thể động hoặc cố định.

#### **🔹 Node 9: Update Sheet (Cập Nhật Trạng Thái)**
- **Chọn Credentials**: `googleSheetsOAuth2Api`.
- **Range**: Cập nhật cột `Message Sent` và `Mail Sent` dựa trên kết quả:
  - `sent` (nếu thành công).
  - `failed` (nếu lỗi).
  - `pending` (nếu chưa gửi).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với một batch nhỏ (ví dụ: 5 liên lạc) để kiểm tra:
   - WhatsApp có gửi được không?
   - Email có được gửi và hiển thị hình ảnh không?
   - Trạng thái trong Google Sheets có được cập nhật không?
2. **Kích hoạt workflow** khi đã kiểm tra xong.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Theo Dõi Log & Báo Cáo**
- **Thêm node `StickyNote`** để ghi log lỗi (ví dụ: WhatsApp bị chặn, email không gửi được).
- **Tạo báo cáo định kỳ** bằng cách kết nối với **Google Data Studio** hoặc **Slack**.

### **🔹 2. Kết Nối Với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi:
  - Workflow hoàn thành.
  - Có lỗi xảy ra (ví dụ: WhatsApp bị chặn).

### **🔹 3. Sử Dụng AI Tự Động Hoàn Thành**
- Kết hợp với **OpenAI API** để tự động tạo nội dung email hoặc tin nhắn WhatsApp dựa trên dữ liệu khách hàng.

### **🔹 4. Chỉnh Sửa Batch Size**
- Nếu gặp lỗi **rate limit**, giảm `Batch Size` xuống 20-30.
- Nếu muốn tăng tốc độ, tăng lên 100-200 (nhưng không quá 500).

### **🔹 5. Sử Dụng Mẫu Email Động**
- Thay vì cố định, **tạo template email động** bằng cách sử dụng **variables** từ Google Sheets (ví dụ: tên khách hàng, mã ưu đãi).

---
## **📌 Kết Luận: Tự Động Hóa Là Lựa Chọn Hiện Thực Cho Doanh Nghiệp**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược marketing và bán hàng thay vì làm việc thủ công. Với **tự động hóa bulk WhatsApp & Email**, cùng **theo dõi trạng thái chi tiết**, bạn không chỉ tiết kiệm thời gian mà còn **tăng hiệu quả và giảm lỗi**.

**Hãy áp dụng ngay từ hôm nay!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/11921)
👉 [Cài n8n trên VPS để chạy 24/7](https://tino.vn/vps-n8n?affid=388)

---
**💡 Cần hỗ trợ thêm?**
- **Khóa học tự động hóa n8n**: [iTechNotion](https://itechnotion.com/)
- **Hỗ trợ kỹ thuật**: [Diễn đàn n8n](https://community.n8n.io/)