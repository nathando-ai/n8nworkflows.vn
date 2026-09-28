---
title: "🚀 Tự Động Hóa Đơn Hàng Mới Shopify → CRM Zoho + Hoá Đơn Harvest + Email Khách Hàng (Không Code)"
description: "Workflow tự động hóa hoàn toàn tự động hóa việc xử lý đơn hàng mới từ Shopify: cập nhật CRM Zoho, tạo hóa đơn trên Harvest, gửi email khuyến mãi và cảm ơn khách hàng. Giúp các sếp tiết kiệm 5+ giờ/ngày và giảm thiểu lỗi thủ công."
slug: "tieu-dong-hoa-don-hang-shopify-zoho-harvest-email"
tags: [n8n, automation, shopify, zoho-crm, harvest, email-marketing, no-code]
keywords: [tự động hóa shopify, workflow n8n shopify zoho, tự động hóa hóa đơn harvest, tự động hóa email khách hàng, giảm thời gian xử lý đơn hàng]
---

# 🚀 **Tự Động Hóa Đơn Hàng Mới Shopify → CRM Zoho + Hoá Đơn Harvest + Email Khách Hàng (Không Code)**

### **💥 Nỗi Đau Của Các Sếp Khi Xử Lý Đơn Hàng Thủ Công**
Hàng ngày, các sếp phải:
- **Lặp đi lặp lại** việc cập nhật thông tin khách hàng từ Shopify sang CRM (Zoho) để theo dõi hành trình mua hàng.
- **Tạo hóa đơn thủ công** trên Harvest, dễ gây lỗi và mất thời gian.
- **Gửi email khuyến mãi/cảm ơn** sau mỗi đơn hàng, nhưng lại quên hoặc gửi sai nội dung.
- **Tốn 5-10 giờ/ngày** cho công việc này, trong khi có thể tự động hóa hoàn toàn!

**Workflow này giải quyết tất cả!** Với chỉ **một lần setup**, các sếp sẽ tự động:
✅ **Cập nhật khách hàng mới** vào Zoho CRM.
✅ **Tạo hóa đơn tự động** trên Harvest.
✅ **Gửi email khuyến mãi** (coupon) và **email cảm ơn** (thank you) cho khách hàng.
✅ **Tạo card Trello** (nếu cần) để quản lý đơn hàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/ngày** cho việc cập nhật đơn hàng thủ công.
- **Giảm thiểu lỗi** trong việc tạo hóa đơn và gửi email.
- **Tự động hóa toàn bộ chu trình khách hàng** từ mua hàng đến cảm ơn.
- **Dữ liệu đồng bộ** giữa Shopify, Zoho CRM và Harvest, tránh mất mát thông tin.
- **Khách hàng hài lòng** với email cá nhân hóa (coupon + cảm ơn).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Shopify** (API Key) để lấy thông tin đơn hàng mới.
✔ **Tài khoản Zoho CRM** (OAuth 2.0) để cập nhật khách hàng mới.
✔ **Tài khoản Harvest** (API Key) để tạo hóa đơn tự động.
✔ **Tài khoản Gmail** (OAuth 2.0) để gửi email coupon và cảm ơn.
✔ **(Tùy chọn)** Tài khoản **Trello** (API Key) để tạo card quản lý đơn hàng.
✔ **(Tùy chọn)** Tài khoản **Mailchimp** (API Key) để gắn tag cho khách hàng mới.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/1206) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (tab "Import").

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **9 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "order created" (Shopify Trigger)**
- **Chọn credentials**: `shopifyApi` (đã cấu hình trước).
- **Lọc đơn hàng mới**:
  - Thêm điều kiện `status: "fulfilled"` (đơn đã hoàn tất) để tránh xử lý đơn hàng chưa hoàn thành.
  - Thêm điều kiện `created_at: "last 24 hours"` (nếu muốn xử lý đơn hàng mới trong 24h).

##### **🔹 Node "Set fields" (Xử lý dữ liệu)**
- **Cấu hình biến**:
  - Thêm biến `customer_email` từ `$.json.customer.email`.
  - Thêm biến `order_total` từ `$.json.total_price`.
  - Thêm biến `customer_name` từ `$.json.customer.first_name + " " + $.json.customer.last_name`.

##### **🔹 Node "IF" (Điều kiện gửi email coupon)**
- **Điều kiện**: `$.json.total_price > 500000` (chỉ gửi coupon nếu đơn hàng > 500k VND).
- **Nếu điều kiện đúng**:
  - **Gmail - coupon**: Sử dụng template email coupon (ví dụ: "Cảm ơn bạn đã mua hàng! Đăng ký email để nhận 10% giảm giá lần mua tiếp theo.").
