---
title: "💰 Tự Động Hóa Hoá Đơn Stripe Từ Đơn Hàng Airtable + Ghi Chép Log Google Sheets (24/7)"
description: "Workflow tự động hóa hoàn toàn không cần code để tạo hoá đơn Stripe từ đơn hàng B2B đã thanh toán trên Airtable, đồng thời ghi chép tất cả thông tin vào Google Sheets để theo dõi. Giúp các sếp tiết kiệm 10+ giờ/tháng, giảm thiểu lỗi thủ công và tối ưu hóa quy trình bán hàng B2B."
slug: "tu-dong-hoa-hoa-don-stripe-tu-airtable-google-sheets"
tags: [n8n, automation, no-code, stripe, airtable, google-sheets, b2b-invoicing]
keywords: [tự động hóa hoá đơn stripe, airtable stripe automation, google sheets logging, workflow n8n b2b, tự động hóa bán hàng b2b, giảm thời gian thủ công]
---

# 🚀 **Tự Động Hóa Hoá Đơn Stripe Từ Airtable + Ghi Chép Log Google Sheets (24/7)**

### **Nỗi Đau Của Các Sếp Trong Quy Trình Bán Hàng B2B**
Các sếp thường phải mất **10-15 giờ/tháng** để:
- **Chuyển đổi đơn hàng** từ Airtable sang hoá đơn Stripe thủ công.
- **Kiểm tra lại** từng đơn hàng để đảm bảo không bỏ sót đơn hàng đã thanh toán.
- **Ghi chép log** vào Google Sheets để theo dõi, nhưng lại phải làm lại nhiều lần vì sai sót.
- **Quên gửi hoá đơn** hoặc gửi muộn, ảnh hưởng đến doanh thu.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động tạo hoá đơn Stripe** từ đơn hàng B2B đã thanh toán trên Airtable **mỗi giờ**.
✅ **Lọc chỉ đơn hàng đã thanh toán** (trạng thái `paid` + tag `B2B`) để tránh tạo hoá đơn sai.
✅ **Ghi chép tất cả thông tin** vào Google Sheets với định dạng chuyên nghiệp, giúp dễ dàng theo dõi và báo cáo.
✅ **Hoàn toàn không cần code**, chỉ cần cấu hình vài bước đơn giản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** (không phải làm thủ công mỗi ngày).
- **Giảm thiểu lỗi** (không quên tạo hoá đơn hoặc gửi sai thông tin).
- **Hoá đơn được tạo tự động** khi đơn hàng được thanh toán, không phụ thuộc vào thời gian làm việc.
- **Dữ liệu được ghi chép chi tiết** vào Google Sheets, giúp dễ dàng **báo cáo, phân tích và theo dõi**.
- **Cá nhân hóa hoá đơn** với thông tin khách hàng từ Airtable (tên, email, số điện thoại).
- **Hoàn toàn miễn phí** (n8n có phiên bản tự host miễn phí, chỉ cần trả phí VPS).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Airtable** với bảng `Orders` có các trường sau:
   - `Customer Name` (Tên khách hàng)
   - `Email` (Email khách hàng)
   - `Phone Number` (Số điện thoại, tùy chọn)
   - `financial_status` (Trạng thái thanh toán, phải có giá trị `paid`)
   - `tags` (Phải có tag `B2B`)

✔ **Tài khoản Stripe** với **API Key** (để tạo khách hàng và hoá đơn).
✔ **Google Sheets** để ghi chép log (cần chia sẻ quyền cho n8n).

