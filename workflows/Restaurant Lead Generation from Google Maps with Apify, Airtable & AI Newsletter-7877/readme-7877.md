---
title: "🍽️ Tự Động Hóa Sinh Lập Lead Đa Chức Năng Từ Google Maps Với Apify, Airtable & AI Newsletter - Giảm 90% Thời Gian Tìm Kiếm Khách Hàng"
description: "Workflow này tự động thu thập, lọc và phân tích dữ liệu quán ăn từ Google Maps, tạo lead chất lượng cao trên Airtable, và tự động gửi newsletter cá nhân hóa qua Gmail - hoàn toàn không cần code. Giúp các sếp nhà hàng, nhà đầu tư hoặc chuyên gia marketing tiết kiệm hàng giờ mỗi tuần."
slug: "tieu-dong-hoa-lead-restaurant-googlemaps-apify-airtable-ai"
tags: [n8n, automation, lead-generation, multimodal-ai, airtable, apify, google-maps-scraping]
keywords: [n8n workflow lead, tự động hóa tìm kiếm khách hàng nhà hàng, apify google maps, airtable tự động hóa, newsletter tự động hóa, AI chatbot n8n]
---

# 🚀 **Tự Động Hóa Sinh Lập Lead Đa Chức Năng Từ Google Maps: Từ Scraping Đến Newsletter AI**

