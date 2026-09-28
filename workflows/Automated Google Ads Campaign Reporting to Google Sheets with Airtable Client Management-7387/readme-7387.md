---
title: "📊 **Tự Động Hóa Báo Cáo Google Ads Sang Google Sheets + Quản Lý Khách Hàng Airtable (Miễn Phí 100%)**"
description: "Workflow tự động hóa thu thập báo cáo chi tiết từ Google Ads, phân loại theo loại chiến dịch (Ecommerce/Lead), và cập nhật tự động vào Google Sheets theo tháng. Giúp các sếp tiết kiệm 10+ giờ/tháng và tránh sai sót thủ công."
slug: "tieu-dong-hoa-bao-cao-google-ads-sang-google-sheets"
tags: [n8n, automation, google-ads, google-sheets, airtable, no-code, marketing-automation]
keywords: [tự động hóa google ads, báo cáo google ads sang google sheets, quản lý khách hàng airtable, workflow n8n marketing, tự động hóa báo cáo quảng cáo]
---

# 🚀 **Tự Động Hóa Báo Cáo Google Ads Sang Google Sheets Với Quản Lý Khách Hàng Airtable**

### **Nỗi Đau Của Các Sếp Marketing**
Hàng tháng, các sếp phải:
❌ **Làm thủ công** báo cáo chi tiết từ Google Ads (tốn 5-10 giờ/tháng).
❌ **Lo lắng sai sót** khi nhập liệu vào Google Sheets (nhập nhầm tháng, loại bỏ dữ liệu quan trọng).
❌ **Không theo dõi được ROI** của từng chiến dịch (Ecommerce vs Lead Generation) một cách chính xác.
❌ **Phải quản lý nhiều khách hàng** nhưng không có hệ thống tự động hóa để cập nhật dữ liệu.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình** – từ thu thập dữ liệu Google Ads đến cập nhật báo cáo vào Google Sheets, **với chỉ 1 lần cấu hình**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không bị giới hạn API của n8n.cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** bằng cách loại bỏ việc nhập liệu thủ công.
- **Báo cáo chính xác 100%** với dữ liệu tự động thu thập từ Google Ads.
- **Phân loại tự động** chiến dịch Ecommerce (ROI) và Lead Generation (chi phí/lead).
- **Cập nhật tự động vào Google Sheets** theo tháng (không cần nhớ nhập liệu).
- **Quản lý khách hàng Airtable** được đồng bộ hóa, tránh mất dữ liệu.
- **Không bị giới hạn API** nhờ cấu trúc xử lý batch và rate limiting.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Ads** (đã cấu hình OAuth 2.0 API).
2. **Tài khoản Google Sheets** (mỗi khách hàng có 1 sheet riêng với cấu trúc cố định).
3. **Tài khoản Airtable** (để quản lý danh sách khách hàng và trạng thái "Active").
4. **API Keys**:
   - `googleAdsOAuth2Api` (cho Google Ads API).
   - `googleSheetsOAuth2Api` (cho Google Sheets API).
   - `airtableTokenApi` (cho Airtable API).
