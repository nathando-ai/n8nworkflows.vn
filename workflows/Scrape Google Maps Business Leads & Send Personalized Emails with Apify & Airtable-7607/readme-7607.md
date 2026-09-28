---
title: "🚀 Tự Động Scrape Dữ Liệu Google Maps & Gửi Email Cá Nhân Hóa Cho Khách Hàng Tiềm Năng (Apify + Airtable)"
description: "Workflow tự động hóa scrape thông tin doanh nghiệp từ Google Maps, lưu trữ trên Airtable và gửi email cá nhân hóa đến khách hàng tiềm năng - tiết kiệm 10+ giờ công mỗi tuần cho bộ phận marketing & sales."
slug: "tieu-dong-scrape-google-maps-va-gui-email-canh-bao"
tags: [n8n, automation, lead-generation, apify, airtable, gmail, no-code]
keywords: [n8n workflow scrape google maps, tự động hóa lead generation, email marketing tự động, apify google maps, airtable automation, gửi email cá nhân hóa]
---

# 🚀 **Tự Động Scrape Dữ Liệu Google Maps & Gửi Email Cá Nhân Hóa Cho Khách Hàng Tiềm Năng**

## **Nỗi Đau Của Các Sếp**
Bộ phận marketing và sales của các sếp thường phải mất **giờ đồng hồ** để:
- Tìm kiếm và thu thập thông tin doanh nghiệp từ Google Maps thủ công.
- Lưu trữ dữ liệu rải rác trên Excel hoặc Google Sheets.
- Gửi email cá nhân hóa cho từng khách hàng tiềm năng, dễ bị bỏ qua hoặc sai thông tin.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Scrape tự động** thông tin doanh nghiệp từ Google Maps (địa chỉ, email, điện thoại, website, đánh giá...).
✅ **Lưu trữ sạch sẽ** trên Airtable với cấu trúc dữ liệu chuyên nghiệp.
✅ **Gửi email cá nhân hóa** đến từng khách hàng với nội dung động, tăng tỷ lệ mở và tương tác.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công/tuần** cho bộ phận marketing & sales.
- **Dữ liệu chính xác & cập nhật** từ Google Maps (không cần update thủ công).
- **Email cá nhân hóa** với tỷ lệ mở cao (tăng 30-50% so với email thông thường).
- **Lưu trữ trung tâm** trên Airtable, dễ dàng phân tích và theo dõi.
- **Hoạt động liên tục** (không phụ thuộc vào giờ làm việc của nhân viên).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scrape Google Maps):
   - [Đăng ký miễn phí tại Apify](https://apify.com/).
   - Chọn **actor**: [Google Maps Email Leads Fast Scraper](https://apify.com/actor/j66N0LgqJT3a7fSzu/input).
   - **API Token**: Tạo tại [Apify API Tokens](https://apify.com/actor/j66N0LgqJT3a7fSzu/tokens).

2. **Tài khoản Airtable**:
   - [Đăng ký miễn phí tại Airtable](https://airtable.com/).
   - **Personal Access Token**: Tạo tại [Airtable Tokens](https://airtable.com/create/tokens).
   - **Base & Table**: Tạo một **Base** mới (ví dụ: "Google Maps Scraping") và một **Table** (ví dụ: "Leads").

3. **Tài khoản Gmail**:
   - **OAuth 2.0 Credentials**: Cấu hình tại [Google Cloud Console](https://console.cloud.google.com/).
   - **Email nguồn** để gửi email cá nhân hóa (không phải email chính của công ty).

4. **n8n Workflow**:
   - **Self-hosted n8n** (không dùng phiên bản miễn phí trên cloud).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/7607](https://n8n.io/workflows/7607) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (tab "Import").

:::note[Lưu ý]
- **Không sử dụng phiên bản n8n cloud** (do giới hạn API và không hỗ trợ tự động hóa liên tục).
- **Không cần code** - workflow này hoàn toàn **no-code**.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: GO (Manual Trigger)**
- **Mục đích**: Khởi động workflow thủ công.
- **Lưu ý**:
  - Các sếp có thể **thay thế bằng Webhook** (để kích hoạt từ URL) hoặc **Cron** (để chạy tự động theo lịch).
  - Ví dụ: `https://domain.com/webhook/your-workflow-id` (cấu hình tại n8n Settings > Webhooks).

#### **🔹 Node 2: APIFY SCRAPE GOOGLE MAPS (HTTP Request)**
- **Mục đích**: Gửi yêu cầu scrape đến Apify.
- **Cách cấu hình**:
  1. **URL API**:
     - Mở [Google Maps Email Leads Fast Scraper](https://console.apify.com/actors/j66N0LgqJT3a7fSzu/input).
     - Click **API** (góc trên phải) → **API Endpoints**.
     - Chọn **Run Actor synchronously and get dataset items** (URL đã bao gồm **API Token** của bạn).
  2. **Body JSON (ví dụ)**:
     ```json
     {
       "area_height": 10,
       "area_width": 10,
       "emails_only": true,
       "gmaps_url": "https://www.google.com/maps/search/training+centers+near+Amiens/",
       "max_results": 200,
       "search_query": "training center"
     }
     ```
     - **Thay đổi**:
       - `search_query`: Từ khóa tìm kiếm (ví dụ: "café", "công ty IT", "trung tâm đào tạo").
       - `gmaps_url`: Khu vực muốn scrape (ví dụ: "Hà Nội", "Đà Nẵng").
       - `max_results`: Số lượng kết quả scrape (mặc định 200).

#### **🔹 Node 3: WAIT (10 giây)**
- **Mục đích**: Đợi Apify hoàn tất scrape.
- **Lưu ý**:
  - Thời gian chờ mặc định **10 giây** (điều chỉnh nếu scrape nhiều kết quả).

#### **🔹 Node 4: CLEAN DATA MAPPING (Set)**
- **Mục đích**: Chuyển đổi dữ liệu thô thành cấu trúc phù hợp với Airtable.
- **Cách cấu hình**:
  - **Assignments** (ví dụ):
    ```json
    {
      "Company": "{{ $json.name }}",
      "Email": "{{ $json.email }}",
      "Phone": "{{ $json.phone_number }}",
      "Website": "{{ $json.website_url }}",
      "LinkedIn": "{{ $json.linkedin }}",
      "Facebook": "{{ $json.facebook }}",
      "City": "{{ $json.city }}",
      "Category": "{{ $json.google_business_categories }}",
      "Google Maps Reviews": "{{ $json.reviews_number }} reviews, rating {{ $json.review_score }}/5",
      "Google Maps Link": "{{ $json.google_maps_url }}"
    }
    ```
  - **Lưu ý**:
    - Nếu dữ liệu từ Apify khác với ví dụ trên, **cần điều chỉnh key** theo cấu trúc thực tế.

#### **🔹 Node 5: AIRTABLE CREATE RECORD**
- **Mục đích**: Lưu dữ liệu vào Airtable.
- **Cách cấu hình**:
  1. **Credentials**:
     - Chọn **Airtable Personal Access Token** (đã tạo trước).
  2. **Base & Table**:
     - Chọn **Base ID** và **Table ID** từ URL Airtable (ví dụ: `appA6eMHOoquiTCeO` và `tblZFszM5ubwwSYDK`).
  3. **Field Mapping**:
     - Đối ứng với **Assignments** ở Node 4 (ví dụ: `Company` → `Company` trong Airtable).
     - **Mode**: Chọn **Map Each Column Manually**.

#### **🔹 Node 6: SEND EMAIL AUTOMATIC (Gmail)**
- **Mục đích**: Gửi email cá nhân hóa đến khách hàng tiềm năng.
- **Cách cấu hình**:
  1. **Credentials**:
     - Chọn **Gmail OAuth2** (đã cấu hình trước).
  2. **Tham số email**:
     - **To**: `{{ $json.fields.Email }}` (địa chỉ email của khách hàng).
     - **Subject**: `{{ $json.fields.Company }} - Cần giải pháp tự động hóa?` (tên công ty).
     - **Message (HTML)**:
       ```html
       <p>Xin chào {{ $json.fields.Company }}!</p>
       <p>Tôi là [Tên của bạn], chuyên hỗ trợ các doanh nghiệp tự động hóa quy trình.</p>
       <p>Tôi thấy {{ $json.fields.Company }} ở {{ $json.fields.City }} đang hoạt động với {{ $json.fields['Google Maps Reviews'] }}.</p>
       <p>Chúng tôi có thể giúp giảm thiểu công việc lặp lại như quản lý khách hàng, gửi email tự động, và tối ưu hóa quy trình?</p>
       <p>Hãy liên hệ với tôi qua <a href="tel:{{ $json.fields.Phone }}">điện thoại</a> hoặc <a href="https://{{ $json.fields.Website }}">website</a> của bạn.</p>
       <p>Chúng tôi sẵn sàng tổ chức một cuộc gọi 15 phút miễn phí để thảo luận!</p>
       <p>Trân trọng,<br>[Tên của bạn]</p>
       ```
  - **Lưu ý**:
    - **Không gửi email spam** (tuân thủ luật GDPR và chính sách Gmail).
    - **Test email** trước khi kích hoạt workflow.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và kiểm tra từng node.
   - Kiểm tra **Airtable** và **Gmail** để xác nhận dữ liệu.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram**
- **Node Slack/Telegram**: Gửi thông báo khi workflow hoàn tất.
- **Cách làm**:
  1. Thêm **Node Slack** (n8n-nodes-base.slack) sau Node 6.
  2. Cấu hình **Webhook URL** từ Slack (Settings > Custom Integrations > Incoming Webhooks).
  3. Nội dung thông báo:
     ```json
     {
       "text": "🚀 Workflow hoàn tất! Đã scrape {{ $json.length }} leads và gửi email.",
       "attachments": [
         {
           "title": "Danh sách leads mới",
           "fields": [
             { "title": "Tên công ty", "value": "{{ $json[0].fields.Company }}", "short": true }
           ]
         }
       ]
     }
     ```

### **🔹 Lưu Log & Báo Cáo Định Kỳ**
- **Node Set (Log)**:
  - Lưu dữ liệu scrape vào **Airtable Table mới** (ví dụ: "Workflow Logs").
  - **Cách làm**:
    ```json
    {
      "Workflow_ID": "{{ $node["GO"].json.nodeId }}",
      "Run_Time": "{{ $node["GO"].json.timestamp }}",
      "Leads_Scraped": "{{ $json.length }}",
      "Status": "Success"
    }
    ```
- **Node Airtable (Báo cáo)**:
  - Tạo **Báo cáo hàng tuần** với số lượng leads scrape và email gửi thành công.

### **🔹 Tăng Cường Personalization**
- **Thêm Node LLM (n8n-nodes-base.llm)**:
  - Sử dụng **AI generate email** động hơn (ví dụ: nội dung email tùy chỉnh theo ngành nghề).
  - **Cách làm**:
    1. Thêm **Node LLM** trước Node Gmail.
    2. Gửi **Prompt** như:
       ```json
       {
         "prompt": "Tạo email cá nhân hóa cho {{ $json.fields.Company }} trong ngành {{ $json.fields.Category }}. Nội dung phải ngắn gọn, chuyên nghiệp và đề xuất giải pháp tự động hóa. Địa chỉ email: {{ $json.fields.Email }}."
       }
       ```
    3. **Mapping** kết quả LLM vào **Subject** và **Message** của email.

### **🔹 Chạy Tự Động Theo Lịch (Cron)**
- **Node Cron**:
  - Thay thế **Manual Trigger** bằng **Cron** để chạy hàng ngày/tuần.
  - **Cách làm**:
    1. Thêm **Node Cron** (n8n-nodes-base.cron).
    2. Cấu hình **Schedule** (ví dụ: `0 9 * * *` - chạy lúc 9h sáng hàng ngày).
    3. **Set Output** để truyền dữ liệu vào Node APIFY.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và đội ngũ marketing/sales bằng cách:
✔ **Tự động scrape** thông tin doanh nghiệp từ Google Maps.
✔ **Lưu trữ sạch sẽ** trên Airtable với cấu trúc chuyên nghiệp.
✔ **Gửi email cá nhân hóa** tăng tỷ lệ tương tác.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một khu vực nhỏ** (ví dụ: 10 kết quả) trước khi chạy toàn bộ.
3. **Kết hợp với Slack/Telegram** để theo dõi kết quả thực thời.

**Nếu có vấn đề**, liên hệ tác giả:
📧 Baptiste Fort: [Baptiste.fort.pro@gmail.com](mailto:Baptiste.fort.pro@gmail.com)

---
**Chúc các sếp thành công với việc tự động hóa lead generation!** 🚀