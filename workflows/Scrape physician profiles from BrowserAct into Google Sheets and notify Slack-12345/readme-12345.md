---
title: "🚀 Tự Động Hoàn Thành Scrape Thông Tin Bác Sĩ Từ Healow → Google Sheets + Thông Báo Slack (Không Cần Code)"
description: "Tự động hóa việc thu thập thông tin bác sĩ (tên, địa chỉ, chuyên khoa) từ Healow, lưu trữ vào Google Sheets và thông báo ngay trên Slack khi có dữ liệu mới. Giúp các sếp tiết kiệm 10+ giờ/tháng làm thủ công."
slug: "tieu-dong-scrape-bac-si-healow-google-sheets-slack"
tags: [n8n, automation, lead-generation, browseract, google-sheets, slack-integration]
keywords: [scrape bác sĩ Healow, tự động hóa lead generation y tế, n8n workflow y tế, scrape dữ liệu bác sĩ, google sheets + slack, browseract api]
---

# 🚀 **Tự Động Scrape Thông Tin Bác Sĩ Từ Healow → Google Sheets + Thông Báo Slack (Không Cần Code)**

### **Nỗi Đau Của Các Sếp Trong Dịch Vụ Y Tế**
Làm thủ công việc thu thập thông tin bác sĩ từ trang Healow (hoặc các trang tương tự) để xây dựng danh sách lead là **một công việc tẻ nhạt, mất thời gian và dễ sai sót**. Các sếp phải:
- **Tìm kiếm thủ công** trên Healow để lấy thông tin (tên, địa chỉ, chuyên khoa).
- **Ghi chép vào Excel/Google Sheets** một cách rườm rà.
- **Nhớ phải cập nhật định kỳ** khi có bác sĩ mới hoặc thông tin thay đổi.
- **Lo lắng mất dữ liệu** khi copy-paste sai hoặc không lưu trữ hệ thống.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình** chỉ với một cú nhấp chuột!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần làm thủ công nữa.
- **Dữ liệu chính xác & cập nhật**: Scrape từ nguồn chính thức Healow.
- **Lưu trữ hệ thống**: Tất cả thông tin bác sĩ được lưu vào Google Sheets với định dạng chuẩn.
- **Thông báo tức thời**: Nhận cảnh báo trên Slack khi có dữ liệu mới.
- **Dễ dàng mở rộng**: Thêm bác sĩ mới chỉ cần cập nhật vị trí.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản BrowserAct** (để scrape Healow):
   - [Đăng ký tài khoản BrowserAct](https://www.browseract.com/) (miễn phí cho 100 scrape/tháng).
   - **Template "Physician Profile Enricher"** đã được tải về (xem hướng dẫn [tại đây](https://docs.browseract.com)).
   - **API Key** của BrowserAct (tìm theo hướng dẫn [đây](https://docs.browseract.com)).

2. **Tài khoản Google Sheets**:
   - Một **Google Sheet** mới với tên **"Physician Profile"** và các cột:
     - `Name` (Tên bác sĩ)
     - `Address` (Địa chỉ)
     - `Specialty` (Chuyên khoa)
   - **Credentials OAuth2** cho Google Sheets (cài đặt trong n8n).

3. **Tài khoản Slack**:
   - **API Token** của Slack (tạo tại [API Slack](https://api.slack.com/apps)).
   - **Channel** để nhận thông báo (ví dụ: `#lead-generation`).

4. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/12345](https://n8n.io/workflows/12345) (hoặc file JSON được cung cấp).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON → Nhấn **Import**.
3. Workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Dán toàn bộ JSON từ file (hoặc [tại đây](https://n8n.io/workflows/12345)) → Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình **cẩn thận** các node sau:

#### **🔹 Node "Define Location" (Set)**
- **Chức năng**: Xác định vị trí scrape (thành phố, tỉnh).
- **Cách chỉnh**:
  - Nhấn **Edit** → Điền vào `City` và `State` (ví dụ: `Hồ Chí Minh`, `Vĩnh Phúc`).
  - Ví dụ:
    ```json
    {
      "json": {
        "city": "Hồ Chí Minh",
        "state": "Vĩnh Phúc"
      }
    }
    ```

#### **🔹 Node "Run BrowserAct Workflow" (BrowserAct)**
- **Chức năng**: Thực hiện scrape từ Healow bằng template đã cài đặt.
- **Cách chỉnh**:
  - **Credentials**: Chọn `browserActApi` (đã cài đặt trước).
  - **Workflow ID**: Nhập **ID của template "Physician Profile Enricher"** (tìm trong BrowserAct).
  - **Input Data**: Sử dụng output từ node "Define Location" (liên kết node bằng cách kéo và thả).

#### **🔹 Node "Splitting Items" (Code)**
- **Chức năng**: Chuyển dữ liệu raw từ BrowserAct thành JSON có cấu trúc.
- **Cách chỉnh**:
  - Nhấn **Edit** → Dùng code sau (nếu cần chỉnh sửa):
    ```javascript
    // Code mặc định (không cần chỉnh nếu scrape thành công)
    return $input.all();
    ```
  - **Lưu ý**: Nếu scrape không thành công, cần debug tại đây.

#### **🔹 Node "Update Leads" (Google Sheets)**
- **Chức năng**: Lưu dữ liệu vào Google Sheets.
- **Cách chỉnh**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đảm bảo tên là **"Physician Profile"**.
  - **Operation**: Đặt là `appendOrUpdate` (thêm hoặc cập nhật nếu có ID trùng).
  - **Headers**: Đảm bảo trùng với cột trong Google Sheets (`Name`, `Address`, `Specialty`).

#### **🔹 Node "Alert Team" (Slack)**
- **Chức năng**: Gửi thông báo khi scrape thành công.
- **Cách chỉnh**:
  - **Credentials**: Chọn `slackApi`.
  - **Channel**: Nhập `#lead-generation` (hoặc channel khác).
  - **Message**: Sử dụng template mặc định (có thể chỉnh sửa):
    ```json
    {
      "text": "🚨 **New Physician Leads Scraped!** 🚨\nCity: {{ $node["Define Location"].json("city") }}\nState: {{ $node["Define Location"].json("state") }}\nTotal: {{ $node["Splitting Items"].json("items").length }}"
    }
    ```

#### **🔹 Node "On-Demand Execution" (Manual Trigger)**
- **Chức năng**: Chạy workflow khi cần (không tự động).
- **Cách chỉnh**:
  - Để mặc định, không cần thay đổi.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thực tế):
   - Nhấn **Run Workflow** (icon play).
   - Kiểm tra **Google Sheets** và **Slack** để xác nhận dữ liệu scrape đúng.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** (icon bật tắt ở góc trên phải).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM HƠN HIỆU QUẢ]
1. **Scrape nhiều vị trí cùng lúc**:
   - Tạo nhiều **node "Define Location"** với các thành phố khác nhau, sau đó kết nối vào node "Run BrowserAct Workflow" bằng **Merge Node** (n8n-nodes-base.merge).

2. **Lưu log scrape**:
   - Thêm **node "Set"** sau "Update Leads" để lưu thời gian scrape vào Google Sheets:
     ```json
     {
       "json": {
         "scrape_time": "{{ $now }}",
         "city": "{{ $node["Define Location"].json("city") }}"
       }
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node "Schedule"** (n8n-nodes-base.schedule) để chạy scrape hàng tuần/tháng và gửi báo cáo Slack.

4. **Kết hợp với CRM**:
   - Sau khi scrape, sử dụng **node "HTTP Request"** để đẩy dữ liệu vào CRM (HubSpot, Zoho, Salesforce).

5. **Tự động hóa email**:
   - Thêm **node "Email"** (n8n-nodes-base.email) để gửi thông báo cho team khi có lead mới.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong lĩnh vực y tế, tự động hóa việc scrape thông tin bác sĩ từ Healow, lưu trữ vào Google Sheets và thông báo trên Slack **một cách hoàn toàn tự động**. **Không cần code**, chỉ cần **cấu hình vài bước đơn giản** là có thể vận hành 24/7.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (BrowserAct, Google Sheets, Slack).
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Bật Active** và **nhận lead mới mỗi khi có dữ liệu mới**!

👉 [Tải workflow ngay](https://n8n.io/workflows/12345) và bắt đầu tự động hóa ngay hôm nay! 🚀

---