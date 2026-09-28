---
title: "🚀 Tự Động Hóa Trích Xuất Dữ Liệu Lead Tiềm Năng Từ Google Maps & LinkedIn Sang Supabase (Không Cần Code)"
description: "Workflow tự động hóa trích xuất thông tin lead từ Google Maps và LinkedIn theo tiêu chí cụ thể, sau đó lưu trữ sạch sẽ vào cơ sở dữ liệu Supabase - giải pháp hoàn hảo cho đội ngũ bán hàng, tuyển dụng và marketing."
slug: "tieu-chuyen-lead-googlemaps-linkedin-supabase"
tags: [n8n, automation, lead-generation, apify, supabase, no-code, sales-automation]
keywords: [tự động hóa lead generation, trích xuất dữ liệu Google Maps, LinkedIn automation, lưu trữ Supabase, workflow n8n, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Trích Xuất Lead Tiềm Năng Từ Google Maps & LinkedIn Sang Supabase**

### **Giải Pháp Cho Các Sếp Bán Hàng, Tuyển Dụng & Marketing**
Hiện nay, việc tìm kiếm và thu thập lead tiềm năng thủ công là một công việc **tốn thời gian, dễ sai sót và khó mở rộng**. Các sếp phải mất hàng giờ để tra cứu thông tin trên Google Maps, LinkedIn, sau đó nhập liệu vào hệ thống - trong khi đó, **các lead quan trọng có thể bị bỏ lỡ** hoặc dữ liệu bị sai sót.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Trích xuất lead** từ Google Maps và LinkedIn theo tiêu chí cụ thể (ngành nghề, vị trí, địa điểm).
✅ **Lọc và sắp xếp dữ liệu** một cách chính xác, sạch sẽ.
✅ **Lưu trữ vào Supabase** (cơ sở dữ liệu cloud hiện đại) để dễ dàng truy xuất và phân tích.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 5-10 giờ/ngày để tra cứu thủ công, workflow này hoàn thành trong **vài phút**.
- **Dữ liệu chính xác**: Tránh sai sót khi nhập liệu, dữ liệu được tự động định dạng và lưu trữ.
- **Tối ưu hóa quy trình bán hàng**: Có thể **lọc lead theo tiêu chí cụ thể** (ngành nghề, vị trí, địa điểm) và **tích hợp với CRM** (như HubSpot, Salesforce) sau này.
- **Hoạt động liên tục**: Chạy tự động mỗi khi có yêu cầu mới, không phụ thuộc vào giờ làm việc.
- **Dễ dàng phân tích**: Dữ liệu được lưu trong **Supabase** (có thể kết nối với Tableau, Power BI, hoặc các công cụ BI khác).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản Supabase** (để lưu trữ dữ liệu):
   - **Supabase URL** và **Supabase Key** (tạo từ [supabase.com](https://supabase.com/)).
   - **Hai bảng dữ liệu** đã được tạo sẵn:
     - `googlemaps` (để lưu thông tin từ Google Maps).
     - `linkedin` (để lưu thông tin từ LinkedIn).
   - **Cấu trúc bảng** (gợi ý):
     | Cột (Google Maps)       | Loại Dữ liệu | Cột (LinkedIn)          | Loại Dữ liệu       |
     |-------------------------|--------------|-------------------------|--------------------|
     | id                      | UUID         | id                      | UUID               |
     | name                    | Text         | firstName               | Text               |
     | address                 | Text         | lastName                | Text               |
     | phone                   | Text         | email                   | Text               |
     | website                 | Text         | headline                | Text               |
     | latitude                | Float        | experience              | Text               |
     | longitude               | Float        | skills                  | Array (JSON)       |
     | ...                     | ...          | connectionCount         | Integer            |

✔ **Tài khoản Apify** (để trích xuất dữ liệu):
   - **Apify OAuth2 API Key** (mã API từ [apify.com](https://apify.com/)).
   - **Quota đủ** (miễn phí có giới hạn, nếu cần nâng cấp, xem [đây](https://apify.com/docs/api/pricing)).

✔ **VPS cho n8n** (để workflow chạy 24/7):
   - **Khuyến nghị**: Cài n8n trên **VPS** (self-hosted) để đảm bảo tính liên tục.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow đã được chia sẻ trên [n8n.io](https://n8n.io/workflows/8417). Các sếp có thể:
- **Tải file JSON** và import vào n8n Editor.
- **Copy JSON** từ trang workflow và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không cần chỉnh sửa toàn bộ workflow** nếu đã có tất cả credentials (API Key, Supabase URL).
- **Nếu muốn test trước**, các sếp có thể **chạy thử với số lượng lead nhỏ** (ví dụ: 5-10 lead) để kiểm tra kết quả.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Workflow sử dụng **hai loại credentials chính**:
1. **Supabase API**:
   - **Tên credentials**: `supabaseApi`
   - **Cấu hình**:
     - **URL**: `https://<Tên_Dự_Anh_Supabase>.supabase.co`
     - **Key**: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...` (tạo từ **Project Settings > API** trong Supabase).
     - **Database**: Chọn **Project Database** (không cần đổi).

2. **Apify OAuth2 API**:
   - **Tên credentials**: `apifyOAuth2Api`
   - **Cấu hình**:
     - **Token**: `apify_oauth_token_<Your_Token>` (tạo từ [Apify Dashboard](https://apify.com/dashboard/tokens)).

#### **B. Cấu Hình Form Trigger**
Node **"Input desired lead"** (Form Trigger) cần được cấu hình để nhận **4 thông tin bắt buộc**:
- **Title/Industry** (ví dụ: "CEO", "Marketing Director").
- **Location** (ví dụ: "Hà Nội", "TP.HCM").
- **Source** (Google Maps, LinkedIn, hoặc Both).
- **Number of results** (số lượng lead muốn lấy, **không bắt buộc**).

:::tip[Mẹo]
- Các sếp có thể **tạo một form mẫu** trong Slack/Telegram để người dùng submit yêu cầu.
- Ví dụ:
  ```
  /lead_request CEO Hà Nội Google Maps 10
  ```
  (Định dạng: `Title Location Source [Number]`).
:::

#### **C. Cấu Hình Supabase Tables**
Workflow sẽ **tự động tạo hai bảng** (`googlemaps` và `linkedin`) nếu chưa có. Tuy nhiên, để **tránh lỗi**, các sếp nên:
1. **Tạo sẵn hai bảng** trong Supabase với cấu trúc như trên.
2. **Kiểm tra quyền truy cập**:
   - Bảng phải có **các cột phù hợp** với dữ liệu trích xuất.
   - **Không cần quyền admin**, chỉ cần quyền **Data Editor**.

#### **D. Cấu Hình Apify Actors**
Workflow sử dụng **hai actor Apify**:
1. **Google Maps Scraper**:
   - **Actor ID**: `apify/google-maps-scraper` (hoặc tương tự, tùy chỉnh theo phiên bản mới nhất).
   - **Input Parameters**:
     - `searchQuery`: `{ "title": $json["Title/Industry"], "location": $json["Location"] }`.
     - `maxItems`: `$json["Number of results"]` (nếu có).

2. **LinkedIn Scraper**:
   - **Actor ID**: `apify/linkedin-scraper` (hoặc phiên bản mới nhất).
   - **Input Parameters**:
     - `searchQuery`: `{ "keywords": $json["Title/Industry"], "location": $json["Location"] }`.
     - `maxItems`: `$json["Number of results"]`.

:::warning[LƯU Ý QUAN TRỌNG]
- **Apify có giới hạn free tier** (500 MB storage, 1000 MB bandwidth/tháng).
- Nếu workflow **vượt quá giới hạn**, các sếp cần **nâng cấp plan** hoặc **lọc lead trước khi lưu**.
- **Không nên chạy đồng thời nhiều workflow** để tránh bị block.
:::

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Điền **một yêu cầu mẫu** vào Form Trigger (ví dụ: "CEO", "Hà Nội", "Google Maps", "5").
   - **Chạy workflow** và kiểm tra:
     - Dữ liệu có được trích xuất không?
     - Dữ liệu có được lưu vào Supabase không?
     - Có lỗi nào xuất hiện không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.
   - **Kiểm tra log** trong n8n để đảm bảo không có lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Với Slack/Telegram**
Các sếp có thể **gửi thông báo kết quả** qua Slack/Telegram khi workflow hoàn thành:
- Sử dụng **node `n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`**.
- **Ví dụ**:
  ```
  "Message": "🚀 Lead generation completed! Found {{ $json["Number of results"] }} leads from {{ $json["Source"] }} in {{ $json["Location"] }}."
  ```

### **2. Lưu Log & Báo Cáo Định Kỳ**
- **Lưu log** vào một bảng `logs` trong Supabase để theo dõi lịch sử.
- **Gửi báo cáo hàng tuần** qua email (sử dụng **node `n8n-nodes-email`**).
- **Ví dụ**:
  ```
  SELECT COUNT(*) FROM googlemaps WHERE created_at > NOW() - INTERVAL '7 days';
  ```

### **3. Lọc Lead Trước Khi Lưu**
- Sử dụng **node `n8n-nodes-base.set`** để **lọc lead** theo tiêu chí (ví dụ: chỉ lưu lead có email).
- **Ví dụ**:
  ```json
  {
    "jsonpath": "$[?(@.email != null)]"
  }
  ```

### **4. Kết Nối Với CRM**
- Sau khi dữ liệu ở Supabase, các sếp có thể **kết nối với HubSpot/Salesforce** để tự động tạo lead trong CRM.
- **Sử dụng node `n8n-nodes-hubspot`** hoặc **`n8n-nodes-salesforce`**.

### **5. Tối Ưu Hóa Apify Actor**
- Nếu **Apify free tier không đủ**, các sếp có thể:
  - **Chạy workflow vào giờ thấp điểm** (đêm).
  - **Sử dụng actor paid** (nếu cần dữ liệu lớn).

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc tìm kiếm lead tiềm năng, đồng thời **tăng cường hiệu quả bán hàng, tuyển dụng và marketing** bằng cách tự động hóa quy trình trích xuất và lưu trữ dữ liệu.

**Hành động ngay hôm nay:**
1. **Chuẩn bị credentials** (Supabase + Apify).
2. **Import workflow** và cấu hình.
3. **Test với số lượng nhỏ** trước khi chạy toàn bộ.
4. **Bật Active** và **theo dõi log** để đảm bảo hoạt động ổn định.

**🚀 CÓ THỂ TĂNG CƯỜNG HƯỚNG DẪN NÀY THÊM:**
- **Tạo một video demo** cho team.
- **Tích hợp với Zapier** để mở rộng khả năng tự động hóa.
- **Sử dụng AI (n8n + LLM)** để phân tích lead trước khi lưu.

**Chúc các sếp thành công với việc tự động hóa lead generation!** 💼🚀