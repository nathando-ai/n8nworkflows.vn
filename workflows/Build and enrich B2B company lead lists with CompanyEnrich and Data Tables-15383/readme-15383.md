---
title: "🚀 Tự Động Hoàn Chỉnh & Tạo Danh Sách Lead B2B Chuyên Nghiệp Với CompanyEnrich & n8n (Không Cần Code)"
description: "Workflow tự động hóa xây dựng và nâng cấp danh sách lead B2B từ đầu vào cơ bản thành dữ liệu chi tiết, chính xác với API CompanyEnrich. Giúp các sếp tiết kiệm 10+ giờ/tháng, giảm sai sót và tăng tỷ lệ chuyển đổi lead."
slug: "tieu-dong-hoan-chinh-danh-sach-lead-b2b"
tags: [n8n, automation, lead-generation, company-enrich, no-code]
keywords: [n8n workflow lead generation, tự động hóa tìm kiếm công ty B2B, enrich company data, API CompanyEnrich, tự động hóa bán hàng B2B]
---

# 🚀 **Tự Động Hoàn Chỉnh & Tạo Danh Sách Lead B2B Chuyên Nghiệp Với CompanyEnrich & n8n**

### **Giải pháp cho các sếp:**
Bạn đã bao giờ phải mất **giờ đồng hồ** để tìm kiếm, thu thập và hoàn chỉnh thông tin của các công ty tiềm năng (lead) để bán hàng, marketing hoặc phân tích thị trường? Hay phải **làm thủ công** trên Excel, copy-paste dữ liệu từ nhiều nguồn khác nhau, và lo lắng về **sai sót, trùng lặp** hay **thông tin không đầy đủ**?

**Workflow này sẽ giải quyết tất cả những vấn đề trên!**
Với **n8n**, bạn có thể tự động hóa toàn bộ quy trình từ **tìm kiếm công ty** (theo tiêu chí như ngành nghề, doanh thu, vị trí) đến **nâng cấp dữ liệu** (thông tin chi tiết về nhân sự, sản phẩm, liên hệ, tài chính) và **lưu trữ vào bảng dữ liệu** sẵn sàng cho CRM hoặc marketing.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng**: Không cần làm thủ công trên Excel hoặc các công cụ khác.
- **Dữ liệu chính xác & đầy đủ**: Thông tin được enrich từ API chuyên nghiệp (CompanyEnrich), bao gồm:
  - Tên công ty, địa chỉ, email, điện thoại.
  - Doanh thu, số nhân viên, ngành nghề.
  - Thông tin liên quan đến sản phẩm/dịch vụ.
