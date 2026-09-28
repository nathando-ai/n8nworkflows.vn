---
title: "🚀 Tự Động Hoá Tìm Kiếm Lead Kinh Doanh Từ Google Maps & Trích Xuất Thông Tin Quản Lý - Olostep + n8n"
description: "Workflow này tự động scrape thông tin doanh nghiệp từ Google Maps (tên, địa chỉ, website, số điện thoại) và trích xuất thông tin quản lý (CEO/Founder) từ trang web doanh nghiệp, sau đó lưu vào Google Sheets. Giúp các sếp tiết kiệm 10-15 giờ/tháng trong việc tìm kiếm lead thủ công."
slug: "tieu-dong-hoa-tim-kiem-lead-google-maps-olostep-n8n"
tags: [n8n, automation, lead-generation, google-maps-scraping, olostep, google-sheets, no-code]
keywords: [tự động hóa tìm kiếm lead, scrape google maps, trích xuất thông tin CEO, n8n workflow lead generation, olostep api, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hoá Tìm Kiếm Lead Kinh Doanh Từ Google Maps & Trích Xuất Thông Tin Quản Lý**

## **Nỗi Đau Của Các Sếp Trong Tìm Kiếm Lead**
Bạn có bao giờ phải:
- **Tốn thời gian** tìm kiếm doanh nghiệp phù hợp trên Google Maps?
- **Lặp lại công việc** nhập liệu thông tin từ website vào CRM?
- **Không biết** ai là người quyết định (CEO/Founder) để liên hệ?
- **Thiếu dữ liệu chi tiết** để xây dựng chiến dịch bán hàng hiệu quả?

Workflow này **giải quyết tất cả** bằng cách tự động scrape thông tin doanh nghiệp từ Google Maps, trích xuất thông tin quản lý từ website, và lưu vào Google Sheets – **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn uy tín với ưu đãi đặc biệt:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
✅ **Dữ liệu chính xác & cập nhật** từ Google Maps và website doanh nghiệp.
✅ **Trích xuất thông tin quản lý** (CEO/Founder) tự động.
✅ **Lưu vào Google Sheets** để dễ dàng quản lý và xuất khẩu sang CRM (HubSpot, Salesforce...).
✅ **Hoạt động liên tục** 24/7, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Olostep** (để scrape Google Maps và website):
   - [Đăng ký Olostep](https://olostep.com/) (miễn phí cho 1000 request/tháng).
   - **API Key** của Olostep (tìm trong Dashboard).
2. **Google Sheets** để lưu kết quả:
   - Tạo một **Google Sheet mới** và chia sẻ với n8n (quyền chỉnh sửa).
   - **Sheet Name** phải được đặt trong node `Append row in sheet`.
3. **Form (tùy chọn)** để người dùng nhập:
   - **Thành phố** (ví dụ: "Hà Nội").
   - **Loại doanh nghiệp** (ví dụ: "Công ty tư vấn marketing").

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/11086](https://n8n.io/workflows/11086) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **10 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Form Trigger (n8n-nodes-base.formTrigger)**
- **Cấu hình**:
  - Thêm **2 trường**:
    - `City` (Text).
    - `Business Type` (Text).
  - **Example**:
    - City: "Hà Nội"
    - Business Type: "Công ty tư vấn SEO"

##### **🔹 Node 2 & 7: HTTP Request (n8n-nodes-base.httpRequest) - Scrape Google Maps & Website**
- **Cấu hình chung**:
  - **Method**: `POST`.
  - **URL**:
    - **Scrape Google Maps**: `https://api.olostep.com/v1/google_maps/search`
    - **Scrape Website**: `https://api.olostep.com/v1/website/scrape`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_OLOSTEP_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (Request Payload)**:
    - **Scrape Google Maps**:
      ```json
      {
        "query": "{{ $node["On form submission"].json["City"] }} {{ $node["On form submission"].json["Business Type"] }}",
        "limit": 50
      }
      ```
    - **Scrape Website**:
      ```json
      {
        "url": "{{ $json["website"] }}",
        "extract": {
          "name": "CEO/Founder",
          "email": "Contact Email"
        }
      }
      ```

##### **🔹 Node 4: Remove Duplicates (n8n-nodes-base.removeDuplicates)**
- **Cấu hình**:
  - Chọn **field** để kiểm tra trùng lặp: `Business Name`.

##### **🔹 Node 5: Split In Batches (n8n-nodes-base.splitInBatches)**
- **Cấu hình**:
  - **Batch Size**: `1` (để scrape từng website một).
  - **Delay Between Batches**: `5000` (5 giây) để tránh bị chặn rate limit.

##### **🔹 Node 8: Google Sheets (n8n-nodes-base.googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google đã kết nối.
  - **Sheet Name**: Đặt tên sheet (ví dụ: "Leads_GoogleMaps").
  - **Range**: `A1` (để append dữ liệu từ hàng A).
  - **Headers**: Chọn các field cần lưu:
    ```
    Business Name, Location, Website, Phone Number, Decision-Maker Name, Contact Email
    ```

##### **🔹 Node 9: Wait (n8n-nodes-base.wait)**
- **Cấu hình**:
  - **Time**: `5000` (5 giây) để tránh bị rate limit khi scrape nhiều website.

##### **🔹 Node 3 & 6: Set (n8n-nodes-base.set)**
- **Cấu hình**:
  - Đảm bảo **field names** trong `parsedInfo` và `name` phù hợp với Google Sheets.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập `City = "Hà Nội"` và `Business Type = "Công ty tư vấn marketing"` vào form.
   - Chạy workflow và kiểm tra Google Sheets.
2. **Bật Active** khi đã kiểm tra xong.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** để thông báo khi có lead mới.
   - **Cách làm**:
     - Sau node `Append row in sheet`, thêm node **Slack** với message:
       ```json
       {
         "text": "🚀 Lead mới từ {{ $json["Business Name"] }} (CEO: {{ $json["Decision-Maker Name"] }})",
         "attachments": [
           {
             "title": "Thông tin chi tiết",
             "fields": [
               { "title": "Website", "value": "{{ $json["Website"] }}", "short": true },
               { "title": "Địa chỉ", "value": "{{ $json["Location"] }}", "short": true },
               { "title": "Email", "value": "{{ $json["Contact Email"] }}", "short": true }
             ]
           }
         ]
       }
       ```

2. **Lưu Log & Báo Cáo Định Kỳ**:
   - Thêm node **Google Drive** để lưu log scrape.
   - Sử dụng **n8n-nodes-base.if** để kiểm tra lỗi và gửi báo cáo lỗi qua email.

3. **Tối Ưu Hóa Rate Limit**:
   - Nếu bị **504 Gateway Timeout**, giảm `Batch Size` xuống `1` và tăng `Delay Between Batches` lên `10000` (10 giây).

4. **Trích Xuất Thông Tin CEO Tự Động**:
   - Nếu Olostep không trích xuất được email, các sếp có thể thêm **LLM Node** (n8n-nodes-ai.llm) để phân tích website và trích xuất thông tin:
     ```json
     {
       "prompt": "Trích xuất email của CEO/Founder từ trang web sau: {{ $json["Website"] }}",
       "model": "gpt-3.5-turbo"
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược bán hàng thay vì tìm kiếm lead thủ công. Bằng cách kết hợp **Google Maps Scraping + Website Scraping + Google Sheets**, các sếp sẽ có được **danh sách lead giàu thông tin**, sẵn sàng để xuất khẩu vào CRM hoặc sử dụng trong chiến dịch marketing.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa lead generation của mình!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/11086)**
**📌 Cần hỗ trợ? Đăng ký tư vấn miễn phí tại [n8n.io](https://n8n.io/)**