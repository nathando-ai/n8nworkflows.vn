---
title: "🚀 Tự Động Hóa Gửi Email Cảnh Báo Thanh Toán Thành Công Cho Admin Trên Sharetribe (Không Cần Code)"
description: "Workflow tự động hóa gửi email cảnh báo đến admin khi có giao dịch thanh toán thành công trên Sharetribe, tiết kiệm thời gian theo dõi thủ công và giảm thiểu lỗi nhầm lẫn. Hỗ trợ quản lý 2 bên thị trường hiệu quả với chi phí thấp."
slug: "tieu-dong-hoa-gui-email-canh-bao-thanh-toan-sharetribe"
tags: [n8n, automation, no-code, sharetribe, gmail, ticket-management]
keywords: [n8n workflow sharetribe, tự động hóa thanh toán sharetribe, gửi email cảnh báo thanh toán, tự động hóa quản lý thị trường 2 bên, n8n gmail alert]
---

# 🚀 **Tự Động Hóa Gửi Email Cảnh Báo Thanh Toán Thành Công Cho Admin Trên Sharetribe**

### **Giải quyết vấn đề gì?**
Các sếp quản lý **Sharetribe** (như sàn giao dịch 2 bên như Airbnb, Uber, hoặc các nền tảng chia sẻ) thường phải **theo dõi thủ công** các giao dịch thanh toán, kiểm tra trạng thái "pre-payment" → "paid", và gửi thông báo cho admin. Điều này **tốn thời gian, dễ sai sót**, và không thể hoạt động 24/7.

**Workflow này tự động hóa toàn bộ quá trình:**
✅ **Nhận thông báo ngay khi giao dịch chuyển từ "pre-payment" → "paid"**
✅ **Lấy thông tin chi tiết giao dịch (người dùng, sản phẩm, số tiền, thời gian)**
✅ **Gửi email cảnh báo đến admin với nội dung cá nhân hóa**
✅ **Hoạt động liên tục, không cần can thiệp thủ công**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công giao dịch hàng ngày.
- **Chính xác 100%**: Không bỏ lỡ giao dịch nào và tránh sai sót trong quá trình kiểm tra.
- **Cá nhân hóa thông báo**: Email bao gồm tất cả thông tin cần thiết (người dùng, sản phẩm, số tiền, thời gian).
- **Hoạt động liên tục**: Workflow chạy 24/7, ngay cả khi admin nghỉ ngơi.
- **Tiết kiệm chi phí**: So với việc thuê nhân viên theo dõi thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Sharetribe**:
   - **API Key OAuth2** (để kết nối với Sharetribe).
   - **Event Subscription** cho các sự kiện giao dịch (`transaction.transition`).
2. **Tài khoản Gmail**:
   - **Email admin** (để nhận cảnh báo).
   - **OAuth2 API Key** của Gmail (để gửi email tự động).
3. **Thông tin cấu hình**:
   - **Tên sàn giao dịch (Marketplace Name)** (để hiển thị trong email).
   - **Danh sách người nhận email** (có thể là admin hoặc nhóm quản trị).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15936) hoặc copy toàn bộ JSON từ đây.
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô **"Import from JSON"**.
- **Lưu workflow** với tên **"Sharetribe Paid Transaction Alert"** (hoặc tên phù hợp).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: When New Sharetribe Event (n8n-nodes-sharetribe.sharetribeTrigger)**
- **Chọn credentials**: `sharetribeOAuth2Api` (đã cấu hình trước khi import).
- **Event Type**: Chọn `"transaction.transition"` (để theo dõi sự kiện chuyển trạng thái giao dịch).
- **Test Connection**: Nhấn **"Test"** để xác nhận kết nối thành công.

##### **🔹 Node 2 & 3: Check Pre-payment Transition & Fetch Last Transition (n8n-nodes-sharetribe.sharetribe)**
- **Credentials**: `sharetribeOAuth2Api`.
- **Key Parameters**:
  - `resource`: `"transaction"`.
  - **Filter**: Các node `IF` sau sẽ kiểm tra trạng thái chuyển đổi từ `"pre-payment"` → `"paid"`. Các sếp cần **điền chính xác tên trạng thái** của Sharetribe (ví dụ: `"pre-payment"`, `"paid"`).
  - **Lưu ý**: Nếu Sharetribe sử dụng trạng thái khác, cần **cập nhật trong node `IF`** (xem phần **Mẹo & gợi ý nâng cao**).

