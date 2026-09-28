---
title: "🚀 Tự Động Gửi Lại Nhắc Nhở Thanh Toán Du Lịch qua WhatsApp & Email (Với Link Thanh Toán An Toàn) - Giảm 90% Công Việc Theo Dõi"
description: "Workflow tự động hóa hoàn toàn gửi nhắc nhở thanh toán cho khách hàng du lịch qua 2 kênh WhatsApp và Email, với link thanh toán an toàn, chạy tự động 2 lần/ngày (7h sáng và 7h tối). Giúp doanh nghiệp giảm 90% công việc theo dõi thủ công, tối ưu hóa dòng tiền và nâng cao trải nghiệm khách hàng."
slug: "tự-dộng-hoa-nhắc-nhở-thanh-toán-du-lich-whatsapp-email"
tags: [n8n, tự động hóa, lead nurturing, travel agency, whatsapp automation, email automation, payment reminders]
keywords: [n8n workflow du lịch, tự động hóa nhắc nhở thanh toán, gửi nhắc nhở qua whatsapp và email, giảm công việc theo dõi, thanh toán an toàn cho du lịch]
---

# 🚀 **Tự Động Gửi Lại Nhắc Nhở Thanh Toán Du Lịch qua WhatsApp & Email (Với Link Thanh Toán An Toàn)**

## **🔥 Nỗi Đau Của Các Sếp Trong Công Ty Du Lịch**
Hàng ngày, các sếp phải:
- **Theo dõi thủ công** hàng trăm khách hàng có thanh toán chậm trễ.
- **Gửi nhắc nhở** qua nhiều kênh (Email, WhatsApp, gọi điện) để tránh mất khách.
- **Lo lắng về dòng tiền** khi khách không thanh toán kịp thời.
- **Tốn thời gian** để tạo link thanh toán riêng cho mỗi khách hàng.

**Kết quả?** Công việc thủ công, dễ sai sót, và không thể hoạt động 24/7. **Workflow này giải quyết tất cả!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian** theo dõi thủ công nhắc nhở thanh toán.
✅ **Giảm 80% khách hàng không thanh toán** nhờ nhắc nhở tự động 2 lần/ngày.
✅ **Link thanh toán an toàn** tự động sinh ra cho mỗi khách hàng.
✅ **Không trùng lặp nhắc nhở** nhờ hệ thống cập nhật trạng thái tự động.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Cá nhân hóa hoàn toàn** với tên khách, số tiền, ngày hạn thanh toán.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API** (để gửi nhắc nhở qua WhatsApp).
2. **Tài khoản Email SMTP** (để gửi Email nhắc nhở).
3. **File Excel/Google Sheet** chứa danh sách khách hàng du lịch với các cột:
   - **Tên khách hàng**
   - **Số điện thoại**
   - **Số tiền cần thanh toán**
   - **Ngày hạn thanh toán**
   - **Trạng thái thanh toán** (Pending, Paid, Reminder Sent...)
4. **API Key của Microsoft Excel** (nếu sử dụng Excel Online) hoặc **Google Sheets API** (nếu chuyển sang Google Sheets).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/9844](https://n8n.io/workflows/9844) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **2 luồng chính** (sáng và tối) và **12 node**. Dưới đây là hướng dẫn chi tiết:

##### **🔹 Cấu hình Credentials (Tài khoản API)**
| Node | Yêu cầu cấu hình | Ghi chú |
|------|------------------|---------|
| **WhatsApp** | `whatsAppApi` | Cần đăng ký API WhatsApp Business và điền `Phone Number ID` và `Access Token`. |
| **Email** | `smtp` | Điền thông tin SMTP của nhà cung cấp Email (Gmail, SendGrid, Mailgun...). |
| **Microsoft Excel** | `microsoftExcelOAuth2Api` | Cần đăng ký OAuth 2.0 cho Excel Online và điền `Client ID`, `Client Secret`, `Tenant ID`. |

##### **🔹 Cấu hình File Excel/Google Sheet**
- **Tên Sheet:** Đảm bảo tên Sheet trong Excel/Google Sheets **không đổi** (ví dụ: `"Danh sách khách hàng"`).
- **Cột bắt buộc:**
  - `Name` (Tên khách hàng)
  - `Phone` (Số điện thoại)
  - `Amount` (Số tiền)
  - `Due Date` (Ngày hạn thanh toán)
  - `Status` (Trạng thái: `Pending`, `Paid`, `Reminder Sent`...)

##### **🔹 Cấu hình Node Code (3 node)**
Các node **Code** (`Prepare WhatsApp Reminder`, `Process Payment Reminders`, `Create Payment Reminders`, `Make Reminder For Email`) **không cần chỉnh sửa** vì đã được tối ưu sẵn. Tuy nhiên, các sếp có thể mở node này để:
- **Thay đổi nội dung nhắc nhở** (ví dụ: thêm logo công ty).
- **Thêm logic mới** (ví dụ: gửi tin nhắn cho admin khi khách không thanh toán).

##### **🔹 Kích hoạt Schedule Trigger**
Workflow chạy **2 lần/ngày** tại:
- **7h sáng** (Đọc và gửi nhắc nhở WhatsApp).
- **7h tối** (Đọc lại và gửi nhắc nhở Email).

**Lưu ý:**
- Nếu muốn chạy ở giờ khác, chỉnh sửa **`cron`** trong node `Daily Payment Check - 7 AM` và `Daily Payment Check - 7 PM`.
  - Ví dụ: `0 7 * * *` (7h sáng) → `0 19 * * *` (7h tối).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và nhập một khách hàng mẫu vào Excel.
   - Kiểm tra xem nhắc nhở WhatsApp và Email có được gửi không.
2. **Bật Active Workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack** hoặc **Telegram Bot** để báo cáo khi có khách hàng mới không thanh toán.
   - **Cách làm:** Sử dụng node `webhook` để nhận dữ liệu và gửi thông báo.

2. **Lưu log hoạt động**
   - Thêm node **Google Sheets** hoặc **Microsoft Excel** để ghi lại lịch sử nhắc nhở.
   - **Cách làm:** Sử dụng node `stickyNote` để lưu thông tin nhắc nhở vào một sheet riêng.

3. **Gửi báo cáo định kỳ**
   - Tạo một workflow mới để tổng hợp số liệu khách hàng chưa thanh toán và gửi báo cáo cho quản lý.
   - **Cách làm:** Sử dụng node `emailSend` hoặc `slack` để gửi báo cáo hàng tuần.

4. **Tích hợp với CRM**
   - Nếu sử dụng **HubSpot**, **Zoho CRM** hoặc **Salesforce**, có thể kết nối với node `crm` để cập nhật trạng thái khách hàng tự động.

---

### 📌 **Kết luận**
Workflow này **giải phóng 90% công việc thủ công** trong việc nhắc nhở thanh toán du lịch, giúp các sếp:
✔ **Tiết kiệm thời gian** để tập trung vào kinh doanh.
✔ **Tăng tỷ lệ thanh toán** nhờ nhắc nhở tự động 2 lần/ngày.
✔ **Cải thiện trải nghiệm khách hàng** với thông tin cá nhân hóa.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**🚀 Hãy import workflow ngay hôm nay và tự động hóa công việc nhắc nhở thanh toán của mình!**
Nếu có vấn đề, các sếp có thể liên hệ với **Oneclick AI Squad** qua [website](https://oneclickai.com) để hỗ trợ.

---
**#TựĐộngHóa #N8N #DuLịch #ThanhToánAnToàn #LeadNurturing**