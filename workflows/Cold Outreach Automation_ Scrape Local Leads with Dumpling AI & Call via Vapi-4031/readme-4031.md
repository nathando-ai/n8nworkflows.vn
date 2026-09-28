---
title: "🚀 Tự Động Hóa Cold Outreach: Scrape Địa Chỉ Local + Gọi Điện Thoại AI - Giảm 90% Công Việc Tìm Khách Hàng"
description: "Workflow tự động hóa tìm kiếm, lọc và gọi điện thoại cho doanh nghiệp local từ Google Maps, kết hợp Dumpling AI và Vapi AI - tiết kiệm 100+ giờ/năm cho các sếp marketing & sales."
slug: "tieu-dong-hoa-cold-outreach-scrape-google-maps-voi-dumpling-ai"
tags: [n8n, automation, cold outreach, dumpling-ai, vapi-ai, google-sheets, no-code]
keywords: [tự động hóa cold outreach, scrape google maps, gọi điện thoại tự động, dumpling ai, vapi ai, n8n workflow, tìm kiếm khách hàng local]
---

# 🚀 **Tự Động Hóa Cold Outreach: Scrape Địa Chỉ Local + Gọi Điện Thoại AI - Không Cần Code**

### **Nỗi Đau Của Các Sếp Marketing & Sales**
Bạn đã từng phải:
- **Tìm kiếm thủ công** hàng trăm địa chỉ doanh nghiệp local (nhà thầu, dịch vụ y tế, cửa hàng tạp hóa...) trên Google Maps?
- **Lọc và gọi điện** cho từng số điện thoại, chỉ để phát hiện ra nhiều số không hoạt động?
- **Mất thời gian quý báu** để theo dõi kết quả gọi điện, chứ chưa kể việc ghi chép vào Excel?

**Workflow này giải quyết tất cả!** Với chỉ một lần kích hoạt, bạn sẽ:
✅ **Scrape** tất cả địa chỉ doanh nghiệp local từ Google Maps theo từ khóa tự động.
✅ **Lọc** số điện thoại hợp lệ và chuẩn hóa định dạng.
✅ **Gọi điện tự động** bằng Vapi AI với script cá nhân hóa.
✅ **Ghi log** tất cả kết quả vào Google Sheets để theo dõi và phân tích.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ/năm**: Không cần tìm kiếm thủ công trên Google Maps.
- **Tỷ lệ thành công cao**: Chỉ gọi điện cho số điện thoại **hợp lệ** và đã được chuẩn hóa.
- **Tự động hóa hoàn toàn**: Gọi điện 24/7, không cần can thiệp người dùng.
- **Báo cáo chi tiết**: Tất cả kết quả gọi điện được ghi log vào Google Sheets, dễ dàng phân tích và theo dõi.
- **Cá nhân hóa gọi điện**: Vapi AI sử dụng tên doanh nghiệp trong script, tăng tỷ lệ thành công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một file Google Sheets với **2 sheet**:
     - `Keywords`: Danh sách từ khóa tìm kiếm (ví dụ: "best plumbers in Chicago", "top dentists in NY").
     - `Called Logs`: Sheet để lưu kết quả gọi điện (các cột: `Business Name`, `Phone Number`, `Call Status`, `Timestamp`).
   - **Quản lý quyền**: Cung cấp quyền `Edit` cho n8n để đọc/write vào file.

