---
title: "🚀 Tự Động Hóa Sinh Lập Lead Tiềm Năng Từ Đáy Sàn Số Hóa Với Decodo & Airtable (Không Code)"
description: "Workflow tự động hóa tìm kiếm, enrich và cập nhật lead từ Google Search và trang liên hệ công ty, tiết kiệm 10+ giờ/tháng cho bộ phận marketing. Kết hợp API Decodo (80% OFF) và Airtable để quản lý lead chuyên nghiệp."
slug: "tieu-dong-hoa-sinh-lap-lead-digital-footprint-decodo-airtable"
tags: [n8n, automation, lead-generation, decodo, airtable, no-code, marketing-automation]
keywords: [n8n workflow lead generation, tự động hóa sinh lập lead, decodo api, airtable automation, tìm kiếm lead từ google, enrich lead contact]
---

# 🚀 **Tự Động Hóa Sinh Lập Lead Tiềm Năng Từ Đáy Sàn Số Hóa (Decodo + Airtable)**

### **Giải pháp cho các sếp marketing:**
Bạn đã từng phải mất **giờ đồng hồ** để tìm kiếm thông tin liên hệ của khách hàng tiềm năng từ Google, sau đó nhập liệu vào Airtable? Hoặc phải **lặp đi lặp lại** các công việc thủ công như:
- Tìm kiếm công ty theo từ khóa kỹ thuật (Klaviyo, HubSpot, Salesforce...)
- Trích xuất email từ trang liên hệ công ty
- Cập nhật lead vào hệ thống quản lý
- Lo lắng về **trùng lặp lead** và **tốn kém API** khi enrich dữ liệu không cần thiết?

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong 18 node, tiết kiệm **10+ giờ/tháng** và **giảm chi phí API** đến 80% nhờ logic điều kiện thông minh.**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Tìm kiếm lead từ Google, enrich thông tin liên hệ, và cập nhật vào Airtable **không cần code**.
- **Tiết kiệm chi phí API:** Chỉ enrich lead khi dữ liệu thiếu (email/trang liên hệ), tránh lãng phí **23k/tháng** (Decodo).
- **Dữ liệu sạch và duy nhất:** Loại bỏ trùng lặp lead, đảm bảo **Airtable** luôn có thông tin mới nhất.
- **Cập nhật liên tục:** Hoạt động **24/7** khi self-hosted trên VPS, không phụ thuộc vào thời gian làm việc.
- **Cá nhân hóa lead:** Phân loại lead theo **nguồn gốc** (Paid Ad vs. Organic) và **trạng thái** (New/Updated).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. API Keys & Credentials**
- **Decodo API Key** (Đăng ký [tại đây](https://visit.decodo.com/c/6679292/3071239/17480) với **mã giảm giá `ATTAN8N`** để **80% OFF** plan 23k/tháng).
- **Airtable API Key** (Tạo từ [Airtable Developer Console](https://airtable.com/api)).

### **2. Airtable Setup (Schema)**
Tạo **1 bảng "Leads"** với các trường sau (định dạng chính xác để workflow hoạt động):
| **Trường**               | **Loại Dữ liệu**       | **Ghi chú**                          |
|---------------------------|------------------------|--------------------------------------|
| `Domain`                  | Single Line Text       | **Trường chính** (ví dụ: `promarketer.ca`) |
| `Primary Email`           | Email                  | Email chính của lead (trống khi chưa enrich) |
| `Contact Page URL`        | URL                    | Trang liên hệ công ty (nếu có)       |
| `Source URL`              | URL                    | Link nguồn tìm kiếm (Google)         |
| `Lead Type`               | Single Select          | Giá trị: `Paid Ad Lead` / `Organic Lead` |
| `Status`                  | Single Select          | Giá trị: `New Lead` / `Updated` / `Enrichment Complete` |

### **3. Hệ thống n8n**
- **Self-hosted** (khuyến nghị) để workflow hoạt động **24/7** (không phụ thuộc vào n8n.io free tier).
  :::info[Gợi ý hạ tầng cho n8n]
  Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
  :::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11023](https://n8n.io/workflows/11023) hoặc copy toàn bộ JSON từ canvas.
- Trong **n8n Editor**, nhấn **Import** và dán JSON vào.
- **Không cần chỉnh sửa** cấu trúc node, chỉ cần **cấu hình credentials** và **tham số** như hướng dẫn dưới đây.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **18 node** với logic phức tạp. Các bước **cấu hình bắt buộc**:

#### **A. Cấu hình Credentials**
1. **Decodo API**:
   - Tạo **credentials mới** trong n8n với tên `decodoApi`.
   - Điền **API Key** từ Decodo (đăng ký với mã `ATTAN8N` để giảm 80%).
   - **Không cần cấu hình thêm** (node sẽ tự động sử dụng).

2. **Airtable API**:
   - Tạo **credentials mới** với tên `airtableTokenApi`.
   - Điền **Airtable API Key** (tạo từ [Airtable Developer Console](https://airtable.com/api)).
   - **Base ID**: Điền ID của bảng "Leads" (tìm trong URL của bảng Airtable).

#### **B. Cấu hình Node Quan Trọng**
1. **`Config: Set Search Params` (Node `set`)**
   - Mở node này và **cập nhật tham số** để phù hợp với mục tiêu lead generation:
     ```json
     {
       "tech_footprint": "We use Klaviyo",  // Thay đổi thành công cụ kỹ thuật mục tiêu (ví dụ: "Salesforce", "HubSpot")
       "target_industry": "site:promarketer.ca"  // Thay đổi thành domain ngành hàng (ví dụ: "site:saas.vn")
     }
     ```
   - **Lưu ý**: Tham số này **quan trọng nhất** vì quyết định **tính hiệu quả** của workflow.

2. **`Airtable: Check Existence` (Node `airtable`)**
   - **Table Name**: Đặt là `"Leads"` (phải trùng với bảng đã tạo).
   - **View Name**: Đặt là `"All Leads"` (hoặc tên view mặc định).
   - **Filter**: Node sẽ tự động lọc dựa trên `Domain` (không cần chỉnh sửa).

3. **`Code: Initial Domain Filter` (Node `code`)**
   - Node này **trích xuất domain** từ kết quả Google Search.
   - **Không cần chỉnh sửa mã** (n8n tự động xử lý), nhưng các sếp có thể mở node này để hiểu logic:
     ```javascript
     // Mã mặc định (không cần thay đổi)
     return $input.all();
     ```

4. **`Code: Finalize Contact Data` (Node `code`)**
   - Node này **xử lý email** từ trang liên hệ (sử dụng Regex).
   - **Không cần chỉnh sửa** (n8n tự động trích xuất email dạng `sales@`, `contact@`).

#### **C. Cấu hình Logic Điều Kiện**
Workflow sử dụng **3 node `if`** để tối ưu chi phí API:
1. **`If: Lead Exists?`**:
   - Nếu lead **đã tồn tại** trong Airtable → **Update** (không enrich lại).
   - Nếu lead **mới** → **Create** và enrich dữ liệu.

2. **`If: Enrichment Needed?`**:
   - Kiểm tra trường `Primary Email` trong Airtable.
   - Nếu **trống** → **Scrape Contact Page** (sử dụng Decodo).
   - Nếu **có dữ liệu** → Bỏ qua bước enrich (tiết kiệm API).

3. **`If: Contact Page Exists?` / `If: Contact Email Exists?`**:
   - Kiểm tra xem trang liên hệ hoặc email đã được **scrape** chưa.
   - Nếu **có** → Bỏ qua bước enrich tiếp theo.

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **Run Workflow** và nhập **domain mẫu** (ví dụ: `promarketer.ca`).
   - Kiểm tra kết quả trong **Airtable** và **Decodo Dashboard** (để theo dõi chi phí API).

2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật `Active`** và chọn **Manual Trigger** (hoặc kết nối với **n8n Trigger** để tự động hóa).

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIẾP CẬN HƠN]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **`slack`** hoặc **`telegram`** sau `Airtable: Update Lead` để **báo cáo lead mới** vào kênh chat.
   - **Cấu hình**:
     ```json
     {
       "message": "🚀 Lead mới được enrich: {{$node["Airtable: Update Lead"].json["fields"]["Domain"]}}",
       "attachments": [
         {
           "title": "Chi tiết lead",
           "text": `Email: {{$node["Airtable: Update Lead"].json["fields"]["Primary Email"]}}`
         }
       ]
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm node **`set`** sau `Airtable: Update Lead` để lưu **thời gian cập nhật** và **nguồn lead**:
     ```json
     {
       "timestamp": "{{$now}}",
       "source": "{{$node["Config: Set Search Params"].json["target_industry"]}}"
     }
     ```
   - Sau đó **merge** với dữ liệu lead bằng node **`set`** (Data Merger).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **`n8n-nodes-base.schedule`** để chạy workflow **hàng ngày** (ví dụ: 8h sáng) và gửi báo cáo qua email:
     ```json
     {
       "to": "marketing@doanhnghiep.com",
       "subject": "Báo cáo lead mới ({{$nowISO}})",
       "text": `Tổng lead mới: {{$node["Airtable: Check Existence"].json.length}}`
     }
     ```

4. **Tối ưu chi phí Decodo**:
   - **Không sử dụng JS Rendering** (node `Decodo: Google Search` đã tắt mặc định).
   - **Lọc domain** trước khi enrich bằng node `Code: Initial Domain Filter` để **giảm số lượng request API**.

5. **Phân loại lead theo ngành**:
   - Thêm trường `Industry` vào Airtable và cập nhật trong node `Config: Set Search Params`:
     ```json
     {
       "tech_footprint": "We use HubSpot",
       "target_industry": "site:saas.vn OR site:fintech.vn"
     }
     ```

---
## 📌 **Kết luận**
Workflow **Automated Lead Generation from Digital Footprints** là **giải pháp hoàn hảo** cho các sếp marketing muốn:
✅ **Tự động hóa sinh lập lead** từ Google Search và trang liên hệ công ty.
✅ **Tiết kiệm thời gian** (10+ giờ/tháng) và **chi phí API** (80% OFF với Decodo).
✅ **Quản lý lead chuyên nghiệp** với Airtable, phân loại và cập nhật liên tục.

**Hành động ngay hôm nay**:
1. **Đăng ký Decodo** với mã `ATTAN8N` để **80% OFF** plan 23k/tháng.
2. **Setup Airtable** với schema chính xác (đã hướng dẫn trên).
3. **Import workflow** và **cấu hình credentials** như hướng dẫn.
4. **Bật Active** và **test run** với domain mẫu.

**Kết quả?** Một hệ thống **tự động hóa lead generation** hoạt động **24/7**, giúp bạn **tăng doanh số** mà không cần viết một dòng code!

---
### **🔗 Tài liệu tham khảo**
- [Decodo API Documentation](https://decodo.com/docs)
- [Airtable API Guide](https://airtable.com/api)
- [n8n Workflow Original](https://n8n.io/workflows/11023)