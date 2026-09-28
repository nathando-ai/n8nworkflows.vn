---
title: "🚀 Tự Động Hóa CRM Email Tối Đa Với Google Sheets & MailerSend (Không Cần Code)"
description: "Workflow tự động hóa CRM email hoàn chỉnh giúp các sếp quản lý gửi email cá nhân hóa, theo dõi trạng thái và tối ưu hóa chiến dịch marketing chỉ với Google Sheets và MailerSend. Tiết kiệm 100% thời gian thủ công, tăng tỷ lệ chuyển đổi và giảm lỗi."
slug: "tieu-dong-hoa-crm-email-google-sheets-mailer-send"
tags: [n8n, automation, marketing-automation, google-sheets, mailer-send, crm-email]
keywords: [n8n workflow crm email, tự động hóa gửi email, marketing automation no-code, google sheets crm, mailer send api]
---

# 🚀 **Tự Động Hóa CRM Email Tối Đa Với Google Sheets & MailerSend**

## **📌 Nỗi Đau Của Các Sếp Khi Gửi Email Thủ Công**
Gửi email marketing thủ công không chỉ tốn thời gian mà còn dễ gặp phải các vấn đề như:
- **Lặp lại dữ liệu**: Gửi email cho cùng một người nhiều lần.
- **Thiếu cá nhân hóa**: Email chung chung không tạo sự kết nối với khách hàng.
- **Không theo dõi trạng thái**: Không biết email đã được gửi thành công hay bị phản hồi "không hợp lệ".
- **Tỷ lệ mở thấp**: Do nội dung không phù hợp với từng khách hàng.
- **Rủi ro pháp lý**: Gửi email cho địa chỉ disposable hoặc không xác thực.

