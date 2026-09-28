---
title: "🚀 Brevo Contact Manager: Tự Động Hóa Quản Lý Khách Hàng, Gửi Email Chào Mừng & Theo Dõi Unsubscribe 100% Không Code"
description: "Workflow này tự động hóa việc thu thập, quản lý khách hàng từ form/webhook, nhập bulk từ Google Sheets, gửi email chào mừng và theo dõi hành vi unsubscribe trên Brevo (SendInBlue). Giúp các sếp tiết kiệm thời gian, tránh trùng lặp và tối ưu hóa chiến dịch marketing."
slug: "brevo-contact-manager-tu-dong-hoa-quan-ly-khach-hang"
tags: [n8n, automation, brevo, sendinblue, google-sheets, lead-generation, no-code]
keywords: [n8n workflow brevo, tự động hóa quản lý khách hàng, gửi email chào mừng tự động, theo dõi unsubscribe, nhập bulk từ google sheets, sendinblue automation]
---

# 🚀 **Brevo Contact Manager: Tự Động Hóa Quản Lý Khách Hàng & Gửi Email Chào Mừng**

Hết sức phiền phức phải không, các sếp? **Nhập liệu khách hàng thủ công**, **lo lắng trùng lặp dữ liệu**, **gửi email chào mừng một một**, và **không biết ai đã hủy đăng ký**? Workflow này sẽ **giải quyết tất cả** với **tự động hóa hoàn toàn** từ form/webhook đến Google Sheets, giúp bạn **tiết kiệm 10+ giờ/tháng** và **tối ưu hóa chiến dịch marketing** mà không cần viết một dòng code nào!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động thu thập khách hàng** từ form, webhook hoặc bulk import từ Google Sheets.
- **Không trùng lặp dữ liệu** nhờ chức năng `Upsert` trên Brevo.
- **Gửi email chào mừng tự động** ngay khi khách hàng đăng ký.
- **Theo dõi hành vi unsubscribe** và cập nhật ngay trên Google Sheets.
- **Tiết kiệm thời gian** lên đến **10+ giờ/tháng** so với cách làm thủ công.
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Brevo (SendInBlue)**:
   - [Đăng ký Brevo miễn phí](https://get.brevo.com/ntbswjrcxch3-5bwioc) (có thể dùng plan Free).
   - **API Key** (để cấu hình trong n8n).
   - **Template ID** của email chào mừng (cần tạo trước trên Brevo).
   - **List ID** của danh sách khách hàng (cần tạo trước trên Brevo).
2. **Google Sheets**:
   - [Clone mẫu sheet này](https://docs.google.com/spreadsheets/d/1xolrgjDUEen8bP7doUzJAdLR4698xxraxCdjWkNY_r0/edit?usp=sharing) và sao chép link.
   - **Cấu trúc cột phải khớp** với trường dữ liệu trong form/webhook (ví dụ: `firstName`, `lastName`, `email`).
3. **n8n Editor**:
   - **Credentials Brevo**:
     - `sendInBlueApi` (dùng cho API SendInBlue).
     - `httpHeaderAuth` (dùng cho HTTP Header Auth, cùng API Key với `sendInBlueApi`).
   - **Credentials Google Sheets**: `googleSheetsOAuth2Api` (cấu hình OAuth2 cho sheet).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/15085) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15085) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này hoạt động theo **3 đường dẫn chính**:
- **Đường dẫn 1: Thu thập từ form/webhook** (real-time).
- **Đường dẫn 2: Nhập bulk từ Google Sheets** (manual).
- **Đường dẫn 3: Theo dõi unsubscribe từ Brevo** (auto).

##### **A. Cấu hình Brevo (SendInBlue)**
- **Node `Upsert a contact`** và `Welcome email`:
  - Điền **`sendInBlueApi`** vào `credentials`.
  - Thiết lập `Template ID` trong `Welcome email` (tìm trên Brevo → Templates → Copy ID).
  - Thiết lập `List ID` trong `Add contact to List` (tìm trên Brevo → Lists → Copy ID).
- **Node `Email unsubscribed`**:
  - Chọn `sendInBlueApi` trong `credentials`.

##### **B. Cấu hình Google Sheets**
- **Node `Get row(s) in sheet`**:
  - Chọn `googleSheetsOAuth2Api` trong `credentials`.
  - Điền **link sheet** và **tab name** (ví dụ: `Sheet1`).
  - Chọn **cột đầu tiên** là `id` (dùng để update sau).
- **Node `Update row in sheet`** và `Update row in sheet1`:
  - Chọn cùng `googleSheetsOAuth2Api`.
  - Điền **cột `status`** để cập nhật trạng thái (ví dụ: `done`, `unsubscribed`).

##### **C. Cấu hình Webhook (nếu dùng form)**
- **Node `Webhook`**:
  - Sử dụng **path** đã cung cấp: `f6397560-5bab-40b0-af4b-5d2ee18d260c`.
  - **Kiểm tra URL webhook** trong n8n và **cấu hình form** (ví dụ: Typeform, Google Form) để gửi dữ liệu đến đây.

##### **D. Cấu hình Manual Trigger (nhập bulk)**
- **Node `When clicking ‘Execute workflow’`**:
  - Chọn `manualTrigger` để chạy workflow khi cần nhập bulk.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Sử dụng **Manual Trigger** để chạy workflow với **1-2 dòng dữ liệu mẫu** từ Google Sheets.
   - Kiểm tra:
     - Dữ liệu có được upsert vào Brevo không?
     - Email chào mừng có được gửi không?
     - Trạng thái trên Google Sheets có được cập nhật không?
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM TIẾP]
- **Kết hợp với Slack/Telegram**:
  - Thêm node `slack` hoặc `telegramBot` sau `Welcome email` để thông báo khi gửi thành công.
- **Lưu log hoạt động**:
  - Thêm node `set` hoặc `googleSheets` để ghi lại thời gian gửi email và trạng thái.
- **Gửi báo cáo định kỳ**:
  - Sử dụng node `sendInBlue` để gửi **báo cáo tổng hợp** (ví dụ: số lượng unsubscribed trong tuần).
- **Tối ưu hóa email**:
  - Sử dụng **dynamic content** trong template Brevo để cá nhân hóa email (ví dụ: `{{firstName}}`).
:::

---

### 📌 **Kết luận**
Workflow **Brevo Contact Manager** là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quản lý khách hàng**, **gửi email chào mừng** và **theo dõi unsubscribe** mà **không cần viết code**. **Chỉ cần 30 phút cấu hình**, bạn đã có một hệ thống **hoạt động 24/7**, **tiết kiệm thời gian** và **tăng hiệu quả marketing**.

**Hãy áp dụng ngay và bắt đầu tự động hóa ngay hôm nay!** 🚀
Nếu có vấn đề, các sếp có thể tham khảo [video hướng dẫn của Davide Boizza](https://youtube.com/@n3witalia) hoặc liên hệ qua [LinkedIn](https://linkedin.com/in/davideboizza).

---
**🔹 Lưu ý cuối cùng**: Đừng quên **backup sheet Google** trước khi thay đổi cấu trúc dữ liệu!