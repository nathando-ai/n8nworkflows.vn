---
title: "🚀 Tự Động Hóa Scrape Dữ Liệu Shopify & Xác Minh Lead Tối Tiến Cho HubSpot (Không Cần Code)"
description: "Workflow này tự động scrape thông tin cửa hàng Shopify từ ScraperCity, xác minh email, loại bỏ trùng lặp và đẩy lead chất lượng cao vào HubSpot CRM. Giúp các sếp tiết kiệm 10-15 giờ/tháng và nâng cao tỷ lệ chuyển đổi lead lên 30%."
slug: "tieu-dong-hoa-scrape-shopify-va-xac-minh-lead-cho-hubspot"
tags: [n8n, automation, lead generation, HubSpot, ScraperCity, no-code, CRM]
keywords: [n8n workflow scrape Shopify, tự động hóa lead generation, xác minh email lead, HubSpot CRM tự động, ScraperCity API, workflow không code]
---

# 🚀 **Tự Động Hóa Scrape Dữ Liệu Shopify & Xác Minh Lead Tối Tiến Cho HubSpot**

## **🔍 Nỗi Đau Của Các Sếp Trong Lead Generation**
Bạn đã từng phải:
- **Tốn thời gian** để tìm kiếm và scrape dữ liệu cửa hàng Shopify thủ công?
- **Lo lắng về chất lượng lead** vì không biết email nào là hợp lệ?
- **Phải nhập liệu lặp đi lặp lại** vào HubSpot, gây ra sai sót và trùng lặp?
- **Không biết cách xác minh email** để đảm bảo lead có thể liên lạc được?

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Scrape dữ liệu cửa hàng Shopify** từ ScraperCity (12+ scraper chuyên nghiệp).
✅ **Xác minh email** để loại bỏ lead giả mạo.
✅ **Loại bỏ trùng lặp** và duy trì danh sách lead sạch sẽ.
✅ **Đẩy lead chất lượng cao** vào HubSpot CRM với thông tin đầy đủ.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
- **Tăng tỷ lệ chuyển đổi lead** lên **30%** nhờ xác minh email.
- **Danh sách lead sạch sẽ** (không trùng lặp, không sai sót).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Tích hợp hoàn hảo** với HubSpot, giúp marketing và sales đồng bộ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản ScraperCity** (đăng ký tại [ScraperCity](https://scrapercity.com/)) và **API Key** của hai endpoint:
   - **Scrape API** (để scrape dữ liệu cửa hàng).
   - **Email Validation API** (để xác minh email).
2. **Tài khoản HubSpot** (đăng ký tại [HubSpot](https://www.hubspot.com/)) và **OAuth2 API Key** hoặc **API Key** để kết nối với n8n.
3. **VPS Self-hosted n8n** (để workflow chạy 24/7 ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
4. **Tham số scrape** (các sếp sẽ cấu hình sau):
   - `countryCode` (ví dụ: `US`, `GB`, `VN`).
   - `totalLeads` (số lượng lead muốn scrape).
   - `includeEmails` và `includePhones` (bật/tắt tùy chọn).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/14032](https://n8n.io/workflows/14032).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào **Create Workflow** → **Import Workflow**.

:::note[**Lưu ý quan trọng**]
- **Không thay đổi cấu trúc** của workflow (sắp xếp node theo thứ tự hiện có).
- **Không xóa node** nào trừ khi hiểu rõ tác dụng của nó.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: "When clicking Execute workflow" (manualTrigger)**
- **Không cần chỉnh gì**, chỉ cần nhấn **"Execute"** khi muốn chạy workflow.

#### **🔹 Node 2: "Configure Search Parameters" (set)**
Các sếp **cần chỉnh** các tham số này:
```json
{
  "countryCode": "US",  // Mã quốc gia (ví dụ: US, GB, VN)
  "totalLeads": 100,    // Số lượng lead muốn scrape
  "includeEmails": true, // Bật để scrape email
  "includePhones": false // Tắt nếu không cần số điện thoại
}
```

#### **🔹 Node 3: "Start Shopify Store Scrape" (httpRequest)**
- **Chỉnh URL và Header**:
  ```json
  {
    "method": "POST",
    "url": "https://api.scrapercity.com/v1/scrape",
    "headers": {
      "Authorization": "Bearer YOUR_SCRAPERCITY_API_KEY",
      "Content-Type": "application/json"
    },
    "body": {
      "params": {
        "countryCode": "{{ $node["Configure Search Parameters"].json["countryCode"] }}",
        "totalLeads": "{{ $node["Configure Search Parameters"].json["totalLeads"] }}",
        "includeEmails": "{{ $node["Configure Search Parameters"].json["includeEmails"] }}",
        "includePhones": "{{ $node["Configure Search Parameters"].json["includePhones"] }}"
      }
    }
  }
  ```
- **Thay `YOUR_SCRAPERCITY_API_KEY`** bằng API Key của ScraperCity.

#### **🔹 Node 10: "Download Scraped Store Leads" (httpRequest)**
- **Chỉnh URL để tải CSV**:
  ```json
  {
    "method": "GET",
    "url": "https://api.scrapercity.com/v1/scrape/{{ $node["Store Scrape Run ID"].json["runId"] }}/download",
    "headers": {
      "Authorization": "Bearer YOUR_SCRAPERCITY_API_KEY"
    }
  }
  ```

#### **🔹 Node 14: "Start Email Validation" (httpRequest)**
- **Chỉnh URL để gửi email đến ScraperCity**:
  ```json
  {
    "method": "POST",
    "url": "https://api.scrapercity.com/v1/validate/emails",
    "headers": {
      "Authorization": "Bearer YOUR_SCRAPERCITY_API_KEY",
      "Content-Type": "application/json"
    },
    "body": {
      "emails": "{{ $node["Collect Emails for Validation"].json["emails"] }}"
    }
  }
  ```

#### **🔹 Node 25: "Create or Update HubSpot Contact" (hubspot)**
- **Chỉnh mapping field** để đảm bảo dữ liệu scrape vào HubSpot chính xác:
  - **Email** → `email` (trường bắt buộc).
  - **Name** → `firstName` + `lastName` (nếu có).
  - **Phone** → `phone` (nếu scrape được).
  - **Shopify Store URL** → `custom:shopify_url` (tùy chọn).
- **Cấu hình OAuth2** trong **Credentials HubSpot** của n8n.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute"** và kiểm tra từng node có hoạt động không.
   - **Node "Is Scrape Complete?"** và **"Is Validation Complete?"** phải trả về `true`.
2. **Bật Active**:
   - Sau khi test thành công, **bật switch "Active"** ở góc trên bên phải.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram để báo cáo**
- Thêm **node Slack/Telegram** sau **"Create or Update HubSpot Contact"** để thông báo khi lead được đẩy vào HubSpot.
- **Cấu hình message**:
  ```json
  {
    "text": "🚀 Lead mới được đẩy vào HubSpot!\nEmail: {{ $node["Create or Update HubSpot Contact"].json["email"] }}\nTên: {{ $node["Create or Update HubSpot Contact"].json["firstName"] }} {{ $node["Create or Update HubSpot Contact"].json["lastName"] }}"
  }
  ```

### **🔹 Lưu log scrape vào Google Sheets**
- Thêm **node Google Sheets** sau **"Download Scraped Store Leads"** để ghi lại lịch sử scrape.
- **Cấu hình sheet**:
  - **Sheet Name**: `Scrape_Log`
  - **Columns**: `Date`, `Run ID`, `Total Leads`, `Status`

### **🔹 Gửi báo cáo định kỳ qua Email**
- Sử dụng **node Email** (Gmail/SMTP) kết hợp với **node Set** để gửi báo cáo hàng tuần.
- **Nội dung email**:
  ```json
  {
    "subject": "Báo cáo Lead Shopify - Tuần {{ $node["Set"].json["week"] }}",
    "text": "Tổng số lead scrape: {{ $node["Set"].json["totalLeads"] }}\nLead hợp lệ: {{ $node["Set"].json["validLeads"] }}"
  }
  ```

### **🔹 Tùy chỉnh filter lead**
- Trong **node "Filter Records with Emails"**, các sếp có thể thêm điều kiện lọc thêm:
  ```json
  {
    "condition": "json['email'].length > 0 && json['phone'].length > 0"
  }
  ```
  (Chỉ giữ lead có cả email **và** số điện thoại).

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc scrape và xác minh lead thủ công, đồng thời **nâng cao chất lượng lead** nhờ xác minh email và loại bỏ trùng lặp. **Kết quả?** Danh sách lead sạch sẽ, đẩy vào HubSpot tự động, và **tỷ lệ chuyển đổi tăng đáng kể**.

**Hành động ngay hôm nay:**
1. **Đăng ký VPS** để self-host n8n (để workflow chạy 24/7).
2. **Import workflow** và cấu hình API Key.
3. **Chạy test** và bắt đầu scrape lead!

👉 **[Tải workflow ngay](https://n8n.io/workflows/14032)** và bắt đầu tự động hóa lead generation của mình! 🚀