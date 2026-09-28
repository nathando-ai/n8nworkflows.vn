---
title: "🚀 Tự Động Hóa Tìm Kiếm & Nhập Công Ty LinkedIn Vào Airtable CRM (Không Cần Code)"
description: "Workflow tự động hóa tìm kiếm công ty mục tiêu trên LinkedIn bằng Ghost Genius API và nhập dữ liệu vào Airtable CRM để xây dựng danh sách prospect chất lượng cao. Giúp các sếp tiết kiệm 100+ giờ tìm kiếm thủ công mỗi tháng."
slug: "tu-dong-hoa-tim-kiem-linkedin-vao-airtable"
tags: [n8n, automation, sales, marketing, airtable, linkedin, ghost-genius-api]
keywords: [n8n workflow linkedin, tự động hóa tìm kiếm công ty, airtable crm, ghost genius api, tìm prospect trên linkedin]
---

# 🚀 **Tự Động Hóa Tìm Kiếm & Nhập Công Ty LinkedIn Vào Airtable CRM**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã từng phải:
- **Tìm kiếm thủ công** hàng trăm công ty mục tiêu trên LinkedIn trong nhiều giờ?
- **Nhập liệu vào CRM** một cách mệt mỏi, dễ bị lỗi và mất thời gian?
- **Bị giới hạn API** khi request quá nhiều lần, dẫn đến mất dữ liệu?