- **Không trùng lặp**: Hệ thống tự động kiểm tra và bỏ qua các lead đã tồn tại.
- **Hoạt động 24/7**: Workflow chạy tự động khi có yêu cầu mới, không phụ thuộc vào giờ làm việc của bạn.
- **Cá nhân hóa**: Thêm các tiêu chí tìm kiếm riêng cho ngành nghề hoặc khu vực của doanh nghiệp.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản API CompanyEnrich**:
   - Đăng ký tại [CompanyEnrich](https://companyenrich.com/) và lấy **API Key**.
   - Thêm **credentials** trong n8n với loại `HTTP Header Auth` (điền `Bearer <API_KEY>`).
2. **Bảng dữ liệu (Data Table)**:
   - Tạo một bảng trong n8n (hoặc kết nối với Google Sheets/Airtable) để lưu trữ lead đã enrich.
   - Cấu trúc bảng cần có các cột: `company_name`, `website`, `email`, `phone`, `revenue`, `employees`, `industry`, `address`, `notes`.
3. **Tiêu chí tìm kiếm (Search Form)**:
   - Các trường như `ngành nghề`, `doanh thu`, `vị trí`, `số nhân viên` (được sử dụng trong form trigger).
4. **VPS (nếu muốn chạy 24/7)**:
   - Để workflow hoạt động liên tục, các sếp nên **self-host n8n** trên VPS.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15383](https://n8n.io/workflows/15383) hoặc copy toàn bộ mã JSON từ trang này.
- Mở **n8n Editor** → Nhấn `Import` → Dán hoặc tải file JSON.
- Workflow sẽ tự động hiển thị trên canvas.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình API CompanyEnrich**
- **Node "Post to Company Search API"** và **"Post to Company Enrich API"** cần **credentials HTTP Header Auth**:
  - **Method**: `POST`
  - **URL**:
    - Search API: `https://api.companyenrich.com/v1/search`
    - Enrich API: `https://api.companyenrich.com/v1/enrich`
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY>` (điền API Key từ CompanyEnrich).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    - **Search API**:
      ```json
      {
        "query": "$search_term", // Thay bằng biến từ form trigger
        "limit": 100,
        "fields": ["name", "website", "industry", "revenue", "employees"]
      }
      ```
    - **Enrich API**:
      ```json
      {
        "company": "$company_data" // Thay bằng dữ liệu từ node trước
      }
      ```

#### **B. Cấu hình Form Trigger**
- **Node "Trigger Search Form"** cần định nghĩa các trường tìm kiếm:
  - Thêm các trường như:
    - `nganh_nghe` (text)
    - `doanh_thu_min` (number)
    - `doanh_thu_max` (number)
    - `so_nhan_vien_min` (number)
    - `so_nhan_vien_max` (number)
    - `dinh_vung` (text)
  - **Lưu ý**: Các trường này sẽ được sử dụng để gọi API search.

#### **C. Cấu hình Data Table**
- **Node "Add Company to Table"** và **"Verify Company Entry"** cần cấu hình bảng dữ liệu:
  - **Table Name**: Đặt tên cho bảng (ví dụ: `leads_enriched`).
  - **Columns**:
    - `company_name`, `website`, `email`, `phone`, `revenue`, `employees`, `industry`, `address`, `notes`.
  - **Node "Verify Company Entry"** (operation: `rowExists`):
    - Kiểm tra xem lead đã tồn tại trong bảng trước khi thêm mới.

#### **D. Lọc và xử lý dữ liệu**
- **Node "Filter by Company Revenue"**:
  - Chỉ giữ lại các công ty có doanh thu trong khoảng `doanh_thu_min` và `doanh_thu_max` từ form.
- **Node "If Company Duplicate Exists"**:
  - Nếu lead đã tồn tại, **node "Skip Processing"** sẽ ngắt workflow để tránh trùng lặp.

#### **E. Batch Processing & Rate Limiting**
- **Node "Batch Process Companies"**:
  - Chia dữ liệu thành batch (ví dụ: 50 công ty/lần) để tránh bị API reject.
- **Node "Wait 1 Second"**:
  - Thêm thời gian chờ giữa các batch để tránh bị chặn bởi API rate limit.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` và nhập dữ liệu mẫu vào form trigger.
   - Kiểm tra kết quả trong **Data Table** để đảm bảo workflow hoạt động chính xác.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁC Ý TƯỚNG MỞ RỘNG**]
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo khi có lead mới được enrich.
2. **Lưu log hoạt động**:
   - Sử dụng **node Sticky Note** để ghi lại lịch sử hoạt động của workflow.
3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow riêng để gửi **báo cáo hàng tuần** về số lead mới, doanh thu trung bình, ngành nghề phổ biến.
4. **Tích hợp với CRM**:
   - Sau khi enrich, tự động thêm lead vào **HubSpot, Salesforce, hoặc Zoho CRM**.
5. **Tự động hóa email follow-up**:
   - Sử dụng **node Email** để gửi email chào hàng cho lead mới.
6. **Lọc lead theo tiêu chí cá nhân hóa**:
   - Thêm các tiêu chí như `tên CEO`, `sản phẩm chính`, `vị trí địa lý` để tăng độ chính xác.
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình tìm kiếm và enrich lead B2B** mà không cần viết một dòng code. Bằng cách kết hợp **API CompanyEnrich** với **n8n**, bạn sẽ có một **dữ liệu lead chuyên nghiệp, chính xác và sẵn sàng sử dụng** cho marketing, bán hàng hoặc phân tích thị trường.

**Hành động ngay hôm nay!**
1. **Đăng ký API CompanyEnrich** và lấy API Key.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật workflow** và bắt đầu tự động hóa lead generation!

**Nếu có bất kỳ câu hỏi nào**, hãy để lại comment bên dưới hoặc liên hệ với tôi qua [LinkedIn](https://linkedin.com/in/safakhan) để được hỗ trợ chi tiết! 🚀

---
**#n8n #Automation #LeadGeneration #CompanyEnrich #NoCode**