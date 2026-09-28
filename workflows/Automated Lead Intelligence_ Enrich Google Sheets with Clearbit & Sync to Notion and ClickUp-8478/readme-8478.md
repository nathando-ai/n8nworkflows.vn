---
title: "🚀 Tự Động Hóa Thông Tin Lead Tối Tiến: Tăng Cường Dữ Liệu Google Sheets Với Clearbit & Đồng Bộ Notion & ClickUp"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tự động tra cứu thông tin công ty từ email, enrich dữ liệu lead, đồng bộ tự động lên Notion và ClickUp - tiết kiệm 80% thời gian nghiên cứu lead thủ công."
slug: "tieu-dong-hoa-thong-tin-lead-clearbit-notion-clickup"
tags: [n8n, automation, lead-generation, google-sheets, notion, clickup, clearbit]
keywords: [n8n workflow lead generation, tự động hóa thông tin công ty, enrich lead với clearbit, đồng bộ google sheets notion clickup, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Thông Tin Lead Tối Tiến: Enrich Dữ Liệu Với Clearbit & Đồng Bộ Notion & ClickUp**

### **💡 Giải quyết vấn đề gì?**
Các sếp bán hàng hay marketing đã từng phải **tìm kiếm thông tin công ty** của lead từ email (domain, logo, ngành nghề, CEO, revenue) bằng cách:
- **Tra cứu thủ công** trên Google, LinkedIn, Clearbit...
- **Ghi chép vào nhiều tab** khác nhau (Excel, Notion, CRM)
- **Đồng bộ dữ liệu** giữa Google Sheets, Notion và ClickUp **một cách rắc rối**

**Kết quả?** Thời gian nghiên cứu lead **tăng gấp 5 lần**, dữ liệu **không đồng bộ**, và **chỉ 20% thời gian** dành cho việc thực sự bán hàng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Trích xuất domain từ email** và tra cứu thông tin công ty chi tiết từ **Clearbit**
✅ **Tự động enrich dữ liệu** (logo, ngành nghề, revenue, CEO, vị trí công ty)
✅ **Cập nhật tự động lên Google Sheets** (dữ liệu sạch, không trùng lặp)
✅ **Tạo task trong ClickUp** và **đăng bài vào Notion** (đồng bộ hoàn hảo)
✅ **Lọc lead chưa được book** để ưu tiên theo dõi

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** nghiên cứu lead (từ 2 tiếng/tháng xuống còn 30 phút).
- **Dữ liệu lead chính xác 100%**, không sai sót như tra cứu thủ công.
- **Đồng bộ tự động** giữa Google Sheets, Notion và ClickUp (không cần copy-paste).
- **Tạo task tự động** trong ClickUp khi lead mới được enrich.
- **Lọc lead chưa được book** để ưu tiên gọi điện/email.
- **Logo công ty tự động** xuất hiện trong Notion và ClickUp (ấn tượng với khách hàng).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Clearbit** (API Key) → [Đăng ký miễn phí](https://clearbit.com/)
✔ **Google Sheets** với:
   - Sheet **Enriched Leads** (cấu trúc có cột: `Email`, `Domain`, `Company Name`, `Logo URL`, `Industry`, `Revenue`, `CEO`, `Job Title`, `Status`)
   - Sheet **Sheet1** (để lưu dữ liệu gốc)
✔ **Tài khoản Notion** (API Key hoặc Integration)
✔ **Tài khoản ClickUp** (API Token)
✔ **Tài khoản n8n** (self-hosted hoặc n8n.cloud)

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/8478) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8478).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **11 node**, các sếp cần **cấu hình kỹ lưỡng** các node sau:

##### **🔹 Node 1: "When clicking ‘Execute workflow’" (ManualTrigger)**
- **Lưu ý:** Node này **không cần cấu hình gì**, chỉ dùng để **bắt đầu workflow thủ công** khi cần.

##### **🔹 Node 2: "Extract Domain from Email" (Function)**
- **Input:** Email của lead (ví dụ: `leads@example.com`).
- **Output:** Trích xuất domain (`example.com`).
- **Lưu ý:** Node này **sử dụng code JavaScript** để trích xuất domain tự động.

##### **🔹 Node 3: "Clearbit Company Enrichment" (HTTP Request)**
- **API Endpoint:** `https://company.clearbit.com/v2/companies/enrich?domain={domain}`
- **Headers:**
  - `Authorization: Bearer {CLEARBIT_API_KEY}`
  - `Content-Type: application/json`
- **Lưu ý:**
  - Thay `{CLEARBIT_API_KEY}` bằng **API Key** của Clearbit.
  - Nếu API trả về lỗi, kiểm tra **domain** có đúng định dạng không (ví dụ: `example.com` chứ không phải `www.example.com`).

##### **🔹 Node 4: "Get Company Logo" (HTTP Request)**
- **API Endpoint:** `https://logo.clearbit.com/{domain}.png`
- **Headers:** Không cần (GET request).
- **Lưu ý:**
  - Nếu logo không tồn tại, Clearbit trả về **404**, workflow sẽ **bỏ qua** và sử dụng logo mặc định.
  - **URL logo** sẽ được lưu vào Google Sheets và Notion.

##### **🔹 Node 5: "Merge Enrichment Data" (Function)**
- **Input:** Dữ liệu từ Clearbit (công ty, ngành nghề, revenue, CEO, vị trí).
- **Output:** **Kết hợp dữ liệu** thành 1 object duy nhất.
- **Lưu ý:** Node này **không cần chỉnh sửa**, chỉ cần **đảm bảo dữ liệu input đầy đủ**.

