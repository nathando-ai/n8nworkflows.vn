---
title: "🚀 Tự Động Hóa Chuyển Dữ Liệu Đơn Hàng Shopify Sang Airtable Cấu Trúc - Không Cần Code!"
description: "Workflow này tự động lấy dữ liệu đơn hàng từ Shopify, xử lý và lưu vào Airtable theo cấu trúc chuyên nghiệp, giúp các sếp tiết kiệm thời gian và tránh sai sót trong quản lý khách hàng và doanh số."
slug: "tieu-dong-hoa-chuyen-du-lieu-don-hang-shopify-sang-airtable"
tags: [n8n, automation, no-code, Shopify, Airtable, CRM, ecommerce]
keywords: [n8n workflow Shopify, tự động hóa đơn hàng, Airtable CRM, quản lý khách hàng tự động, kết nối Shopify Airtable]
---

# 🚀 **Tự Động Hóa Chuyển Dữ Liệu Đơn Hàng Shopify Sang Airtable - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Quản Lý Đơn Hàng Thủ Công**
Hàng ngày, các sếp phải:
- **Chuyển dữ liệu đơn hàng** từ Shopify sang Airtable một cách thủ công → **Tốn thời gian** (thậm chí mất cả ngày).
- **Sai sót trong nhập liệu** → Khách hàng bị nhầm lẫn, đơn hàng không theo dõi được.
- **Không theo dõi chi tiết sản phẩm** → Không biết khách mua gì, kích thước, màu sắc → **Không thể personalize marketing** sau này.
- **Không có hệ thống tự động** → Khi doanh số tăng, việc nhập liệu thủ công trở nên **không thể quản lý** được.

**Workflow này giải quyết tất cả!** Nó **tự động lấy dữ liệu đơn hàng từ Shopify**, **xử lý và lưu vào Airtable** theo cấu trúc chuyên nghiệp, giúp các sếp:
✅ **Tiết kiệm 10-20 giờ/tuần** (không cần nhập liệu thủ công).
✅ **Tránh sai sót** (dữ liệu chính xác 100%).
✅ **Quản lý khách hàng hiệu quả** (theo dõi lịch sử mua hàng, chi tiết sản phẩm).
✅ **Cơ sở dữ liệu sẵn sàng cho marketing tự động** (email, SMS, loyalty program).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% đơn hàng** → Không cần nhập liệu thủ công.
- **Dữ liệu chi tiết sản phẩm** → Biết khách mua gì (màu, kích thước, SKU) → **Cơ sở cho marketing cá nhân hóa**.
- **Hệ thống tự động số hóa đơn** → Không cần tính thủ công.
- **Dữ liệu sẵn sàng cho báo cáo** → Theo dõi doanh số, khách hàng VIP, sản phẩm hot.
- **Không giới hạn quy mô** → Khi doanh số tăng, workflow vẫn hoạt động **ổn định 24/7**.
- **Kết nối với nhiều công cụ khác** → Sau này có thể mở rộng với **Slack, Email, Google Sheets, LLM...**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Shopify** (cần **API Key** để kích hoạt webhook).
✔ **Tài khoản Airtable** (cần **API Key** để kết nối).
✔ **Bảng Airtable đã chuẩn bị**:
   - **Customer Sheet** (để lưu thông tin khách hàng).
   - **Sales Sheet** (để lưu chi tiết đơn hàng).