✔ **VPS** (nếu tự host n8n) hoặc tài khoản n8n cloud (nếu dùng phiên bản cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8950) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (đường dẫn: `https://n8n.io/editor`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **9 node chính**, các sếp cần chú ý cấu hình các node sau:

##### **🕒 Hourly Trigger (Giao Điểm Mỗi Giờ)**
- **Cấu hình:** Đặt interval là **1 giờ** (hoặc tùy chỉnh theo nhu cầu).
- **Lưu ý:**
  - Để **test**, các sếp có thể thay đổi thành **Manual Trigger** trước.
  - **Chú ý timezone** để workflow hoạt động trong giờ làm việc của doanh nghiệp.

##### **📊 Fetch B2B Order (Lấy Đơn Hàng từ Airtable)**
- **Cấu hình:**
  - Thay thế **Record ID** trong node bằng **ID của bảng `Orders`** trong Airtable của các sếp.
  - Cập nhật **Base ID** và **Table ID** trong credentials `airtableTokenApi`.
- **Lưu ý:**
  - **Không bao giờ commit ID thật vào repo công khai** (để bảo mật).
  - Đảm bảo bảng Airtable có **các trường bắt buộc** như trên.

##### **🔍 Filter B2B Paid Orders (Lọc Đơn Hàng Đã Thanh Toán)**
- **Cấu hình:**
  - **Điều kiện lọc:**
    - `financial_status = "paid"`
    - `tags contains "B2B"`
  - **Logic:** **AND** (cả hai điều kiện phải đúng).
- **Lưu ý:**
  - Nếu cấu trúc bảng khác, các sếp có thể **cập nhật lại điều kiện**.

##### **👤 Create Stripe Customer (Tạo Khách Hàng Stripe)**
- **Cấu hình:**
  - **Mapping dữ liệu** từ Airtable sang Stripe:
    - `Customer Name` → `name`
    - `Email` → `email`
    - `Phone Number` (nếu có) → `phone`
  - **Chọn `continueOnFail`** để tránh lỗi nếu khách hàng đã tồn tại.
- **Lưu ý:**
  - Stripe sẽ **trả về ID khách hàng cũ** nếu email đã tồn tại.

##### **📄 Process Line Items (Xử Lý Các Mục Chi Tiết Đơn Hàng)**
- **Cấu hình:**
  - Node này **chia nhỏ đơn hàng thành các mục chi tiết** để tạo hoá đơn chi tiết.
  - **Nếu không có dữ liệu**, node sẽ tạo **dữ liệu mẫu** để test.
- **Lưu ý:**
  - Các sếp có thể **cập nhật logic trong code** nếu cần.

##### **🧾 Create Stripe Invoice (Tạo Hoá Đơn Stripe)**
- **Cấu hình:**
  - **Tham số quan trọng:**
    - `customer`: ID khách hàng từ bước trước.
    - `currency`: Tiền tệ của đơn hàng (ví dụ: `USD`).
    - `days_until_due`: **30 ngày** (hoặc tùy chỉnh).
    - `auto_advance: false` (hoá đơn sẽ ở trạng thái **draft** trước khi finalize).
- **Lưu ý:**
  - **Không gửi hoá đơn tự động** (để cho các sếp kiểm tra trước khi gửi).

##### **✅ Finalize Invoice (Hoàn Thành Hoá Đơn)**
- **Cấu hình:**
  - **Tham số:**
    - `auto_advance: true` (hoá đơn sẽ được gửi tự động sau khi finalize).
    - **Sử dụng ID hoá đơn** từ bước trước.
- **Lưu ý:**
  - Sau khi finalize, hoá đơn sẽ **trở thành payable** và khách hàng có thể thanh toán.

##### **📊 Format Data for Sheets (Định Hình Dữ Liệu Cho Google Sheets)**
- **Cấu hình:**
  - Node này **chuyển đổi dữ liệu** thành định dạng phù hợp để ghi vào Google Sheets.
  - **Dữ liệu bao gồm:**
    - Thông tin hoá đơn (ID, số hoá đơn, trạng thái).
    - Thông tin khách hàng (tên, email, số điện thoại).
    - Số tiền (được chuyển từ **cents** sang **ngàn đồng**).
    - **URL** để khách hàng xem hoá đơn trực tuyến.
    - **Thời gian tạo hoá đơn**.

##### **📋 Log to Google Sheets (Ghi Chép Log Vào Google Sheets)**
- **Cấu hình:**
  - **Thay thế `YOUR_SPREADSHEET_ID`** bằng **ID của Google Sheets** của các sếp.
  - **Cập nhật tên sheet và tên tab** (ví dụ: `Invoice Logs`).
  - **Cấp quyền** cho n8n truy cập vào Google Sheets.
- **Lưu ý:**
  - **Không bao giờ commit ID thật vào repo công khai** (để bảo mật).
  - Đảm bảo **cột đầu tiên** trong sheet có tên trùng với **dữ liệu đầu ra** từ node `Format Data for Sheets`.

---

#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run:** Chạy **test data** để kiểm tra workflow có hoạt động đúng không.
- **Bật Active:** Sau khi kiểm tra xong, **bật workflow** để nó chạy tự động mỗi giờ.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
Các sếp có thể **tối ưu hóa workflow** thêm bằng cách:
1. **Kết nối với Slack/Telegram** để thông báo khi hoá đơn được tạo thành công.
   - **Cách làm:** Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau node `Finalize Invoice`.
   - **Dữ liệu gửi:** Thông báo như:
     ```
     📄 Hoá đơn #{{$node["Create Stripe Invoice"].jsonpath("$.invoice.id")}} đã được tạo thành công!
     🔗 Xem hoá đơn: {{$node["Create Stripe Invoice"].jsonpath("$.invoice.hosted_invoice_url")}}
     ```

2. **Ghi log vào cơ sở dữ liệu** (ví dụ: PostgreSQL) thay vì Google Sheets.
   - **Cách làm:** Thay thế node `googleSheets` bằng `n8n-nodes-base.database`.

3. **Gửi email tự động** khi hoá đơn được tạo.
   - **Cách làm:** Thêm node `n8n-nodes-base.email` sau node `Finalize Invoice`.
   - **Nội dung email:**
     ```
     Xin chào {{customer.name}},
     Hoá đơn #{{invoice.number}} đã được tạo thành công. Vui lòng thanh toán trước ngày {{due_date}}.
     🔗 Xem hoá đơn: {{invoice.hosted_invoice_url}}
     ```

4. **Tự động gửi báo cáo hàng tháng** về doanh thu từ Stripe.
   - **Cách làm:** Sử dụng **Schedule Trigger** với interval **1 tháng** và kết hợp với node `stripe` để lấy dữ liệu báo cáo.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc làm thủ công hoá đơn, đồng thời **giảm thiểu lỗi** và **tối ưu hóa quy trình bán hàng B2B**. Với **cấu hình đơn giản** và **hoạt động tự động 24/7**, các sếp có thể tập trung vào **quản lý khách hàng** và **phát triển doanh nghiệp** thay vì làm việc vặt.

**🚀 Hãy áp dụng ngay workflow này và tiết kiệm thời gian cho doanh nghiệp!**
Nếu có bất kỳ câu hỏi nào, các sếp có thể **trả lời comment** hoặc liên hệ với cộng đồng n8n để hỗ trợ.

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/8950)** (để tham khảo và import).