Workflow này **tự động hóa toàn bộ quy trình** từ tìm kiếm công ty trên LinkedIn đến nhập dữ liệu vào Airtable CRM, giúp bạn **tiết kiệm 100+ giờ/tháng** và **xây dựng danh sách prospect chất lượng cao** một cách chính xác, không cần viết code.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tìm kiếm tự động** công ty theo keyword, ngành nghề, vị trí, quy mô (tối đa 1000 công ty/lần).
✅ **Lọc & xử lý dữ liệu** (số follower, trang web, mô tả) để chọn ra những prospect **chất lượng cao**.
✅ **Tránh trùng lặp** bằng cách kiểm tra trước khi nhập vào Airtable.
✅ **Nhập liệu tự động** vào CRM với thông tin chi tiết (tên, website, LinkedIn, mô tả, nhãn mác).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✅ **Tối ưu API** bằng cách chia batch và đặt thời gian chờ (2s/request) để tránh bị block.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Ghost Genius API** (để tìm kiếm công ty trên LinkedIn):
   - [Đăng ký miễn phí tại Ghost Genius](https://ghostgenius.fr/) và lấy **API Key**.
   - [Tìm hiểu API Documentation](https://ghostgenius.fr/docs).

2. **Tài khoản Airtable** (để lưu trữ CRM):
   - Tạo **base mới** tên **"CRM"** và thêm các cột bắt buộc:
     - `name` (text, mặc định)
     - `website` (URL)
     - `LinkedIn` (URL)
     - `id` (number, để tránh trùng lặp)
     - **Cột tùy chỉnh** (ví dụ: `tagline`, `description`, `category`).

3. **Credentials cho n8n**:
   - **Header Auth** (để kết nối với Ghost Genius API):
     - **Tên**: `Authorization`
     - **Giá trị**: `Bearer <API_KEY_CỦA_BẠN>` (thay `<API_KEY_CỦA_BẠN>` bằng key thực tế).
   - **Airtable Token API** (để nhập dữ liệu):
     - Tạo từ [Airtable API Documentation](https://airtable.com/api).

4. **Dữ liệu tìm kiếm**:
   - Các tiêu chí như **ngành nghề**, **kích thước công ty**, **vị trí**, **keyword** sẽ được đặt trong node **"Set Variables"**.
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/3717](https://n8n.io/workflows/3717) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (tab **"Import"**).

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **10 node chính**, các sếp cần chú ý cấu hình như sau:

#### **🔹 Node "Search Companies" (Tìm Kiếm Công Ty)**
- **Tham số quan trọng**:
  - **URL**: `https://api.ghostgenius.fr/v1/companies/search`
  - **Headers**:
    - `Authorization: Bearer <API_KEY>`
    - `Content-Type: application/json`
  - **Body (JSON)**:
    ```json
    {
      "query": "Growth Marketing Agency",
      "page": 1,
      "per_page": 100,
      "filters": {
        "size": "11-50",
        "location": "US",
        "has_job_postings": true
      }
    }
    ```
  - **Lưu ý**:
    - Thay đổi `query`, `size`, `location` theo tiêu chí của bạn.
    - **Không vượt quá 1000 công ty/lần** (tương đương 100 trang LinkedIn).
    - Để **test kết quả**, thay đổi `page` trong **Set Variables** (node sau).

#### **🔹 Node "Get Company Info" (Lấy Thông Tin Chi Tiết)**
- **Tham số quan trọng**:
  - **URL**: `https://api.ghostgenius.fr/v1/companies/{company_id}`
  - **Headers**: Giống như node trước (`Authorization`).
  - **Dynamic Value**:
    - Thay `{company_id}` bằng `$node["Search Companies"].json[].id` (từ kết quả tìm kiếm).

#### **🔹 Node "Filter Valid Companies" (Lọc Công Ty Chất Lượng)**
- **Điều kiện lọc**:
  - **Số follower ≥ 200** (để đảm bảo uy tín).
  - **Có website** (trang web công ty được liệt kê).
  - **Customize**: Các sếp có thể điều chỉnh số lượng follower hoặc thêm điều kiện khác.

#### **🔹 Node "Check If Company Exists" (Kiểm Tra Trùng Lặp)**
- **Tham số Airtable**:
  - **Operation**: `search`
  - **Filter**: `id = $node["Get Company Info"].json.id` (tránh nhập trùng).
  - **Lưu ý**: Nếu công ty đã tồn tại, workflow sẽ **bỏ qua** và không nhập lại.

#### **🔹 Node "Add Company to CRM" (Nhập Vào Airtable)**
- **Tham số Airtable**:
  - **Operation**: `create`
  - **Fields** (các trường cần nhập):
    ```json
    {
      "name": $node["Get Company Info"].json.name,
      "website": $node["Get Company Info"].json.website,
      "LinkedIn": $node["Get Company Info"].json.url,
      "id": $node["Get Company Info"].json.id,
      "tagline": $node["Get Company Info"].json.tagline,
      "description": $node["Get Company Info"].json.description,
      "category": "Growth Marketing Agency 11-50 🌍",
      "country": "🇺𸇸 United States"  // Thay đổi theo nhu cầu
    }
    ```
  - **Lưu ý**: Các sếp có thể **tùy chỉnh nhãn mác (`category`)** và **quốc gia (`country`)**.

#### **🔹 Node "Set Variables" (Đặt Tiêu Chí Tìm Kiếm)**
- **Các biến cần thiết**:
  - `search_query`: "Growth Marketing Agency" (keyword tìm kiếm).
  - `company_size`: "11-50" (kích thước công ty).
  - `location`: "US" (vị trí).
  - `max_pages`: 10 (số trang để test, sau đó tăng lên 1000).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Click **"Test workflow"** để chạy với dữ liệu mẫu.
   - Kiểm tra **Airtable** xem có nhập dữ liệu không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
🔹 **Tìm kiếm theo quốc gia**:
   - Sử dụng **Ghost Genius Locations ID Finder** để lấy mã quốc gia chính xác: [Tìm mã quốc gia](https://ghostgenius.fr/tools/search-sales-navigator-locations-id).
   - Ví dụ: `location: "VN"` (Việt Nam) thay vì `US`.

🔹 **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để nhận thông báo khi workflow hoàn thành hoặc lỗi.
   - Ví dụ: Gửi tin nhắn `"Đã tìm kiếm x công ty mới vào CRM!"`.

🔹 **Gửi báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Email** để tự động gửi báo cáo số lượng công ty mới được nhập mỗi tháng.

🔹 **Tối ưu API**:
   - Nếu bị giới hạn rate, giảm `delay` trong node **splitInBatches** từ 2s xuống 1s (nhưng không quá thấp để tránh bị block).

🔹 **Xử lý lỗi**:
   - Thêm node **Error Handling** (ví dụ: nếu API trả về lỗi, gửi email cảnh báo).
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc tìm kiếm và nhập liệu thủ công, đồng thời **xây dựng danh sách prospect chất lượng cao** một cách tự động. **Chỉ cần 5 phút setup**, bạn đã có một **CRM được tự động hóa 100%**!

👉 **Bắt đầu ngay**:
1. **Import workflow** từ [n8n.io/workflows/3717](https://n8n.io/workflows/3717).
2. **Cấu hình API Key** và **Airtable**.
3. **Test và bật workflow** để bắt đầu tìm kiếm!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cần hỗ trợ?** Liên hệ tác giả Matthieu qua [LinkedIn](https://www.linkedin.com/in/matthieu-belin83/)!