✔ **N8n Self-hosted** (không dùng phiên bản miễn phí để tránh giới hạn).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6494](https://n8n.io/workflows/6494) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON và **paste** vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **9 node**, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **🔹 Node 1: Webhook (Trigger)**
- **Tên node**: `create order`
- **Cấu hình**:
  - **Path**: `createorder` (để Shopify gửi dữ liệu đến đây).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (sử dụng mặc định).
- **Lưu ý**:
  - **Cần kích hoạt Webhook trên Shopify**:
    1. Vào **Shopify Admin → Settings → Notifications**.
    2. Tìm **Orders** → Chọn **Create Order**.
    3. Nhập **URL Webhook**: `https://[your-n8n-domain]/webhook/createorder` (địa chỉ VPS của bạn).
    4. **Save**.

##### **🔹 Node 2: Airtable (Search Records - Customer Sheet)**
- **Tên node**: `Order Sheet`
- **Cấu hình**:
  - **Credentials**: Chọn `airtableTokenApi` (đã cấu hình trước).
  - **Operation**: `search`.
  - **Base ID**: ID của bảng **Customer Sheet** trên Airtable.
  - **Fields**: Chỉ cần **Email** (để tìm khách hàng đã tồn tại).
- **Lưu ý**:
  - **Nếu khách hàng mới**, workflow sẽ tự động thêm vào **Customer Sheet**.
  - **Nếu khách hàng cũ**, workflow sẽ **cập nhật lại thông tin**.

##### **🔹 Node 3: Code (Auto-Increment S No)**
- **Tên node**: `Generating S No1`
- **Cấu hình**:
  - **JavaScript Code** (đã sẵn trong workflow):
    ```javascript
    const firstItem = $input.all()[0];
    let sNo = firstItem.S_No || 0;
    sNo += 1;
    firstItem.S_No = sNo;
    return [firstItem];
    ```
  - **Lưu ý**:
    - **S_No** là **số tự động tăng** cho đơn hàng (ví dụ: 1, 2, 3...).
    - Nếu **không có S_No**, nó sẽ tự động bắt đầu từ **0**.

##### **🔹 Node 4: Airtable (Upsert - Customer Sheet)**
- **Tên node**: `CustomerSheet`
- **Cấu hình**:
  - **Credentials**: Chọn `airtableTokenApi`.
  - **Operation**: `upsert` (thêm hoặc cập nhật).
  - **Base ID**: ID của bảng **Customer Sheet**.
  - **Fields**: Đảm bảo **Email** là **Primary Key** (để tránh trùng lặp).
- **Lưu ý**:
  - **Nếu khách hàng mới**, workflow sẽ **thêm mới**.
  - **Nếu khách hàng cũ**, workflow sẽ **cập nhật lại thông tin**.

##### **🔹 Node 5: Airtable (Create Record - Sales Sheet)**
- **Tên node**: `Sheet` (hoặc tên tương tự)
- **Cấu hình**:
  - **Credentials**: Chọn `airtableTokenApi`.
  - **Operation**: `create`.
  - **Base ID**: ID của bảng **Sales Sheet**.
  - **Fields**: Đảm bảo **S_No** (số tự động) và **Order ID** (từ Shopify) được lưu.
- **Lưu ý**:
  - **Workflow sẽ lưu toàn bộ chi tiết đơn hàng**, bao gồm:
    - **Thông tin khách hàng** (tên, email, số điện thoại).
    - **Chi tiết sản phẩm** (màu, kích thước, SKU, giá).
    - **Tổng tiền, thuế, phí vận chuyển**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **một đơn hàng mẫu** từ Shopify đến Webhook.
  - Kiểm tra **Airtable** xem dữ liệu có được lưu chính xác không.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau **Airtable** để **báo cáo đơn hàng mới** ngay khi khách mua hàng.
   - **Cách làm**:
     - Thêm **node Slack** (n8n-nodes-base.slack).
     - Cấu hình **webhook URL** từ Slack.
     - Gửi tin nhắn: `📦 Đơn hàng mới từ khách hàng: {{$json["customer"]["first_name"]}} - Tổng tiền: {{$json["total_price"]}}`.

2. **Lưu Log & Báo Cáo Định Kỳ**:
   - Thêm **node Email** (n8n-nodes-base.email) để gửi **báo cáo doanh số hàng ngày/tuần**.
   - **Cách làm**:
     - Sử dụng **node Schedule** (n8n-nodes-base.schedule) để chạy hàng ngày.
     - Gửi email với **tổng doanh số, sản phẩm bán chạy nhất**.

3. **Tích Hợp với Google Sheets**:
   - Nếu các sếp muốn **dữ liệu trên Google Sheets**, thêm **node Google Sheets** (n8n-nodes-base.googleSheets).
   - **Cách làm**:
     - Chọn **Sheet** và **Range** (ví dụ: `Sheet1!A1`).
     - Chọn **mode**: `createUpdate`.

4. **Xử Lý Đơn Hàng Trạng Thái Khác**:
   - Nếu muốn **chỉ lấy đơn hàng mới** (không phải đã hủy/xóa), thêm **node Filter** (n8n-nodes-base.filter) sau Webhook.
   - **Cấu hình**:
     - **Condition**: `{{$json["status"]}} === "fulfilled"` (chỉ lấy đơn hàng đã hoàn tất).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc **nhập liệu thủ công**, đồng thời **tạo ra một hệ thống quản lý khách hàng và đơn hàng chuyên nghiệp**, sẵn sàng cho **marketing tự động và phân tích dữ liệu**.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình **Webhook Shopify + Airtable**.
3. **Test và bật workflow** để **tự động hóa đơn hàng** ngay từ bây giờ!

**🚀 Kết quả?** Một **hệ thống CRM tự động**, **không sai sót**, và **sẵn sàng mở rộng** cho tương lai!

---
**💡 Cần hỗ trợ?** Hãy để lại bình luận hoặc liên hệ với tôi để được tư vấn chi tiết!