##### **🔹 Node 4: Fetch Marketplace Name (n8n-nodes-sharetribe.sharetribe)**
- **Credentials**: `sharetribeOAuth2Api`.
- **Key Parameters**:
  - `resource`: `"marketplace"`.
  - **ID Marketplace**: Sử dụng `{{$node["When New Sharetribe Event"].json["marketplace_id"]}}` (để lấy ID từ sự kiện giao dịch).

##### **🔹 Node 5: Prepare Email Fields (n8n-nodes-base.set)**
- **Cấu hình các trường email**:
  - **Subject**: `"New Paid Transaction Alert: {{$node["Fetch Marketplace Name"].json["name"]}}"` (hiển thị tên sàn).
  - **Body**: Thêm thông tin chi tiết như:
    ```html
    <p><strong>Transaction ID:</strong> {{$node["Retrieve Transaction Details"].json["id"]}}</p>
    <p><strong>Buyer:</strong> {{$node["Retrieve Transaction Details"].json["buyer"]["name"]}}</p>
    <p><strong>Amount:</strong> {{$node["Retrieve Transaction Details"].json["amount"]}} {{{$node["Retrieve Transaction Details"].json["currency"]}}}</p>
    <p><strong>Product:</strong> {{$node["Retrieve Transaction Details"].json["product"]["name"]}}</p>
    ```
  - **Lưu ý**: Các sếp có thể **thêm/loại bỏ trường** tùy thuộc vào yêu cầu.

##### **🔹 Node 6: Send Admin Payment Email (n8n-nodes-base.gmail)**
- **Credentials**: `gmailOAuth2` (đã cấu hình trước).
- **Recipient**: Điền **email admin** (ví dụ: `admin@example.com`).
- **Subject & Body**: Sử dụng dữ liệu từ node `Prepare Email Fields`.
- **Test Email**: Nhấn **"Test"** để gửi email mẫu trước khi kích hoạt.

##### **🔹 Node 7 & 8: Retrieve Transaction Details (n8n-nodes-sharetribe.sharetribe)**
- **Credentials**: `sharetribeOAuth2Api`.
- **Key Parameters**:
  - `resource`: `"transaction"`.
  - **ID Transaction**: Sử dụng `{{$node["When New Sharetribe Event"].json["transaction_id"]}}`.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chọn **"Run Workflow"** với dữ liệu mẫu (nếu có sự kiện giao dịch mới).
- **Active Workflow**: Nhấn **"Active"** để workflow chạy tự động khi có giao dịch mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Cập nhật trạng thái chuyển đổi**:
   - Nếu Sharetribe sử dụng trạng thái khác (ví dụ: `"waiting_for_payment"` → `"completed"`), các sếp cần **điều chỉnh trong node `IF`**:
     ```json
     {
       "path": "$.transition.from",
       "operator": "equals",
       "values": ["waiting_for_payment"]
     }
     ```
     và
     ```json
     {
       "path": "$.transition.to",
       "operator": "equals",
       "values": ["completed"]
     }
     ```

2. **Gửi email đến nhóm quản trị**:
   - Thay vì gửi cho 1 email, các sếp có thể **gửi đến nhóm** (ví dụ: `admin1@example.com, admin2@example.com`).
   - Hoặc sử dụng **Slack/Telegram** thay vì Gmail (cài node `n8n-nodes-slack` hoặc `n8n-nodes-telegram`).

3. **Lưu log giao dịch**:
   - Thêm node `n8n-nodes-base.airtable` hoặc `n8n-nodes-base.googleSheets` để **lưu lịch sử giao dịch** vào bảng Excel/Google Sheets.

4. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.date`** để kiểm tra ngày và gửi **báo cáo tổng hợp** hàng tuần cho admin.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý Sharetribe, **tránh bỏ lỡ giao dịch** và **cải thiện trải nghiệm quản lý** với thông báo tự động. **Chỉ cần import, cấu hình và kích hoạt** là xong!

**Hành động ngay:**
1. **Import workflow** từ [đây](https://n8n.io/workflows/15936).
2. **Cấu hình Sharetribe & Gmail** theo hướng dẫn.
3. **Kích hoạt và theo dõi** các giao dịch thanh toán thành công!

Nếu cần **hỗ trợ tùy chỉnh** hoặc **phát triển thêm tính năng**, liên hệ với **Greg Long** (tác giả workflow) qua [LinkedIn](https://www.linkedin.com/in/greglong/) hoặc [GitHub](https://github.com/greglong).

---
**🚀 Cám ơn các sếp đã sử dụng n8n để tự động hóa quá trình!**