5. **Dữ liệu Airtable chuẩn bị**:
   - Cột `Google Ads Account ID` (để liên kết với Google Ads).
   - Cột `Google Sheets URL` (để cập nhật báo cáo).
   - Cột `Campaign Type` (Ecommerce/Lead).
   - Cột `Status` (phải là "Active" để workflow xử lý).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7387](https://n8n.io/workflows/7387) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Editor → Nhấn `Import` → Chọn file JSON.
  2. Hoặc copy toàn bộ JSON vào ô `Import Workflow` và nhấn `Import`.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 Phase** (xem chi tiết dưới đây), nhưng các bước **cần chú ý nhất** là:

##### **A. Cấu Hình Airtable (Phase 2)**
- **Node "Récupération info airtable"**:
  - **Credentials**: Chọn `airtableTokenApi` (đã cấu hình trước).
  - **Base ID**: Điền ID của bảng Airtable chứa khách hàng.
  - **Table Name**: Điền tên bảng (ví dụ: "Clients").
  - **Filter**: Cần lọc chỉ khách hàng có `Status = "Active"` (sử dụng `{{ $json["fields"]["Status"] }} == "Active"` trong `filterByFormula`).

##### **B. Cấu Hình Google Ads API (Phase 4 & 5)**
- **Node "Query Ecommerce" và "Query Lead"**:
  - **Credentials**: Chọn `googleAdsOAuth2Api`.
  - **URL**: Sử dụng template mặc định (n8n sẽ tự động tạo từ `customerId` trong Airtable).
  - **Query Parameters**:
    - `service`: `GoogleAdsService/v16/customers`.
    - `customerId`: `{{ $json["fields"]["Google Ads Account ID"] }}`.
    - `select`: `metrics.cost_micros, metrics.conversions_value, metrics.conversions`.
    - **Lọc chiến dịch có chi tiêu > 0**:
      ```json
      {
        "predicate": {
          "fieldName": "metrics.cost_micros",
          "operator": "GREATER_THAN",
          "comparisonValue": "0"
        }
      }
      ```

##### **C. Xử Lý Dữ Liệu (Phase 6)**
- **Node "Tri données ecommerce" và "Tri données lead"**:
  - **Code JavaScript**: Chuyển đổi `cost_micros` (đơn vị micros) thành tiền (ví dụ: `cost_micros / 1e6`).
  - **Ví dụ mã trong Code Node**:
    ```javascript
    // Chuyển đổi cost_micros sang USD/EUR
    const costInUSD = $input.all().map(item => ({
      ...item,
      cost: item.metrics.cost_micros / 1e6,
      conversionValue: item.metrics.conversions_value / 1e6
    }));
    return costInUSD;
    ```

##### **D. Cập Nhật Google Sheets (Phase 7 & 8)**
- **Node "Remplissage ecommerce" và "Remplissage lead"**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: Trích xuất từ URL Google Sheets của khách hàng (ví dụ: `{{ $json["fields"]["Google Sheets URL"].split("/d/")[1].split("/edit")[0] }}`).
  - **Sheet Name**: Đặt cố định (ví dụ: "Báo cáo").
  - **Range**: **Tự động tính toán cột tháng** (ví dụ: `B2:B11` cho tháng 1, `C2:C11` cho tháng 2).
    - Sử dụng **Code Node "Formatage requete ecommerce"** để tính toán:
      ```javascript
      // Tính toán cột tháng (B=1, C=2,...)
      const month = new Date().getMonth() + 1;
      const column = String.fromCharCode(65 + month);
      return `${column}2:${column}11`;
      ```
  - **Data**: Đảm bảo dữ liệu có cấu trúc:
    ```json
    [
      { "r": "2", "v": "Performance Max" },
      { "r": "3", "v": "1500000" }, // Cost (micros)
      { "r": "4", "v": "50" }       // Conversions
    ]
    ```

##### **E. Schedule Trigger (Phase 1)**
- **Node "10 du mois"**:
  - **Cron Expression**: `0 0 10 3 * ?` (chạy vào ngày 3 tháng mỗi tháng lúc 10:00 AM).
  - **Lưu ý**: Nếu muốn chạy vào ngày khác, chỉnh sửa cron (ví dụ: `0 0 10 15 * ?` cho ngày 15).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **1 khách hàng mẫu** trong Airtable và chạy **Manual Trigger** để kiểm tra.
   - Kiểm tra:
     - Dữ liệu Google Ads có được thu thập không?
     - Dữ liệu có được cập nhật vào Google Sheets không?
     - Cột tháng có đúng không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Thêm **Node Slack/Telegram** sau `Wait1` để thông báo khi workflow hoàn thành.
   - Ví dụ:
     ```json
     {
      "type": "n8n-nodes-base.slack",
      "credentials": "slackApiToken",
      "options": {
        "channel": "#báo-cáo-google-ads",
        "text": "📊 Báo cáo tháng {{ $json["month"] }} đã tự động cập nhật cho {{ $json["clientName"] }}!"
      }
     }
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm **Node StickyNote** để lưu log lỗi hoặc thành công:
     ```json
     {
      "type": "n8n-nodes-base.stickyNote",
      "options": {
        "content": `🔹 Khách hàng: {{ $json["clientName"] }} \n🔹 Ngày chạy: {{ $json["date"] }} \n🔹 Trạng thái: {{ $json["status"] }}`
      }
     }
     ```

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **Node Email** để gửi báo cáo tổng hợp hàng tháng cho team:
     ```json
     {
      "type": "n8n-nodes-base.email",
      "credentials": "gmailOAuth2Api",
      "options": {
        "to": "team@doanhnghiep.com",
        "subject": "Báo cáo Google Ads Tháng {{ $json["month"] }}",
        "html": "Xin chào, \n\nDữ liệu báo cáo đã tự động cập nhật. Link xem: {{ $json["googleSheetsUrl"] }}"
      }
     }
     ```

4. **Quản Lý API Rate Limit**:
   - Nếu gặp lỗi `quota exceeded`, tăng **thời gian chờ** (`Wait` node) từ 1 phút lên 2-3 phút.

---

### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc nhập liệu thủ công, đồng thời **tăng độ chính xác** của báo cáo Google Ads. Với **chỉ 1 lần cấu hình**, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng**.
✅ **Tránh sai sót** khi nhập liệu.
✅ **Theo dõi ROI** của từng chiến dịch một cách tự động.
✅ **Quản lý khách hàng** một cách hệ thống hóa.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để tránh giới hạn API).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để nó làm việc tự động hàng tháng!

**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ với Growth AI để tối ưu hóa workflow! 🚀