- **Nếu điều kiện sai**:
  - **Gmail - thankyou**: Sử dụng template email cảm ơn (ví dụ: "Cảm ơn bạn đã mua hàng! Chúng tôi sẽ liên hệ lại trong 24h.").

##### **🔹 Node "Zoho" (Cập nhật CRM)**
- **Tham số**:
  - `operation: "upsert"` (cập nhật hoặc thêm mới khách hàng).
  - `resource: "contact"` (dữ liệu khách hàng).
  - **Mã trường**:
    - `Email`: `$.json.customer.email`
    - `First Name`: `$.json.customer.first_name`
    - `Last Name`: `$.json.customer.last_name`
    - `Phone`: `$.json.customer.phone` (nếu có).
    - **Thêm trường tùy chọn**:
      - `Order Total`: `$.order_total` (để theo dõi doanh số).
      - `Last Order Date`: `$.json.created_at` (ngày mua hàng).

##### **🔹 Node "Harvest" (Tạo hóa đơn)**
- **Tham số**:
  - `operation: "create"` (tạo hóa đơn mới).
  - `resource: "invoice"`.
  - **Mã trường**:
    - `Subject`: `Đơn hàng #${$.json.id}`.
    - `Customer`: `$.json.customer.email` (hoặc ID khách hàng từ Zoho).
    - `Amount`: `$.order_total` (số tiền từ đơn hàng).
    - **Thêm trường tùy chọn**:
      - `Description`: `Chi tiết đơn hàng: ${$.json.line_items[0].title}` (nếu có sản phẩm).
      - `Due Date`: `Ngày tạo hóa đơn + 7 ngày`.

##### **🔹 Node "Trello" (Tùy chọn - Quản lý đơn hàng)**
- **Tham số**:
  - `boardId`: ID board Trello của bạn.
  - `listId`: ID list "Đơn hàng mới".
  - **Mã trường**:
    - `name`: `Đơn hàng #${$.json.id} - ${$.json.customer.first_name}`.
    - `desc`: `Chi tiết: ${$.json.line_items[0].title} (${$.order_total})`.
    - `labels`: `["Shopify", "Chờ xử lý"]`.

##### **🔹 Node "Mailchimp" (Tùy chọn - Gắn tag)**
- **Tham số**:
  - `resource: "memberTag"`.
  - **Mã trường**:
    - `email_address`: `$.json.customer.email`.
    - `tag_name`: `shopify_customer` (tag để phân loại khách hàng từ Shopify).

---

#### **3. Kích Hoạt ⚡️**
- **Test run** với một đơn hàng mẫu:
  1. Tạo một đơn hàng giả trên Shopify (hoặc sử dụng đơn hàng thực).
  2. Chạy workflow và kiểm tra:
     - Đơn hàng có xuất hiện trên Zoho CRM không?
     - Hóa đơn có tạo trên Harvest không?
     - Email coupon/thank you có gửi được không?
     - (Nếu dùng Trello) Card có tạo trên Trello không?
- **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi báo cáo hàng ngày**:
   - Thêm node **Gmail** hoặc **Slack** để gửi báo cáo tổng hợp đơn hàng mới mỗi sáng.
   - Ví dụ: "Tổng doanh số ngày hôm qua: 15.000.000 VND, số đơn hàng: 30."

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo đơn hàng mới cho team.
   - Ví dụ: "🚀 Đơn hàng mới từ khách hàng: [Tên Khách Hàng], Tổng: [Số tiền]."

3. **Lưu log hoạt động**:
   - Thêm node **Set** để lưu dữ liệu đơn hàng vào **Google Sheets** hoặc **Notion** để theo dõi lịch sử.

4. **Tự động gắn tag Mailchimp cho khách hàng VIP**:
   - Nếu đơn hàng > 1.000.000 VND, gắn tag `vip` để phân loại khách hàng.

5. **Tạo template email động**:
   - Sử dụng **n8n-nodes-base.llm** (nếu có) để tự động tạo nội dung email cảm ơn cá nhân hóa dựa trên đơn hàng.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc lặp lại** và tự động hóa toàn bộ chu trình từ đơn hàng Shopify đến CRM, hóa đơn và email khách hàng. **Chỉ cần setup một lần**, workflow sẽ hoạt động 24/7, giúp tiết kiệm thời gian và tăng hiệu suất kinh doanh.

**👉 Hãy áp dụng ngay và tự động hóa đơn hàng của mình!**
Nếu có vấn đề, các sếp có thể tham khảo [community n8n](https://community.n8n.io/) hoặc liên hệ với tác giả [Lorena](https://n8n.io/workflows/1206) để hỗ trợ.

---
**🚀 Cảm ơn các sếp đã đọc!** Chúc các sếp thành công với tự động hóa! 🎉