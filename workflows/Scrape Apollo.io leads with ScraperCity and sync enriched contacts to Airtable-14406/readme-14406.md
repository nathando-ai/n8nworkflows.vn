---
title: "🚀 Tự Động Hóa Scrape Leads Apollo.io & Đồng Bộ Khách Hàng Tăng Cường Vào Airtable Với ScraperCity (Không Code)"
description: "Workflow tự động hóa scrape leads B2B từ Apollo.io qua ScraperCity, lọc bỏ trùng lặp, giữ lại email hợp lệ và đồng bộ hóa dữ liệu vào Airtable 24/7. Giúp các sếp tiết kiệm 10+ giờ/tháng và nâng cao chất lượng leads."
slug: "tieu-dong-hoa-scrape-apollo-io-va-dong-bo-airtable"
tags: [n8n, automation, lead-generation, scraping, airtable, scrapercity, api-integration]
keywords: [n8n workflow scrape leads, tự động hóa lead generation, đồng bộ airtable, scrape apollo.io, lead enrichment, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Scrape Leads Apollo.io & Đồng Bộ Khách Hàng Tăng Cường Vào Airtable (Không Code)**

### **Giải pháp cho các sếp bán hàng, marketing hoặc team sales:**
Bạn đã từng phải **tìm kiếm thủ công leads trên Apollo.io**, **lọc bỏ trùng lặp**, **kiểm tra email hợp lệ** và **ghi vào Airtable**? Quá trình này tiêu tốn **10+ giờ/tháng** và dễ gây sai sót. **Workflow này tự động hóa toàn bộ quy trình chỉ với một cú nhấp chuột!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ scrape nhanh)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** – Không cần scrape thủ công trên Apollo.io.
✅ **Dữ liệu leads sạch** – Bỏ trùng lặp, giữ lại email hợp lệ, chuẩn hóa dữ liệu.
✅ **Đồng bộ tự động** – Leads được push vào Airtable ngay khi scrape hoàn tất.
✅ **Hoạt động 24/7** – Không phụ thuộc vào thời gian làm việc của team.
✅ **Tăng chất lượng leads** – Lọc theo tiêu chí cụ thể (job title, ngành nghề, size company).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản ScraperCity** (để scrape Apollo.io) + **API Key** (mua gói phù hợp).
📌 **Tài khoản Airtable** + **API Key** (cấu hình trong n8n).
📌 **Table Airtable** đã có sẵn với các cột phù hợp (các sếp sẽ được hướng dẫn chi tiết sau).
📌 **Thông tin search parameters** (job titles, ngành nghề, size company, số lượng leads).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14406](https://n8n.io/workflows/14406) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import nhanh**:
  ```bash
  curl -o scrape_apollo_airtable.json "https://raw.githubusercontent.com/n8n-io/workflows/master/workflows/14406.json"
  ```
  Sau đó nhấn **Import** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình ScraperCity (API Key & Search Parameters)**
1. **Node "Start Apollo Lead Scrape" (HTTP Request)**
   - **Credentials**: Chọn `httpHeaderAuth` (đã tạo trước khi import).
   - **Headers**:
     - `Authorization: Bearer <API_KEY_SCRAPERCITY>`
     - `Content-Type: application/json`
   - **Body (JSON)**:
     ```json
     {
       "jobTitles": ["CEO", "CTO", "Founder"],  // Thay đổi theo nhu cầu
       "industries": ["Tech", "Finance"],      // Ngành nghề
       "companySize": "10-50",                 // Size company
       "leadCount": 500                        // Số lượng leads
     }
     ```

2. **Node "Configure Search Parameters" (Set)**
   - Điền các tham số search vào `json`:
     ```json
     {
       "jobTitles": ["CEO", "CTO"],
       "industries": ["Tech"],
       "companySize": "10-50",
       "leadCount": 500
     }
     ```

#### **B. Cấu hình Airtable (API Key & Table)**
1. **Node "Save Leads to Airtable" (Airtable)**
   - **Credentials**: Chọn `airtableTokenApi` (đã tạo trước khi import).
   - **Base ID**: Thay thế bằng `BASE_ID` của Airtable (tìm trong URL: `https://airtable.com/<BASE_ID>`).
   - **Table Name**: Tên table muốn đồng bộ (ví dụ: "Leads_Apollo").
   - **Fields**: Đảm bảo table có các cột phù hợp với output của **Parse and Normalize Leads** (ví dụ: `name`, `email`, `jobTitle`, `company`).

#### **C. Node "Parse and Normalize Leads" (Code)**
- **Mã JavaScript mặc định** đã chuẩn hóa dữ liệu, nhưng các sếp có thể **tùy chỉnh** để phù hợp với structure Airtable:
  ```javascript
  // Dữ liệu đầu vào từ ScraperCity
  const leads = $input.all();

  // Chuyển đổi thành format chuẩn
  const normalizedLeads = leads.map(lead => ({
    name: lead.name || "N/A",
    email: lead.email || "",
    jobTitle: lead.jobTitle || "N/A",
    company: lead.company || "N/A",
    phone: lead.phone || "",
    linkedin: lead.linkedin || ""
  }));

  return normalizedLeads;
  ```

#### **D. Node "Filter Contacts with Email" (Filter)**
- **Lọc giữ lại chỉ leads có email hợp lệ**:
  ```json
  {
    "jsonpath": "$[?(@.email && @.email != '')]"
  }
  ```

#### **E. Node "Remove Duplicate Contacts" (Remove Duplicates)**
- **Chọn key deduplicate**: Thường là `email` (để tránh trùng lặp).
  ```json
  {
    "key": "email"
  }
  ```

---

### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhấn **Execute workflow** và kiểm tra:
     - Scrape có hoàn tất không?
     - Dữ liệu có được đồng bộ vào Airtable không?
2. **Bật Active workflow** khi đã kiểm tra xong.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng tốc độ scrape**:
   - Giảm thời gian `Wait 60 Seconds` (ví dụ: 30s) nếu scrape nhanh.
   - Sử dụng **gói API ScraperCity cao cấp** để giảm thời gian chờ.

2. **Tăng chất lượng leads**:
   - Thêm **filter mới** trong node `Filter Contacts` (ví dụ: chỉ giữ leads có `phone` hoặc `linkedin`):
     ```json
     {
       "jsonpath": "$[?(@.email && @.email != '' && @.phone != '')]"
     }
     ```

3. **Lưu log & báo cáo**:
   - Thêm node **Slack/Telegram** để thông báo khi scrape hoàn tất:
     ```json
     {
       "text": "✅ Scrape Apollo.io hoàn tất! Đã đồng bộ {{ $jsonpath("$.length") }} leads vào Airtable."
     }
     ```

4. **Automate định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần:
     ```json
     {
       "cronTime": "0 0 * * *"  // Chạy hàng ngày lúc 00:00
     }
     ```

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp từ việc scrape leads thủ công, đồng thời **tăng chất lượng dữ liệu** với tính năng lọc trùng lặp và email hợp lệ. **Đồng bộ hóa tự động vào Airtable** giúp team sales **nhận leads sẵn sàng sử dụng** ngay lập tức.

🚀 **Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** với một batch nhỏ để đảm bảo hoạt động.
3. **Bật Active workflow** và **quên việc scrape thủ công**!

**Nếu có vấn đề**, các sếp có thể tham khảo [diễn đàn n8n](https://community.n8n.io/) hoặc liên hệ với **ScraperCity** để hỗ trợ API. **Chúc các sếp thành công!** 💪