2. **Tài khoản Dumpling AI**:
   - **API Key**: Đăng ký tại [Dumpling AI](https://dumpling.ai/) và lấy `API Key` từ Dashboard.
   - **Endpoint**: `search-google-map` (được sử dụng trong node `Scrape Google Map Businesses`).

3. **Tài khoản Vapi AI**:
   - **API Key**: Đăng ký tại [Vapi AI](https://vapi.ai/) và lấy `API Key` từ Dashboard.
   - **Script gọi điện**: Các sếp có thể tùy chỉnh script trong node `Initiate Vapi AI Call` (ví dụ: `"Hello [Business Name], this is [Your Name] from [Your Company]..."`).

4. **n8n Self-Hosted**:
   - Workflow này **không hoạt động trên n8n Cloud** do yêu cầu API Key và xử lý dữ liệu lớn.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) hoặc [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4031) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → Nhấn `Import` → Chọn file JSON hoặc dán JSON vào ô `Import Workflow`.
- Workflow sẽ xuất hiện trên canvas với **9 node** như mô tả.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Credentials**
- **Google Sheets OAuth2**:
  - Tạo **credentials mới** trong n8n:
    - `Type`: `Google Sheets OAuth2`.
    - Đăng nhập Google và cấp quyền cho n8n truy cập vào file Sheets.
  - Gán credentials này cho node:
    - `Get Search Keywords from Google Sheets`.
    - `Log Called Business Info to Sheet`.

- **HTTP Header Auth (Dumpling AI & Vapi AI)**:
  - Tạo **credentials mới** trong n8n:
    - `Type`: `HTTP Header Auth`.
    - Điền `Authorization: Bearer {API_KEY}` (thay `{API_KEY}` bằng API Key từ Dumpling AI và Vapi AI).
  - Gán credentials này cho node:
    - `Scrape Google Map Businesses using Dumpling AI`.
    - `Initiate Vapi AI Call to Business`.

##### **B. Cấu Hình Node Chi Tiết**
1. **`Get Search Keywords from Google Sheets`**:
   - **Sheet Name**: Đặt là `Keywords` (sheet chứa từ khóa tìm kiếm).
   - **Range**: `A1:A` (giả sử từ khóa ở cột A, bắt đầu từ hàng 1).

2. **`Scrape Google Map Businesses using Dumpling AI`**:
   - **Method**: `POST`.
   - **URL**: `https://api.dumpling.ai/v1/search-google-map`.
   - **Headers**:
     - `Content-Type: application/json`.
     - `Authorization: Bearer {API_KEY}` (đã cấu hình trong credentials).
   - **Body**:
     ```json
     {
       "query": "{{$node["Get Search Keywords from Google Sheets"].json["$"]}}",
       "location": "auto", // Tự động xác định vị trí từ từ khóa (ví dụ: "Chicago" trong "best plumbers in Chicago")
       "limit": 50 // Số kết quả scrape mỗi lần
     }
     ```

3. **`Filter Valid Phone Numbers Only`**:
   - **Condition**: `json["$"].phone !== "" && json["$"].phone !== null`.

4. **`Format Phone Number for Calling`**:
   - **Expression** (để chuẩn hóa số điện thoại):
     ```javascript
     // Ví dụ: Chuyển số US thành +1XXXYYYYZZZ
     if (json["$"].phone.startsWith("+1")) {
       return json["$"].phone;
     } else if (json["$"].phone.length === 10 && !json["$"].phone.startsWith("0")) {
       return "+1" + json["$"].phone;
     } else {
       return json["$"].phone; // Giả sử số đã đúng định dạng
     }
     ```

5. **`Initiate Vapi AI Call to Business`**:
   - **Method**: `POST`.
   - **URL**: `https://api.vapi.ai/v1/calls`.
   - **Headers**:
     - `Content-Type: application/json`.
     - `Authorization: Bearer {API_KEY}` (credentials Vapi AI).
   - **Body**:
     ```json
     {
       "phone": "{{$node["Format Phone Number for Calling"].json["$"]}}",
       "script": "Hello {{json["$"].name}}, this is [Your Name] from [Your Company]. We noticed your business on Google Maps and would love to discuss a partnership. Could you take a moment to chat? Thank you!",
       "language": "en"
     }
     ```

6. **`Log Called Business Info to Sheet`**:
   - **Sheet Name**: `Called Logs`.
   - **Range**: `A1:D` (giả sử cột A: Business Name, B: Phone, C: Call Status, D: Timestamp).
   - **Operation**: `append` (thêm dữ liệu mới vào cuối sheet).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` và chọn **1 từ khóa** từ sheet `Keywords` để test.
   - Kiểm tra:
     - Có scrape được danh sách doanh nghiệp không?
     - Số điện thoại đã được lọc và chuẩn hóa chưa?
     - Vapi AI có gọi điện thành công không?
     - Dữ liệu đã ghi log vào `Called Logs` chưa?

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.
   - **Lưu ý**: Workflow này **không tự động chạy** khi có dữ liệu mới trong sheet `Keywords`. Các sếp cần:
     - **Kích hoạt thủ công** mỗi khi muốn scrape mới (node `Start Workflow Manually`).
     - **Hoặc** kết hợp với **n8n Trigger Node** (ví dụ: `n8n-nodes-base.webhook`) để tự động kích hoạt khi có thay đổi trong sheet.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Hóa Kích Hoạt Workflow**:
   - Thêm **node Webhook** vào đầu workflow để kích hoạt tự động khi có sự kiện (ví dụ: nhận được email hoặc thay đổi trong Google Sheets).
   - Cấu hình **Google Apps Script** để gọi Webhook khi sheet `Keywords` được cập nhật.

2. **Lưu Log Chi Tiết Hơn**:
   - Thêm cột `Call Duration` và `Call Result` vào sheet `Called Logs` để theo dõi thời gian gọi và kết quả (thành công/thất bại).

3. **Kết Hợp Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo kết quả gọi điện ngay khi workflow hoàn thành.
   - Ví dụ: `"📞 Gọi điện thành công cho [Business Name] - Số điện thoại: [Phone]"` trên Slack.

4. **Tùy Chỉnh Script Gọi Điện**:
   - Sử dụng **node LLM** (nếu có) để tự động tạo script gọi điện cá nhân hóa dựa trên ngành nghề của doanh nghiệp.

5. **Lọc Kết Quả Gọi Điện**:
   - Thêm node **Google Sheets** để lọc ra danh sách doanh nghiệp đã gọi thành công và chuyển vào sheet `FollowUp` để tiếp cận sau.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing & sales muốn tự động hóa **tìm kiếm và gọi điện cho khách hàng local** một cách hiệu quả. Bằng cách kết hợp **Dumpling AI** (scrape Google Maps), **Vapi AI** (gọi điện tự động) và **Google Sheets** (theo dõi kết quả), bạn sẽ:
✔ **Tiết kiệm thời gian** lên đến 90% so với phương pháp thủ công.
✔ **Tăng tỷ lệ thành công** với gọi điện cá nhân hóa.
✔ **Theo dõi dễ dàng** tất cả hoạt động qua Google Sheets.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** và cấu hình credentials như hướng dẫn.
2. **Import workflow** và test với 1-2 từ khóa.
3. **Bật Active** và bắt đầu tự động hóa cold outreach của mình!

---
**💡 Chia sẻ & Đánh Giá**
Nếu workflow này hữu ích, hãy **đánh giá** và **chia sẻ** với đồng nghiệp. Các sếp có thể **tùy chỉnh** script gọi điện hoặc thêm node khác để phù hợp với nhu cầu cụ thể. **Hỏi đáp và hỗ trợ** có thể được thực hiện trên [n8n Community](https://community.n8n.io/) hoặc [Dumpling AI Forum](https://forum.dumpling.ai/).

---