### **Nỗi Đau Của Các Sếp Nhà Hàng & Chuyên Gia Marketing**
Các sếp nhà hàng, nhà đầu tư hoặc chuyên gia marketing thường phải mất **hàng giờ mỗi tuần** để:
- **Tìm kiếm và lọc** quán ăn từ Google Maps theo tiêu chí cụ thể (đánh giá, số review, vị trí).
- **Tạo lead** và cập nhật vào Airtable (hoặc CRM khác) một cách thủ công.
- **Tự động hóa báo cáo** hoặc newsletter định kỳ để giữ liên lạc với khách hàng tiềm năng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Scraping tự động** dữ liệu quán ăn từ Google Maps (thông qua Apify).
✅ **Lọc & sắp xếp** theo đánh giá, số review, và thông tin quan trọng nhất.
✅ **Tạo lead chất lượng** trên Airtable (hoặc Airtable Base).
✅ **Tự động gửi newsletter cá nhân hóa** qua Gmail, dựa trên dữ liệu lead mới nhất.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Lead chính xác & cá nhân hóa**: Chỉ giữ lại quán ăn có đánh giá cao (>500 review).
- **Newsletter tự động**: AI tự động tổng hợp và gửi báo cáo định kỳ.
- **Hoạt động 24/7**: Không cần can thiệp người dùng, workflow chạy liên tục.
- **Dữ liệu sạch & sắp xếp**: Dữ liệu được lọc, sắp xếp và chuẩn hóa trước khi lưu.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch vụ               | Thông Tin Cần Thiết                          | Ghi Chú                                  |
|-----------------------|---------------------------------------------|-------------------------------------------|
| **Apify**             | API Key (trong `apifyApi`)                  | Đăng ký tại [Apify](https://apify.com/)  |
| **OpenAI (GPT-4.1)**  | API Key (trong `openAiApi`)                  | Đăng ký tại [OpenAI](https://openai.com/) |
| **Gmail**             | OAuth2 Credentials (trong `gmailOAuth2`)     | Cài đặt ứng dụng OAuth trong Gmail       |
| **Airtable**          | API Token (trong `airtableTokenApi`)        | Lấy từ [Airtable API](https://airtable.com/api) |

### **2. Cấu Hình Cần Chuẩn Bị**
- **Actor Apify**: Sử dụng [Actor "Google Maps Scraper"](https://apify.com/actor/Google-Maps-Scraper) (hoặc actor tương tự).
- **Airtable Base**: Tạo một **Base mới** để lưu lead (cấu trúc bảng sẽ được tự động tạo).
- **Gmail**: Địa chỉ email chính thức để gửi newsletter.

### **3. Hệ Thống**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7877](https://n8n.io/workflows/7877) (chọn "Export").
2. **Mở n8n Editor** và nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Xác nhận import** và workflow sẽ hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/7877](https://n8n.io/workflows/7877) (chọn "Export" → "Copy JSON").
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
3. **Xác nhận** và workflow sẽ được tạo.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **15 node** với các bước logic chính. Dưới đây là **các node quan trọng cần cấu hình kỹ**:

#### **🔹 Node 1: "Run an Actor" (Apify)**
- **Mục đích**: Chạy Actor Apify để scrap dữ liệu từ Google Maps.
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `apifyApi` (đã thêm API Key trước đó).
  - **Key Parameters**:
    - `actorId`: ID của Actor "Google Maps Scraper" (ví dụ: `apify/actor-google-maps-scraper`).
    - `datasetId`: ID của Dataset sẽ lưu kết quả (tạo mới trên Apify).
    - `input`: Tham số đầu vào cho Actor (ví dụ: `{"searchTerm": "quán phở Hà Nội", "maxItems": 100}`).

#### **🔹 Node 2: "Get dataset items" (Apify)**
- **Mục đích**: Lấy dữ liệu đã scrap từ Apify.
- **Cấu hình**:
  - **Credentials**: `apifyApi`.
  - **Key Parameters**:
    - `datasetId`: ID Dataset tương tự như trên.

#### **🔹 Node 3: "If" (Lọc dữ liệu)**
- **Mục đích**: Chỉ giữ lại item có `reviews > 0` và `rating > 3.5`.
- **Cấu hình**:
  - **Condition**: `{{ $json["reviews"] > 0 && $json["rating"] > 3.5 }}`.

#### **🔹 Node 4: "Sort by Review Count and Rating"**
- **Mục đích**: Sắp xếp lead theo số review (từ cao đến thấp) và rating.
- **Cấu hình**:
  - **Sort By**: `reviews` (giảm) → `rating` (giảm).

#### **🔹 Node 5: "OpenAI Chat Model" (GPT-4.1)**
- **Mục đích**: AI tự động tổng hợp lead để tạo newsletter.
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Prompt mẫu** (cần chỉnh sửa theo yêu cầu):
    ```json
    {
      "role": "user",
      "content": "Tóm tắt các lead mới nhất từ Google Maps (dữ liệu sau) thành một newsletter cá nhân hóa. Dữ liệu:
      {{ $json }}
      - Yêu cầu:
        1. Tóm tắt 3 lead top (có review > 500).
        2. Đưa ra 3 điểm mạnh của mỗi lead.
        3. Gợi ý cách tiếp cận khách hàng tiềm năng.
        4. Dùng giọng điệu chuyên nghiệp và thân thiện."
    }
    ```

#### **🔹 Node 6: "Lead Creator" (Airtable)**
- **Mục đích**: Tạo lead mới trên Airtable.
- **Cấu hình**:
  - **Credentials**: `airtableTokenApi`.
  - **Key Parameters**:
    - `baseId`: ID của Base Airtable (lấy từ URL: `https://airtable.com/<baseId>`).
    - `tableName`: Tên bảng (ví dụ: "Leads").
    - **Fields cần tạo**:
      ```json
      {
        "Name": "{{ $json["name"] }}",
        "Rating": "{{ $json["rating"] }}",
        "Reviews": "{{ $json["reviews"] }}",
        "Address": "{{ $json["address"] }}",
        "Phone": "{{ $json["phone"] || "N/A" }}",
        "Website": "{{ $json["website"] || "N/A" }}",
        "Description": "{{ $json["description"] }}"
      }
      ```

#### **🔹 Node 7: "Send a message" (Gmail)**
- **Mục đích**: Gửi newsletter tự động qua Gmail.
- **Cấu hình**:
  - **Credentials**: `gmailOAuth2`.
  - **Key Parameters**:
    - `to`: Email nhận (ví dụ: `marketing@congty.com`).
    - `subject`: "Newsletter Lead mới từ Google Maps - Ngày {{ $date.now('YYYY-MM-DD') }}".
    - **Body**: Nội dung từ AI (được truyền từ node OpenAI).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** và chọn **dữ liệu mẫu** (ví dụ: `{"searchTerm": "quán bánh mì Sài Gòn", "maxItems": 5}`).
   - Kiểm tra:
     - Dữ liệu có được scrap không?
     - Lead có được tạo trên Airtable không?
     - Email có được gửi không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack/Telegram để Báo Lỗi**
- Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi workflow gặp lỗi.
- **Cách làm**:
  - Thêm node `webhook` (Slack/Telegram) sau node `If` (lỗi Apify).
  - Gửi tin nhắn mẫu: `Workflow gặp lỗi khi scrap: {{ $error.message }}`.

### **2. Lưu Log Dữ Liệu**
- Sử dụng **node "Set"** để lưu log vào Airtable Base khác.
- **Cấu hình**:
  ```json
  {
    "Log": "{{ $json }}",
    "Timestamp": "{{ $date.now('YYYY-MM-DD HH:mm:ss') }}",
    "Status": "Success"
  }
  ```

### **3. Gửi Newsletter Định Kỳ (Hàng Tuần/Hàng Tháng)**
- Sử dụng **node "Schedule"** (n8n Premium) hoặc **Google Calendar Trigger** để kích hoạt workflow định kỳ.
- **Cách làm**:
  1. Thêm node `schedule` (n8n Premium) hoặc `formTrigger` (nếu dùng Google Calendar).
  2. Kết nối với node `Aggregate` để tổng hợp lead mới nhất.

### **4. Cải Tiến AI với Prompt Đa Ngôn Ngữ**
- Nếu làm việc với khách hàng quốc tế, chỉnh sửa prompt OpenAI để hỗ trợ nhiều ngôn ngữ:
  ```json
  {
    "role": "user",
    "content": "Tóm tắt lead này sang tiếng Anh và tiếng Việt. Dữ liệu: {{ $json }}"
  }
  ```

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp nhà hàng, nhà đầu tư và chuyên gia marketing bằng cách:
✔ **Tự động hóa scrap** dữ liệu từ Google Maps.
✔ **Lọc & sắp xếp** lead chất lượng cao.
✔ **Tạo lead trên Airtable** một cách tự động.
✔ **Gửi newsletter cá nhân hóa** qua Gmail.

**Hành động ngay hôm nay**:
1. **Chuẩn bị tài khoản** (Apify, OpenAI, Gmail, Airtable).
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test run** và bật Active để bắt đầu tự động hóa!

**Cần hỗ trợ?** Đăng ký **hỗ trợ chuyên nghiệp** từ [n8n Community](https://community.n8n.io/) hoặc liên hệ tác giả [Pramod Rathoure](https://n8n.io/workflows/7877) để tối ưu workflow theo nhu cầu cụ thể.

---
**#TựĐộngHóa #LeadGeneration #Apify #Airtable #AINewsletter**