**Workflow này giải quyết tất cả đó!** Với **Google Sheets** làm cơ sở dữ liệu và **MailerSend** làm công cụ gửi email, các sếp có thể:
✅ **Tự động hóa toàn bộ quy trình** từ lấy dữ liệu đến gửi email.
✅ **Cá nhân hóa email** với tên, mã giảm giá, và nội dung phù hợp.
✅ **Theo dõi trạng thái** của mỗi email (đã gửi, không hợp lệ, disposable).
✅ **Chạy 24/7** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, tự động hóa từ A đến Z.
- **Tăng tỷ lệ chuyển đổi**: Email cá nhân hóa với tên, mã giảm giá và nội dung phù hợp.
- **Giảm lỗi**: Kiểm tra địa chỉ email disposable và tránh gửi email không hợp lệ.
- **Theo dõi chi tiết**: Biết được trạng thái của mỗi email (đã gửi, không hợp lệ, disposable).
- **Tối ưu hóa chi phí**: Gửi email chỉ cho khách hàng có thông tin hợp lệ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với 3 bảng dữ liệu đã chuẩn bị:
   - **`transaction`**: Lưu trữ thông tin người dùng và trạng thái email.
   - **`template`**: Danh sách template email (tên, mã giảm giá, mã quà tặng).
   - **`segment1`**: Dữ liệu khách hàng (email, số điện thoại, tên).
   *(Link Google Sheet mẫu: [Đây](https://docs.google.com/spreadsheets/d/17KqltP-NqchPhZV7gk6QToqCZX6IiA5EBkDCBNsIX_0/edit?usp=sharing))*
2. **Tài khoản MailerSend** với:
   - **API Key** (tạo tại [MailerSend Dashboard](https://mailersend.com/)).
   - **Email sender đã xác thực** (phải được MailerSend chấp thuận).
   - **Template email** đã tạo sẵn (ID template sẽ được lấy từ `type_template_id` trong Google Sheets).
3. **Credentials cho n8n**:
   - **Google API**: Cấu hình trong `n8n` (Settings > Credentials > Add Google Sheets).
   - **HTTP Header Auth**: Cấu hình cho MailerSend (Settings > Credentials > Add HTTP Header Auth).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/10179](https://n8n.io/workflows/10179).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và nhấn **Paste JSON** trong giao diện.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1: Thêm người dùng vào `transaction`** (trạng thái `0-processing`).
- **Phần 2: Gửi email tự động** (trạng thái `1-sending`).

#### **🔹 Cấu Hình Cần Thay Đổi**
| **Node**               | **Lưu Ý**                                                                 | **Tham Số Cần Điền**                          |
|------------------------|---------------------------------------------------------------------------|-----------------------------------------------|
| **Setup Flow**         | Chọn `flow_id` tương ứng với template email muốn gửi.                     | `flow_id` (ví dụ: `v28xxl2sq8dg785k`)        |
| **Get user_id from cdp** | Lấy dữ liệu từ bảng `segment1` trong Google Sheets.                     | `Sheet Name`: `segment1`                     |
| **Add records By Status Processing** | Thêm người dùng vào `transaction` với trạng thái `0-processing`. | `Sheet Name`: `transaction`                  |
| **Send an template HTML Mailerlite** | Cấu hình gửi email qua MailerSend. | `API Key`: (Từ MailerSend Dashboard)          |
|                        |                                                                           | `from.email`: (Email đã xác thực)            |
|                        |                                                                           | `template_id`: (Lấy từ `type_template_id` trong `template`) |

#### **🔹 Cấu Hình MailerSend (Quá Trình Gửi Email)**
1. **Kiểm tra email disposable**:
   - Node **Disposal Check** sẽ tự động loại bỏ email disposable.
   - Nếu email không hợp lệ, trạng thái sẽ được cập nhật thành `3-no-email` hoặc `4-disposal-email`.
2. **Gửi email**:
   - Node **Send an template HTML Mailerlite** sẽ gửi email với:
     - **Personalization**: `first_name`, `discount_code`, `gift_code`.
     - **Template ID**: Lấy từ `type_template_id` trong `template`.
   - Sau khi gửi thành công, trạng thái sẽ được cập nhật thành `2-sent`.

#### **🔹 Cấu Hình Schedule Trigger**
- **Phần 1 (Thêm người dùng)**: Có thể kích hoạt thủ công hoặc theo lịch.
- **Phần 2 (Gửi email)**: Được kích hoạt **mỗi 30 phút** để gửi email cho người dùng ở trạng thái `1-sending`.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn một `flow_id` và chạy **Test Run** để kiểm tra workflow.
   - Kiểm tra Google Sheets xem dữ liệu có được thêm/cập nhật đúng không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Thêm Báo Cáo Định Kỳ**
- Sử dụng **n8n-nodes-base.scheduleTrigger** để tạo một workflow báo cáo hàng tuần:
  - Lấy dữ liệu từ `transaction` với trạng thái `2-sent`.
  - Gửi báo cáo qua **Slack/Email** hoặc xuất ra **Google Sheets**.

### **2. Kết Nối Với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi:
  - Email được gửi thành công.
  - Email bị loại bỏ vì disposable.
  - Có lỗi trong quá trình gửi.

### **3. Tự Động Xóa Dữ Liệu Cũ**
- Sử dụng **n8n-nodes-base.filter** để loại bỏ người dùng đã gửi email thành công (`status = 2-sent`) sau 30 ngày.

### **4. Kết Hợp Với CRM Khác**
- Nếu sử dụng **HubSpot, ActiveCampaign** hoặc **Segment**, có thể kết nối với n8n để đồng bộ dữ liệu khách hàng tự động.

---

## 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quy trình CRM email**, từ lấy dữ liệu đến gửi email cá nhân hóa, theo dõi trạng thái và tối ưu hóa chiến dịch marketing. **Không cần code, không cần chuyên gia IT**, chỉ cần cấu hình đúng các bước trên.

**Hãy áp dụng ngay và tiết kiệm thời gian, tăng hiệu quả marketing!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/10179)**
**📌 [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/17KqltP-NqchPhZV7gk6QToqCZX6IiA5EBkDCBNsIX_0/edit?usp=sharing)**