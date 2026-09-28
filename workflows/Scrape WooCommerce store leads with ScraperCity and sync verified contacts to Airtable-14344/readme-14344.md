---
title: "🚀 Tự Động Hóa Scrape Dữ Liệu WooCommerce & Đồng Bộ Lead Chất Lượng Vào Airtable (Không Code)"
description: "Workflow tự động hóa scrape dữ liệu từ các cửa hàng WooCommerce, lọc và đồng bộ lead có email/điện thoại hợp lệ vào Airtable - tiết kiệm 100% thời gian thủ công, giảm sai sót, và cung cấp cơ sở dữ liệu lead chất lượng cao cho chiến dịch outreach."
slug: "tieu-dong-hoa-scrape-woocommerce-dong-bo-airtable"
tags: [n8n, automation, lead-generation, web-scraping, airtable, scrapercity]
keywords: [n8n workflow scrape WooCommerce, tự động hóa lead generation, đồng bộ lead Airtable, ScraperCity API, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Scrape WooCommerce & Đồng Bộ Lead Chất Lượng Vào Airtable**

### **Giải Pháp Cho Các Sếp Bán Hàng Online**
Bạn đã bao giờ phải **quét thủ công** danh sách cửa hàng WooCommerce để tìm lead, sau đó **lọc và nhập dữ liệu** vào Airtable để chuẩn bị cho chiến dịch outreach? Hoặc phải **lo lắng về tính chính xác** của dữ liệu khi làm thủ công? Workflow này sẽ **tự động hóa toàn bộ quy trình** với **ScraperCity** và **Airtable**, giúp bạn:
✅ **Tiết kiệm 10+ giờ/tháng** cho việc scrape và xử lý lead.
✅ **Lấy lead chất lượng cao** (có email/điện thoại) từ các cửa hàng WooCommerce.
✅ **Tránh trùng lặp** và đồng bộ dữ liệu **liên tục, chính xác**.
✅ **Cập nhật tự động** khi có lead mới, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Tiết kiệm thời gian**    | Không cần scrape thủ công, workflow chạy tự động mỗi khi kích hoạt.         |
| **Lead chất lượng cao**   | Chỉ đồng bộ lead **có email hoặc điện thoại**, loại bỏ lead không hợp lệ. |
| **Không trùng lặp**       | Xóa bỏ email trùng lặp trước khi đồng bộ vào Airtable.                       |
| **Cập nhật liên tục**    | Sau khi scrape xong, dữ liệu tự động **upsert** vào Airtable (thêm mới hoặc cập nhật). |
| **Dễ dàng mở rộng**      | Có thể kết nối với **Slack/Telegram** để thông báo khi có lead mới.          |

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản ScraperCity** (đăng ký tại [app.scrapercity.com](https://app.scrapercity.com)) và **API Key**.
✔ **Airtable Base** với các trường phù hợp (ví dụ: `Email`, `Phone`, `Store URL`, `Name`).
✔ **API Key Airtable** (mở rộng từ [Airtable API](https://airtable.com/api)).
✔ **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo ổn định).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/14344](https://n8n.io/workflows/14344) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Xác nhận import.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Dán toàn bộ mã JSON từ [n8n.io/workflows/14344](https://n8n.io/workflows/14344) (chọn **Copy JSON**).
3. Xác nhận.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình ScraperCity**
1. **Tạo Credential HTTP Header Auth**:
   - Trong **Credentials** (cột bên trái), nhấn **+ Add** → Chọn **HTTP Header Auth**.
   - Đặt tên: `scrapercity-api-key`.
   - Điền **API Key** từ ScraperCity vào **Header Value** (dạng `Bearer YOUR_API_KEY`).
   - **Gắn credential này** vào các node:
     - `Start WooCommerce Lead Scrape`
     - `Poll Scrape Status`
     - `Download Scraped Results`

2. **Cấu hình "Configure Scrape Parameters"**:
   - Thay đổi các tham số scrape theo nhu cầu:
     - `platform`: `woocommerce` (không thay đổi).
     - `countryCode`: `VN` (hoặc `US`, `GB` tùy quốc gia).
     - `totalLeads`: Số lead muốn scrape (ví dụ: `500`).
     - `collectEmails`: `true` (để scrape email).

#### **B. Cấu Hình Airtable**
1. **Tạo Credential Airtable**:
   - Trong **Credentials**, nhấn **+ Add** → Chọn **Airtable**.
   - Đặt tên: `airtable-leads`.
   - Điền:
     - **API Key**: API Key từ Airtable.
     - **Base ID**: ID của Airtable Base (tìm trong URL: `https://airtable.com/<base-id>`).
     - **Table Name**: Tên bảng muốn đồng bộ (ví dụ: `WooCommerce_Leads`).

2. **Kiểm tra trường dữ liệu**:
   - Đảm bảo bảng Airtable có các trường phù hợp với dữ liệu scrape (ví dụ: `Email`, `Phone`, `Store URL`, `Name`).

#### **C. Cấu Hình Node "Filter Contacts"**
- Node này **lọc giữ lại chỉ lead có email hoặc điện thoại**.
- Nếu muốn **chỉ lead có cả email và điện thoại**, chỉnh sửa code trong node **`Parse and Clean CSV Results`** (xem phần **Mẹo nâng cao**).

#### **D. Thời gian chờ (Wait Nodes)**
- Node **`Wait Before First Poll`**: Thời gian đầu tiên chờ trước khi kiểm tra trạng thái scrape (giữ nguyên `30s`).
- Node **`Wait 60 Seconds Before Retry`**: Thời gian chờ giữa các lần retry (giữ nguyên `60s`).

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** (node `manualTrigger`).
   - Kiểm tra **Log** để xem workflow có chạy đúng không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** từ `false` sang `true`.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Thêm Thông Báo Slack/Email Khi Có Lead Mới**
- **Cách làm**:
  - Sau node **`Upsert Lead into Airtable`**, thêm node **`Slack`** hoặc **`Email`**.
  - Cấu hình để gửi thông báo khi có lead mới được đồng bộ.
- **Lợi ích**: Các sếp được **cập nhật tức thời** khi có lead chất lượng.

### **2. Lọc Lead Stricter (Cả Email và Điện Thoại)**
- Mở node **`Parse and Clean CSV Results`** (type: `code`).
- Thay đổi code để **chỉ giữ lead có cả email và điện thoại**:
  ```javascript
  // Thay đổi từ:
  const filteredLeads = data.map(row => ({
    email: row.email,
    phone: row.phone,
    storeUrl: row.storeUrl,
    name: row.name
  })).filter(row => row.email || row.phone);

  // Sang:
  const filteredLeads = data.map(row => ({
    email: row.email,
    phone: row.phone,
    storeUrl: row.storeUrl,
    name: row.name
  })).filter(row => row.email && row.phone);
  ```

### **3. Lưu Log Scrape Vào Google Sheets**
- Thêm node **`Google Sheets`** sau node **`Download Scraped Results`**.
- Cấu hình để ghi **Run ID**, **thời gian scrape**, và **số lead** vào sheet.
- **Lợi ích**: Theo dõi lịch sử scrape và tối ưu hóa quy trình.

### **4. Chạy Workflow Định Kỳ (Ví dụ: Mỗi Ngày)**
- Sử dụng **n8n Cron Trigger** để chạy workflow tự động mỗi ngày.
- **Cách làm**:
  1. Thêm node **`Cron Trigger`** vào đầu workflow.
  2. Cấu hình biểu thức cron (ví dụ: `0 0 * * *` để chạy mỗi ngày 00:00).

---

## 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc scrape và xử lý lead thủ công. Bằng cách kết hợp **ScraperCity** (dữ liệu chính xác) và **Airtable** (đồng bộ tự động), bạn sẽ có một **cơ sở dữ liệu lead chất lượng cao**, sẵn sàng cho chiến dịch outreach.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** với số lead nhỏ trước khi chạy toàn bộ.
3. **Bật Active** và **đợi workflow tự động hóa cho bạn!**

---
**💡 Bạn có thể tùy chỉnh workflow này để scrape từ các nền tảng khác (Shopify, Etsy) bằng cách thay đổi `platform` trong node `Configure Scrape Parameters`. Hãy thử nghiệm và tối ưu hóa cho phù hợp với nhu cầu của doanh nghiệp!**