##### **🔹 Node 6: "Append to Enriched Leads Sheet" (Google Sheets)**
- **Sheet Name:** `Enriched Leads` (phải **trùng với tên sheet** trong Google Sheets).
- **Range:** `A2` (để dữ liệu mới được append vào dòng mới).
- **Headers:** `Email, Domain, Company Name, Logo URL, Industry, Revenue, CEO, Job Title, Status`.
- **Lưu ý:**
  - **Kiểm tra quyền truy cập** của n8n vào Google Sheets (cần **quyền chỉnh sửa**).
  - Nếu sheet không tồn tại, **tạo sheet mới** với cấu trúc trên.

##### **🔹 Node 7: "Check If Unbooked" (If)**
- **Condition:** Kiểm tra cột `Status` trong Google Sheets.
  - Nếu `Status = "Unbooked"`, workflow tiếp tục.
  - Nếu `Status = "Booked"`, workflow **dừng lại**.
- **Lưu ý:** Nếu cột `Status` chưa có dữ liệu, **cần thêm logic** (có thể sử dụng node **Function** để mặc định `Unbooked`).

##### **🔹 Node 8: "Get row(s) in sheet1" (Google Sheets)**
- **Sheet Name:** `Sheet1` (sheet lưu dữ liệu gốc).
- **Range:** `A2:I` (lấy toàn bộ hàng chứa email).
- **Lưu ý:** Nếu sheet này không tồn tại, **tạo sheet mới** và **điền dữ liệu mẫu** (ví dụ: `Email, Domain, Company Name, ...`).

##### **🔹 Node 9: "Merge" (Merge)**
- **Input:** Dữ liệu từ `Enriched Leads` và `Sheet1`.
- **Output:** **Kết hợp 2 dataset** thành 1.
- **Lưu ý:** Node này **tự động merge** dựa trên cột `Email`.

##### **🔹 Node 10: "Create a database page" (Notion)**
- **Database Name:** `Leads` (phải **trùng với tên database** trong Notion).
- **Properties:**
  - `Email` → `Email`
  - `Company Name` → `Company`
  - `Logo URL` → `Logo`
  - `Industry` → `Industry`
  - `Revenue` → `Revenue`
  - `CEO` → `CEO`
  - `Job Title` → `Job Title`
  - `Status` → `Status`
- **Lưu ý:**
  - **Tạo database `Leads` trong Notion** trước khi chạy workflow.
  - **Cấu hình Integration Notion** trong n8n (API Key).

##### **🔹 Node 11: "Create a task" (ClickUp)**
- **Space/Board:** Chọn **Board** trong ClickUp (ví dụ: `Leads`).
- **Task Name:** `Follow up with {Company Name}`.
- **Assignee:** Chọn **người phụ trách** (ví dụ: `Sales Team`).
- **Status:** `To Do`.
- **Description:** `Lead: {Email} - Company: {Company Name} - Industry: {Industry}`.
- **Lưu ý:**
  - **Tạo Board `Leads` trong ClickUp** trước khi chạy workflow.
  - **Cấu hình API Token ClickUp** trong n8n.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Điền **email** vào node `ManualTrigger` (ví dụ: `rahul@example.com`).
   - Kiểm tra **Google Sheets**, **Notion** và **ClickUp** có cập nhật dữ liệu không.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động enrich lead từ email mới**
   - Sử dụng **webhook** (ví dụ: từ **Zapier** hoặc **Make**) để **gửi email mới** vào workflow.
   - Cấu hình node `ManualTrigger` thành **HTTP Request** để nhận dữ liệu từ bên ngoài.

2. **Gửi báo cáo định kỳ**
   - Sử dụng **n8n Schedule Node** để **tự động enrich lại tất cả lead** hàng tuần.
   - **Lưu log** vào Google Sheets với cột `Last Updated`.

3. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack/Telegram** để **báo cáo kết quả enrich** ngay khi hoàn thành.
   - Ví dụ: `🚀 Lead {Company Name} đã được enrich thành công! Logo: [URL]`

4. **Lọc lead theo ngành nghề**
   - Sử dụng **node Filter** để **chỉ enrich lead** trong ngành **Tech/Finance/SaaS**.
   - Ví dụ: `Industry = "Technology"`

5. **Tự động gửi email follow-up**
   - Kết hợp với **node Email** (Gmail/SendGrid) để **gửi email tự động** khi lead được enrich.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **bán hàng và chiến lược**, thay vì **làm thủ công**. Với **Clearbit**, dữ liệu lead trở nên **chính xác và chi tiết**, trong khi **Notion và ClickUp** được đồng bộ **một cách hoàn hảo**.

**Hành động ngay!**
1. **Import workflow** và **cấu hình API keys**.
2. **Test với 1-2 lead mẫu**.
3. **Bật workflow** và **nhận dữ liệu lead enrich tự động** mỗi khi có lead mới!

**🚀 Cần hỗ trợ?** Đăng ký **khóa học tự động hóa n8n** của [n8n Vietnam](https://n8n.vn) để học cách **tạo workflow tự động hóa phù hợp với doanh nghiệp của bạn!**

---
**#TựĐộngHóa #LeadGeneration #n8n #Clearbit #Notion #ClickUp**